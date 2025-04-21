# Instalacja nowej wersji PowerShell za pomocą Winget

## Wyszukiwanie PowerShell w Winget

Aby znaleźć dostępne wersje PowerShell w Winget, użyj poniższego polecenia:

```powershell
winget search Microsoft.PowerShell
```

---

## Instalacja PowerShell

Aby zainstalować najnowszą wersję PowerShell z Winget, użyj poniższego polecenia:

```powershell
winget install --id Microsoft.PowerShell --source winget
```

---

## Uwagi

- **Winget**: Winget to menedżer pakietów w systemie Windows. Upewnij się, że jest zainstalowany i skonfigurowany na Twoim systemie przed wykonaniem powyższych poleceń.
- **Uprawnienia administratora**: Polecenia mogą wymagać uruchomienia w PowerShell z uprawnieniami administratora.
