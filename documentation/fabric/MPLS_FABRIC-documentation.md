# MPLS_FABRIC

# Table of Contents
<!-- toc -->

- [Fabric Switches and Management IP](#fabric-switches-and-management-ip)
  - [Fabric Switches with inband Management IP](#fabric-switches-with-inband-management-ip)
- [Fabric Topology](#fabric-topology)
- [Fabric IP Allocation](#fabric-ip-allocation)
  - [Fabric Point-To-Point Links](#fabric-point-to-point-links)
  - [Point-To-Point Links Node Allocation](#point-to-point-links-node-allocation)
  - [Loopback Interfaces (BGP EVPN Peering)](#loopback-interfaces-bgp-evpn-peering)
  - [Loopback0 Interfaces Node Allocation](#loopback0-interfaces-node-allocation)
  - [ISIS CLNS interfaces](#isis-clns-interfaces)

<!-- toc -->
# Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision |
| --- | ---- | ---- | ------------- | -------- | -------------------------- |
| MPLS_FABRIC | p | p4 | 10.30.30.104/24 | - | Provisioned |
| MPLS_FABRIC | p | p6 | 10.30.30.106/24 | - | Provisioned |
| MPLS_FABRIC | pe | pe1 | 10.30.30.101/24 | vEOS-LAB | Provisioned |
| MPLS_FABRIC | pe | pe2 | 10.30.30.102/24 | vEOS-LAB | Provisioned |
| MPLS_FABRIC | pe | pe3 | 10.30.30.103/24 | vEOS-LAB | Provisioned |
| MPLS_FABRIC | pe | pe5 | 10.30.30.105/24 | vEOS-LAB | Provisioned |
| MPLS_FABRIC | rr | rr7 | 10.30.30.107/24 | vEOS-LAB | Provisioned |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

## Fabric Switches with inband Management IP
| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

# Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| p | p4 | Ethernet1 | pe | pe3 | Ethernet1 |
| p | p4 | Ethernet2 | pe | pe5 | Ethernet2 |
| p | p4 | Ethernet3 | rr | rr7 | Ethernet4 |
| p | p6 | Ethernet1 | pe | pe5 | Ethernet1 |
| p | p6 | Ethernet2 | pe | pe1 | Ethernet2 |
| pe | pe1 | Ethernet1 | pe | pe2 | Ethernet1 |
| pe | pe1 | Ethernet3 | rr | rr7 | Ethernet2 |
| pe | pe2 | Ethernet2 | pe | pe3 | Ethernet2 |
| pe | pe3 | Ethernet3 | rr | rr7 | Ethernet1 |
| pe | pe5 | Ethernet3 | rr | rr7 | Ethernet3 |

# Fabric IP Allocation

## Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |

## Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| p4 | Ethernet1 | unnumbered Loopback0 | pe3 | Ethernet1 | unnumbered Loopback0 |
| p4 | Ethernet2 | unnumbered Loopback0 | pe5 | Ethernet2 | unnumbered Loopback0 |
| p4 | Ethernet3 | unnumbered Loopback0 | rr7 | Ethernet4 | unnumbered Loopback0 |
| p6 | Ethernet1 | unnumbered Loopback0 | pe5 | Ethernet1 | unnumbered Loopback0 |
| p6 | Ethernet2 | unnumbered Loopback0 | pe1 | Ethernet2 | unnumbered Loopback0 |
| pe1 | Ethernet1 | unnumbered Loopback0 | pe2 | Ethernet1 | unnumbered Loopback0 |
| pe1 | Ethernet3 | unnumbered Loopback0 | rr7 | Ethernet2 | unnumbered Loopback0 |
| pe2 | Ethernet2 | unnumbered Loopback0 | pe3 | Ethernet2 | unnumbered Loopback0 |
| pe3 | Ethernet3 | unnumbered Loopback0 | rr7 | Ethernet1 | unnumbered Loopback0 |
| pe5 | Ethernet3 | unnumbered Loopback0 | rr7 | Ethernet3 | unnumbered Loopback0 |

## Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 100.70.0.0/24 | 256 | 7 | 2.74 % |

## Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| MPLS_FABRIC | p4 | 100.70.0.4/32 |
| MPLS_FABRIC | p6 | 100.70.0.6/32 |
| MPLS_FABRIC | pe1 | 100.70.0.1/32 |
| MPLS_FABRIC | pe2 | 100.70.0.2/32 |
| MPLS_FABRIC | pe3 | 100.70.0.3/32 |
| MPLS_FABRIC | pe5 | 100.70.0.5/32 |
| MPLS_FABRIC | rr7 | 100.70.0.7/32 |

## ISIS CLNS interfaces

| POD | Node | CLNS Address |
| --- | ---- | ------------ |
| MPLS_FABRIC | p4 | 49.0001.0000.0000.0004.00 |
| MPLS_FABRIC | p6 | 49.0001.0000.0000.0006.00 |
| MPLS_FABRIC | pe1 | 49.0001.0000.0000.0001.00 |
| MPLS_FABRIC | pe2 | 49.0001.0000.0000.0002.00 |
| MPLS_FABRIC | pe3 | 49.0001.0000.0000.0003.00 |
| MPLS_FABRIC | pe5 | 49.0001.0000.0000.0005.00 |
| MPLS_FABRIC | rr7 | 49.0001.0000.0000.0007.00 |

