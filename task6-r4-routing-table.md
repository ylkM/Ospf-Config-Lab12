# Task 6 — Check R4's Routing Table

## Command

```
R4# show ip route
```

## What to look for

R4 is three hops from R1 through the OSPF domain, so it learns the default route as an **OSPF External Type 2 (O*E2)** route rather than a locally originated static route:

```
O*E2  0.0.0.0/0 [110/1] via 10.0.24.1, 00:xx:xx, FastEthernet1/0
```

- `O*E2` — the `*` marks it as a candidate default route; `E2` means the cost shown is only the **external** cost as set on the ASBR (R1), and does not accumulate the internal OSPF cost of the path back to R1 (that's the difference between E1 and E2 external routes — E2 is the default type used by `default-information originate`).
- The next hop is R1's directly reachable neighbor from R4's perspective — since R2 and R3 are equal-cost paths back toward R1, you may see the default route reachable via either FastEthernet1/0 (through R2) or FastEthernet2/0 (through R3), or both, depending on ECMP.

## Fill in from your own lab run

```
<paste your `show ip route` output for R4 here>
```

**Answer:** _One_ default route (`0.0.0.0/0`) is added to R4's table, learned as an `O*E2` external OSPF route with R1 (`1.1.1.1`) as the originating ASBR. If R1's ASBR router-id shows in `show ip ospf database external`, that confirms R1 as the source.
