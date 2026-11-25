# 👻 Proxmox – osierocony stan HA po usunięciu węzła

> **Do czego:** usunięty (albo przemianowany) węzeł wciąż widnieje w HA – w GUI i w `ha-manager status`.

Typowe objawy:

```text
master pve4 (idle, Tue Jul 14 15:57:44 2026)
lrm pve4 (unable to read lrm status)
unable to read file '/etc/pve/nodes/pve4/lrm_status'
```

Węzeł zniknął z klastra, ale HA dalej czyta stary plik `manager_status`.

## TL;DR

```bash
# na KAŻDYM węźle
systemctl stop pve-ha-lrm pve-ha-crm
# na JEDNYM węźle
rm -f /etc/pve/ha/manager_status
# na KAŻDYM węźle
systemctl start pve-ha-lrm pve-ha-crm
ha-manager status
```

---

## Kroki

1. **Zatrzymaj usługi HA na wszystkich węzłach**

   ```bash
   systemctl stop pve-ha-lrm
   systemctl stop pve-ha-crm
   ```

2. **Usuń zapisany stan HA** (na jednym węźle – `/etc/pve` jest wspólny dla klastra)

   ```bash
   rm -f /etc/pve/ha/manager_status
   ```

3. **Uruchom usługi HA na wszystkich węzłach**

   ```bash
   systemctl start pve-ha-lrm
   systemctl start pve-ha-crm
   ```

4. **Odczekaj kilkanaście sekund** – HA sam odbuduje stan.

5. **Sprawdź**

   ```bash
   ha-manager status
   ```

## Efekt

Wpisy `master pve4`, `lrm pve4` i `unable to read lrm status` znikają, a stan HA jest odbudowany na podstawie aktualnych węzłów.

---

## Uwagi

- Na czas zatrzymania usług HA nie pilnuje maszyn – rób to, gdy klaster jest sprawny.
- Powiązane: [removing-node-from-cluster.md](removing-node-from-cluster.md), [removing-orphaned-replication-jobs.md](removing-orphaned-replication-jobs.md).

---

[← Spis treści](../README.md)
