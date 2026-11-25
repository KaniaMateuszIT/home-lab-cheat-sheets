# ⬇️ Instalacja najnowszego PowerShell (winget)

> **Do czego:** instalacja PowerShell 7+ obok wbudowanego Windows PowerShell 5.1.

## TL;DR

```powershell
winget install --id Microsoft.PowerShell --source winget
```

---

## 1. Wyszukanie dostępnych wersji

```powershell
winget search Microsoft.PowerShell
```

| Id | Co to jest |
|---|---|
| `Microsoft.PowerShell` | wersja stabilna – tej zwykle chcesz |
| `Microsoft.PowerShell.Preview` | wersja testowa |

## 2. Instalacja

```powershell
winget install --id Microsoft.PowerShell --source winget
```

## 3. Aktualizacja i sprawdzenie wersji

```powershell
winget upgrade --id Microsoft.PowerShell
pwsh -Command '$PSVersionTable.PSVersion'
```

Nowy PowerShell uruchamiasz poleceniem `pwsh` (stary to `powershell`). W Windows Terminal pojawi się jako osobny profil.

---

## Uwagi

- **winget** jest wbudowany w Windows 10/11 (pakiet *App Installer* ze Sklepu Microsoft).
- Instalacja może poprosić o uprawnienia administratora.
- Dalej: ładny prompt – [oh-my-posh.md](oh-my-posh.md).

---

[← Spis treści](../README.md)
