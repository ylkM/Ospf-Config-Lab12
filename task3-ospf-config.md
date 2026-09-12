# Task 3 — Enable OSPF on Every Interface, Configure Passive Interfaces

## Enabling OSPF directly on the interface

Rather than a broad `network` statement using a wildcard mask that could accidentally sweep in unintended interfaces, each interface is enabled individually using its own /32 wildcard:

```
router ospf 1
 network <interface-ip> 0.0.0.0 area 0
```

This is done for every OSPF-participating interface on R1–R4 (see `configs/`).

> R1's link to ISPR1 (`203.0.113.0/30`) is **not** included in any `network` statement — it is outside the OSPF domain entirely and is handled by redistribution in Task 5, not OSPF itself.

## Passive interfaces

A passive interface still gets advertised into OSPF (so its subnet appears in the routing tables of every router) but **does not** send/receive Hellos or form a neighbor relationship on that interface. Use it on any interface that will never have another OSPF router attached:

| Router | Passive interface | Why |
|---|---|---|
| R1 | Loopback0 | Loopbacks never have neighbors |
| R2 | Loopback0 | Loopbacks never have neighbors |
| R3 | Loopback0 | Loopbacks never have neighbors |
| R4 | Loopback0 | Loopbacks never have neighbors |
| R4 | Gig0/0 | Faces the LAN switch/PC — no OSPF router there |

```
router ospf 1
 passive-interface Loopback0
 passive-interface GigabitEthernet0/0   ! R4 only
```

## Verify

```
show ip ospf interface brief
show ip protocols
show ip ospf neighbor
```

`show ip ospf interface brief` marks passive interfaces with `0` neighbors expected/possible; `show ip protocols` lists them explicitly under "Passive Interface(s)".
