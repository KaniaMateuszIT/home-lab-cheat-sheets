# Windows Cheat Sheet

## Uruchamianie aplikacji jako inny użytkownik, aby dało się połączyć korzystając z konta online
Ustaw mail na zgodny z kontem Microsoft obecnym na komputerze!  
Podaj hasło - później tym samym hasłem będzie logowanie do Zdalnego Pulpitu (RDP)
```powershell
runas /u:MicrosoftAccount\username@example.com winver
```
