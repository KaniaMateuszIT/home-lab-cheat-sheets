# FIO - Test zapisu sekwencyjnego

Poniżej znajduje się przykład wykorzystania narzędzia FIO (Flexible I/O Tester) do przeprowadzenia testu zapisu sekwencyjnego na dysku.

---

## Polecenie

```bash
fio --name=seq_write --ioengine=libaio --rw=write --bs=1M --numjobs=1 --size=2G --runtime=30 --time_based --direct=1 --filename=/mnt/testdisk/testfile
```

---

## Wyjaśnienie parametrów

- `--name=seq_write`: Nazwa testu, w tym przypadku `seq_write`.
- `--ioengine=libaio`: Użycie silnika wejścia/wyjścia `libaio` (asynchroniczne operacje wejścia/wyjścia).
- `--rw=write`: Test typu `write`, czyli sekwencyjny zapis danych.
- `--bs=1M`: Wielkość bloku danych ustawiona na 1 MB.
- `--numjobs=1`: Liczba równoległych zadań ustawiona na 1 (pojedynczy wątek).
- `--size=2G`: Rozmiar pliku testowego wynosi 2 GB.
- `--runtime=30`: Test będzie trwał przez maksymalnie 30 sekund.
- `--time_based`: Włączenie trybu czasowego (test zakończy się po czasie określonym w `--runtime`).
- `--direct=1`: Operacje wejścia/wyjścia będą wykonywane bez buforowania w pamięci podręcznej systemu.
- `--filename=/mnt/testdisk/testfile`: Ścieżka do pliku testowego, który zostanie utworzony na testowanym dysku.

---

## Efekt

Po uruchomieniu polecenia narzędzie FIO stworzy plik testowy o rozmiarze 2 GB na ścieżce `/mnt/testdisk/testfile`, a następnie wykona test zapisu sekwencyjnego przez 30 sekund. Wyniki testu zostaną wyświetlone w terminalu, w tym:
- Przepustowość (MB/s).
- IOPS (operacje wejścia/wyjścia na sekundę).
- Opóźnienia.

**Uwaga:** Upewnij się, że masz odpowiednie uprawnienia do zapisu w lokalizacji `/mnt/testdisk/` oraz wystarczającą ilość wolnego miejsca na testowanym dysku.