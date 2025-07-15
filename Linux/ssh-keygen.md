# Usuwanie starego klucza SSH z known_hosts

Gdy stawiasz nowy serwer pod tym samym adresem IP, stary klucz SSH zapisany w pliku `~/.ssh/known_hosts` może powodować błąd przy próbie połączenia. Aby go usunąć, użyj poniższej komendy:

---

## 1. **Usunięcie wpisu dla IP**

```bash
ssh-keygen -R 192.168.1.40
```
- Zamień `192.168.1.40` na adres IP lub nazwę hosta nowego serwera.

---

## 2. **Opis działania**

- Komenda usuwa wpis powiązany z danym IP/hostem z pliku `~/.ssh/known_hosts`.
- Dzięki temu przy kolejnym połączeniu zaakceptujesz nowy klucz serwera.

---

## 3. **Szybkie sprawdzenie wpisów**

Wyświetlenie wpisów dla danego IP:
```bash
grep "192.168.1.40" ~/.ssh/known_hosts
```

---

## Uwagi

- Stosuj tę komendę tylko, gdy masz pewność, że serwer został zmieniony.
- Nie usuwaj wpisów bez potrzeby – chronią Cię przed atakami typu "man-in-the-middle".
