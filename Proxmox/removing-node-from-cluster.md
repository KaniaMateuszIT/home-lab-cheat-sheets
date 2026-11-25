# ➖ Usuwanie węzła z klastra Proxmox

> **Do czego:** trwałe usunięcie węzła (tu: `pve3`) z klastra – np. po awarii albo wymianie sprzętu.
> **Wykonuj na:** dowolnym **pozostającym** węźle klastra.

## TL;DR

```bash
# węzeł pve3 wyłączony na stałe
pvecm delnode pve3
rm -r /etc/pve/nodes/pve3        # po upewnieniu się, że nic z niego nie jest potrzebne
```

---

## Sposób standardowy – `pvecm delnode`

1. **Przenieś** z `pve3` maszyny i kontenery (albo zrób ich kopie).
2. **Wyłącz** `pve3` – i nie włączaj go ponownie w tej samej sieci z tą samą konfiguracją.
3. Na innym węźle:

   ```bash
   pvecm nodes            # sprawdź nazwę węzła
   pvecm delnode pve3
   ```

4. Usuń pozostały katalog z konfiguracją węzła (wcześniej zrób kopię):

   ```bash
   cp -a /etc/pve/nodes /root/nodes_backup
   rm -r /etc/pve/nodes/pve3
   ```

## Sposób ręczny – gdy `delnode` nie działa

1. **Kopia zapasowa:**

   ```bash
   cp -a /etc/pve/nodes /root/nodes_backup
   cp /etc/pve/corosync.conf /root/corosync.conf.bak
   ```

2. **Usuń katalog węzła:**

   ```bash
   rm -r /etc/pve/nodes/pve3
   ```

3. **Edytuj `corosync.conf`:**

   ```bash
   nano /etc/pve/corosync.conf
   ```

   - usuń cały blok węzła:

     ```text
     node {
         name: pve3
         nodeid: 3
         quorum_votes: 1
         ring0_addr: 192.168.0.3
     }
     ```

   - w sekcji `totem` **zwiększ `config_version` o 1** – inaczej zmiana nie rozejdzie się po klastrze.

4. **Odśwież certyfikaty i corosync:**

   ```bash
   pvecm updatecerts
   systemctl restart corosync
   ```

5. **Sprawdź:**

   ```bash
   pvecm status
   ```

---

## Uwagi

- **Brak kworum** (np. został jeden węzeł z dwóch) i `/etc/pve` jest tylko do odczytu? Tymczasowo: `pvecm expected 1`.
- Po usunięciu węzła mogą zostać „duchy” w HA i replikacji:
  - [removing-orphaned-ha-state.md](removing-orphaned-ha-state.md)
  - [removing-orphaned-replication-jobs.md](removing-orphaned-replication-jobs.md)

## Źródła

- [Proxmox VE – Cluster Manager, Remove a Cluster Node](https://pve.proxmox.com/wiki/Cluster_Manager#_remove_a_cluster_node)

---

[← Spis treści](../README.md)
