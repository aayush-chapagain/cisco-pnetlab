
## Lab Objective
Learn how to configure and troubleshoot IPv4 addressing on Cisco routers.

## Lab Purpose
IPv4 addressing is one of the most fundamental skills for a Cisco engineer. The CCNA exam may also test the ability to troubleshoot an inc
orrectly configured IPv4 address, so knowing the right `show` commands to diagnose issues is essential.

## Lab Topology
![Topology](topology.png)

| Interface   | IP Address     |
|-------------|----------------|
| Loopback10  | 10.10.10.3/25  |
| Loopback20  | 10.20.20.3/28  |
| Loopback30  | 10.30.30.3/29  |

- R1 S0/0 (DCE): `172.16.1.1/26`
- R3 S0/0: `172.16.1.2/26`

## Tasks

### Task 1
Configure the hostnames on R1 and R3 as shown in the topology.
:

