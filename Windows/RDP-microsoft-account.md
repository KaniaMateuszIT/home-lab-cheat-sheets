# Windows Cheat Sheet

## Uruchamianie aplikacji jako inny użytkownik, aby dało się połączyć korzystając z konta MS

Wprowadź hasło do konta Microsoft podczas uruchamiania aplikacji. To samo hasło będzie później używane do logowania do Zdalnego Pulpitu (RDP).  
**Uruchomienie aplikacji jako inny użytkownik:**
   Wykorzystaj poniższą komendę w PowerShell:
   ```powershell
   runas /u:MicrosoftAccount\username@example.com winver
   ```
   Zamień `username@example.com` na adres e-mail swojego konta Microsoft.
