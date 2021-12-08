# MPLS_FABRIC

# Table of Contents

- [Fabric Switches and Management IP](#fabric-switches-and-management-ip)
  - [Fabric Switches with inband Management IP](#fabric-switches-with-inband-management-ip)
- [Fabric Topology](#fabric-topology)
- [Fabric IP Allocation](#fabric-ip-allocation)
  - [Fabric Point-To-Point Links](#fabric-point-to-point-links)
  - [Point-To-Point Links Node Allocation](#point-to-point-links-node-allocation)
  - [Loopback Interfaces (BGP EVPN Peering)](#loopback-interfaces-bgp-evpn-peering)
  - [Loopback0 Interfaces Node Allocation](#loopback0-interfaces-node-allocation)
  - [ISIS CLNS interfaces](#isis-clns-interfaces)
  - [VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)](#vtep-loopback-vxlan-tunnel-source-interfaces-vteps-only)
  - [VTEP Loopback Node allocation](#vtep-loopback-node-allocation)

# Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision |
| --- | ---- | ---- | ------------- | -------- | -------------------------- |
| MPLS_FABRIC | p | P-01 | 10.92.61.162/26 | - | Provisioned |
| MPLS_FABRIC | p | P-02 | 10.92.61.164/26 | - | Provisioned |
| MPLS_FABRIC | pe | PE-01 | 10.30.30.101/24 | vEOS-LAB | Provisioned |
| MPLS_FABRIC | pe | PE-02 | 10.30.30.102/24 | vEOS-LAB | Provisioned |
| MPLS_FABRIC | pe | PE-03 | 10.30.30.103/24 | vEOS-LAB | Provisioned |
| MPLS_FABRIC | pe | PE-04 | 10.30.30.105/24 | vEOS-LAB | Provisioned |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

## Fabric Switches with inband Management IP
| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

# Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| p | P-01 | Ethernet1/1 | pe | PE-01 | Ethernet1/1 |
| p | P-01 | Ethernet2/1 | pe | PE-02 | Ethernet50/1 |
| p | P-01 | Ethernet25/1 | p | P-02 | Ethernet25/1 |
| p | P-01 | Ethernet26/1 | pe | PE-03 | Ethernet55/1 |
| p | P-02 | Ethernet1/1 | pe | PE-04 | Ethernet1/1 |
| p | P-02 | Ethernet2/1 | pe | PE-04 | Ethernet2/1 |
| p | P-02 | Ethernet4/1 | pe | PE-03 | Ethernet50/1 |
| p | P-02 | Ethernet26/1 | pe | PE-02 | Ethernet55/1 |
| pe | PE-01 | Ethernet2/1 | pe | PE-02 | Ethernet49/1 |

# Fabric IP Allocation

## Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |

## Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| P-01 | Ethernet1/1 | 100.64.48.2/31 | PE-01 | Ethernet1/1 | 100.64.48.3/31 |
| P-01 | Ethernet2/1 | 100.64.48.4/31 | PE-02 | Ethernet50/1 | 100.64.48.5/31 |
| P-01 | Ethernet25/1 | 100.64.48.0/31 | P-02 | Ethernet25/1 | 100.64.48.1/31 |
| P-01 | Ethernet26/1 | 100.64.48.6/31 | PE-03 | Ethernet55/1 | 100.64.48.7/31 |
| P-02 | Ethernet1/1 | 100.64.48.12/31 | PE-04 | Ethernet1/1 | 100.64.48.13/31 |
| P-02 | Ethernet2/1 | 100.64.48.12/31 | PE-04 | Ethernet2/1 | 100.64.48.13/31 |
| P-02 | Ethernet4/1 | 100.64.48.10/31 | PE-03 | Ethernet50/1 | 100.64.48.11/31 |
| P-02 | Ethernet26/1 | 100.64.48.8/31 | PE-02 | Ethernet55/1 | 100.64.48.9/31 |
| PE-01 | Ethernet2/1 | 100.64.48.14/31 | PE-02 | Ethernet49/1 | 100.64.48.15/31 |

## Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 100.70.0.0/24 | 256 | 6 | 2.35 % |

## Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| MPLS_FABRIC | P-01 | 100.70.0.4/32 |
| MPLS_FABRIC | P-02 | 100.70.0.6/32 |
| MPLS_FABRIC | PE-01 | 100.70.0.1/32 |
| MPLS_FABRIC | PE-02 | 100.70.0.2/32 |
| MPLS_FABRIC | PE-03 | 100.70.0.3/32 |
| MPLS_FABRIC | PE-04 | 100.70.0.4/32 |

## ISIS CLNS interfaces

| POD | Node | CLNS Address |
| --- | ---- | ------------ |
| MPLS_FABRIC | P-01 | 49.0001.0000.0000.0004.00 |
| MPLS_FABRIC | P-02 | 49.0001.0000.0000.0006.00 |
| MPLS_FABRIC | PE-01 | 49.0001.0000.0001.0001.00 |
| MPLS_FABRIC | PE-02 | 49.0001.0000.0001.0002.00 |
| MPLS_FABRIC | PE-03 | 49.0001.0000.0001.0003.00 |
| MPLS_FABRIC | PE-04 | 49.0001.0000.0001.0004.00 |

## VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| --------------------- | ------------------- | ------------------ | ------------------ |

## VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |