# Task 5 — R1 as ASBR: Advertise a Default Route into OSPF

R1 sits between the OSPF domain and ISPR1. It needs a route to the outside world, and it needs to tell the rest of the OSPF domain "send your unknown/external traffic to me."

## Step 1 — Give R1 a way out

```
ip route 0.0.0.0 0.0.0.0 203.0.113.2
```

## Step 2 — Originate the default into OSPF

```
router ospf 1
 default-information originate
```

This only advertises the default if R1 already has one in its own routing table. If you want R1 to advertise it unconditionally (even without its own working default), add `always`:

```
router ospf 1
 default-information originate always
```

This lab uses the conditional form (no `always`), since R1 genuinely has a static default route pointing at the ISP.

## Verify

```
show ip route | include Gateway
show ip ospf database external
```

On R1 you should see `ip ospf database` list a Type-5 LSA for `0.0.0.0/0` originated by R1 (router-id `1.1.1.1`).
