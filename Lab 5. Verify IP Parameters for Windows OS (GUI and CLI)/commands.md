# Lab 5 — Command Reference

## Task 1: Check IP Configuration

```
ipconfig /all
```

PowerShell alternative:
```
Get-NetAdapter | Select-Object Name, Status, InterfaceDescription
```

List interface names/status (useful before running netsh commands):
```
netsh interface show interface
netsh interface ip show config
```

## Task 2: Configure Static IP (CLI alternative to GUI)

> Requires an elevated (Administrator) Command Prompt.

```
# Set static IP + subnet mask + gateway
netsh interface ip set address name="Ethernet" static 192.168.1.50 255.255.255.0 192.168.1.1

# Set primary DNS (wipes existing DNS entries)
netsh interface ip set dns name="Ethernet" static 8.8.8.8

# Add secondary DNS
netsh interface ip add dns name="Ethernet" 8.8.4.4 index=2
```

Revert back to DHCP:
```
netsh interface ip set address name="Ethernet" dhcp
netsh interface ip set dns name="Ethernet" dhcp
```

Verify:
```
ipconfig /all
```

## Task 3: View Routing Table

```
route print
```

PowerShell alternative:
```
Get-NetRoute
```

## Task 4: Refresh and Renew IP Address

```
ipconfig /release
ipconfig /renew
```

Related:
```
ipconfig /flushdns
ipconfig /displaydns
```
