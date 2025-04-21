# Windows Cheat Sheet

## Uruchamianie aplikacji jako inny użytkownik, aby dało się połączyć korzystając z konta MS

 
**Uruchomienie aplikacji jako inny użytkownik:**
   Wykorzystaj poniższą komendę w PowerShell:
   ```powershell
   runas /u:MicrosoftAccount\username@example.com winver
   ```
   Zamień `username@example.com` na adres e-mail swojego konta Microsoft.  
   Następnie wprowadź hasło do konta Microsoft, to samo hasło będzie później używane do logowania do Zdalnego Pulpitu (RDP).  
   Jeśli wszystko wykonało się pomyślnie to zobaczysz winver.
