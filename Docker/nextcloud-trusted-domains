# Nextcloud Trusted Domains Configuration

## Opis

`trusted_domains` to część konfiguracji Nextcloud, która pozwala określić listę domen i adresów IP, z których można bezpiecznie uzyskać dostęp do instalacji Nextcloud. Dzięki tej konfiguracji serwer Nextcloud akceptuje tylko żądania pochodzące z określonych domen lub adresów IP, co zwiększa bezpieczeństwo.

## Przykładowa konfiguracja

Poniżej przedstawiono przykład konfiguracji `trusted_domains`:

```php
'trusted_domains' => [
    'localhost',
    'nextcloud.mateuszkania.ovh',
    'next.mateuszkania.ovh',
    '192.168.1.200:8080',
],
```

### Wyjaśnienie powyższej konfiguracji:
- `localhost` – umożliwia dostęp lokalny (z tego samego serwera, na którym działa Nextcloud).
- `nextcloud.mateuszkania.ovh` – adres domeny publicznej dla instalacji Nextcloud.
- `next.mateuszkania.ovh` – alternatywny adres domeny publicznej dla Nextcloud.
- `192.168.1.200:8080` – lokalny adres IP z portem, dostępny w sieci wewnętrznej.

## Gdzie dodać konfigurację?

1. Otwórz plik `config.php`, znajdujący się w katalogu konfiguracyjnym Nextcloud, zazwyczaj w lokalizacji:
   ```
   /var/www/nextcloud/config/config.php
   ```

2. Znajdź sekcję z `trusted_domains` lub dodaj ją, jeśli jeszcze nie istnieje.

3. Wprowadź powyższą konfigurację, dostosowując nazwy domen i adresy IP do swoich potrzeb.

## Uwagi
- Pamiętaj, aby lista `trusted_domains` była zgodna z domenami i adresami IP, z których faktycznie korzystasz, aby uniknąć problemów z dostępem.
- Jeśli dodasz nową domenę lub adres IP, zrestartuj serwer WWW (np. Apache lub Nginx), aby zmiany zostały zastosowane.
