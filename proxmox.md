# Usuwanie węzła z klastra Proxmox

Aby usunąć węzeł z klastra w systemie Proxmox, wykonaj poniższe kroki:

1. **Zrób kopię zapasową konfiguracji węzłów**
   ```bash
   cp -a /etc/pve/nodes /root/nodes_backup
