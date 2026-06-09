# A.1. Preparación del sistema operativo

Para la implementación se utilizó una **Raspberry Pi 4 Model B con 4 GB de RAM**.  
El sistema operativo instalado fue **Raspberry Pi OS Lite (64-bit)**, seleccionado por su ligereza y estabilidad.

## A.1.1 Pasos de instalación

1. Descargar la imagen desde la página oficial:  
   https://www.raspberrypi.com/software/
2. Grabar la imagen en una tarjeta microSD utilizando **Raspberry Pi Imager**.
3. Antes de iniciar el sistema por primera vez, habilitar SSH creando un archivo vacío llamado `ssh` en la partición `boot`.
4. Insertar la tarjeta en la Raspberry Pi y encender el dispositivo.

## A.1.2. Actualización inicial del sistema

Tras el arranque inicial, se recomienda actualizar el sistema:

```bash
sudo apt update && sudo apt upgrade -y
