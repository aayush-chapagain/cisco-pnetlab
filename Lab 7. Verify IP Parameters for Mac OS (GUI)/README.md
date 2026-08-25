# Lab 7. Verify IP Parameters for Mac OS (GUI)

## Lab Objective
The objective of this lab is to provide hands-on practice configuring and verifying IP addressing under macOS, using the GUI.

## Lab Purpose
Like Windows and Linux, macOS ships with built-in tools to configure and verify IP parameters. This lab covers viewing IP configuration, setting a static IP, and renewing a DHCP lease.

## Lab Topology
This lab is performed directly on a Mac (physical or virtual) with a wired or wireless network connection — no PNETLab topology is required. If using a non-macOS system, an online macOS environment (e.g. OnWorks) can be substituted.

## Task 1: Check IP Configuration (GUI)

1. Open **System Settings > Network** (on older macOS: **System Preferences > Network**).
2. Select the active connection (Wi-Fi or Ethernet) in the left-hand list.
3. Click **Details…** next to it (older macOS: click **Advanced…**).
4. Go to the **TCP/IP** tab to see IP address, subnet mask, and router (default gateway).
5. Go to the **DNS** tab to see configured DNS servers.
6. Go to the **Hardware** tab (under Details) to see the MAC address.

## Task 2: Configure Static IP Address (GUI)

1. **System Settings > Network**, select the active connection, click **Details…**.
2. Go to the **TCP/IP** tab.
3. Change **Configure IPv4** from *Using DHCP* to **Manually**.
4. Enter:
   - IP Address
   - Subnet Mask
   - Router (default gateway)
5. Go to the **DNS** tab and click **+** to add DNS server(s) manually.
6. Click **OK**, then **Apply**.

## Task 3: Renew IP Address (GUI)

1. **System Settings > Network**, select the active connection, click **Details…**.
2. Go to the **TCP/IP** tab.
3. Ensure **Configure IPv4** is set to **Using DHCP**.
4. Click **Renew DHCP Lease** (the button only appears when the connection is set to DHCP, not Manual).

A CLI alternative (`ifconfig` / `networksetup` / `ipconfig`) exists for all three tasks and is documented in [commands.md](commands.md) for reference, but this lab is completed via the GUI as specified.

## Notes
- Menu names differ slightly by macOS version (`System Settings` on macOS Ventura 13+, `System Preferences` on earlier versions) — the settings themselves are the same.
- After testing Task 2, switch **Configure IPv4** back to **Using DHCP** to restore normal connectivity.

## Files
- [Commands reference](commands.md)

## Status
✅ Done
