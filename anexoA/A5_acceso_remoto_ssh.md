# A.5. Configuración de acceso remoto mediante SSH

El acceso remoto se habilitó mediante:

```bash
sudo systemctl enable ssh
sudo systemctl start ssh

Para mayor seguridad, se recomienda cambiar la contraseña del usuario por defecto:

```bash
passwd
