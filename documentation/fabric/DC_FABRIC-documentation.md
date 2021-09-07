# DC_FABRIC

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
  - [VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)](#vtep-loopback-vxlan-tunnel-source-interfaces-vteps-only)
  - [VTEP Loopback Node allocation](#vtep-loopback-node-allocation)

<!-- toc -->
# Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision |
| --- | ---- | ---- | ------------- | -------- | -------------------------- |
| DC1_FABRIC | l3leaf | dc1-borderleaf1a | 10.30.30.116/24 | vEOS-LAB | Provisioned |
| DC1_FABRIC | l3leaf | dc1-borderleaf1b | 10.30.30.117/24 | vEOS-LAB | Provisioned |
| DC1_FABRIC | l3leaf | dc1-serverleaf1a | 10.30.30.114/24 | vEOS-LAB | Provisioned |
| DC1_FABRIC | l3leaf | dc1-serverleaf1b | 10.30.30.115/24 | vEOS-LAB | Provisioned |
| DC1_FABRIC | spine | dc1-spine1 | 10.30.30.112/24 | - | Provisioned |
| DC1_FABRIC | spine | dc1-spine2 | 10.30.30.113/24 | - | Provisioned |
| DC2_FABRIC | l3leaf | dc2-borderleaf1 | 10.30.30.118/24 | vEOS-LAB | Provisioned |
| DC2_FABRIC | l3leaf | dc2-serverleaf1 | 10.30.30.120/24 | vEOS-LAB | Provisioned |
| DC2_FABRIC | spine | dc2-spine1 | 10.30.30.119/24 | - | Provisioned |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

## Fabric Switches with inband Management IP
| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

# Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| l3leaf | dc1-borderleaf1a | Ethernet1 | spine | dc1-spine1 | Ethernet3 |
| l3leaf | dc1-borderleaf1a | Ethernet2 | spine | dc1-spine2 | Ethernet3 |
| l3leaf | dc1-borderleaf1a | Ethernet3 | mlag_peer | dc1-borderleaf1b | Ethernet3 |
| l3leaf | dc1-borderleaf1a | Ethernet4 | mlag_peer | dc1-borderleaf1b | Ethernet4 |
| l3leaf | dc1-borderleaf1a | Ethernet5 | l3leaf | dc2-borderleaf1 | Ethernet6 |
| l3leaf | dc1-borderleaf1b | Ethernet1 | spine | dc1-spine1 | Ethernet4 |
| l3leaf | dc1-borderleaf1b | Ethernet2 | spine | dc1-spine2 | Ethernet4 |
| l3leaf | dc1-borderleaf1b | Ethernet5 | l3leaf | dc2-borderleaf1 | Ethernet5 |
| l3leaf | dc1-serverleaf1a | Ethernet1 | spine | dc1-spine1 | Ethernet1 |
| l3leaf | dc1-serverleaf1a | Ethernet2 | spine | dc1-spine2 | Ethernet1 |
| l3leaf | dc1-serverleaf1a | Ethernet3 | mlag_peer | dc1-serverleaf1b | Ethernet3 |
| l3leaf | dc1-serverleaf1a | Ethernet4 | mlag_peer | dc1-serverleaf1b | Ethernet4 |
| l3leaf | dc1-serverleaf1b | Ethernet1 | spine | dc1-spine1 | Ethernet2 |
| l3leaf | dc1-serverleaf1b | Ethernet2 | spine | dc1-spine2 | Ethernet2 |
| l3leaf | dc2-borderleaf1 | Ethernet1 | spine | dc2-spine1 | Ethernet1 |
| l3leaf | dc2-serverleaf1 | Ethernet1 | spine | dc2-spine1 | Ethernet2 |

# Fabric IP Allocation

## Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |
| 100.64.10.0/24 | 256 | 16 | 6.25 % |
| 100.64.20.0/24 | 256 | 4 | 1.57 % |

## Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| dc1-borderleaf1a | Ethernet1 | 100.64.10.13/31 | dc1-spine1 | Ethernet3 | 100.64.10.12/31 |
| dc1-borderleaf1a | Ethernet2 | 100.64.10.15/31 | dc1-spine2 | Ethernet3 | 100.64.10.14/31 |
| dc1-borderleaf1a | Ethernet5 | 100.64.48.0/31 | dc2-borderleaf1 | Ethernet6 | 100.64.48.1/31 |
| dc1-borderleaf1b | Ethernet1 | 100.64.10.19/31 | dc1-spine1 | Ethernet4 | 100.64.10.18/31 |
| dc1-borderleaf1b | Ethernet2 | 100.64.10.21/31 | dc1-spine2 | Ethernet4 | 100.64.10.20/31 |
| dc1-borderleaf1b | Ethernet5 | 100.64.48.2/31 | dc2-borderleaf1 | Ethernet5 | 100.64.48.3/31 |
| dc1-serverleaf1a | Ethernet1 | 100.64.10.1/31 | dc1-spine1 | Ethernet1 | 100.64.10.0/31 |
| dc1-serverleaf1a | Ethernet2 | 100.64.10.3/31 | dc1-spine2 | Ethernet1 | 100.64.10.2/31 |
| dc1-serverleaf1b | Ethernet1 | 100.64.10.7/31 | dc1-spine1 | Ethernet2 | 100.64.10.6/31 |
| dc1-serverleaf1b | Ethernet2 | 100.64.10.9/31 | dc1-spine2 | Ethernet2 | 100.64.10.8/31 |
| dc2-borderleaf1 | Ethernet1 | 100.64.20.1/31 | dc2-spine1 | Ethernet1 | 100.64.20.0/31 |
| dc2-serverleaf1 | Ethernet1 | 100.64.20.7/31 | dc2-spine1 | Ethernet2 | 100.64.20.6/31 |

## Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 100.64.11.0/24 | 256 | 6 | 2.35 % |
| 100.64.21.0/24 | 256 | 3 | 1.18 % |

## Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| DC1_FABRIC | dc1-borderleaf1a | 100.64.11.6/32 |
| DC1_FABRIC | dc1-borderleaf1b | 100.64.11.7/32 |
| DC1_FABRIC | dc1-serverleaf1a | 100.64.11.4/32 |
| DC1_FABRIC | dc1-serverleaf1b | 100.64.11.5/32 |
| DC1_FABRIC | dc1-spine1 | 100.64.11.1/32 |
| DC1_FABRIC | dc1-spine2 | 100.64.11.2/32 |
| DC2_FABRIC | dc2-borderleaf1 | 100.64.21.4/32 |
| DC2_FABRIC | dc2-serverleaf1 | 100.64.21.5/32 |
| DC2_FABRIC | dc2-spine1 | 100.64.21.1/32 |

## VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| --------------------- | ------------------- | ------------------ | ------------------ |
| 100.64.12.0/24 | 256 | 4 | 1.57 % |
| 100.64.22.0/24 | 256 | 2 | 0.79 % |

## VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
| DC1_FABRIC | dc1-borderleaf1a | 100.64.12.6/32 |
| DC1_FABRIC | dc1-borderleaf1b | 100.64.12.6/32 |
| DC1_FABRIC | dc1-serverleaf1a | 100.64.12.4/32 |
| DC1_FABRIC | dc1-serverleaf1b | 100.64.12.4/32 |
| DC2_FABRIC | dc2-borderleaf1 | 100.64.22.4/32 |
| DC2_FABRIC | dc2-serverleaf1 | 100.64.22.5/32 |
