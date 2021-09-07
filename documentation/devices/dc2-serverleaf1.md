# dc2-serverleaf1
# Table of Contents
<!-- toc -->

- [Management](#management)
  - [Management Interfaces](#management-interfaces)
  - [Name Servers](#name-servers)
  - [NTP](#ntp)
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
  - [VLAN Interfaces](#vlan-interfaces)
  - [VXLAN Interface](#vxlan-interface)
- [Routing](#routing)
  - [Service Routing Protocols Model](#service-routing-protocols-model)
  - [Virtual Router MAC Address](#virtual-router-mac-address)
  - [IP Routing](#ip-routing)
  - [IPv6 Routing](#ipv6-routing)
  - [Static Routes](#static-routes)
  - [Router BGP](#router-bgp)
- [BFD](#bfd)
  - [Router BFD](#router-bfd)
- [Multicast](#multicast)
  - [IP IGMP Snooping](#ip-igmp-snooping)
- [Filters](#filters)
  - [Prefix-lists](#prefix-lists)
  - [Route-maps](#route-maps)
- [ACL](#acl)
- [VRF Instances](#vrf-instances)
  - [VRF Instances Summary](#vrf-instances-summary)
  - [VRF Instances Device Configuration](#vrf-instances-device-configuration)
- [Quality Of Service](#quality-of-service)
- [EOS CLI](#eos-cli)

<!-- toc -->
# Management

## Management Interfaces

### Management Interfaces Summary

#### IPv4

| Management Interface | description | Type | VRF | IP Address | Gateway |
| -------------------- | ----------- | ---- | --- | ---------- | ------- |
| Management1 | oob_management | oob | MGMT | 10.30.30.120/24 | 10.30.30.1 |

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
   ip address 10.30.30.120/24
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

## NTP

### NTP Summary

- Local Interface: Management1

- VRF: MGMT

| Node | Primary |
| ---- | ------- |
| 0.se.pool.ntp.org | true |
| 1.se.pool.ntp.org | - |

### NTP Device Configuration

```eos
!
ntp local-interface vrf MGMT Management1
ntp server vrf MGMT 0.se.pool.ntp.org prefer
ntp server vrf MGMT 1.se.pool.ntp.org
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

| CV Compression | Ingest gRPC URL | Ingest Authentication Key | Smash Excludes | Ingest Exclude | Ingest VRF |  NTP VRF | AAA Disabled |
| -------------- | --------------- | ------------------------- | -------------- | -------------- | ---------- | -------- | ------ |
| gzip | 10.20.20.20:9910 | dudeface | ale,flexCounter,hardware,kni,pulse,strata | /Sysdb/cell/1/agent,/Sysdb/cell/2/agent | MGMT | MGMT | False |

### TerminAttr Daemon Device Configuration

```eos
!
daemon TerminAttr
   exec /usr/bin/TerminAttr -ingestgrpcurl=10.20.20.20:9910 -cvcompression=gzip -ingestauth=key,dudeface -smashexcludes=ale,flexCounter,hardware,kni,pulse,strata -ingestexclude=/Sysdb/cell/1/agent,/Sysdb/cell/2/agent -ingestvrf=MGMT -taillogs
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
| 1 | TENANT_A_INSIDE_L3_TEST_1 | - |
| 2 | TENANT_A_INSIDE_L3_TEST_2 | - |
| 1275 | TENANT_B_INSIDE_L3_TEST_2_1 | - |
| 1520 | TENANT_B_INSIDE_L3_TEST_2_246 | - |
| 1521 | TENANT_B_INSIDE_L3_TEST_2_247 | - |

## VLANs Device Configuration

```eos
!
vlan 1
   name TENANT_A_INSIDE_L3_TEST_1
!
vlan 2
   name TENANT_A_INSIDE_L3_TEST_2
!
vlan 1275
   name TENANT_B_INSIDE_L3_TEST_2_1
!
vlan 1520
   name TENANT_B_INSIDE_L3_TEST_2_246
!
vlan 1521
   name TENANT_B_INSIDE_L3_TEST_2_247
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
| Ethernet1 | P2P_LINK_TO_DC2-SPINE1_Ethernet2 | routed | - | 100.64.20.7/31 | default | 9214 | false | - | - |

### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   description P2P_LINK_TO_DC2-SPINE1_Ethernet2
   no shutdown
   mtu 9214
   no switchport
   ip address 100.64.20.7/31
```

## Loopback Interfaces

### Loopback Interfaces Summary

#### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | EVPN_Overlay_Peering | default | 100.64.21.5/32 |
| Loopback1 | VTEP_VXLAN_Tunnel_Source | default | 100.64.22.5/32 <br> 100.64.255.255/32 secondary |

#### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | EVPN_Overlay_Peering | default | - |
| Loopback1 | VTEP_VXLAN_Tunnel_Source | default | - |


### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description EVPN_Overlay_Peering
   no shutdown
   ip address 100.64.21.5/32
!
interface Loopback1
   description VTEP_VXLAN_Tunnel_Source
   no shutdown
   ip address 100.64.22.5/32
   ip address 100.64.255.255/32 secondary
```

## VLAN Interfaces

### VLAN Interfaces Summary

| Interface | Description | VRF |  MTU | Shutdown |
| --------- | ----------- | --- | ---- | -------- |
| Vlan1 |  TENANT_A_INSIDE_L3_TEST_1  |  TENANT_A_INSIDE  |  -  |  false  |
| Vlan2 |  TENANT_A_INSIDE_L3_TEST_2  |  TENANT_A_INSIDE  |  -  |  false  |
| Vlan1275 |  TENANT_B_INSIDE_L3_TEST_2_1  |  TENANT_B_INSIDE  |  -  |  false  |
| Vlan1520 |  TENANT_B_INSIDE_L3_TEST_2_246  |  TENANT_B_INSIDE  |  -  |  false  |
| Vlan1521 |  TENANT_B_INSIDE_L3_TEST_2_247  |  TENANT_B_INSIDE  |  -  |  false  |

#### IPv4

| Interface | VRF | IP Address | IP Address Virtual | IP Router Virtual Address | VRRP | ACL In | ACL Out |
| --------- | --- | ---------- | ------------------ | ------------------------- | ---- | ------ | ------- |
| Vlan1 |  TENANT_A_INSIDE  |  -  |  10.0.1.1/24  |  -  |  -  |  -  |  -  |
| Vlan2 |  TENANT_A_INSIDE  |  -  |  10.0.2.1/24  |  -  |  -  |  -  |  -  |
| Vlan1275 |  TENANT_B_INSIDE  |  -  |  10.1.1.1/24  |  -  |  -  |  -  |  -  |
| Vlan1520 |  TENANT_B_INSIDE  |  -  |  10.1.246.1/24  |  -  |  -  |  -  |  -  |
| Vlan1521 |  TENANT_B_INSIDE  |  -  |  10.1.247.1/24  |  -  |  -  |  -  |  -  |


### VLAN Interfaces Device Configuration

```eos
!
interface Vlan1
   description TENANT_A_INSIDE_L3_TEST_1
   no shutdown
   vrf TENANT_A_INSIDE
   ip address virtual 10.0.1.1/24
!
interface Vlan2
   description TENANT_A_INSIDE_L3_TEST_2
   no shutdown
   vrf TENANT_A_INSIDE
   ip address virtual 10.0.2.1/24
!
interface Vlan1275
   description TENANT_B_INSIDE_L3_TEST_2_1
   no shutdown
   vrf TENANT_B_INSIDE
   ip address virtual 10.1.1.1/24
!
interface Vlan1520
   description TENANT_B_INSIDE_L3_TEST_2_246
   no shutdown
   vrf TENANT_B_INSIDE
   ip address virtual 10.1.246.1/24
!
interface Vlan1521
   description TENANT_B_INSIDE_L3_TEST_2_247
   no shutdown
   vrf TENANT_B_INSIDE
   ip address virtual 10.1.247.1/24
```

## VXLAN Interface

### VXLAN Interface Summary

#### Source Interface: Loopback1

#### UDP port: 4789

#### VLAN to VNI Mappings

| VLAN | VNI |
| ---- | --- |
| 1 | 10001 |
| 2 | 10002 |
| 1275 | 21275 |
| 1520 | 21520 |
| 1521 | 21521 |

#### VRF to VNI Mappings

| VLAN | VNI |
| ---- | --- |
| TENANT_A_INSIDE | 10 |
| TENANT_B_INSIDE | 20 |

### VXLAN Interface Device Configuration

```eos
!
interface Vxlan1
   vxlan source-interface Loopback1
   vxlan udp-port 4789
   vxlan vlan 1 vni 10001
   vxlan vlan 2 vni 10002
   vxlan vlan 1275 vni 21275
   vxlan vlan 1520 vni 21520
   vxlan vlan 1521 vni 21521
   vxlan vrf TENANT_A_INSIDE vni 10
   vxlan vrf TENANT_B_INSIDE vni 20
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
| TENANT_A_INSIDE | true |
| TENANT_B_INSIDE | true |

### IP Routing Device Configuration

```eos
!
ip routing
no ip routing vrf MGMT
ip routing vrf TENANT_A_INSIDE
ip routing vrf TENANT_B_INSIDE
```
## IPv6 Routing

### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | false || MGMT | false |
| TENANT_A_INSIDE | false |
| TENANT_B_INSIDE | false |


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

## Router BGP

### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 65000.211|  100.64.21.5 |

| BGP Tuning |
| ---------- |
| no bgp default ipv4-unicast |
| distance bgp 20 200 200 |
| graceful-restart restart-time 300 |
| graceful-restart |
| bgp asn notation asdot |
| maximum-paths 4 ecmp 4 |

### Router BGP Peer Groups

#### EVPN-OVERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | evpn |
| Source | Loopback0 |
| Bfd | true |
| Ebgp multihop | 10 |
| Send community | all |
| Maximum routes | 0 (no limit) |

#### IPv4-UNDERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | ipv4 |
| Send community | all |
| Maximum routes | 12000 |

### BGP Neighbors

| Neighbor | Remote AS | VRF |
| -------- | --------- | --- |
| 100.64.20.6 | 65000.200 | default |
| 100.64.21.4 | 65000.210 | default |
| 1.2.3.4 | 65499.100 | TENANT_A_INSIDE |

### Router BGP EVPN Address Family

#### Router BGP EVPN MAC-VRFs

##### VLAN Based

| VLAN | Route-Distinguisher | Both Route-Target | Import Route Target | Export Route-Target | Redistribute |
| ---- | ------------------- | ----------------- | ------------------- | ------------------- | ------------ |
| 1 | 100.64.21.5:10001 | 65000:10001 | - | - | learned |
| 2 | 100.64.21.5:10002 | 65000:10002 | - | - | learned |
| 1275 | 100.64.21.5:21275 | 65000:21275 | - | - | learned |
| 1520 | 100.64.21.5:21520 | 65000:21520 | - | - | learned |
| 1521 | 100.64.21.5:21521 | 65000:21521 | - | - | learned |

#### Router BGP EVPN VRFs

| VRF | Route-Distinguisher | Redistribute |
| --- | ------------------- | ------------ |
| TENANT_A_INSIDE | 100.64.21.5:10 | connected |
| TENANT_B_INSIDE | 100.64.21.5:20 | connected |

### Router BGP Device Configuration

```eos
!
router bgp 65000.211
   router-id 100.64.21.5
   no bgp default ipv4-unicast
   distance bgp 20 200 200
   graceful-restart restart-time 300
   graceful-restart
   bgp asn notation asdot
   maximum-paths 4 ecmp 4
   neighbor EVPN-OVERLAY-PEERS peer group
   neighbor EVPN-OVERLAY-PEERS update-source Loopback0
   neighbor EVPN-OVERLAY-PEERS bfd
   neighbor EVPN-OVERLAY-PEERS ebgp-multihop 10
   neighbor EVPN-OVERLAY-PEERS password 7 $1c$U4tL2vQP9QwZlxIV1K3/pw==
   neighbor EVPN-OVERLAY-PEERS send-community
   neighbor EVPN-OVERLAY-PEERS maximum-routes 0
   neighbor IPv4-UNDERLAY-PEERS peer group
   neighbor IPv4-UNDERLAY-PEERS password 7 $1c$U4tL2vQP9QwZlxIV1K3/pw==
   neighbor IPv4-UNDERLAY-PEERS send-community
   neighbor IPv4-UNDERLAY-PEERS maximum-routes 12000
   neighbor 100.64.20.6 peer group IPv4-UNDERLAY-PEERS
   neighbor 100.64.20.6 remote-as 65000.200
   neighbor 100.64.20.6 description dc2-spine1_Ethernet2
   neighbor 100.64.21.4 peer group EVPN-OVERLAY-PEERS
   neighbor 100.64.21.4 remote-as 65000.210
   neighbor 100.64.21.4 description dc2-borderleaf1
   neighbor 100.64.21.4 route-map RM-EVPN-FILTER-AS65000.210 out
   redistribute connected route-map RM-CONN-2-BGP
   !
   vlan 1
      rd 100.64.21.5:10001
      route-target both 65000:10001
      redistribute learned
   !
   vlan 2
      rd 100.64.21.5:10002
      route-target both 65000:10002
      redistribute learned
   !
   vlan 1275
      rd 100.64.21.5:21275
      route-target both 65000:21275
      redistribute learned
   !
   vlan 1520
      rd 100.64.21.5:21520
      route-target both 65000:21520
      redistribute learned
   !
   vlan 1521
      rd 100.64.21.5:21521
      route-target both 65000:21521
      redistribute learned
   !
   address-family evpn
      neighbor EVPN-OVERLAY-PEERS activate
   !
   address-family ipv4
      no neighbor EVPN-OVERLAY-PEERS activate
      neighbor IPv4-UNDERLAY-PEERS activate
   !
   vrf TENANT_A_INSIDE
      rd 100.64.21.5:10
      route-target import evpn 65000:10
      route-target export evpn 65000:10
      router-id 100.64.21.5
      neighbor 1.2.3.4 remote-as 65499.100
      neighbor 1.2.3.4 password 7 $1c$U4tL2vQP9QwZlxIV1K3/pw==
      neighbor 1.2.3.4 description something-test
      neighbor 1.2.3.4 ebgp-multihop 5
      neighbor 1.2.3.4 send-community
      redistribute connected
      !
      address-family ipv4
         neighbor 1.2.3.4 activate
   !
   vrf TENANT_B_INSIDE
      rd 100.64.21.5:20
      route-target import evpn 65000:20
      route-target export evpn 65000:20
      router-id 100.64.21.5
      redistribute connected
```

# BFD

## Router BFD

### Router BFD Multihop Summary

| Interval | Minimum RX | Multiplier |
| -------- | ---------- | ---------- |
| 5000 | 5000 | 3 |

### Router BFD Multihop Device Configuration

```eos
!
router bfd
   multihop interval 5000 min-rx 5000 multiplier 3
```

# Multicast

## IP IGMP Snooping

### IP IGMP Snooping Summary

IGMP snooping is globally enabled.


### IP IGMP Snooping Device Configuration

```eos
```

# Filters

## Prefix-lists

### Prefix-lists Summary

#### PL-LOOPBACKS-EVPN-OVERLAY

| Sequence | Action |
| -------- | ------ |
| 10 | permit 100.64.21.0/24 eq 32 |
| 20 | permit 100.64.22.0/24 eq 32 |
| 30 | permit 100.64.255.255/32 |

### Prefix-lists Device Configuration

```eos
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 100.64.21.0/24 eq 32
   seq 20 permit 100.64.22.0/24 eq 32
   seq 30 permit 100.64.255.255/32
```

## Route-maps

### Route-maps Summary

#### RM-CONN-2-BGP

| Sequence | Type | Match and/or Set |
| -------- | ---- | ---------------- |
| 10 | permit | match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY |

#### RM-EVPN-FILTER-AS65000.210

| Sequence | Type | Match and/or Set |
| -------- | ---- | ---------------- |
| 10 | deny | match as 65000.210 |

### Route-maps Device Configuration

```eos
!
route-map RM-CONN-2-BGP permit 10
   match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY
!
route-map RM-EVPN-FILTER-AS65000.210 deny 10
   match as 65000.210
!
route-map RM-EVPN-FILTER-AS65000.210 permit 20
```

# ACL

# VRF Instances

## VRF Instances Summary

| VRF Name | IP Routing |
| -------- | ---------- |
| MGMT | disabled |
| TENANT_A_INSIDE | enabled |
| TENANT_B_INSIDE | enabled |

## VRF Instances Device Configuration

```eos
!
vrf instance MGMT
!
vrf instance TENANT_A_INSIDE
!
vrf instance TENANT_B_INSIDE
```

# Quality Of Service

# EOS CLI

```eos
!
management security
   password encryption-key common

```