# 🖥️ RDP na komputer z kontem Microsoft

> **Do czego:** Pulpit zdalny odrzuca poprawne hasło do konta Microsoft, gdy na komputerze logujesz się PIN-em lub Windows Hello.

**Dlaczego:** przy logowaniu PIN-em / Windows Hello Windows nie ma lokalnie zapamiętanego **hasła** do konta Microsoft, a RDP (uwierzytelnianie NLA) potrzebuje właśnie hasła. Jednorazowe uruchomienie czegokolwiek „jako ten użytkownik” z hasłem zapisuje je w systemie.

## TL;DR

```powershell
runas /u:MicrosoftAccount\twoj.adres@example.com winver
```

Wpisz hasło do konta Microsoft → pojawi się okno `winver` → od teraz RDP przyjmie to hasło.

---

## Kroki

1. Na komputerze, do którego chcesz się łączyć, otwórz PowerShell albo wiersz poleceń.
2. Uruchom (z adresem e-mail swojego konta Microsoft):

   ```powershell
   runas /u:MicrosoftAccount\twoj.adres@example.com winver
   ```

3. Podaj **hasło** do konta Microsoft (nie PIN).
4. Jeśli otworzy się okno z wersją Windows (`winver`) – gotowe.

## Logowanie przez RDP

| Pole | Wartość |
|---|---|
| Użytkownik | adres e-mail konta Microsoft (albo `MicrosoftAccount\twoj.adres@example.com`) |
| Hasło | hasło do konta Microsoft |

---

## Uwagi

- Pulpit zdalny musi być włączony: **Ustawienia → System → Pulpit zdalny** (wymaga Windows Pro/Enterprise).
- Po zmianie hasła do konta Microsoft powtórz krok z `runas`.
- Dostęp spoza domu: [remote-desktop-tailscale-wol.md](remote-desktop-tailscale-wol.md).

---

[← Spis treści](../README.md)
