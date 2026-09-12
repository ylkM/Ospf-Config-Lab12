# Task 7 — Inspecting OSPF Hello Messages in Simulation Mode

## How to capture one

1. Switch to **Simulation** mode in Packet Tracer.
2. Filter the Event List to show only OSPF.
3. Click **Capture/Forward** until a Hello packet appears on one of the router-to-router links.
4. Click the envelope icon on the packet, then open the **OSPF** layer in the PDU details window.

## Fields present in the Hello packet

| Field | Purpose |
|---|---|
| Version | OSPF version number (2 for IPv4) |
| Type | Packet type = 1 (Hello) |
| Packet length | Size of the OSPF packet |
| Router ID | Sender's OSPF router ID (e.g. R1's `1.1.1.1`) |
| Area ID | OSPF area the interface belongs to (`0.0.0.0` here) |
| Checksum | Integrity check of the packet |
| Authentication type / data | Authentication method in use (none, simple, MD5) |
| Network mask | Subnet mask of the sending interface |
| Hello interval | Seconds between Hellos (10s on broadcast/point-to-point by default) |
| Options | Capability flags (e.g. E-bit for external routing) |
| Router priority | Used in DR/BDR election on multi-access networks |
| Router dead interval | Time before a silent neighbor is declared down (default 40s) |
| Designated Router (DR) | IP of the elected DR on that segment, if any |
| Backup Designated Router (BDR) | IP of the elected BDR on that segment, if any |
| List of neighbors | Router IDs of neighbors the sender has already heard from on that interface |

## Fill in from your own capture

```
<paste the OSPF Hello field values you observed here>
```
