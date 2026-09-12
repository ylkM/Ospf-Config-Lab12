# Task 2 — Loopback Interfaces

Each router gets a `/32` loopback used as a stable router ID and for OSPF testing.

## Commands

```
interface Loopback0
 ip address <x.x.x.x> 255.255.255.255
```

| Router | Loopback |
|---|---|
| R1 | 1.1.1.1/32 |
| R2 | 2.2.2.2/32 |
| R3 | 3.3.3.3/32 |
| R4 | 4.4.4.4/32 |

## Verify

```
show ip interface brief | include Loopback
```

Loopback interfaces come up as soon as they're created (no `no shutdown` needed) and stay up as long as the router is running.
