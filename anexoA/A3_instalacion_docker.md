# A.3. Instalación de Docker

Docker se instaló utilizando el script oficial:

```bash
curl -fsSL https://get.docker.com | sudo sh

Añadir el usuario al grupo docker:

```bash
sudo usermod -aG docker $USER

Verificar la instalación:

```bash
docker --version
