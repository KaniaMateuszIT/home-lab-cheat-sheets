# 🛡️ AdGuard Home w Dockerze

> **Do czego:** serwer DNS blokujący reklamy i trackery w całej sieci domowej.
> **Wymaga:** Docker + Docker Compose, wolny port 53 na hoście.

## TL;DR

```bash
mkdir -p ~/adguard && cd ~/adguard
# wklej docker-compose.yml z punktu 1, potem:
docker compose up -d
# kreator pierwszego uruchomienia: http://<IP_serwera>:3000
```

---

## 1. `docker-compose.yml`

```yaml
services:
  adguardhome:
    container_name: adguardhome
    image: adguard/adguardhome:latest
    restart: unless-stopped
    network_mode: host          # DNS na porcie 53 hosta, widać prawdziwe IP klientów
    volumes:
      - ./conf:/opt/adguardhome/conf
      - ./work:/opt/adguardhome/work
    environment:
      - TZ=Europe/Warsaw
```

Katalogi `conf` (konfiguracja) i `work` (dane, statystyki) utworzą się same przy pierwszym starcie.

## 2. Uruchomienie

```bash
docker compose up -d
```

Kreator pierwszego uruchomienia jest pod `http://<IP_serwera>:3000`. Wybierz w nim port panelu (np. 80) i ustaw login.

### Port 53 zajęty? (Debian / Ubuntu z `systemd-resolved`)

```bash
sudo sed -i 's/^#\?DNSStubListener=.*/DNSStubListener=no/' /etc/systemd/resolved.conf
sudo systemctl restart systemd-resolved
```

---

## 3. Serwery DNS-over-HTTPS (Upstream DNS)

Gotowe do wklejenia w **Settings → DNS settings → Upstream DNS servers**:

```text
https://cloudflare-dns.com/dns-query
https://dns.quad9.net/dns-query
https://dns10.quad9.net/dns-query
https://dns.adguard-dns.com/dns-query
https://doh.opendns.com/dns-query
https://dns.google/dns-query
https://doh.mullvad.net/dns-query
```

## 4. Warto włączyć

| Opcja | Gdzie | Po co |
|---|---|---|
| **Parallel requests** | DNS settings → Upstream DNS servers | pyta wszystkie serwery naraz i bierze najszybszą odpowiedź |
| **DNSSEC** | DNS settings → DNS server configuration | weryfikuje podpisy odpowiedzi DNS |

## 5. Listy blokowania

**Filters → DNS blocklists → Add blocklist → Choose from the list:**

- AdGuard DNS filter
- AdAway Default Blocklist
- HaGeZi's Pro++ Blocklist
- OISD Blocklist Big
- POL: CERT Polska List of malicious domains
- POL: Polish filters for Pi-hole
- uBlock₀ filters – Badware risks

---

## Uwagi

- Żeby blokowanie działało w całej sieci, ustaw IP serwera AdGuard jako **DNS w DHCP routera**.
- Dobrze mieć drugi serwer DNS (druga instancja AdGuard lub zapasowy resolver), inaczej awaria kontenera = brak internetu.
- Przeniesienie AdGuard na inny serwer: [moving-containers-between-servers.md](moving-containers-between-servers.md).

## Źródła

- [AdGuard Home – GitHub i dokumentacja](https://github.com/AdguardTeam/AdGuardHome)

---

[← Spis treści](../README.md)
