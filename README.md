# Floating Static Routes Lab

A routing lab covering dynamic routing verification and floating static routes as a backup path between two routers (R1 and R2) in Enterprise A.

## Devices

| Device | Role |
|--------|------|
| PC1 | Client host |
| R1 | Enterprise A router |
| R2 | Enterprise A router |
| SRV1 | Internal server |
| 1.1.1.1 | Remote server reached over the Internet |

## Objectives

- Read and interpret the routing tables of R1 and R2
- Identify the dynamic routing protocol in use
- Trace the path PC1 takes to SRV1 and to the Internet
- Configure floating static routes as backup routes
- Verify failover when the R1-R2 link goes down

---

## Task 1: Check the Routing Tables of R1 and R2

Commands used:

```
R1# show ip route
R2# show ip route
```

Questions:

1. Which dynamic routing protocol is Enterprise A using?
2. Which route will be used if PC1 tries to access SRV1?
3. Which route will be used if PC1 tries to access remote server 1.1.1.1 over the Internet?
4. Test by pinging SRV1 and 1.1.1.1.

```
PC1> ping <SRV1 IP>
PC1> ping 1.1.1.1
```

**Findings:**

- Dynamic routing protocol:
- Route to SRV1:
- Route to 1.1.1.1:
- Ping SRV1 result:
- Ping 1.1.1.1 result:

---

## Task 2: Configure Floating Static Routes on R1 and R2

Goal: allow PC1 to reach SRV1 if the link between R1 and R2 fails.

A floating static route is a static route with an administrative distance (AD) higher than the dynamic routing protocol's AD. It stays out of the routing table while the dynamic route is available, and is installed only when the dynamic route disappears.

Configuration (replace the placeholders with the values from your topology):

```
R1(config)# ip route <SRV1 network> <mask> <next-hop on R2> <AD higher than dynamic protocol>
R2(config)# ip route <PC1 network> <mask> <next-hop on R1> <AD higher than dynamic protocol>
```

Verify:

```
R1# show ip route static
R2# show ip route static
```

Question: Do the routes enter the routing tables of R1 and R2?

**Findings:**

- R1 routing table:
- R2 routing table:
- Explanation:

---

## Task 3: Shut Down G0/2/0 on R1 or R2

```
R1(config)# interface g0/2/0
R1(config-if)# shutdown
```

Verify:

```
R1# show ip route
R2# show ip route
PC1> ping <SRV1 IP>
```

Questions:

1. Do the floating static routes enter the routing tables of R1 and R2?
2. Does the ping from PC1 to SRV1 succeed?

**Findings:**

- Floating static routes installed:
- Ping PC1 to SRV1 result:

---
![Network Topology](topology.png)

## Conclusion

Summary of what the lab demonstrated about dynamic routes, administrative distance, and backup routing with floating static routes.
