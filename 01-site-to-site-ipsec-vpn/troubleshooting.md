# Troubleshooting: Site-to-Site IPsec VPN

Use this checklist in order. The tunnel may be configured but remain idle until interesting traffic is sent.

## 1. Check interfaces and IP addressing

On each router:

```text
show ip interface brief
show running-config
```

Confirm interfaces are up/up, masks are correct, and there are no duplicate addresses. Check that each PC has the correct IP, subnet mask, and default gateway.

## 2. Check routing before IPsec

```text
show ip route
ping 10.0.0.2
ping 10.0.0.5
ping 10.0.0.6
```

From R1, confirm R3's peer address (10.0.0.6) is reachable through R2. From R3, confirm R1's peer address (10.0.0.1) is reachable. If peer reachability fails, fix interfaces and transit routing first.

## 3. Check that the VPN settings match

Compare R1 and R3:
- IKE policy number and encryption, hash, authentication, and Diffie-Hellman group.
- Pre-shared key and remote peer address.
- IPsec transform set.
- Crypto map sequence and transform set.
- Interesting-traffic ACLs, which should mirror each other in reverse.
- Crypto map applied to the correct WAN-facing interface.

## 4. Generate interesting traffic

From PC-A, ping PC-B (192.168.20.10). The first ping can time out while negotiation starts. Repeat the test, then inspect:

```text
show crypto isakmp sa
show crypto ipsec sa
show access-lists 110
```

Exact command availability and output depend on the Packet Tracer device/IOS support. A healthy IKE session commonly shows a state such as `QM_IDLE` on classic IOS. IPsec encapsulation/decapsulation counters should increase when matching traffic passes.

## 5. Common symptoms

| Symptom | Likely checks |
|---|---|
| Peer address unreachable | Interface status, IP/mask, R2 routing, WAN ACLs |
| IKE negotiation fails | Matching policy, pre-shared key, peer IP, supported algorithms |
| IKE appears established but no protected traffic | ACL 110, crypto map binding, LAN routes, host gateways |
| Encapsulation rises but decapsulation does not | Reverse route, reverse ACL, peer configuration, return traffic |
| Commands unsupported in Packet Tracer | Check router model and supported simulated IOS features |

## 6. Evidence to capture

Add real screenshots to `screenshots/` showing:
1. Full topology with labels and IP subnets.
2. Successful PC-A to PC-B connectivity.
3. IKE security association output.
4. IPsec encapsulation/decapsulation counters after traffic.

Do not mark the lab as verified until the tests have actually succeeded. Packet Tracer may simulate only a subset of IOS VPN features.
