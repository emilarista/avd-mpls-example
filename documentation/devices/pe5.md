# pe5
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
- [VLANs](#vlans)
  - [VLANs Summary](#vlans-summary)
  - [VLANs Device Configuration](#vlans-device-configuration)
- [Interfaces](#interfaces)
  - [Ethernet Interfaces](#ethernet-interfaces)
  - [Loopback Interfaces](#loopback-interfaces)
- [Routing](#routing)
  - [Service Routing Protocols Model](#service-routing-protocols-model)
  - [Virtual Router MAC Address](#virtual-router-mac-address)
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
- [Patch Panel](#patch-panel)
  - [Patch Panel Summary](#patch-panel-summary)
  - [Patch Panel Configuration](#patch-panel-configuration)
- [Multicast](#multicast)
  - [IP IGMP Snooping](#ip-igmp-snooping)
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
| Management1 | oob_management | oob | MGMT | 10.30.30.105/24 | 10.30.30.1 |

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
   ip address 10.30.30.105/24
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

STP mode: **mstp**

### MSTP Instance and Priority

| Instance(s) | Priority |
| -------- | -------- |
| 0 | 4096 |

### Global Spanning-Tree Settings


## Spanning Tree Device Configuration

```eos
!
spanning-tree mode mstp
spanning-tree mst 0 priority 4096
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

# VLANs

## VLANs Summary

| VLAN ID | Name | Trunk Groups |
| ------- | ---- | ------------ |
| 10 | TENANT_A_L2_SERVICE | - |
| 20 | TENANT_B_L2_SERVICE | - |

## VLANs Device Configuration

```eos
!
vlan 10
   name TENANT_A_L2_SERVICE
!
vlan 20
   name TENANT_B_L2_SERVICE
```

# Interfaces

## Ethernet Interfaces

### Ethernet Interfaces Summary

#### L2

| Interface | Description | Mode | VLANs | Native VLAN | Trunk Group | Channel-Group |
| --------- | ----------- | ---- | ----- | ----------- | ----------- | ------------- |
| Ethernet5 |  CPE_TENANT_A_SITE5_eth0 | access | 10 | - | - | - |
| Ethernet6.10 |  - | access | - | - | - | - |

*Inherited from Port-Channel Interface

#### IPv4

| Interface | Description | Type | Channel Group | IP Address | VRF |  MTU | Shutdown | ACL In | ACL Out |
| --------- | ----------- | -----| ------------- | ---------- | ----| ---- | -------- | ------ | ------- |
| Ethernet1 | P2P_LINK_TO_p6_Ethernet1 | routed | - | 100.64.48.20/31 | default | 1500 | false | - | - |
| Ethernet2 | P2P_LINK_TO_p4_Ethernet2 | routed | - | 100.64.48.17/31 | default | 1500 | false | - | - |
| Ethernet3 | P2P_LINK_TO_rr7_Ethernet3 | routed | - | unnumbered loopback0 | default | 1600 | false | - | - |
| Ethernet6.100 | TENANT_B_SITE_3_L3VPN_SUBIF | l3dot1q | - | 123.1.2.2/31 | TENANT_B_INTRA | - | false | - | - |

#### IPv6

| Interface | Description | Type | Channel Group | IPv6 Address | VRF | MTU | Shutdown | ND RA Disabled | Managed Config Flag | IPv6 ACL In | IPv6 ACL Out |
| --------- | ----------- | ---- | --------------| ------------ | --- | --- | -------- | -------------- | -------------------| ----------- | ------------ |
| Ethernet1 | P2P_LINK_TO_p6_Ethernet1 | routed | - | - | default | 1500 | false | - | *- | - | - |
| Ethernet2 | P2P_LINK_TO_p4_Ethernet2 | routed | - | - | default | 1500 | false | - | *- | - | - |

#### ISIS

| Interface | Channel Group | ISIS Instance | ISIS Metric | Mode | ISIS Circuit Type |
| --------- | ------------- | ------------- | ----------- | ---- | ----------------- |
| Ethernet1 | - | MPLS_UNDERLAY | 60 | point-to-point | level-2 |
| Ethernet2 | - | MPLS_UNDERLAY | 60 | point-to-point | level-2 |
| Ethernet3 | - | MPLS_UNDERLAY | 50 | point-to-point | level-1-2 |

### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   description P2P_LINK_TO_p6_Ethernet1
   no shutdown
   speed 100full
   mtu 1500
   no switchport
   ip address 100.64.48.20/31
   ipv6 enable
   isis enable MPLS_UNDERLAY
   isis circuit-type level-2
   isis metric 60
   isis network point-to-point
   no isis hello padding
   mpls ip
!
interface Ethernet2
   description P2P_LINK_TO_p4_Ethernet2
   no shutdown
   speed 100full
   mtu 1500
   no switchport
   ip address 100.64.48.17/31
   ipv6 enable
   isis enable MPLS_UNDERLAY
   isis circuit-type level-2
   isis metric 60
   isis network point-to-point
   no isis hello padding
   mpls ip
!
interface Ethernet3
   description P2P_LINK_TO_rr7_Ethernet3
   no shutdown
   mtu 1600
   no switchport
   ip address unnumbered loopback0
   isis enable MPLS_UNDERLAY
   isis circuit-type level-1-2
   isis metric 50
   isis network point-to-point
   no isis hello padding
   mpls ip
!
interface Ethernet5
   description CPE_TENANT_A_SITE5_eth0
   no shutdown
   switchport
   switchport access vlan 10
   switchport mode access
   spanning-tree portfast
!
interface Ethernet6
   no shutdown
   no switchport
!
interface Ethernet6.10
   no shutdown
   encapsulation vlan
     client dot1q 10
!
interface Ethernet6.100
   description TENANT_B_SITE_3_L3VPN_SUBIF
   no shutdown
   encapsulation dot1q vlan 100
   vrf TENANT_B_INTRA
   ip address 123.1.2.2/31
!
interface Ethernet7
   no shutdown
   no switchport
   no lldp transmit
   no lldp receive
```

## Loopback Interfaces

### Loopback Interfaces Summary

#### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | MPLS_Overlay_peering | default | 100.70.0.5/32 |

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
   ip address 100.70.0.5/32
   isis enable MPLS_UNDERLAY
   isis passive
   node-segment ipv4 index 205
```

# Routing
## Service Routing Protocols Model

Multi agent routing protocol model enabled

```eos
!
service routing protocols model multi-agent
```

## Virtual Router MAC Address

### Virtual Router MAC Address Summary

#### Virtual Router MAC Address: 00:1c:73:00:dc:00

### Virtual Router MAC Address Configuration

```eos
!
ip virtual-router mac-address 00:1c:73:00:dc:00
```

## IP Routing

### IP Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | true|| MGMT | false |
| TENANT_B_INTRA | true |
| TENANT_B_WAN | true |

### IP Routing Device Configuration

```eos
!
ip routing
no ip routing vrf MGMT
ip routing vrf TENANT_B_INTRA
ip routing vrf TENANT_B_WAN
```
## IPv6 Routing

### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | true | | MGMT | false |
| TENANT_B_INTRA | false |
| TENANT_B_WAN | false |

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
| Net-ID | 49.0001.0000.0001.0005.00 |
| Type | level-1-2 |
| Address Family | ipv4 unicast |
| Log Adjacency Changes | True |
| SR MPLS Enabled | True |
| SR MPLS Router-ID | 100.70.0.5 |

### ISIS Interfaces Summary

| Interface | ISIS Instance | ISIS Metric | Interface Mode |
| --------- | ------------- | ----------- | -------------- |
| Ethernet1 | MPLS_UNDERLAY | 60 | point-to-point |
| Ethernet2 | MPLS_UNDERLAY | 60 | point-to-point |
| Ethernet3 | MPLS_UNDERLAY | 50 | point-to-point |
| Loopback0 | MPLS_UNDERLAY | - | passive |

### Router ISIS Device Configuration

```eos
!
router isis MPLS_UNDERLAY
   net 49.0001.0000.0001.0005.00
   is-type level-1-2
   advertise passive-only
   router-id ipv4 100.70.0.5
   log-adjacency-changes
   timers local-convergence-delay 15000 protected-prefixes
   !
   address-family ipv4 unicast
      maximum-paths 4
      fast-reroute ti-lfa mode link-protection
   !
   segment-routing mpls
      router-id 100.70.0.5
      no shutdown
```

## Router BGP

### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 65000|  100.70.0.5 |

| BGP Tuning |
| ---------- |
| no bgp default ipv4-unicast |
| distance bgp 20 200 200 |
| graceful-restart restart-time 300 |
| graceful-restart |
| maximum-paths 4 ecmp 4 |

### Router BGP Peer Groups

#### MPLS-OVERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | mpls-vpn |
| Remote AS | 65000 |
| Source | Loopback0 |
| Bfd | true |
| Send community | all |
| Maximum routes | 0 (no limit) |

### BGP Neighbors

| Neighbor | Remote AS | VRF | Send-community | Maximum-routes |
| -------- | --------- | --- | -------------- | -------------- |
| 100.70.0.7 | Inherited from peer group MPLS-OVERLAY-PEERS | default | Inherited from peer group MPLS-OVERLAY-PEERS | Inherited from peer group MPLS-OVERLAY-PEERS |
| 100.70.0.8 | Inherited from peer group MPLS-OVERLAY-PEERS | default | Inherited from peer group MPLS-OVERLAY-PEERS | Inherited from peer group MPLS-OVERLAY-PEERS |
| 123.1.1.3 | 65202 | TENANT_B_INTRA | - | - |
| 192.168.48.3 | 65202 | TENANT_B_WAN | - | - |

### Router BGP EVPN Address Family

#### EVPN Neighbor Default Encapsulation

| Neighbor Default Encapsulation | Next-hop-self Source Interface |
| ------------------------------ | ------------------------------ |
| mpls | Loopback0 |

#### Router BGP EVPN MAC-VRFs

##### VLAN Based

| VLAN | Route-Distinguisher | Both Route-Target | Import Route Target | Export Route-Target | Redistribute |
| ---- | ------------------- | ----------------- | ------------------- | ------------------- | ------------ |
| 10 | 100.70.0.5:10010 | 65000:10010 | - | - | learned |
| 20 | 100.70.0.5:20020 | 65000:20020 | - | - | learned |

#### Router BGP VPWS Instances

| Instance | Route-Distinguisher | Both Route-Target| Pseudowire | Local ID | Remote ID |
| -------- | ------------------- | -----------------| ---------- | -------- | --------- |
| TENANT_A | 100.70.0.5:1000 | 65000:1000 | TEN_A_site2_site5_eline | 57 | 25 |

#### Router BGP EVPN VRFs

| VRF | Route-Distinguisher | Redistribute |
| --- | ------------------- | ------------ |
| TENANT_B_INTRA | 100.70.0.5:19 | connected |
| TENANT_B_WAN | 100.70.0.5:20 | connected |

### Router BGP Device Configuration

```eos
!
router bgp 65000
   router-id 100.70.0.5
   no bgp default ipv4-unicast
   distance bgp 20 200 200
   graceful-restart restart-time 300
   graceful-restart
   maximum-paths 4 ecmp 4
   neighbor MPLS-OVERLAY-PEERS peer group
   neighbor MPLS-OVERLAY-PEERS remote-as 65000
   neighbor MPLS-OVERLAY-PEERS update-source Loopback0
   neighbor MPLS-OVERLAY-PEERS bfd
   neighbor MPLS-OVERLAY-PEERS password 7 $1c$U4tL2vQP9QwZlxIV1K3/pw==
   neighbor MPLS-OVERLAY-PEERS send-community
   neighbor MPLS-OVERLAY-PEERS maximum-routes 0
   neighbor 100.70.0.7 peer group MPLS-OVERLAY-PEERS
   neighbor 100.70.0.7 description rr7
   neighbor 100.70.0.8 peer group MPLS-OVERLAY-PEERS
   neighbor 100.70.0.8 description rr8
   !
   vlan 10
      rd 100.70.0.5:10010
      route-target both 65000:10010
      redistribute learned
   !
   vlan 20
      rd 100.70.0.5:20020
      route-target both 65000:20020
      redistribute learned
   !
   vpws TENANT_A
      rd 100.70.0.5:1000
      route-target import export evpn 65000:1000
      !
      pseudowire TEN_A_site2_site5_eline
         evpn vpws id local 57 remote 25
   !
   address-family evpn
      neighbor default encapsulation mpls next-hop-self source-interface Loopback0
      neighbor MPLS-OVERLAY-PEERS activate
   !
   address-family ipv4
      no neighbor MPLS-OVERLAY-PEERS activate
   !
   address-family vpn-ipv4
      neighbor MPLS-OVERLAY-PEERS activate
      neighbor default encapsulation mpls next-hop-self source-interface Loopback0
   !
   address-family vpn-ipv6
      neighbor MPLS-OVERLAY-PEERS activate
      neighbor default encapsulation mpls next-hop-self source-interface Loopback0
   !
   vrf TENANT_B_INTRA
      rd 100.70.0.5:19
      route-target import evpn 65000:19
      route-target export evpn 65000:19
      router-id 100.70.0.5
      neighbor 123.1.1.3 remote-as 65202
      neighbor 123.1.1.3 password 7 $1c$U4tL2vQP9QwZlxIV1K3/pw==
      neighbor 123.1.1.3 description TENANT_B_CPE_SITE5
      redistribute connected
      !
      address-family ipv4
         neighbor 123.1.1.3 activate
   !
   vrf TENANT_B_WAN
      rd 100.70.0.5:20
      route-target import vpn-ipv4 65000:20
      route-target export vpn-ipv4 65000:20
      router-id 100.70.0.5
      neighbor 192.168.48.3 remote-as 65202
      neighbor 192.168.48.3 password 7 $1c$U4tL2vQP9QwZlxIV1K3/pw==
      neighbor 192.168.48.3 description TENANT_B_CPE_SITE5
      redistribute connected
      !
      address-family ipv4
         neighbor 192.168.48.3 activate
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
| Ethernet3 | True | - | - |
| Loopback0 | - | - | - |

# Patch Panel

## Patch Panel Summary

| Patch Name | Enabled | Connector A Type | Connector A Endpoint | Connector B Type | Connector B Endpoint |
| ---------- | ------- | ---------------- | -------------------- | ---------------- | -------------------- |
| TEN_A_site2_site5_eline | True | Interface | Ethernet7 | Pseudowire | bgp vpws TENANT_A pseudowire TEN_A_site2_site5_eline |
| TEN_B_site3_site5_eline | True | Interface | Ethernet6.10 | Pseudowire | bgp vpws TENANT_B pseudowire TEN_B_site3_site5_eline |

## Patch Panel Configuration

```eos
!
patch panel
   patch TEN_A_site2_site5_eline
      connector 1 interface Ethernet7
      connector 2 pseudowire bgp vpws TENANT_A pseudowire TEN_A_site2_site5_eline
   !
   patch TEN_B_site3_site5_eline
      connector 1 interface Ethernet6.10
      connector 2 pseudowire bgp vpws TENANT_B pseudowire TEN_B_site3_site5_eline
   !
```

# Multicast

## IP IGMP Snooping

### IP IGMP Snooping Summary

IGMP snooping is globally enabled.


### IP IGMP Snooping Device Configuration

```eos
```

# Filters

# ACL

# VRF Instances

## VRF Instances Summary

| VRF Name | IP Routing |
| -------- | ---------- |
| MGMT | disabled |
| TENANT_B_INTRA | enabled |
| TENANT_B_WAN | enabled |

## VRF Instances Device Configuration

```eos
!
vrf instance MGMT
!
vrf instance TENANT_B_INTRA
!
vrf instance TENANT_B_WAN
```

# Quality Of Service

# EOS CLI

```eos
!
management security
   password encryption-key common

```
