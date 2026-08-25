# Lab 7 — Command Reference (CLI alternative to GUI)

> The lab task is GUI-based; these are the CLI equivalents for reference, run in Terminal.

## Task 1: Check IP Configuration

```
ifconfig en0
```

List all interfaces:
```
ifconfig -a
```

Find which interface name maps to Wi-Fi/Ethernet:
```
networksetup -listallhardwareports
```

Full config (IP, subnet, router, DNS) for a named service:
```
networksetup -getinfo "Wi-Fi"
```

Just the current IP:
```
ipconfig getifaddr en0
```

## Task 2: Configure Static IP

> Requires `sudo`. Replace `"Wi-Fi"` with the exact service name from `networksetup -listallnetworkservices`.

```
sudo networksetup -setmanual "Wi-Fi" 192.168.1.50 255.255.255.0 192.168.1.1
sudo networksetup -setdnsservers "Wi-Fi" 8.8.8.8 8.8.4.4
```

Revert to DHCP:
```
sudo networksetup -setdhcp "Wi-Fi"
sudo networksetup -setdnsservers "Wi-Fi" empty
```

Verify:
```
networksetup -getinfo "Wi-Fi"
```

## Task 3: Renew IP Address

```
sudo ipconfig set en0 DHCP
```

Also useful:
```
sudo dscacheutil -flushcache      # flush DNS cache, equivalent of ipconfig /flushdns
```

## Bonus: Routing Table
```
netstat -rn
```
or:
```
route -n get default
```
