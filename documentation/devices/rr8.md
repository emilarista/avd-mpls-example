# rr8
# Table of Contents

- [Management](#management)
  - [Management Interfaces](#management-interfaces)
  - [Name Servers](#name-servers)
  - [Management API HTTP](#management-api-http)
- [Authentication](#authentication)
  - [Local Users](#local-users)
- [Monitoring](#monitoring)
  - [TerminAttr Daemon](#terminattr-daemon)
  - [SFlow](#sflow)
- [Spanning Tree](#spanning-tree)
  - [Spanning Tree Summary](#spanning-tree-summary)
  - [Spanning Tree Device Configuration](#spanning-tree-device-configuration)
- [Internal VLAN Allocation Policy](#internal-vlan-allocation-policy)
  - [Internal VLAN Allocation Policy Summary](#internal-vlan-allocation-policy-summary)
  - [Internal VLAN Allocation Policy Configuration](#internal-vlan-allocation-policy-configuration)
- [Interfaces](#interfaces)
  - [Ethernet Interfaces](#ethernet-interfaces)
  - [Loopback Interfaces](#loopback-interfaces)
- [Routing](#routing)
  - [Service Routing Protocols Model](#service-routing-protocols-model)
  - [IP Routing](#ip-routing)
  - [IPv6 Routing](#ipv6-routing)
  - [Static Routes](#static-routes)
  - [Router ISIS](#router-isis)
  - [Router BGP](#router-bgp)
- [BFD](#bfd)
  - [Router BFD](#router-bfd)
- [MPLS](#mpls)
  - [MPLS and LDP](#mpls-and-ldp)
  - [MPLS Interfaces](#mpls-interfaces)
- [Multicast](#multicast)
- [Filters](#filters)
- [ACL](#acl)
- [VRF Instances](#vrf-instances)
  - [VRF Instances Summary](#vrf-instances-summary)
  - [VRF Instances Device Configuration](#vrf-instances-device-configuration)
- [Quality Of Service](#quality-of-service)
- [EOS CLI](#eos-cli)

# Management

## Management Interfaces

### Management Interfaces Summary

#### IPv4

| Management Interface | description | Type | VRF | IP Address | Gateway |
| -------------------- | ----------- | ---- | --- | ---------- | ------- |
| Management1 | oob_management | oob | MGMT | 10.30.30.108/24 | 10.30.30.1 |

#### IPv6

| Management Interface | description | Type | VRF | IPv6 Address | IPv6 Gateway |
| -------------------- | ----------- | ---- | --- | ------------ | ------------ |
| Management1 | oob_management | oob | MGMT | -  | - |

### Management Interfaces Device Configuration

```eos
!
interface Management1
   description oob_management
   no shutdown
   vrf MGMT
   ip address 10.30.30.108/24
```

## Name Servers

### Name Servers Summary

| Name Server | Source VRF |
| ----------- | ---------- |
| 10.20.20.13 | MGMT |
| 8.8.8.8 | MGMT |

### Name Servers Device Configuration

```eos
ip name-server vrf MGMT 8.8.8.8
ip name-server vrf MGMT 10.20.20.13
```

## Management API HTTP

### Management API HTTP Summary

| HTTP | HTTPS |
| ---------- | ---------- |
| default | true |

### Management API VRF Access

| VRF Name | IPv4 ACL | IPv6 ACL |
| -------- | -------- | -------- |
| MGMT | - | - |


### Management API HTTP Configuration

```eos
!
management api http-commands
   protocol https
   no shutdown
   !
   vrf MGMT
      no shutdown
```

# Authentication

## Local Users

### Local Users Summary

| User | Privilege | Role |
| ---- | --------- | ---- |
| cvpadmin | 15 | network-admin |
| emil | 15 | network-admin |

### Local Users Device Configuration

```eos
!
username cvpadmin privilege 15 role network-admin secret sha512 $6$WRH0YV9I461XA.qn$BYsYGThSIHOh4ic8qdjnHWq9Zi/l0W8Ws4DZ5Y5yI3hBBWGP03W3ggXWdY7MTqVA8plRvaazG/U8CeMPkT5aE.
username emil privilege 15 role network-admin secret sha512 $6$kiCAKn8fb8T12ClP$UchWUxo0y/CpYptWYxj7pC8uzjoUJnvi4lSg1c009mqJG2inlUDQdTi/YVY4M0dzgf4LOkaVtL7U11ZRkP7Rm/
```

# Monitoring

## TerminAttr Daemon

### TerminAttr Daemon Summary

| CV Compression | CloudVision Servers | VRF | Authentication | Smash Excludes | Ingest Exclude | Bypass AAA |
| -------------- | ------------------- | --- | -------------- | -------------- | -------------- | ---------- |
| gzip | 10.20.20.20:9910 | MGMT | key,dudeface | ale,flexCounter,hardware,kni,pulse,strata | /Sysdb/cell/1/agent,/Sysdb/cell/2/agent | False |

### TerminAttr Daemon Device Configuration

```eos
!
daemon TerminAttr
   exec /usr/bin/TerminAttr -cvaddr=10.20.20.20:9910 -cvauth=key,dudeface -cvvrf=MGMT -smashexcludes=ale,flexCounter,hardware,kni,pulse,strata -ingestexclude=/Sysdb/cell/1/agent,/Sysdb/cell/2/agent -taillogs
   no shutdown
```

## SFlow

### SFlow Summary

| VRF | SFlow Source Interface | SFlow Destination | Port |
| --- | ---------------------- | ----------------- | ---- |
| MGMT | - | 127.0.0.1 | 6343  |
| MGMT | Management1 | - | - |

sFlow Sample Rate: 40000

sFlow is enabled.

### SFlow Device Configuration

```eos
!
sflow sample 40000
sflow vrf MGMT destination 127.0.0.1
sflow vrf MGMT source-interface Management1
sflow run
```

# Spanning Tree

## Spanning Tree Summary

STP mode: **none**

### Global Spanning-Tree Settings


## Spanning Tree Device Configuration

```eos
!
spanning-tree mode none
```

# Internal VLAN Allocation Policy

## Internal VLAN Allocation Policy Summary

| Policy Allocation | Range Beginning | Range Ending |
| ------------------| --------------- | ------------ |
| ascending | 3700 | 3900 |

## Internal VLAN Allocation Policy Configuration

```eos
!
vlan internal order ascending range 3700 3900
```

# Interfaces

## Ethernet Interfaces

### Ethernet Interfaces Summary

#### L2

| Interface | Description | Mode | VLANs | Native VLAN | Trunk Group | Channel-Group |
| --------- | ----------- | ---- | ----- | ----------- | ----------- | ------------- |

*Inherited from Port-Channel Interface

#### IPv4

| Interface | Description | Type | Channel Group | IP Address | VRF |  MTU | Shutdown | ACL In | ACL Out |
| --------- | ----------- | -----| ------------- | ---------- | ----| ---- | -------- | ------ | ------- |
| Ethernet1 | P2P_LINK_TO_pe2_Ethernet3 | routed | - | 100.64.48.7/31 | default | 1500 | false | - | - |
| Ethernet2 | P2P_LINK_TO_rr7_Ethernet5 | routed | - | 100.64.48.23/31 | default | 1500 | false | - | - |

#### IPv6

| Interface | Description | Type | Channel Group | IPv6 Address | VRF | MTU | Shutdown | ND RA Disabled | Managed Config Flag | IPv6 ACL In | IPv6 ACL Out |
| --------- | ----------- | ---- | --------------| ------------ | --- | --- | -------- | -------------- | -------------------| ----------- | ------------ |
| Ethernet1 | P2P_LINK_TO_pe2_Ethernet3 | routed | - | - | default | 1500 | false | - | *- | - | - |
| Ethernet2 | P2P_LINK_TO_rr7_Ethernet5 | routed | - | - | default | 1500 | false | - | *- | - | - |

#### ISIS

| Interface | Channel Group | ISIS Instance | ISIS Metric | Mode | ISIS Circuit Type |
| --------- | ------------- | ------------- | ----------- | ---- | ----------------- |
| Ethernet1 | - | MPLS_UNDERLAY | 60 | point-to-point | level-2 |
| Ethernet2 | - | MPLS_UNDERLAY | 60 | point-to-point | level-2 |

### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   description P2P_LINK_TO_pe2_Ethernet3
   no shutdown
   speed 100full
   mtu 1500
   no switchport
   ip address 100.64.48.7/31
   ipv6 enable
   isis enable MPLS_UNDERLAY
   isis circuit-type level-2
   isis metric 60
   isis network point-to-point
   no isis hello padding
   mpls ip
!
interface Ethernet2
   description P2P_LINK_TO_rr7_Ethernet5
   no shutdown
   speed 100full
   mtu 1500
   no switchport
   ip address 100.64.48.23/31
   ipv6 enable
   isis enable MPLS_UNDERLAY
   isis circuit-type level-2
   isis metric 60
   isis network point-to-point
   no isis hello padding
   mpls ip
```

## Loopback Interfaces

### Loopback Interfaces Summary

#### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | MPLS_Overlay_peering | default | 100.70.0.8/32 |

#### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | MPLS_Overlay_peering | default | - |

#### ISIS

| Interface | ISIS instance | ISIS metric | Interface mode |
| -------- | -------- | -------- | -------- |
| Loopback0 | MPLS_UNDERLAY |  - |  passive |

### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description MPLS_Overlay_peering
   no shutdown
   ip address 100.70.0.8/32
   isis enable MPLS_UNDERLAY
   isis passive
   node-segment ipv4 index 108
```

# Routing
## Service Routing Protocols Model

Multi agent routing protocol model enabled

```eos
!
service routing protocols model multi-agent
```

## IP Routing

### IP Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | true|| MGMT | false |

### IP Routing Device Configuration

```eos
!
ip routing
no ip routing vrf MGMT
```
## IPv6 Routing

### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | true | | MGMT | false |

### IPv6 Routing Device Configuration

```eos
!
ipv6 unicast-routing
```

## Static Routes

### Static Routes Summary

| VRF | Destination Prefix | Next Hop IP             | Exit interface      | Administrative Distance       | Tag               | Route Name                    | Metric         |
| --- | ------------------ | ----------------------- | ------------------- | ----------------------------- | ----------------- | ----------------------------- | -------------- |
| MGMT  | 0.0.0.0/0 |  10.30.30.1  |  -  |  1  |  -  |  -  |  - |

### Static Routes Device Configuration

```eos
!
ip route vrf MGMT 0.0.0.0/0 10.30.30.1
```

## Router ISIS

### Router ISIS Summary

| Settings | Value |
| -------- | ----- |
| Instance | MPLS_UNDERLAY |
| Net-ID | 49.0001.0000.0002.0008.00 |
| Type | level-1-2 |
| Address Family | ipv4 unicast |
| Log Adjacency Changes | True |
| SR MPLS Enabled | True |
| SR MPLS Router-ID | 100.70.0.8 |

### ISIS Interfaces Summary

| Interface | ISIS Instance | ISIS Metric | Interface Mode |
| --------- | ------------- | ----------- | -------------- |
| Ethernet1 | MPLS_UNDERLAY | 60 | point-to-point |
| Ethernet2 | MPLS_UNDERLAY | 60 | point-to-point |
| Loopback0 | MPLS_UNDERLAY | - | passive |

### Router ISIS Device Configuration

```eos
!
router isis MPLS_UNDERLAY
   net 49.0001.0000.0002.0008.00
   is-type level-1-2
   advertise passive-only
   router-id ipv4 100.70.0.8
   log-adjacency-changes
   timers local-convergence-delay 15000 protected-prefixes
   !
   address-family ipv4 unicast
      maximum-paths 4
      fast-reroute ti-lfa mode link-protection
   !
   segment-routing mpls
      router-id 100.70.0.8
      no shutdown
```

## Router BGP

### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 65000|  100.70.0.8 |

| BGP AS | Cluster ID |
| ------ | --------- |
| 65000|  7.7.7.7 |

| BGP Tuning |
| ---------- |
| no bgp default ipv4-unicast |
| distance bgp 20 200 200 |
| graceful-restart restart-time 300 |
| graceful-restart |
| bgp route-reflector preserve-attributes always |
| maximum-paths 4 ecmp 4 |

### Router BGP Peer Groups

#### MPLS-OVERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | mpls-vpn |
| Remote AS | 65000 |
| Route Reflector Client | Yes |
| Source | Loopback0 |
| Bfd | true |
| Send community | all |
| Maximum routes | 0 (no limit) |

### BGP Neighbors

| Neighbor | Remote AS | VRF | Send-community | Maximum-routes |
| -------- | --------- | --- | -------------- | -------------- |
| 100.70.0.1 | Inherited from peer group MPLS-OVERLAY-PEERS | default | Inherited from peer group MPLS-OVERLAY-PEERS | Inherited from peer group MPLS-OVERLAY-PEERS |
| 100.70.0.2 | Inherited from peer group MPLS-OVERLAY-PEERS | default | Inherited from peer group MPLS-OVERLAY-PEERS | Inherited from peer group MPLS-OVERLAY-PEERS |
| 100.70.0.3 | Inherited from peer group MPLS-OVERLAY-PEERS | default | Inherited from peer group MPLS-OVERLAY-PEERS | Inherited from peer group MPLS-OVERLAY-PEERS |
| 100.70.0.5 | Inherited from peer group MPLS-OVERLAY-PEERS | default | Inherited from peer group MPLS-OVERLAY-PEERS | Inherited from peer group MPLS-OVERLAY-PEERS |

### Router BGP EVPN Address Family

#### EVPN Neighbor Default Encapsulation

| Neighbor Default Encapsulation | Next-hop-self Source Interface |
| ------------------------------ | ------------------------------ |
| mpls | - |

#### Router BGP EVPN MAC-VRFs

#### Router BGP EVPN VRFs

### Router BGP Device Configuration

```eos
!
router bgp 65000
   router-id 100.70.0.8
   bgp cluster-id 7.7.7.7
   no bgp default ipv4-unicast
   distance bgp 20 200 200
   graceful-restart restart-time 300
   graceful-restart
   bgp route-reflector preserve-attributes always
   maximum-paths 4 ecmp 4
   neighbor MPLS-OVERLAY-PEERS peer group
   neighbor MPLS-OVERLAY-PEERS remote-as 65000
   neighbor MPLS-OVERLAY-PEERS update-source Loopback0
   neighbor MPLS-OVERLAY-PEERS route-reflector-client
   neighbor MPLS-OVERLAY-PEERS bfd
   neighbor MPLS-OVERLAY-PEERS password 7 $1c$U4tL2vQP9QwZlxIV1K3/pw==
   neighbor MPLS-OVERLAY-PEERS send-community
   neighbor MPLS-OVERLAY-PEERS maximum-routes 0
   neighbor 100.70.0.1 peer group MPLS-OVERLAY-PEERS
   neighbor 100.70.0.1 description pe1
   neighbor 100.70.0.2 peer group MPLS-OVERLAY-PEERS
   neighbor 100.70.0.2 description pe2
   neighbor 100.70.0.3 peer group MPLS-OVERLAY-PEERS
   neighbor 100.70.0.3 description pe3
   neighbor 100.70.0.5 peer group MPLS-OVERLAY-PEERS
   neighbor 100.70.0.5 description pe5
   !
   address-family evpn
      neighbor default encapsulation mpls
      neighbor MPLS-OVERLAY-PEERS activate
   !
   address-family ipv4
      no neighbor MPLS-OVERLAY-PEERS activate
   !
   address-family vpn-ipv4
      neighbor MPLS-OVERLAY-PEERS activate
   !
   address-family vpn-ipv6
      neighbor MPLS-OVERLAY-PEERS activate
```

# BFD

## Router BFD

### Router BFD Multihop Summary

| Interval | Minimum RX | Multiplier |
| -------- | ---------- | ---------- |
| 5000 | 5000 | 3 |

### Router BFD Device Configuration

```eos
!
router bfd
   multihop interval 5000 min-rx 5000 multiplier 3
```

# MPLS

## MPLS and LDP

### MPLS and LDP Summary

| Setting | Value |
| -------- | ---- |
| MPLS IP Enabled | True |
| LDP Enabled | False |
| LDP Router ID | - |
| LDP Interface Disabled Default | - |
| LDP Transport-Address Interface | - |

### MPLS and LDP Configuration

```eos
!
mpls ip
```

## MPLS Interfaces

| Interface | MPLS IP Enabled | LDP Enabled | IGP Sync |
| --------- | --------------- | ----------- | -------- |
| Ethernet1 | True | - | - |
| Ethernet2 | True | - | - |
| Loopback0 | - | - | - |

# Multicast

# Filters

# ACL

# VRF Instances

## VRF Instances Summary

| VRF Name | IP Routing |
| -------- | ---------- |
| MGMT | disabled |

## VRF Instances Device Configuration

```eos
!
vrf instance MGMT
```

# Quality Of Service

# EOS CLI

```eos
!
management security
   password encryption-key common

```
