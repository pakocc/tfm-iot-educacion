# G.3. Código completo de la NodeMCU

El siguiente listado muestra el programa desarrollado para la placa **NodeMCU (ESP8266)**. Este código implementa la lectura de sensores, el control de actuadores, la comunicación mediante **[MQTT](ca://s?q=Protocolo_MQTT)** y la generación de alertas locales (zumbador) y remotas (correo electrónico a través de **[Node‑RED](ca://s?q=NodeRED_IoT)**).

```cpp
#include <ESP8266WiFi.h>
#include <PubSubClient.h>
#include <DHT.h>
#include <Servo.h>

// --- WiFi ---
const char* ssid = "TU_WIFI";
const char* password = "TU_PASS";

// --- MQTT ---
const char* mqtt_server = "IP_DEL_BROKER";
WiFiClient espClient;
PubSubClient client(espClient);

// --- DHT11 ---
#define DHTPIN D4
#define DHTTYPE DHT11
DHT dht(DHTPIN, DHTTYPE);

// --- Sensor magnetico ---
#define MAGNETIC_PIN D5

// --- Sensor de gases ---
#define GAS_PIN A0

// --- Servo puerta principal ---
Servo servo;
#define SERVO_PIN D6

// --- Motor puerta corredera (L293D) ---
#define MOTOR_IN1 D1
#define MOTOR_IN2 D2

// --- Finales de carrera ---
#define FC_ABIERTO D7
#define FC_CERRADO D8

// --- Semaforo LEDs ---
#define LED_ROJO D0
#define LED_AMARILLO D3
#define LED_VERDE D9

// --- Zumbador ---
#define BUZZER_PIN D10

unsigned long lastMsg = 0;
unsigned long tiempoPuertaAbierta = 0;

// --- Funciones de alerta sonora ---
void buzzer_continuo() {
  digitalWrite(BUZZER_PIN, HIGH);
}

void buzzer_off() {
  digitalWrite(BUZZER_PIN, LOW);
}

void buzzer_intermitente(int tiempo) {
  digitalWrite(BUZZER_PIN, HIGH);
  delay(tiempo);
  digitalWrite(BUZZER_PIN, LOW);
  delay(tiempo);
}

void buzzer_pitidos(int veces, int duracion) {
  for (int i = 0; i < veces; i++) {
    digitalWrite(BUZZER_PIN, HIGH);
    delay(duracion);
    digitalWrite(BUZZER_PIN, LOW);
    delay(duracion);
  }
}

// --- Conexion WiFi ---
void setup_wifi() {
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
  }
}

// --- Callback MQTT ---
void callback(char* topic, byte* payload, unsigned int length) {
  String msg;
  for (unsigned int i = 0; i < length; i++) {
    msg += (char)payload[i];
  }

  if (String(topic) == "casa/puerta_principal/cmd") {
    if (msg == "abrir")  servo.write(90);
    if (msg == "cerrar") servo.write(0);
  }

  if (String(topic) == "casa/puerta_corredera/cmd") {
    if (msg == "abrir") {
      digitalWrite(MOTOR_IN1, HIGH);
      digitalWrite(MOTOR_IN2, LOW);
    }
    if (msg == "cerrar") {
      digitalWrite(MOTOR_IN1, LOW);
      digitalWrite(MOTOR_IN2, HIGH);
    }
    if (msg == "parar") {
      digitalWrite(MOTOR_IN1, LOW);
      digitalWrite(MOTOR_IN2, LOW);
    }
  }
}

// --- Reconexion MQTT ---
void reconnect() {
  while (!client.connected()) {
    client.connect("NodeMCU");
    client.subscribe("casa/puerta_principal/cmd");
    client.subscribe("casa/puerta_corredera/cmd");
  }
}

// --- Setup ---
void setup() {
  Serial.begin(115200);
  setup_wifi();
  client.setServer(mqtt_server, 1883);
  client.setCallback(callback);

  dht.begin();
  servo.attach(SERVO_PIN);

  pinMode(MAGNETIC_PIN, INPUT_PULLUP);
  pinMode(GAS_PIN, INPUT);
  pinMode(MOTOR_IN1, OUTPUT);
  pinMode(MOTOR_IN2, OUTPUT);
  pinMode(FC_ABIERTO, INPUT_PULLUP);
  pinMode(FC_CERRADO, INPUT_PULLUP);
  pinMode(LED_ROJO, OUTPUT);
  pinMode(LED_AMARILLO, OUTPUT);
  pinMode(LED_VERDE, OUTPUT);
  pinMode(BUZZER_PIN, OUTPUT);
  digitalWrite(BUZZER_PIN, LOW);
}

// --- Loop principal ---
void loop() {
  if (!client.connected()) {
    reconnect();
  }
  client.loop();

  unsigned long now = millis();
  if (now - lastMsg > 5000) {
    lastMsg = now;

    float t = dht.readTemperature();
    float h = dht.readHumidity();
    int gas = analogRead(GAS_PIN);
    int puerta = digitalRead(MAGNETIC_PIN);

    client.publish("casa/temperatura", String(t).c_str());
    client.publish("casa/humedad", String(h).c_str());
    client.publish("casa/gases", String(gas).c_str());
    client.publish("casa/puerta_principal/estado",
                   puerta == LOW ? "abierta" : "cerrada");

    // --- Alerta gases altos ---
    if (gas > 600) {
      buzzer_continuo();
      client.publish("casa/alerta/gases", "alto");
    } else {
      buzzer_off();
    }

    // --- Alerta puerta principal abierta demasiado tiempo ---
    if (puerta == LOW) {
      if (millis() - tiempoPuertaAbierta > 10000) {
        buzzer_pitidos(3, 200);
        client.publish("casa/alerta/puerta_principal", "abierta_tiempo");
      }
    } else {
      tiempoPuertaAbierta = millis();
    }

    // --- Estado puerta corredera ---
    if (digitalRead(FC_ABIERTO) == LOW) {
      client.publish("casa/puerta_corredera/estado", "abierta");
      digitalWrite(LED_VERDE, HIGH);
      digitalWrite(LED_ROJO, LOW);
      digitalWrite(LED_AMARILLO, LOW);
    } else if (digitalRead(FC_CERRADO) == LOW) {
      client.publish("casa/puerta_corredera/estado", "cerrada");
      digitalWrite(LED_VERDE, LOW);
      digitalWrite(LED_ROJO, HIGH);
      digitalWrite(LED_AMARILLO, LOW);
    } else {
      client.publish("casa/puerta_corredera/estado", "intermedia");
      digitalWrite(LED_VERDE, LOW);
      digitalWrite(LED_ROJO, LOW);
      digitalWrite(LED_AMARILLO, HIGH);
      buzzer_intermitente(150);
      client.publish("casa/alerta/corredera", "atascada");
    }
  }
}
```

## Descripción del funcionamiento del programa

El programa desarrollado para la NodeMCU implementa la lógica completa de sensorización, actuación y comunicación del sistema domótico. En primer lugar, el dispositivo establece la conexión WiFi y configura el cliente MQTT, suscribiéndose a los topics necesarios para recibir órdenes de control desde **[Node‑RED](ca://s?q=NodeRED_IoT)**. A continuación, se inicializan los sensores (DHT11, sensor magnético, sensor de gases y finales de carrera) y los actuadores (servo, motor de la puerta corredera, semáforo LED y zumbador).

El bucle principal realiza periódicamente la lectura de todos los sensores y publica sus valores mediante MQTT, permitiendo su monitorización en tiempo real. Sobre estas lecturas se aplican diversas condiciones de seguridad: detección de gases altos, puerta principal abierta durante un tiempo prolongado y estado anómalo de la puerta corredera. Cuando se cumple alguna de estas condiciones, el sistema genera alertas locales mediante el zumbador y alertas remotas publicando mensajes específicos en los topics de aviso.

El programa también gestiona la recepción de comandos MQTT procedentes de Node‑RED, permitiendo el control remoto de la puerta principal mediante un servo y de la puerta corredera mediante un motor DC gobernado por un L293D. El semáforo LED refleja en todo momento el estado de la puerta corredera, diferenciando entre abierta, cerrada y posición intermedia. En conjunto, el código implementa un sistema domótico completo, robusto y reproducible, adecuado para su uso en entornos educativos y experimentales.
