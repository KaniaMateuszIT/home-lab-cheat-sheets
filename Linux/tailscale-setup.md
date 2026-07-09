# Tailscale – konfiguracja jako Exit Node i Subnet Router (Proxmox VE 9)

Poniżej przedstawiono konfigurację Tailscale na **Proxmox VE 9 (Debian 13 Trixie)**, umożliwiającą:

- działanie jako **Exit Node**,
- udostępnianie sieci lokalnych (**Subnet Router**).

---

## 1. Instalacja Tailscale

Zainstaluj najnowszą wersję Tailscale:

```bash
curl -fsSL https://tailscale.com/install.sh | sh
```

---

## 2. Włącz przekazywanie pakietów (IP Forwarding)

Utwórz dedykowany plik konfiguracyjny:

```bash
cat >/etc/sysctl.d/99-tailscale.conf <<EOF
net.ipv4.ip_forward = 1
net.ipv6.conf.all.forwarding = 1
EOF
```

Załaduj nową konfigurację:

```bash
sysctl --system
```

Zweryfikuj ustawienia:

```bash
sysctl net.ipv4.ip_forward
sysctl net.ipv6.conf.all.forwarding
```

Oba polecenia powinny zwrócić:

```text
net.ipv4.ip_forward = 1
net.ipv6.conf.all.forwarding = 1
```

---

## 3. Zaloguj urządzenie do Tailscale

```bash
tailscale up
```

Po wykonaniu polecenia otworzy się link do logowania w przeglądarce.

---

## 4. Włącz Exit Node oraz Subnet Router

Uruchom:

```bash
tailscale up \
  --advertise-exit-node \
  --advertise-routes=192.168.1.0/24,192.168.10.0/24,192.168.50.0/24
```

> Dostosuj adresy sieci do swojej konfiguracji.

### Parametry

- `--advertise-exit-node` – udostępnia serwer jako Exit Node.
- `--advertise-routes` – udostępnia wskazane sieci lokalne innym urządzeniom w Tailscale.

---

## 5. Zatwierdź w panelu administracyjnym

Po wykonaniu powyższego polecenia zaloguj się do panelu administracyjnego Tailscale i zaakceptuj:

- ✅ Exit Node
- ✅ Advertised Routes

Do momentu ich zatwierdzenia funkcje nie będą dostępne dla innych urządzeń.

---

## Efekt

Po wykonaniu wszystkich kroków serwer będzie:

- działał jako **Exit Node**,
- udostępniał sieci:
  - `192.168.1.0/24`
  - `192.168.10.0/24`
  - `192.168.50.0/24`
- przekazywał ruch IPv4 oraz IPv6.

Konfiguracja jest zgodna z Proxmox VE 9 (Debian 13 Trixie) i aktualnymi zaleceniami Tailscale.
