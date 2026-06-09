# A.2. Configuración de red

La Raspberry Pi se configuró para operar principalmente mediante conexión **Ethernet**, garantizando estabilidad y baja latencia.

## A.2.1. Configuración mediante DHCP

En la mayoría de entornos educativos, el router asigna automáticamente una dirección IP.  
Para comprobarla:

```bash
ip a

## A.2.2. Configuración de IP estática (opcional)

En caso de necesitar una IP fija, puede configurarse editando el archivo dhcpcd.conf:

```bash
/etc/dhcpcd.conf

interface eth0
static ip_address=192.168.0.34/24
static routers=192.168.0.1
static domain_name_servers=192.168.0.1
