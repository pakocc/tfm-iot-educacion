# B.3. Archivo docker-compose.yml
A continuación se presenta el archivo docker-compose.yml utilizado para desplegar todos los servicios de forma conjunta:

```bash
version: "3.9"

services:

  mosquitto:
    image: eclipse-mosquitto:latest
    container_name: mosquitto
    restart: always
    ports:
      - "1883:1883"
    volumes:
      - /home/pi/iot/mosquitto/config:/mosquitto/config
      - /home/pi/iot/mosquitto/data:/mosquitto/data
      - /home/pi/iot/mosquitto/log:/mosquitto/log
    networks:
      - iotnet

  nodered_mudeti:
    image: nodered/node-red:latest
    container_name: nodered_mudeti
    restart: always
    ports:
      - "1880:1880"
    volumes:
      - /home/pi/iot/nodered/mudeti:/data
    networks:
      - iotnet

  nodered_alumno1:
    image: nodered/node-red:latest
    container_name: nodered_alumno1
    restart: always
    ports:
      - "1884:1880"
    volumes:
      - /home/pi/iot/nodered/alumno1:/data
    networks:
      - iotnet

  nodered_alumno2:
    image: nodered/node-red:latest
    container_name: nodered_alumno2
    restart: always
    ports:
      - "1885:1880"
    volumes:
      - /home/pi/iot/nodered/alumno2:/data
    networks:
      - iotnet

  nodered_alumno3:
    image: nodered/node-red:latest
    container_name: nodered_alumno3
    restart: always
    ports:
      - "1886:1880"
    volumes:
      - /home/pi/iot/nodered/alumno3:/data
    networks:
      - iotnet

networks:
  iotnet:
    driver: bridge
```
