# Proxmox QDevice - Konfiguracja dla klastra 2-węzłowego

Proxmox QDevice to narzędzie umożliwiające zwiększenie dostępności klastra w konfiguracji dwuwęzłowej. Dzięki QDevice klaster może uniknąć problemów z kworum w przypadku awarii jednego z węzłów.

---

## Przewodnik konfiguracji

1. **Utwórz klaster Proxmox:**

   Jeśli jeszcze nie masz klastra, utwórz go na jednym z węzłów:
   ```bash
   pvecm create <cluster-name>
   ```

   Następnie dołącz drugi węzeł do klastra:
   ```bash
   pvecm add <IP-węzła-klastra>
   ```

2. **Zainstaluj pakiet corosync-qdevice na wszystkich serwerach Proxmox:**

   Jeśli jeszcze nie masz klastra, utwórz go na jednym z węzłów:
   ```bash
   apt update
   apt install corosync-qdevice
   ```

3. **Zainstaluj Proxmox QDevice:**

   Na obu węzłach zainstaluj pakiet `corosync-qdevice`:
   ```bash
   apt update
   apt install corosync-qdevice
   ```

4. **Zainstaluj `corosync-qnetd` na serwerze QDevice:**

   Na serwerze zdalnym zainstaluj pakiet `corosync-qnetd`, który obsługuje QDevice:
   ```bash
   apt update
   apt install corosync-qnetd
   ```

   Uruchom `corosync-qnetd`:
   ```bash
   systemctl start corosync-qnetd
   systemctl enable corosync-qnetd
   ```

5. **Dodaj QDevice do klastra:**

   Na głównym węźle klastra dodaj QDevice:
   ```bash
   pvecm qdevice setup 192.168.1.100
   ```

   - `192.168.1.100`: Adres IP serwera QDevice.

6. **Weryfikacja konfiguracji:**

   Sprawdź stan klastra, aby upewnić się, że QDevice działa poprawnie:
   ```bash
   pvecm status
   ```

---

## Korzyści z użycia QDevice

- **Redundancja:** Pozwala uniknąć sytuacji, w której klaster traci kworum w przypadku awarii jednego węzła.
- **Prosta konfiguracja:** Wymaga jedynie serwera z systemem Linux jako QDevice.

---

## Przykładowe źródło
Pełny przewodnik dostępny jest na stronie [WunderTech](https://www.wundertech.net/how-to-create-a-2-node-cluster-in-proxmox/).
