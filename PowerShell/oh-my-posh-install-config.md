# Instalacja i konfiguracja Oh My Posh w PowerShell

Poniżej znajdują się kroki instalacji i konfiguracji narzędzia **Oh My Posh** do personalizacji promptu w PowerShell.

---

## 1. Instalacja Oh My Posh

Zainstaluj Oh My Posh za pomocą `winget`:
```powershell
winget install JanDeDobbeleer.OhMyPosh -s winget
```

---

## 2. Instalacja czcionki

Oh My Posh wymaga odpowiedniej czcionki obsługującej symbole Powerline. Zainstaluj zalecaną czcionkę za pomocą poniższego polecenia:
```powershell
oh-my-posh font install
```

Polecana czcionka: **Ubuntu Sans** (lub inna zainstalowana podczas powyższego procesu).

---

## 3. Tworzenie profilu PowerShell

1. Utwórz plik profilu (jeśli nie istnieje):
   ```powershell
   New-Item -Path $PROFILE -Type File -Force
   ```

2. Otwórz plik profilu w edytorze tekstu (np. Notepad):
   ```powershell
   notepad $PROFILE
   ```

---

## 4. Inicjalizacja Oh My Posh

Dodaj poniższą linię do swojego profilu PowerShell (otwartego w Notepadzie):
```powershell
oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH/tokyo.omp.json" | Invoke-Expression
```

---

## 5. Zastosowanie zmian

Załaduj profil, aby zastosować zmiany bez konieczności restartu PowerShell:
```powershell
. $PROFILE
```

---

## Efekt

Po wykonaniu powyższych kroków, Twój prompt w PowerShell będzie spersonalizowany i dostosowany do wybranego motywu (w tym przypadku `tokyo.omp.json`).
