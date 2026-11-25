# 🔑 SSH – usunięcie starego klucza hosta z `known_hosts`

> **Do czego:** błąd *„REMOTE HOST IDENTIFICATION HAS CHANGED!”* po postawieniu nowego serwera pod tym samym adresem IP.

## TL;DR

```bash
ssh-keygen -R 192.168.1.40
```

---

## 1. Usunięcie wpisu

```bash
ssh-keygen -R 192.168.1.40            # adres IP
ssh-keygen -R serwer.lan              # nazwa hosta
ssh-keygen -R "[192.168.1.40]:2222"   # SSH na niestandardowym porcie
```

Polecenie usuwa wpis z `~/.ssh/known_hosts` (kopia zapasowa trafia do `known_hosts.old`). Przy następnym połączeniu SSH zapyta o akceptację nowego klucza.

## 2. Podgląd wpisów

```bash
ssh-keygen -F 192.168.1.40
```

(Wpisy w `known_hosts` są często zahashowane, więc zwykły `grep` po IP ich nie znajdzie.)

---

## Uwagi

- Usuwaj wpis tylko wtedy, gdy **wiesz**, że serwer się zmienił (reinstalacja, nowa VM pod starym IP).
- Nieoczekiwana zmiana klucza może oznaczać atak *man-in-the-middle* – nie ignoruj tego ostrzeżenia odruchowo.

---

[← Spis treści](../README.md)
