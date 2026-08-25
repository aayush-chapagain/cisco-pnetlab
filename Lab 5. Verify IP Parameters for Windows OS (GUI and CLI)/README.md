# Lab 5. Verify IP Parameters for Windows OS (GUI and CLI)

## Lab Objective
The objective of this lab is to provide hands-on practice configuring and verifying IP addressing under the Windows operating system, using both the GUI and the command line.

## Lab Purpose
Network engineers are often called on to walk end users through basic steps to find their IP configuration, DNS servers, default gateway, or routing table — or to configure a static IP directly. Verifying IP addressing at the client end is also a core troubleshooting skill. This lab covers viewing IP configuration, setting a static IP, viewing the local routing table, and releasing/renewing a DHCP lease.

## Lab Topology
This lab is performed directly on a Windows machine (physical or virtual) with a wired or wireless network connection — no PNETLab topology is required. If using a non-Windows OS, an online Windows environment (e.g. OnWorks) can be substituted.

## Task 1: Check IP Configuration (GUI and CLI)

**GUI:**
1. Open `Settings > Network & Internet > Status > Properties`, or run `ncpa.cpl` and right-click the active adapter → **Status** → **Details**.
2. Review the IPv4 address, subnet mask, default gateway, DNS servers, and MAC address.

**CLI:**
```
ipconfig /all
```
Returns everything shown in the GUI, plus adapter description, DHCP lease times, and DNS suffix.

## Task 2: Configure Static IP Address (GUI)

1. Run `ncpa.cpl`, right-click the adapter → **Properties**.
2. Select **Internet Protocol Version 4 (TCP/IPv4)** → **Properties**.
3. Choose **Use the following IP address** and enter:
   - IP address
   - Subnet mask
   - Default gateway
   - Preferred / alternate DNS server
4. Click **OK** → **OK** to apply.

A CLI alternative (`netsh interface ip set address`) exists and is documented in [commands.md](commands.md) for reference, but this task is completed via the GUI as specified.

## Task 3: View Windows Routing Table

**CLI:**
```
route print
```
or the PowerShell equivalent:
```
Get-NetRoute
```
The IPv4 table is listed above the IPv6 table. A destination of `0.0.0.0` (mask `0.0.0.0`) is the default route; all other entries are specific routes.

## Task 4: Refresh and Renew IP Address

**CLI:**
```
ipconfig /release
ipconfig /renew
```
Related commands worth knowing: `ipconfig /flushdns` (clears the local DNS resolver cache) and `ipconfig /displaydns` (shows cached DNS entries).

## Notes
- Static IP configuration and `netsh` commands that change adapter settings require an elevated (Administrator) Command Prompt.
- After completing Task 2/4 testing, revert the adapter to DHCP (`netsh interface ip set address name="<Adapter>" dhcp`) to restore normal connectivity.

## Files
- [Commands reference](commands.md)

## Status
✅ Done
