# 🔁 Proxmox – osierocone zadania replikacji

> **Do czego:** po usunięciu węzła zostały zadania replikacji, których nie da się usunąć z GUI, a w logach pojawia się:

```text
hostname lookup 'pve1' failed - failed to get address info for: pve1: Name or service not known
```

## TL;DR

```bash
pvesr list
pvesr delete 104-0 --force      # gdy zwykłe delete nie pomaga
# ostateczność: usuń blok zadania z /etc/pve/replication.cfg
```

---

## Kroki

1. **Spróbuj z GUI:** `VM/CT → Replication` → zaznacz zadanie → **Remove**.

2. **Nie znika? Z wiersza poleceń:**

   ```bash
   pvesr list                 # lista zadań i ich ID
   pvesr delete <JobID>       # np. pvesr delete 104-0
   ```

   Zwykłe `delete` próbuje posprzątać repliki na węźle docelowym – a ten już nie istnieje. Wtedy pomoże:

   ```bash
   pvesr delete 104-0 --force
   ```

3. **Nadal jest? Ręcznie z konfiguracji:**

   ```bash
   nano /etc/pve/replication.cfg
   ```

   Usuń cały blok zadania, np.:

   ```text
   local: 104-0
           target pve1
           remove_job full
           schedule */30
           source vesemir
   ```

4. **Przeładuj usługi:**

   ```bash
   systemctl restart pvescheduler
   systemctl reload pvedaemon
   ```

5. **Sprawdź:**

   ```bash
   pvesr list
   ```

## Efekt

Osierocone zadania znikają z konfiguracji i nie generują błędów w harmonogramie.

---

## Uwagi

- Powiązane: [removing-node-from-cluster.md](removing-node-from-cluster.md), [removing-orphaned-ha-state.md](removing-orphaned-ha-state.md).

---

[← Spis treści](../README.md)
