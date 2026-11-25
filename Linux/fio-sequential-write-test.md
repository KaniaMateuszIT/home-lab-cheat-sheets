# 📊 FIO – test zapisu sekwencyjnego dysku

> **Do czego:** pomiar prędkości zapisu dysku (MB/s, IOPS, opóźnienia), np. przed wrzuceniem go do NAS-a albo puli ZFS.
> **Wymaga:** `sudo apt install fio`

## TL;DR

```bash
fio --name=seq_write --ioengine=libaio --rw=write --bs=1M --numjobs=1 --size=2G \
    --runtime=30 --time_based --direct=1 --filename=/mnt/testdisk/testfile
rm /mnt/testdisk/testfile
```

---

## Parametry

| Parametr | Znaczenie |
|---|---|
| `--name=seq_write` | nazwa testu |
| `--ioengine=libaio` | asynchroniczne wejście/wyjście Linuksa |
| `--rw=write` | zapis sekwencyjny |
| `--bs=1M` | blok 1 MB |
| `--numjobs=1` | jeden wątek |
| `--size=2G` | plik testowy 2 GB |
| `--runtime=30` + `--time_based` | test trwa 30 s (plik jest zapisywany w kółko) |
| `--direct=1` | z pominięciem pamięci podręcznej systemu – mierzy dysk, a nie RAM |
| `--filename=...` | plik testowy **na testowanym dysku** |

## Wynik

W podsumowaniu interesują Cię:

- `bw=` – przepustowość (MB/s),
- `IOPS=` – operacje na sekundę,
- `lat` – opóźnienia.

## Inne warianty

| Test | Zmień |
|---|---|
| odczyt sekwencyjny | `--rw=read` |
| losowy zapis 4K (bazy danych, VM) | `--rw=randwrite --bs=4k --iodepth=32` |
| losowy odczyt 4K | `--rw=randread --bs=4k --iodepth=32` |

---

## Uwagi

- Potrzebujesz prawa zapisu w `/mnt/testdisk/` i co najmniej 2 GB wolnego miejsca.
- **Nie** podawaj jako `--filename` samego urządzenia (np. `/dev/sdb`) – test zapisu nadpisze dane na dysku.
- Po teście usuń plik testowy.

---

[← Spis treści](../README.md)
