# Instalacja i Konfiguracja AdGuard Home

## Opis

AdGuard Home to potężny serwer DNS, który blokuje reklamy i trackery w całej sieci. Poniższy przewodnik przedstawia kroki instalacji AdGuard Home za pomocą Dockera oraz konfigurację zaawansowanych funkcji, aby zapewnić optymalną wydajność i bezpieczeństwo.

## Kroki instalacji

1. **Utwórz katalog dla AdGuard Home:**
   ```bash
   mkdir ~/adguard
   cd ~/adguard
   ```

2. **Utwórz plik `docker-compose.yml`:**
   Użyj edytora tekstu (np. nano) i dodaj poniższą konfigurację:
   ```yaml
   services:
     adguardhome:
       container_name: adguardhome
       image: adguard/adguardhome:latest
       restart: unless-stopped
       network_mode: "host"
       volumes:
         - ./conf:/opt/adguardhome/conf
         - ./work:/opt/adguardhome/work
       environment:
         - TZ=Europe/Warsaw
   ```

3. **Uruchom AdGuard Home za pomocą Docker Compose:**
   ```bash
   docker compose up -d
   ```

## Serwery DNS-over-HTTPS (DoH)

Poniżej znajduje się lista rekomendowanych serwerów DNS-over-HTTPS (DoH), które można skonfigurować w AdGuard Home w celu zwiększenia prywatności:

- [Cloudflare DNS](https://cloudflare-dns.com/dns-query)
- [Quad9 DNS](https://dns.quad9.net/dns-query)
- [Quad9 DNS (alternatywny)](https://dns10.quad9.net/dns-query)
- [AdGuard DNS](https://dns.adguard-dns.com/dns-query)
- [OpenDNS](https://doh.opendns.com/dns-query)
- [Google DNS](https://dns.google/dns-query)
- [Mullvad DNS](https://doh.mullvad.net/dns-query)

## Rekomendowane funkcje do włączenia

1. **Równoległe żądania (Parallel Requests)**
   - Poprawiają wydajność zapytań DNS dzięki jednoczesnemu wysyłaniu żądań do wielu resolverów.

2. **DNSSEC**
   - Zapewnia dodatkową warstwę bezpieczeństwa poprzez weryfikację odpowiedzi DNS.

## Bloklisty DNS

Poniżej znajduje się lista rekomendowanych bloklist, które zwiększają skuteczność blokowania reklam i trackerów:

- **AdGuard DNS filter**
- **AdAway Default Blocklist**
- **HaGeZi's Pro++ Blocklist**
- **OISD Blocklist Big**
- **POL: CERT Polska List of malicious domains**
- **POL: Polish filters for Pi-hole**
- **uBlock₀ filters – Badware risks**

## Uwagi konfiguracyjne

- Upewnij się, że katalogi `conf` i `work` zostały utworzone w folderze AdGuard Home, ponieważ są one montowane przez kontener Dockera do przechowywania konfiguracji i danych roboczych.
- Skonfiguruj swoje urządzenia tak, aby korzystały z serwera DNS AdGuard Home, co zapewni ochronę w całej sieci.

## Dodatkowe informacje

Więcej szczegółów i zaawansowane konfiguracje znajdziesz w [dokumentacji AdGuard Home](https://github.com/AdguardTeam/AdGuardHome).
