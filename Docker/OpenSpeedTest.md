# Instalacja i Konfiguracja OpenSpeedTest

## Opis

OpenSpeedTest to narzędzie umożliwiające testowanie prędkości sieci. Poniższy przewodnik przedstawia kroki instalacji OpenSpeedTest za pomocą Dockera oraz konfigurację portu zgodnie z Twoimi preferencjami.

## Kroki instalacji

1. **Utwórz katalog dla OpenSpeedTest:**
   ```bash
   mkdir ~/openspeedtest
   cd ~/openspeedtest
   ```

2. **Utwórz plik `docker-compose.yml`:**
   Użyj edytora tekstu (np. nano) i dodaj poniższą konfigurację:
   ```yaml
   services:
     openspeedtest:
       image: openspeedtest/latest
       container_name: openspeedtest
       restart: unless-stopped
       ports:
         - "3004:3000"   # <--- zmień jeśli chcesz inny port
   ```

3. **Uruchom OpenSpeedTest za pomocą Docker Compose:**
   ```bash
   docker compose up -d
   ```

## Uwagi konfiguracyjne

- **Zmiana portu**: Jeśli chcesz użyć innego portu niż `3004`, zmień liczbę przed dwukropkiem (np. `4000:3000`) w sekcji `ports` w pliku `docker-compose.yml`.
- Po uruchomieniu aplikacja będzie dostępna pod adresem:
  ```
  http://<IP_serwera>:3004
  ```
  Jeśli zmienisz port, dostosuj końcówkę URL do odpowiedniego numeru portu.

## Dodatkowe informacje

Więcej szczegółowych informacji znajdziesz w [OpenSpeedTest Documentation](https://openspeedtest.com/).
