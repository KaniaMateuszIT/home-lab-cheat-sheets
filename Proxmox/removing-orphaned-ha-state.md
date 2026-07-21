# Czyszczenie osieroconego stanu HA po usunięciu węzła z klastra Proxmox

Po usunięciu lub zmianie nazwy węzła w klastrze Proxmox może się zdarzyć, że system HA nadal przechowuje jego stary stan. W GUI lub w wyniku polecenia `ha-manager status` mogą pojawić się wpisy podobne do:

```text
master pve4 (idle, Tue Jul 14 15:57:44 2026)
lrm pve4 (unable to read lrm status)
unable to read file '/etc/pve/nodes/pve4/lrm_status'
```

Mimo że węzeł został poprawnie usunięty z klastra, HA nadal korzysta ze starego pliku `manager_status`.

## Kroki

1. **Zatrzymaj usługi HA na wszystkich węzłach klastra**

   Na każdym węźle wykonaj:

   ```bash
   systemctl stop pve-ha-lrm
   systemctl stop pve-ha-crm
   ```

2. **Usuń zapisany stan HA**

   Na jednym z węzłów usuń plik:

   ```bash
   rm -f /etc/pve/ha/manager_status
   ```

3. **Uruchom ponownie usługi HA**

   Na każdym węźle wykonaj:

   ```bash
   systemctl start pve-ha-lrm
   systemctl start pve-ha-crm
   ```

4. **Poczekaj kilkanaście sekund**

   HA automatycznie odbuduje swój stan.

5. **Sprawdź status HA**

   ```bash
   ha-manager status
   ```

## Efekt

Po wykonaniu powyższych kroków stary wpis dotyczący usuniętego węzła zniknie. W wyniku polecenia `ha-manager status` nie powinny już pojawiać się wpisy typu:

```text
master pve4
lrm pve4
unable to read lrm status
```

Stan HA zostanie odbudowany na podstawie aktualnych węzłów klastra.
