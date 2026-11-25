# ☁️ Nextcloud – `trusted_domains`

> **Do czego:** pozbycie się komunikatu *„Access through untrusted domain”* – lista domen i adresów, pod którymi Nextcloud odpowiada.

## TL;DR

```bash
# Nextcloud w Dockerze (oficjalny obraz) – dodanie domeny pod indeksem 2
docker exec -u www-data nextcloud php occ config:system:set trusted_domains 2 --value=nextcloud.example.com
```

---

## 1. Przykładowa konfiguracja

```php
'trusted_domains' => [
    'localhost',
    'nextcloud.example.com',
    'example.com',
    '192.168.1.200:8080',
],
```

| Wpis | Znaczenie |
|---|---|
| `localhost` | dostęp z tego samego serwera |
| `nextcloud.example.com` | domena publiczna |
| `example.com` | alternatywna domena |
| `192.168.1.200:8080` | adres IP z portem w sieci lokalnej |

## 2. Gdzie to wpisać

**Sposób 1 – polecenie `occ` (bez edycji pliku):**

```bash
# podgląd aktualnej listy
docker exec -u www-data nextcloud php occ config:system:get trusted_domains
# dodanie / nadpisanie wpisu o danym indeksie
docker exec -u www-data nextcloud php occ config:system:set trusted_domains 3 --value=192.168.1.200:8080
```

Bez Dockera: `sudo -u www-data php /var/www/nextcloud/occ ...`

**Sposób 2 – ręcznie w `config.php`:**

| Instalacja | Plik |
|---|---|
| Docker (oficjalny obraz) | `/var/www/html/config/config.php` w kontenerze (zwykle w wolumenie) |
| Klasyczna | `/var/www/nextcloud/config/config.php` |

Znajdź tablicę `trusted_domains` (albo dodaj ją) i dopisz swoje domeny.

---

## Uwagi

- Wpisuj **dokładnie** to, co jest w pasku adresu przeglądarki (z portem, jeśli inny niż 80/443).
- Za reverse proxy ustaw też `overwriteprotocol` i `trusted_proxies`, inaczej pojawią się błędy przekierowań.

---

[← Spis treści](../README.md)
