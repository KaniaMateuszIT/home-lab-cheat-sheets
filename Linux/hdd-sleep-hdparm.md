# 💤 Usypianie dysków HDD (`hdparm`)

> **Do czego:** sprawdzanie, czy dysk śpi, usypianie go od razu albo po czasie bezczynności – ciszej i mniej prądu w serwerze.
> **Wymaga:** `sudo apt install hdparm smartmontools`

## TL;DR

```bash
lsblk                                   # jakie dyski są w systemie
sudo hdparm -C /dev/sdX                 # stan: active/idle albo standby
sudo hdparm -Y /dev/sdX                 # uśpij teraz
sudo hdparm -S 120 /dev/disk/by-id/ata-<MODEL>_<SERIAL>   # usypiaj po 10 min bezczynności
```

---

## 1. Lista dysków

```bash
lsblk
ls -l /dev/disk/by-id/ | grep -v part   # stałe nazwy dysków (model + numer seryjny)
```

Do ustawień na stałe używaj ścieżek z `/dev/disk/by-id/` – `sda`/`sdb` mogą się zamienić po restarcie.

## 2. Stan dysku

```bash
sudo hdparm -C /dev/sdX
```

| Wynik | Znaczenie |
|---|---|
| `active/idle` | dysk się kręci |
| `standby` | dysk śpi |

## 3. Usypianie

**Od razu:**

```bash
sudo hdparm -Y /dev/sdX
```

**Po czasie bezczynności (`-S`):**

```bash
sudo hdparm -S 12 /dev/disk/by-id/ata-<MODEL>_<SERIAL>
```

| Wartość `-S` | Czas |
|---|---|
| `0` | nigdy nie usypiaj |
| `1`–`240` | wartość × 5 s (`12` = 1 min, `120` = 10 min, `240` = 20 min) |
| `241`–`251` | (wartość − 240) × 30 min (`242` = 1 h) |

**Na stałe** – dopisz do `/etc/hdparm.conf`:

```text
/dev/disk/by-id/ata-<MODEL>_<SERIAL> {
    spindown_time = 120
}
```

## 4. SMART a usypianie

Monitorowanie SMART potrafi co chwilę budzić dysk. Zamiast wyłączać SMART, każ `smartd` pomijać śpiące dyski – w `/etc/smartd.conf` dodaj `-n standby`:

```text
DEVICESCAN -a -n standby,q
```

```bash
sudo systemctl restart smartd
```

Wyłączenie SMART na dysku (ostateczność – tracisz ostrzeżenia o awarii):

```bash
sudo smartctl -s off /dev/disk/by-id/ata-<MODEL>_<SERIAL>
```

---

## Uwagi

- Częste usypianie i budzenie zużywa mechanikę dysku – nie ustawiaj bardzo krótkich czasów na dyskach, które są często używane.
- Dysk w RAID/ZFS albo z aktywnym serwisem (np. indeksowanie, Docker) i tak może się budzić – sprawdź `hdparm -C` po kilku minutach.

---

[← Spis treści](../README.md)
