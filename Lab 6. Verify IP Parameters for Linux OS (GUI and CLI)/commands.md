# Lab 6 — Command Reference

## Task 1: Check IP Configuration

```
ip addr show
ip a
ifconfig -a                    # legacy, net-tools package
nmcli device show
nmcli device status            # quick per-device summary
```

## Task 2: Configure Static IP

> Commands below require root/`sudo`. Replace `eth0` / `"Wired connection 1"` with your actual interface/connection name (check with `ip a` or `nmcli con show`).

**NetworkManager (persistent):**
```
nmcli con mod "Wired connection 1" ipv4.addresses 192.168.1.50/24
nmcli con mod "Wired connection 1" ipv4.gateway 192.168.1.1
nmcli con mod "Wired connection 1" ipv4.dns "8.8.8.8 8.8.4.4"
nmcli con mod "Wired connection 1" ipv4.method manual
nmcli con up "Wired connection 1"
```

**`ip` command (immediate, non-persistent):**
```
sudo ip addr add 192.168.1.50/24 dev eth0
sudo ip route add default via 192.168.1.1
```

**Revert to DHCP:**
```
nmcli con mod "Wired connection 1" ipv4.method auto
nmcli con up "Wired connection 1"
```

**Verify:**
```
ip addr show
nmcli device show
```

## Task 3: View Routing Table

```
ip route
ip r
route -n                       # legacy, net-tools package
netstat -rn                    # legacy, net-tools package
```

## Task 4: Refresh and Renew IP Address

**NetworkManager:**
```
nmcli con down "Wired connection 1"
nmcli con up "Wired connection 1"
```

**dhclient (non-NetworkManager / server distros):**
```
sudo dhclient -r eth0
sudo dhclient eth0
```

**systemd-networkd (if used instead of NetworkManager):**
```
sudo networkctl renew eth0
```
