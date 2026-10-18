# Networking Infrastructure Labs

Hands-on networking labs focused on routing, switching, VPNs, and infrastructure troubleshooting.

## Labs

### 1. Cisco Packet Tracer: Site-to-Site IPsec VPN
- **Status:** Documentation and example configurations drafted; not yet verified against the original Packet Tracer file.
- **Goal:** Connect two private LANs securely through an intermediate routed network using a site-to-site IPsec VPN.
- **Path:** [01-site-to-site-ipsec-vpn](./01-site-to-site-ipsec-vpn/)

## Repository structure

```text
.
├── README.md
└── 01-site-to-site-ipsec-vpn/
    ├── README.md
    ├── configs/
    │   ├── R1-VPN-Gateway.txt
    │   ├── R2-Transit-Router.txt
    │   └── R3-VPN-Gateway.txt
    ├── troubleshooting.md
    └── screenshots/
        └── README.md
```

## Important notes

- Router interface names and IOS feature support can differ by Packet Tracer device/model. Adjust interface names to match your topology.
- These are example configurations based on the documented addressing plan, not exports from a recovered `.pkt` file.
- Replace the example pre-shared key before using this in any environment beyond a disposable lab.
- No screenshot or successful tunnel verification is claimed until evidence is added.

## Skills demonstrated

IP addressing, static routing, IKE Phase 1, IPsec Phase 2, interesting traffic ACLs, crypto maps, and troubleshooting with IOS show commands.
