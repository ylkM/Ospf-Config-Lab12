# Task 1 — Hostnames, IP Addressing, and Enabling Interfaces

Configure the hostname and interface IP addresses on R1, R2, R3, and R4, then bring each interface up. ISPR1 is left unconfigured.

## Commands (pattern used on every router)

```
enable
configure terminal
hostname <name>
!
interface <type><number>
 description <link description>
 ip address <address> <mask>
 no shutdown
```

## Addressing Table

| Device | Interface | IP Address | Connects To |
|---|---|---|---|
| ISPR1 | Gig0/0/0 | 203.0.113.2/30 | R1 Gig3/0 |
| R1 | Gig3/0 | 203.0.113.1/30 | ISPR1 |
| R1 | Gig0/0 | 10.0.12.1/30 | R2 Gig0/0 |
| R1 | Fa1/0 | 10.0.13.1/30 | R3 Fa1/0 |
| R2 | Gig0/0 | 10.0.12.2/30 | R1 Gig0/0 |
| R2 | Fa1/0 | 10.0.24.1/30 | R4 Fa1/0 |
| R3 | Fa1/0 | 10.0.13.2/30 | R1 Fa1/0 |
| R3 | Fa2/0 | 10.0.34.1/30 | R4 Fa2/0 |
| R4 | Fa1/0 | 10.0.24.2/30 | R2 Fa1/0 |
| R4 | Fa2/0 | 10.0.34.2/30 | R3 Fa2/0 |
| R4 | Gig0/0 | 192.168.4.254/24 | LAN Switch |
| PC | NIC | 192.168.4.1/24 | Switch Fa0/1 |

See `configs/R1.txt` – `configs/R4.txt` for the full interface blocks.

## Verify

```
show ip interface brief
show cdp neighbors
```

Every interface that should be up should show `up / up`, and each router should see the expected directly connected neighbor via CDP.
