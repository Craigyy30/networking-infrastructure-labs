# Site-to-Site IPsec VPN | Cisco Packet Tracer

## Objective

Build a routed network in which two private LANs communicate through a site-to-site IPsec VPN between R1 and R3. R2 is the transit router and is not an IPsec peer.

## Topology

```text
PC-A -- SW-A -- R1 -------- R2 -------- R3 -- SW-B -- PC-B
                 VPN peer    transit    VPN peer
```

## Example addressing plan

| Device / interface | Address | Purpose |
|---|---|---|
| PC-A | 192.168.10.10/24 | Host in LAN A |
| R1 G0/0 | 192.168.10.1/24 | LAN A gateway |
| R1 G0/1 | 10.0.0.1/30 | R1-to-R2 link |
| R2 G0/0 | 10.0.0.2/30 | R2-to-R1 link |
| R2 G0/1 | 10.0.0.5/30 | R2-to-R3 link |
| R3 G0/0 | 10.0.0.6/30 | R3-to-R2 link |
| R3 G0/1 | 192.168.20.1/24 | LAN B gateway |
| PC-B | 192.168.20.10/24 | Host in LAN B |

Set PC-A's default gateway to `192.168.10.1` and PC-B's default gateway to `192.168.20.1`.

> Interface names are examples. Some Packet Tracer router models use `Fa0/0`, `Gi0/0/0`, or other names. Match the commands to your actual device.

## Files

- `configs/R1-VPN-Gateway.txt`: R1 addressing, routing, IKE/IPsec, and crypto map.
- `configs/R2-Transit-Router.txt`: transit interfaces and routes to both LANs.
- `configs/R3-VPN-Gateway.txt`: R3 addressing, routing, IKE/IPsec, and crypto map.
- `troubleshooting.md`: test sequence and common faults.
- `screenshots/`: add genuine screenshots from your Packet Tracer session.

## Suggested build and test sequence

1. Cable devices and configure IP addresses.
2. Configure PC addressing and default gateways.
3. Configure routing between the three routers.
4. Verify the WAN peer addresses can reach each other before configuring IPsec.
5. Apply matching IKE policies, pre-shared keys, transform sets, interesting-traffic ACLs, and crypto maps on R1 and R3.
6. Generate traffic from PC-A to PC-B to trigger negotiation.
7. Check IKE/IPsec security associations and packet counters on both VPN peers.
8. Test repeated pings and confirm that the IPsec counters increase.

## Security and verification notes

The example uses a lab-only pre-shared key, `LabOnly-ChangeMe123!`. Change it consistently on both peers. Use stronger modern settings where supported by the chosen IOS image. Group 2 is retained for compatibility with some educational images and is not recommended for production use.

The original `.pkt` file was not available when these notes were prepared. The configurations are written examples and have not been executed or verified in Packet Tracer yet.
