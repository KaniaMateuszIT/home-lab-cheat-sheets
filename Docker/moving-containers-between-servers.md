# Przenoszenie kontenerów Docker pomiędzy serwerami

Poniżej przedstawiono kroki umożliwiające przenoszenie danych kontenerów Docker pomiędzy serwerami. Proces obejmuje utworzenie kopii zapasowej danych, przesłanie jej na nowy serwer oraz przywrócenie danych.

---

## Tworzenie kopii zapasowej danych kontenera

1. **Utwórz archiwum danych kontenera:**
   Użyj poniższego polecenia, aby stworzyć kopię danych z konkretnej lokalizacji w kontenerze:
   ```bash
   docker run --rm --volumes-from <container> -v $(pwd):/backup busybox tar cvfz /backup/backup.tar.gz <container-path>
   ```
   Przykłady:
   - Dla kontenera `adguard-home` i ścieżki `/app/pb_data`:
     ```bash
     sudo docker run --rm --volumes-from adguard-home -v $(pwd):/backup busybox tar cvfz /backup/backup.tar.gz /app/pb_data
     ```
   - Dla kontenera `adguard-home` i wielu ścieżek (`/opt/adguardhome/conf` oraz `/opt/adguardhome/work`):
     ```bash
     sudo docker run --rm --volumes-from adguard-home -v $(pwd):/backup busybox tar cvfz /backup/backup.tar.gz /opt/adguardhome/conf /opt/adguardhome/work
     ```

---

## Przesyłanie kopii zapasowej na nowy serwer

1. **Prześlij plik kopii zapasowej na nowy serwer:**
   Użyj polecenia `scp`, aby przesłać plik na zdalny serwer:
   ```bash
   scp -v /backup.tar.gz mateusz@192.168.1.200:/home/mateusz/
   ```

   W powyższym przykładzie:
   - `/backup.tar.gz` to lokalizacja kopii zapasowej.
   - `mateusz@192.168.1.200` to użytkownik i adres IP zdalnego serwera.
   - `/home/mateusz/` to lokalizacja docelowa na serwerze.

---

## Przywracanie danych na nowym serwerze

1. **Rozpakowanie danych w kontenerze:**
   Użyj poniższego polecenia, aby przywrócić dane w kontenerze na nowym serwerze:
   ```bash
   docker run --rm --volumes-from <container> -v $(pwd):/backup busybox sh -c "cd <container-path> && tar xvfz /backup/backup.tar.gz --strip 1"
   ```
   Przykład:
   - Dla kontenera `upsnap` i ścieżki `/app/pb_data`:
     ```bash
     sudo docker run --rm --volumes-from upsnap -v $(pwd):/backup busybox sh -c "cd /app/pb_data && tar xvfz /backup/backup.tar.gz --strip 2"
     ```

---

## Uwagi

- **Parametr `--volumes-from`:** Pozwala na dostęp do wolumenu innego kontenera.
- **Parametr `--strip`:** Określa liczbę poziomów katalogów do pominięcia podczas rozpakowywania.
- **`scp`:** Używany do transferu plików pomiędzy serwerami.

Proces ten pozwala na łatwe przeniesienie danych kontenerów Docker pomiędzy serwerami, zachowując ich integralność.
