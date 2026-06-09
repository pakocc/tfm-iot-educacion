# A.4. Instalación de Portainer

Portainer se utilizó para gestionar los contenedores de forma visual.

```bash
docker volume create portainer_data

docker run -d \
  -p 9000:9000 \
  --name portainer \
  --restart=always \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v portainer_data:/data \
  portainer/portainer-ce:latest

El acceso local se realiza mediante:

http://192.168.0.34:9000
