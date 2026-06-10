# E.5. Código completo del firmware para NodeMCU

A continuación se presenta un ejemplo de firmware utilizado para:

- **[conectar la placa a la red Wi‑Fi](ca://s?q=Conexion_WiFi_NodeMCU)**,
- **[establecer comunicación con el broker MQTT](ca://s?q=Conexion_MQTT_NodeMCU)**,
- **[publicar lecturas del sensor DHT11](ca://s?q=Publicar_DHT11_MQTT)**,
- **[recibir comandos para controlar un LED](ca://s?q=Control_LED_MQTT)**.

```cpp
#include <ESP8266WiFi.h>
#include <PubSubClient.h>
#include <DHT.h>

#define DHTPIN 2        // GPIO2 (D4)
#define DHTTYPE DHT11
#define LEDPIN 4        // GPIO4 (D2)

const char* ssid = "NOMBRE_WIFI";
const char* password = "CONTRASENA_WIFI";

const char* mqtt_server = "192.168.0.34";
const char* mqtt_user = "alumno1";
const char* mqtt_pass = "****";

WiFiClient espClient;
PubSubClient client(espClient);
DHT dht(DHTPIN, DHTTYPE);

void callback(char* topic, byte* payload, unsigned int length) {
  if (strcmp(topic, "aula/user1/actuador/led") == 0) {
    if (payload[0] == '1') digitalWrite(LEDPIN, HIGH);
    else digitalWrite(LEDPIN, LOW);
  }
}

void reconnect() {
  while (!client.connected()) {
    if (client.connect("ESP8266Client", mqtt_user, mqtt_pass)) {
      client.subscribe("aula/user1/actuador/led");
    } else {
      delay(2000);
    }
  }
}

void setup() {
  pinMode(LEDPIN, OUTPUT);
  dht.begin();

  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) delay(500);

  client.setServer(mqtt_server, 1883);
  client.setCallback(callback);
}

void loop() {
  if (!client.connected()) reconnect();
  client.loop();

  float t = dht.readTemperature();
  float h = dht.readHumidity();

  if (!isnan(t)) {
    client.publish("aula/user1/sensor/temperatura",
    String(t).c_str());
  }
  if (!isnan(h)) {
    client.publish("aula/user1/sensor/humedad",
    String(h).c_str());
  }

  delay(5000);
}
```
