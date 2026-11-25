# 🎨 Oh My Posh – ładny prompt w PowerShell

> **Do czego:** kolorowy prompt z gałęzią Gita, czasem wykonania, statusem itp.
> **Wymaga:** PowerShell 7 ([install-powershell-winget.md](install-powershell-winget.md)), Windows Terminal.

## TL;DR

```powershell
winget install JanDeDobbeleer.OhMyPosh -s winget
oh-my-posh font install meslo
notepad $PROFILE    # dopisz linię z punktu 4, zapisz
. $PROFILE
```

---

## 1. Instalacja

```powershell
winget install JanDeDobbeleer.OhMyPosh -s winget
```

Po instalacji **zamknij i otwórz terminal**, żeby zadziałało polecenie `oh-my-posh`.

## 2. Czcionka z ikonami (Nerd Font)

Motywy używają ikon, więc potrzebna jest czcionka *Nerd Font*:

```powershell
oh-my-posh font install meslo
```

Następnie w **Windows Terminal → Ustawienia → profil PowerShell → Wygląd → Krój czcionki** wybierz **MesloLGM Nerd Font**. Bez tego w prompcie zobaczysz kwadraciki zamiast ikon. (Polecenie `oh-my-posh font install` bez nazwy pokaże listę innych czcionek.)

## 3. Profil PowerShell

```powershell
if (!(Test-Path $PROFILE)) { New-Item -Path $PROFILE -Type File -Force }
notepad $PROFILE
```

## 4. Włączenie motywu

Dopisz do profilu jedną linię:

```powershell
oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH/tokyo.omp.json" | Invoke-Expression
```

Jeśli `$env:POSH_THEMES_PATH` jest pusty, podaj motyw adresem:

```powershell
oh-my-posh init pwsh --config 'https://raw.githubusercontent.com/JanDeDobbeleer/oh-my-posh/main/themes/tokyo.omp.json' | Invoke-Expression
```

## 5. Zastosowanie zmian

```powershell
. $PROFILE
```

---

## Uwagi

- **„running scripts is disabled on this system”** – zezwól na skrypty dla swojego konta:
  `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned`
- Inne motywy: [galeria motywów Oh My Posh](https://ohmyposh.dev/docs/themes) – podmień `tokyo` na nazwę z galerii.

## Źródła

- [Oh My Posh – dokumentacja](https://ohmyposh.dev/docs/installation/windows)

---

[← Spis treści](../README.md)
