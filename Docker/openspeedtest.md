# 🚀 OpenSpeedTest w Dockerze

> **Do czego:** test prędkości sieci lokalnej (Wi-Fi, LAN, VPN) z przeglądarki – bez wychodzenia do internetu.
> **Wymaga:** Docker + Docker Compose.

## TL;DR

```bash
docker run -d --name openspeedtest --restart unless-stopped -p 3004:3000 openspeedtest/latest
# test: http://<IP_serwera>:3004
```

---

## 1. `docker-compose.yml`

```bash
mkdir -p ~/openspeedtest && cd ~/openspeedtest
```

```yaml
services:
  openspeedtest:
    image: openspeedtest/latest
    container_name: openspeedtest
    restart: unless-stopped
    ports:
      - "3004:3000"   # <port na hoście>:<port w kontenerze>
```

## 2. Uruchomienie

```bash
docker compose up -d
```

Test otwierasz w przeglądarce: `http://<IP_serwera>:3004`.

---

## Uwagi

- **Inny port:** zmień tylko liczbę **przed** dwukropkiem (np. `"4000:3000"`) i adres w przeglądarce.
- Wynik pokazuje przepustowość między **urządzeniem a serwerem** – idealne do sprawdzenia Wi-Fi albo tunelu Tailscale.
- Przez reverse proxy (np. Nginx Proxy Manager) zwiększ limit rozmiaru żądania, inaczej test uploadu się urwie.

## Źródła

- [OpenSpeedTest – dokumentacja](https://openspeedtest.com/)

---

[← Spis treści](../README.md)
