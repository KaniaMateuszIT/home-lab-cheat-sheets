# Usuwanie osieroconych zadań replikacji w Proxmox

Czasami po usunięciu węzła z klastra zadania replikacji pozostają w konfiguracji i nie da się ich usunąć z poziomu GUI. W logach pojawia się błąd podobny do:

```
hostname lookup 'pve1' failed - failed to get address info for: pve1: Name or service not known
```

## Kroki

1. **Spróbuj usunąć zadanie z poziomu GUI**

   Przejdź do:

   ```
   CT/VM → Replication
   ```

   Zaznacz zadanie i kliknij **Remove**.

2. **Jeżeli zadanie nie znika, spróbuj usunąć je z CLI**

   Wyświetl listę zadań:

   ```bash
   pvesr list
   ```

   Usuń wybrane zadanie:

   ```bash
   pvesr delete <JobID>
   ```

   Przykład:

   ```bash
   pvesr delete 104-0
   ```

3. **Jeżeli zadanie nadal pozostaje, usuń je ręcznie z konfiguracji**

   Otwórz plik:

   ```bash
   nano /etc/pve/replication.cfg
   ```

   Usuń cały blok odpowiadający zadaniu, np.:

   ```
   local: 104-0
           target pve1
           remove_job full
           schedule */30
           source vesemir
   ```

4. **Przeładuj usługi Proxmox**

   ```bash
   systemctl reload pvescheduler
   systemctl reload pvedaemon
   ```

5. **Sprawdź, czy zadanie zostało usunięte**

   ```bash
   pvesr list
   ```

## Efekt

Po wykonaniu powyższych kroków osierocone zadania replikacji zostaną usunięte z konfiguracji i nie będą już generować błędów w harmonogramie.
