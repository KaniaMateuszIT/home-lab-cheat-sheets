# Zarządzanie dyskami w systemie Linux

Poniżej przedstawiono zestaw poleceń do zarządzania dyskami w systemie Linux, w tym sprawdzanie stanu dysków oraz ich usypianie.

---

## 1. **Lista dysków (lsblk)**

Wyświetlenie listy dysków i ich układu:
```bash
lsblk
```

---

## 2. **Sprawdzanie stanu dysku**

Aby sprawdzić aktualny stan dysku (np. czy jest aktywny, czy w trybie uśpienia), użyj polecenia:
```bash
sudo hdparm -C /dev/sdX
```
- Zamień `sdX` na odpowiedni identyfikator dysku (np. `sda`).

---

## 3. **Usypianie dysku**

### Natychmiastowe usypianie
Aby natychmiast uśpić dysk, użyj:
```bash
sudo hdparm -Y /dev/sdX
```
- `sdX`: Identyfikator dysku.

### Automatyczne usypianie
Aby skonfigurować czas bezczynności, po którym dysk zostanie uśpiony, użyj:
```bash
sudo hdparm -S 12 /dev/disk/by-id/ata-TOSHIBA_HDWD110_88SZMK7MS
```
- `-S 12`: Określa czas bezczynności w jednostkach (12 = 1 minuta).
- `/dev/disk/by-id/ata-TOSHIBA_HDWD110_88SZMK7MS`: Ścieżka do konkretnego dysku.

---

## 4. **Wyłączenie SMART**

Aby wyłączyć monitoring SMART na dysku:
```bash
sudo smartctl -s off /dev/disk/by-id/ata-TOSHIBA_HDWD110_88SZMK7MS
```
- `/dev/disk/by-id/ata-TOSHIBA_HDWD110_88SZMK7MS`: Ścieżka do konkretnego dysku.

---

## Uwagi:
- Upewnij się, że masz odpowiednie uprawnienia administracyjne (np. używając `sudo`).
- Zawsze sprawdzaj ścieżki do dysków (`lsblk` lub `ls /dev/disk/by-id/`), aby uniknąć błędów.
- Funkcje takie jak usypianie i wyłączanie SMART mogą wpływać na wydajność i żywotność dysku.
