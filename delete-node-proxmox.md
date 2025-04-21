# Usuwanie węzła z klastra Proxmox na systemie Debian

Poniżej przedstawiono kroki, które należy wykonać, aby usunąć węzeł o nazwie `pve3` z klastra Proxmox na systemie Debian.

## Kroki:

1. **Utworzenie kopii zapasowej konfiguracji węzłów:**

   Skopiuj cały katalog `/etc/pve/nodes` do lokalizacji kopii zapasowej w `/root/nodes_backup`:
   ```bash
   cp -a /etc/pve/nodes /root/nodes_backup
   ```

2. **Usunięcie katalogu węzła:**

   Usuń katalog odpowiadający węzłowi `pve3` w lokalizacji `/etc/pve/nodes`:
   ```bash
   rm -r /etc/pve/nodes/pve3
   ```

3. **Edycja pliku konfiguracyjnego `corosync`:**

   Otwórz plik `/etc/pve/corosync.conf` w edytorze tekstu:
   ```bash
   nano /etc/pve/corosync.conf
   ```
   Usuń cały blok konfiguracji odpowiadający węzłowi `pve3`. Przykładowy blok:
   ```
   node {
       name: pve3
       nodeid: 3
       quorum_votes: 1
       ring0_addr: 192.168.0.3
   }
   ```

4. **Zaktualizowanie certyfikatów klastra:**

   Wykonaj komendę aktualizującą certyfikaty klastra:
   ```bash
   pvecm updatecerts
   ```

5. **Ponowne uruchomienie usługi `corosync`:**

   Zrestartuj usługę `corosync`:
   ```bash
   systemctl restart corosync
   ```

## Efekt:
Po wykonaniu powyższych kroków węzeł `pve3` zostanie pomyślnie usunięty z klastra.
