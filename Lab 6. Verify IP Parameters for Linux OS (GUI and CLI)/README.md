# Lab 6. Verify IP Parameters for Linux OS (GUI and CLI)

## Lab Objective
The objective of this lab is to provide hands-on practice configuring and verifying IP addressing under Linux, using both the desktop GUI and the command line.

## Lab Purpose
Like Windows, Linux distributions ship with built-in commands for configuring IP addressing and troubleshooting TCP/IP settings. This lab covers viewing IP configuration, setting a static IP, viewing the local routing table, and releasing/renewing a DHCP lease.

## Lab Topology
This lab is performed directly on a Linux machine (physical or virtual) with a wired or wireless network connection — no PNETLab topology is required. If using a non-Linux OS, an online Linux environment (e.g. OnWorks) can be substituted. Steps below assume a NetworkManager-based distro (Ubuntu Desktop, Fedora, etc.); commands note the non-NetworkManager alternative where it differs.

## Task 1: Check IP Configuration (GUI and CLI)

**GUI:**
1. Open **Settings > Network**, click the gear/settings icon next to the active connection (Wired or Wi-Fi).
2. The **Details** / **IPv4** tab shows IP address, subnet mask, default gateway, DNS servers, and hardware (MAC) address.

**CLI:**
```
ip addr show
```
or shorthand:
```
ip a
```
Shows every interface, its IPv4/IPv6 addresses, and state (UP/DOWN). Legacy equivalent: `ifconfig -a` (from `net-tools`, not installed by default on newer distros).

For a NetworkManager-specific view (connection name, DNS, gateway in one place):
```
nmcli device show
```

## Task 2: Configure Static IP Address (GUI and CLI)

**GUI:**
1. Open **Settings > Network**, click the gear icon next to the active connection.
2. Go to the **IPv4** tab.
3. Change **IPv4 Method** from *Automatic (DHCP)* to **Manual**.
4. Enter Address, Netmask, and Gateway, plus DNS servers (toggle "Automatic" off for DNS to set them manually).
5. Click **Apply**, then toggle the connection off and on (or click the connection name in the top network menu) for it to take effect.

**CLI (NetworkManager — persistent, survives reboot):**
```
nmcli con mod "Wired connection 1" ipv4.addresses 192.168.1.50/24
nmcli con mod "Wired connection 1" ipv4.gateway 192.168.1.1
nmcli con mod "Wired connection 1" ipv4.dns "8.8.8.8 8.8.4.4"
nmcli con mod "Wired connection 1" ipv4.method manual
nmcli con up "Wired connection 1"
```

**CLI (`ip` command — immediate, does NOT survive reboot):**
```
sudo ip addr add 192.168.1.50/24 dev eth0
sudo ip route add default via 192.168.1.1
```

Full command syntax and the revert-to-DHCP steps are in [commands.md](commands.md).

## Task 3: View Linux Routing Table

**CLI:**
```
ip route
```
or:
```
ip r
```
Legacy equivalent:
```
route -n
```
The line starting `default via <gateway>` is the default route; all other lines are specific routes to directly connected or configured networks.

## Task 4: Refresh and Renew IP Address

**CLI (NetworkManager):**
```
nmcli con down "Wired connection 1"
nmcli con up "Wired connection 1"
```

**CLI (`dhclient`, on distros that use it):**
```
sudo dhclient -r eth0
sudo dhclient eth0
```

## Notes
- Interface names vary by distro/hardware (`eth0`, `enp0s3`, `ens33`, etc.) — confirm the exact name with `ip a` or `nmcli con show` before running any command that targets an interface by name.
- Commands that change routing or addressing (`ip addr add`, `ip route add`, `nmcli con mod`) require root or `sudo`.
- After testing Task 2/4, revert the connection to DHCP (`nmcli con mod "Wired connection 1" ipv4.method auto && nmcli con up "Wired connection 1"`) to restore normal connectivity.

## Files
- [Commands reference](commands.md)

## Status
✅ Done
