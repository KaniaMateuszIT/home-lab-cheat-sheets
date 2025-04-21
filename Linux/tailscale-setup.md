# Tailscale: Konfiguracja jako Exit Node

Poniżej przedstawiono kroki konfiguracji Tailscale jako węzła zapewniającego dostęp do sieci lokalnej oraz działającego jako Exit Node.

---

## Kroki konfiguracji:

1. **Włącz przekazywanie pakietów IPv4 i IPv6:**

   Dodaj poniższe linie do pliku `/etc/sysctl.conf`:
   ```bash
   echo "net.ipv4.ip_forward=1" >> /etc/sysctl.conf
   echo "net.ipv6.conf.all.forwarding=1" >> /etc/sysctl.conf
   ```

   Załaduj zmiany w konfiguracji systemowej:
   ```bash
   sysctl -p
   ```

2. **Uruchom Tailscale z odpowiednimi opcjami:**

   Użyj poniższego polecenia, aby skonfigurować węzeł jako Exit Node oraz reklamować trasy do sieci lokalnej:
   ```bash
   tailscale up --advertise-exit-node --advertise-routes=192.168.1.0/24
   ```

   - `--advertise-exit-node`: Umożliwia użycie tego węzła jako Exit Node.
   - `--advertise-routes=192.168.1.0/24`: Reklamuje trasę do sieci lokalnej (np. `192.168.1.0/24`).

---

## Efekt

Po wykonaniu powyższych kroków:
- Węzeł Tailscale będzie pełnił funkcję Exit Node.
- Będzie również udostępniał dostęp do sieci lokalnej o adresacji `192.168.1.0/24` innym urządzeniom w sieci Tailscale.

**Uwaga:** Upewnij się, że Twój serwer ma odpowiednie reguły zapory sieciowej oraz że Tailscale jest poprawnie skonfigurowany w panelu administracyjnym.
