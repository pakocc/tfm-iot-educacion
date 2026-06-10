# F.4. Acceso remoto seguro mediante Tailscale

Para permitir la administración remota sin necesidad de abrir puertos en el router, se integró **[Tailscale](ca://s?q=Tailscale_red_privada_virtual)** como solución de red privada virtual basada en WireGuard. Tailscale proporciona:

- **[una dirección IP privada segura](ca://s?q=IP_privada_Tailscale)** (por ejemplo, `100.x.x.x`),
- **[cifrado extremo a extremo](ca://s?q=Cifrado_extremo_a_extremo_Tailscale)**,
- **[acceso remoto desde cualquier ubicación](ca://s?q=Acceso_remoto_Tailscale)**,
- **[supervisión del aula sin presencia física](ca://s?q=Supervision_remota_IoT)**.

El servicio `tailscaled` se configuró para iniciarse automáticamente con el sistema, garantizando disponibilidad continua.

## F.4.1. MagicDNS y ACLs

Se habilitó la función **[MagicDNS](ca://s?q=MagicDNS_Tailscale)**, que permite acceder a la Raspberry Pi mediante un nombre de dominio interno sin necesidad de recordar direcciones IP.

Además, se configuraron **[listas de control de acceso (ACLs)](ca://s?q=ACLs_Tailscale)** en el panel de Tailscale para:

- **[restringir el acceso únicamente al docente](ca://s?q=Restriccion_acceso_docente)**,
- **[limitar los servicios accesibles (Portainer, Node‑RED, SSH)](ca://s?q=Limitacion_servicios_Tailscale)**,
- **[reforzar la seguridad del entorno educativo](ca://s?q=Seguridad_entorno_educativo_IoT)**.

Estas medidas garantizan un acceso remoto seguro, controlado y adecuado para entornos formativos.
