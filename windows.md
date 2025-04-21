# Windows Cheat Sheet

## Uruchamianie aplikacji jako inny użytkownik
#### Test
```powershell
<!-- Ustaw mail na zgodny z kontem Microsoft obecnym na komputerze -->
runas /u:MicrosoftAccount\username@example.com winver
<!-- Podajesz hasło - później tym samym hasłem będzie logowanie do Zdalnego Pulpitu (RDP) -->
```
