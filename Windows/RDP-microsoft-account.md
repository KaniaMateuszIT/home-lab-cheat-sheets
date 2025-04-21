# Windows Cheat Sheet

## Uruchamianie aplikacji jako inny użytkownik, aby dało się połączyć korzystając z konta MS

1. **Ustawienie e-maila zgodnego z kontem Microsoft obecnym na komputerze:**
   Upewnij się, że e-mail używany do logowania jest zgodny z kontem Microsoft na komputerze.

2. **Podanie hasła:**
   Wprowadź hasło do konta Microsoft podczas uruchamiania aplikacji. To samo hasło będzie później używane do logowania do Zdalnego Pulpitu (RDP).

3. **Uruchomienie aplikacji jako inny użytkownik:**
   Wykorzystaj poniższą komendę w PowerShell:
   ```powershell
   runas /u:MicrosoftAccount\username@example.com winver
   ```
   Zamień `username@example.com` na adres e-mail swojego konta Microsoft.
