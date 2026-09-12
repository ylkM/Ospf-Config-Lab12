# OSPF Single-Area Lab — R1, R2, R3, R4

A four-router, single-area OSPF (Area 0) lab with an ASBR (R1) redistributing a default route from an ISP connection.



## Repo Structure

```
.
├── README.md
├── topology.svg
├── configs/
│   ├── R1.txt
│   ├── R2.txt
│   ├── R3.txt
│   └── R4.txt
└── docs/
    ├── task1-hostnames-and-ips.md
    ├── task2-loopbacks.md
    ├── task3-ospf-config.md
    ├── task4-reference-bandwidth.md
    ├── task5-asbr-default-route.md
    ├── task6-r4-routing-table.md
    └── task7-ospf-hello-fields.md
```

## Lab Tasks

| #  Task 
|---|---|---|
| 1 | Configure hostnames and IP addresses on each device; enable interfaces (ISPR1 not required) 
| 2 | Configure a loopback interface on each router 
| 3 | Enable OSPF directly on each interface; configure passive interfaces 
| 4 | Set the reference bandwidth so a FastEthernet interface costs 100 
| 5 | Configure R1 as an ASBR advertising a default route into OSPF 
| 6 | Check R4's routing table — what default route(s) were added?  
| 7 | Inspect OSPF Hello messages in Simulation mode — what fields does the Hello contain? |
## Addressing Table

| Device | Interface | IP Address | Connects To |
|---|---|---|---|
| ISPR1 | Gig0/0/0 | 203.0.113.2/30 | R1 Gig3/0 |
| R1 | Gig3/0 | 203.0.113.1/30 | ISPR1 |
| R1 | Gig0/0 | 10.0.12.1/30 | R2 Gig0/0 |
| R1 | Fa1/0 | 10.0.13.1/30 | R3 Fa1/0 |
| R1 | Loopback0 | 1.1.1.1/32 | — |
| R2 | Gig0/0 | 10.0.12.2/30 | R1 Gig0/0 |
| R2 | Fa1/0 | 10.0.24.1/30 | R4 Fa1/0 |
| R2 | Loopback0 | 2.2.2.2/32 | — |
| R3 | Fa1/0 | 10.0.13.2/30 | R1 Fa1/0 |
| R3 | Fa2/0 | 10.0.34.1/30 | R4 Fa2/0 |
| R3 | Loopback0 | 3.3.3.3/32 | — |
| R4 | Fa1/0 | 10.0.24.2/30 | R2 Fa1/0 |
| R4 | Fa2/0 | 10.0.34.2/30 | R3 Fa2/0 |
| R4 | Gig0/0 | 192.168.4.254/24 | LAN Switch |
| R4 | Loopback0 | 4.4.4.4/32 | — |
| PC | NIC | 192.168.4.1/24 | Switch Fa0/1 |

## Applying the Configs

Paste the contents of the matching file in `configs/` into each router's `configure terminal` prompt, in order:

```
Router> enable
Router# configure terminal
Router(config)# <paste file contents>
Router(config)# end
Router# write memory
```
