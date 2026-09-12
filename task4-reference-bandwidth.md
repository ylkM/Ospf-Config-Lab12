# Task 4 — Reference Bandwidth

By default OSPF cost = `100,000,000 / bandwidth (bps)`, using a reference bandwidth of 100 Mbps. That makes every interface faster than FastEthernet (100 Mbps) — like GigabitEthernet — compute to the same cost of 1, which under-represents faster links.

To make a FastEthernet interface land on a cost of **100** instead of 1, raise the reference bandwidth to 10 Gbps (10,000 Mbps):

```
router ospf 1
 auto-cost reference-bandwidth 10000
```

Cost check: `10,000 Mbps / 100 Mbps = 100`. ✅

This must be configured identically on **every** router in the OSPF domain (R1–R4) — a mismatched reference bandwidth between routers causes inconsistent path-cost calculations across the network (Cisco IOS will warn about this on mismatch).

## Verify

```
show ip ospf | include reference
show ip ospf interface FastEthernet1/0 | include cost
```

`FastEthernet` interfaces should show a cost of `100`; `GigabitEthernet` interfaces should show a cost of `10` (10,000/1000).
