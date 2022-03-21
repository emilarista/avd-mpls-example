# pe1
# Table of Contents

- [Management](#management)
  - [Management Interfaces](#management-interfaces)
  - [Name Servers](#name-servers)
  - [Management API HTTP](#management-api-http)
- [Authentication](#authentication)
  - [Local Users](#local-users)
- [Monitoring](#monitoring)
  - [TerminAttr Daemon](#terminattr-daemon)
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
  - [Port-Channel Interfaces](#port-channel-interfaces)
  - [Loopback Interfaces](#loopback-interfaces)
  - [VLAN Interfaces](#vlan-interfaces)
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
  - [Route-maps](#route-maps)
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
| Management1 | oob_management | oob | MGMT | 10.30.30.101/24 | 10.30.30.1 |

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
   ip address 10.30.30.101/24
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
| ---- | ----- |
| False | True |

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

# Spanning Tree

## Spanning Tree Summary

STP mode: **mstp**

### MSTP Instance and Priority

| Instance(s) | Priority |
| -------- | -------- |
| 0 | 4096 |

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
| 2020 | TENANT_B_INSIDE_FW | - |

## VLANs Device Configuration

```eos
!
vlan 10
   name TENANT_A_L2_SERVICE
!
vlan 2020
   name TENANT_B_INSIDE_FW
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
| Ethernet1 | P2P_LINK_TO_pe2_Ethernet1 | routed | - | 100.64.48.0/31 | default | 1500 | false | - | - |
| Ethernet2 | P2P_LINK_TO_p6_Ethernet2 | routed | - | 100.64.48.2/31 | default | 1500 | false | - | - |
| Ethernet3 | P2P_LINK_TO_rr7_Ethernet2 | routed | - | 100.64.48.4/31 | default | 1500 | false | - | - |
| Ethernet21/1 | TENANT_B_SITE_3_INTRA_L3VPN | routed | - | 172.16.3.0/31 | INTERNET | - | false | - | - |

#### IPv6

| Interface | Description | Type | Channel Group | IPv6 Address | VRF | MTU | Shutdown | ND RA Disabled | Managed Config Flag | IPv6 ACL In | IPv6 ACL Out |
| --------- | ----------- | ---- | --------------| ------------ | --- | --- | -------- | -------------- | -------------------| ----------- | ------------ |
| Ethernet1 | P2P_LINK_TO_pe2_Ethernet1 | routed | - | - | default | 1500 | false | - | *- | - | - |
| Ethernet3 | P2P_LINK_TO_rr7_Ethernet2 | routed | - | - | default | 1500 | false | - | *- | - | - |

#### ISIS

| Interface | Channel Group | ISIS Instance | ISIS Metric | Mode | ISIS Circuit Type | Hello Padding | Authentication Mode |
| --------- | ------------- | ------------- | ----------- | ---- | ----------------- | ------------- | ------------------- |
| Ethernet1 | - | CORE | 60 | point-to-point | level-2 | False | md5 |
| Ethernet2 | - | CORE | 60 | point-to-point | level-2 | True | - |
| Ethernet3 | - | CORE | 60 | point-to-point | level-2 | False | md5 |

### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   description P2P_LINK_TO_pe2_Ethernet1
   no shutdown
   speed 100full
   mtu 1500
   no switchport
   ip address 100.64.48.0/31
   ipv6 enable
   isis enable CORE
   isis circuit-type level-2
   isis metric 60
   isis network point-to-point
   no isis hello padding
   isis authentication mode md5
   isis authentication key 7 $1c$sTNAlR6rKSw=
   mpls ip
   mpls ldp interface
   mpls ldp igp sync
!
interface Ethernet2
   description P2P_LINK_TO_p6_Ethernet2
   no shutdown
   speed 100full
   mtu 1500
   no switchport
   ip address 100.64.48.2/31
   isis enable CORE
   isis circuit-type level-2
   isis metric 60
   isis network point-to-point
   isis hello padding
   mpls ip
   mpls ldp interface
   mpls ldp igp sync
!
interface Ethernet3
   description P2P_LINK_TO_rr7_Ethernet2
   no shutdown
   speed 100full
   mtu 1500
   no switchport
   ip address 100.64.48.4/31
   ipv6 enable
   isis enable CORE
   isis circuit-type level-2
   isis metric 60
   isis network point-to-point
   no isis hello padding
   isis authentication mode md5
   isis authentication key 7 $1c$sTNAlR6rKSw=
   mpls ip
   mpls ldp interface
   mpls ldp igp sync
!
interface Ethernet5
   description CPE_TENANT_A_SITE1_Ethernet1
   no shutdown
   channel-group 5 mode active
!
interface Ethernet21/1
   description TENANT_B_SITE_3_INTRA_L3VPN
   no shutdown
   no switchport
   vrf INTERNET
   ip address 172.16.3.0/31
```

## Port-Channel Interfaces

### Port-Channel Interfaces Summary

#### L2

| Interface | Description | Type | Mode | VLANs | Native VLAN | Trunk Group | LACP Fallback Timeout | LACP Fallback Mode | MLAG ID | EVPN ESI |
| --------- | ----------- | ---- | ---- | ----- | ----------- | ------------| --------------------- | ------------------ | ------- | -------- |

#### Flexible Encapsulation Interfaces

| Interface | Description | Type | Vlan ID | Client Unmatched | Client Dot1q VLAN | Client Dot1q Outer Tag | Client Dot1q Inner Tag | Network Retain Client Encapsulation | Network Dot1q VLAN | Network Dot1q Outer Tag | Network Dot1q Inner Tag |
| --------- | ----------- | ---- | ------- | -----------------| ----------------- | ---------------------- | ---------------------- | ----------------------------------- | ------------------ | ----------------------- | ----------------------- |
| Port-Channel5.10 | - | l2dot1q | - | False | 10 | - | - | True | - | - | - |
| Port-Channel5.111 | - | l2dot1q | 111 | False | 111 | - | - | True | - | - | - |
| Port-Channel5.222 | - | l2dot1q | 222 | False | 222 | - | - | True | - | - | - |
| Port-Channel5.333 | - | l2dot1q | 434 | False | 333 | - | - | True | - | - | - |
| Port-Channel5.1000 | - | l2dot1q | - | False | 1000 | - | - | True | - | - | - |
| Port-Channel5.1001 | - | l2dot1q | - | False | 1001 | - | - | True | - | - | - |
| Port-Channel5.1002 | - | l2dot1q | - | False | 1002 | - | - | True | - | - | - |
| Port-Channel5.1003 | - | l2dot1q | - | False | 1003 | - | - | True | - | - | - |

### Port-Channel Interfaces Device Configuration

```eos
!
interface Port-Channel5
   description CPE_TENANT_A_SITE1_EVPN-A-A-PortChannel
   no shutdown
   no switchport
   evpn ethernet-segment
      identifier 0000:0000:0303:0202:0101
      route-target import 03:03:02:02:01:01
   lacp system-id 0303.0202.0101
!
interface Port-Channel5.10
   no shutdown
   encapsulation vlan
      client dot1q 10 network client
!
interface Port-Channel5.111
   vlan id 111
   encapsulation vlan
      client dot1q 111 network client
   evpn ethernet-segment
      identifier 0000:0000:0303:0202:0111
      route-target import 03:03:02:02:01:11
!
interface Port-Channel5.222
   vlan id 222
   encapsulation vlan
      client dot1q 222 network client
   evpn ethernet-segment
      identifier 0000:0000:0303:0202:0222
      route-target import 03:03:02:02:02:22
!
interface Port-Channel5.333
   vlan id 434
   encapsulation vlan
      client dot1q 333 network client
   evpn ethernet-segment
      identifier 0000:0000:0303:0202:0222
      route-target import 03:03:02:02:02:22
!
interface Port-Channel5.1000
   no shutdown
   encapsulation vlan
      client dot1q 1000 network client
!
interface Port-Channel5.1001
   no shutdown
   encapsulation vlan
      client dot1q 1001 network client
!
interface Port-Channel5.1002
   no shutdown
   encapsulation vlan
      client dot1q 1002 network client
!
interface Port-Channel5.1003
   no shutdown
   encapsulation vlan
      client dot1q 1003 network client
```

## Loopback Interfaces

### Loopback Interfaces Summary

#### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | MPLS_Overlay_peering | default | 100.70.0.1/32 |

#### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | MPLS_Overlay_peering | default | - |

#### ISIS

| Interface | ISIS instance | ISIS metric | Interface mode |
| --------- | ------------- | ----------- | -------------- |
| Loopback0 | CORE | - | passive |

### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description MPLS_Overlay_peering
   no shutdown
   ip address 100.70.0.1/32
   isis enable CORE
   isis passive
   mpls ldp interface
   node-segment ipv4 index 201
```

## VLAN Interfaces

### VLAN Interfaces Summary

| Interface | Description | VRF |  MTU | Shutdown |
| --------- | ----------- | --- | ---- | -------- |
| Vlan2020 | TENANT_B_INSIDE_FW | TENANT_B_INTRA | - | false |

#### IPv4

| Interface | VRF | IP Address | IP Address Virtual | IP Router Virtual Address | VRRP | ACL In | ACL Out |
| --------- | --- | ---------- | ------------------ | ------------------------- | ---- | ------ | ------- |
| Vlan2020 |  TENANT_B_INTRA  |  10.1.255.2/27  |  -  |  10.1.255.1  |  -  |  -  |  -  |


### VLAN Interfaces Device Configuration

```eos
!
interface Vlan2020
   description TENANT_B_INSIDE_FW
   no shutdown
   vrf TENANT_B_INTRA
   ip address 10.1.255.2/27
   ip virtual-router address 10.1.255.1
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
| default | true |
| INTERNET | true |
| MGMT | false |
| TENANT_B_INTRA | true |

### IP Routing Device Configuration

```eos
!
ip routing
ip routing vrf INTERNET
no ip routing vrf MGMT
ip routing vrf TENANT_B_INTRA
```
## IPv6 Routing

### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | false |
| INTERNET | false |
| MGMT | false |
| TENANT_B_INTRA | false |

## Static Routes

### Static Routes Summary

| VRF | Destination Prefix | Next Hop IP             | Exit interface      | Administrative Distance       | Tag               | Route Name                    | Metric         |
| --- | ------------------ | ----------------------- | ------------------- | ----------------------------- | ----------------- | ----------------------------- | -------------- |
| MGMT | 0.0.0.0/0 | 10.30.30.1 | - | 1 | - | - | - |

### Static Routes Device Configuration

```eos
!
ip route vrf MGMT 0.0.0.0/0 10.30.30.1
```

## Router ISIS

### Router ISIS Summary

| Settings | Value |
| -------- | ----- |
| Instance | CORE |
| Net-ID | 49.0001.0000.0001.0001.00 |
| Type | level-1-2 |
| Address Family | ipv4 unicast |
| Router-ID | 100.70.0.1 |
| Log Adjacency Changes | True |
| MPLS LDP Sync Default | True |
| Local Convergence Delay (ms) | 15000 |
| Advertise Passive-only | True |
| SR MPLS Enabled | True |

### ISIS Interfaces Summary

| Interface | ISIS Instance | ISIS Metric | Interface Mode |
| --------- | ------------- | ----------- | -------------- |
| Ethernet1 | CORE | 60 | point-to-point |
| Ethernet2 | CORE | 60 | point-to-point |
| Ethernet3 | CORE | 60 | point-to-point |
| Loopback0 | CORE | - | passive |

### ISIS Segment-routing Node-SID

| Loopback | IPv4 Index | IPv6 Index |
| -------- | ---------- | ---------- |
| Loopback0 | 201 | - |

### Router ISIS Device Configuration

```eos
!
router isis CORE
   net 49.0001.0000.0001.0001.00
   is-type level-1-2
   router-id ipv4 100.70.0.1
   log-adjacency-changes
   mpls ldp sync default
   timers local-convergence-delay 15000 protected-prefixes
   advertise passive-only
   !
   address-family ipv4 unicast
      maximum-paths 4
      fast-reroute ti-lfa mode link-protection
   !
   segment-routing mpls
      no shutdown
```

## Router BGP

### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 65000|  100.70.0.1 |

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
| Address Family | mpls |
| Remote AS | 65000 |
| Source | Loopback0 |
| BFD | True |
| Send community | all |
| Maximum routes | 0 (no limit) |

### BGP Neighbors

| Neighbor | Remote AS | VRF | Shutdown | Send-community | Maximum-routes | Allowas-in | BFD | RIB Pre-Policy Retain |
| -------- | --------- | --- | -------- | -------------- | -------------- | ---------- | --- | -------------- |
| 100.70.0.7 | Inherited from peer group MPLS-OVERLAY-PEERS | default | - | Inherited from peer group MPLS-OVERLAY-PEERS | Inherited from peer group MPLS-OVERLAY-PEERS | - | Inherited from peer group MPLS-OVERLAY-PEERS | - |
| 100.70.0.8 | Inherited from peer group MPLS-OVERLAY-PEERS | default | - | Inherited from peer group MPLS-OVERLAY-PEERS | Inherited from peer group MPLS-OVERLAY-PEERS | - | Inherited from peer group MPLS-OVERLAY-PEERS | - |
| 172.16.3.1 | 65501 | INTERNET | - | - | 0 (no limit) | - | - | - |
| 10.1.255.4 | 12345 | TENANT_B_INTRA | - | - | - | - | - | - |

### Router BGP EVPN Address Family

#### EVPN Peer Groups

| Peer Group | Activate |
| ---------- | -------- |
| MPLS-OVERLAY-PEERS | True |

#### EVPN Neighbor Default Encapsulation

| Neighbor Default Encapsulation | Next-hop-self Source Interface |
| ------------------------------ | ------------------------------ |
| mpls | Loopback0 |

### Router BGP VLANs

| VLAN | Route-Distinguisher | Both Route-Target | Import Route Target | Export Route-Target | Redistribute |
| ---- | ------------------- | ----------------- | ------------------- | ------------------- | ------------ |
| 10 | 100.70.0.1:10010 | 65000:10010 | - | - | learned |
| 2020 | 100.70.0.1:22020 | 65000:22020 | - | - | learned |

### Router BGP VPWS Instances

| Instance | Route-Distinguisher | Both Route-Target | MPLS Control Word | Label Flow | MTU | Pseudowire | Local ID | Remote ID |
| -------- | ------------------- | ----------------- | ----------------- | -----------| --- | ---------- | -------- | --------- |
| TENANT_A | 100.70.0.1:1000 | 65000:1000 | False | False | - | TEN_A_site3_site5_eline_vlan_based_10 | 10010 | 58010 |
| TENANT_A | 100.70.0.1:1000 | 65000:1000 | False | False | - | TEN_A_site3_site5_eline_vlan_based_1000 | 11000 | 59000 |
| TENANT_A | 100.70.0.1:1000 | 65000:1000 | False | False | - | TEN_A_site3_site5_eline_vlan_based_1001 | 11001 | 59001 |
| TENANT_A | 100.70.0.1:1000 | 65000:1000 | False | False | - | TEN_A_site3_site5_eline_vlan_based_1002 | 11002 | 59002 |
| TENANT_A | 100.70.0.1:1000 | 65000:1000 | False | False | - | TEN_A_site3_site5_eline_vlan_based_1003 | 11003 | 59003 |

### Router BGP VRFs

| VRF | Route-Distinguisher | Redistribute |
| --- | ------------------- | ------------ |
| INTERNET | 100.70.0.1:19 | connected |
| TENANT_B_INTRA | 100.70.0.1:19 | connected |

### Router BGP Device Configuration

```eos
!
router bgp 65000
   router-id 100.70.0.1
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
      rd 100.70.0.1:10010
      route-target both 65000:10010
      redistribute learned
   !
   vlan 2020
      rd 100.70.0.1:22020
      route-target both 65000:22020
      redistribute learned
   !
   vpws TENANT_A
      rd 100.70.0.1:1000
      route-target import export evpn 65000:1000
      !
      pseudowire TEN_A_site3_site5_eline_vlan_based_10
         evpn vpws id local 10010 remote 58010
      !
      pseudowire TEN_A_site3_site5_eline_vlan_based_1000
         evpn vpws id local 11000 remote 59000
      !
      pseudowire TEN_A_site3_site5_eline_vlan_based_1001
         evpn vpws id local 11001 remote 59001
      !
      pseudowire TEN_A_site3_site5_eline_vlan_based_1002
         evpn vpws id local 11002 remote 59002
      !
      pseudowire TEN_A_site3_site5_eline_vlan_based_1003
         evpn vpws id local 11003 remote 59003
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
   vrf INTERNET
      rd 100.70.0.1:19
      route-target import evpn 65000:19
      route-target export evpn 65000:19
      router-id 100.70.0.1
      neighbor 172.16.3.1 remote-as 65501
      neighbor 172.16.3.1 description TENANT_B_CPE_SITE3
      neighbor 172.16.3.1 maximum-routes 0
      neighbor 172.16.3.1 default-originate
      redistribute connected
      !
      address-family ipv4
         neighbor 172.16.3.1 activate
   !
   vrf TENANT_B_INTRA
      rd 100.70.0.1:19
      route-target import vpn-ipv4 65000:19
      route-target import vpn-ipv6 65000:19
      route-target export vpn-ipv4 65000:19
      route-target export vpn-ipv6 65000:19
      router-id 100.70.0.1
      neighbor 10.1.255.4 remote-as 12345
      neighbor 10.1.255.4 password 7 $1c$U4tL2vQP9QwZlxIV1K3/pw==
      neighbor 10.1.255.4 description TENANT_B_CPE_SITE3
      neighbor 10.1.255.4 route-map RM-TENANT_B_INTRA-10.1.255.4-SET-NEXT-HOP-OUT out
      redistribute connected
      !
      address-family ipv4
         neighbor 10.1.255.4 activate
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
| LDP Enabled | True |
| LDP Router ID | 100.70.0.1 |
| LDP Interface Disabled Default | True |
| LDP Transport-Address Interface | Loopback0 |

### MPLS and LDP Configuration

```eos
!
mpls ip
!
mpls ldp
   interface disabled default
   router-id 100.70.0.1
   no shutdown
   transport-address interface Loopback0
```

## MPLS Interfaces

| Interface | MPLS IP Enabled | LDP Enabled | IGP Sync |
| --------- | --------------- | ----------- | -------- |
| Ethernet1 | True | True | True |
| Ethernet2 | True | True | True |
| Ethernet3 | True | True | True |
| Loopback0 | - | True | - |

# Patch Panel

## Patch Panel Summary

| Patch Name | Enabled | Connector A Type | Connector A Endpoint | Connector B Type | Connector B Endpoint |
| ---------- | ------- | ---------------- | -------------------- | ---------------- | -------------------- |
| TEN_A_site3_site5_eline_vlan_based_1000 | True | Interface | Port-Channel5.1000 | Pseudowire | bgp vpws TENANT_A pseudowire TEN_A_site3_site5_eline_vlan_based_1000 |
| TEN_A_site3_site5_eline_vlan_based_1001 | True | Interface | Port-Channel5.1001 | Pseudowire | bgp vpws TENANT_A pseudowire TEN_A_site3_site5_eline_vlan_based_1001 |
| TEN_A_site3_site5_eline_vlan_based_1002 | True | Interface | Port-Channel5.1002 | Pseudowire | bgp vpws TENANT_A pseudowire TEN_A_site3_site5_eline_vlan_based_1002 |
| TEN_A_site3_site5_eline_vlan_based_1003 | True | Interface | Port-Channel5.1003 | Pseudowire | bgp vpws TENANT_A pseudowire TEN_A_site3_site5_eline_vlan_based_1003 |
| TEN_A_site3_site5_eline_vlan_based_10 | True | Interface | Port-Channel5.10 | Pseudowire | bgp vpws TENANT_A pseudowire TEN_A_site3_site5_eline_vlan_based_10 |

## Patch Panel Configuration

```eos
!
patch panel
   patch TEN_A_site3_site5_eline_vlan_based_1000
      connector 1 interface Port-Channel5.1000
      connector 2 pseudowire bgp vpws TENANT_A pseudowire TEN_A_site3_site5_eline_vlan_based_1000
   !
   patch TEN_A_site3_site5_eline_vlan_based_1001
      connector 1 interface Port-Channel5.1001
      connector 2 pseudowire bgp vpws TENANT_A pseudowire TEN_A_site3_site5_eline_vlan_based_1001
   !
   patch TEN_A_site3_site5_eline_vlan_based_1002
      connector 1 interface Port-Channel5.1002
      connector 2 pseudowire bgp vpws TENANT_A pseudowire TEN_A_site3_site5_eline_vlan_based_1002
   !
   patch TEN_A_site3_site5_eline_vlan_based_1003
      connector 1 interface Port-Channel5.1003
      connector 2 pseudowire bgp vpws TENANT_A pseudowire TEN_A_site3_site5_eline_vlan_based_1003
   !
   patch TEN_A_site3_site5_eline_vlan_based_10
      connector 1 interface Port-Channel5.10
      connector 2 pseudowire bgp vpws TENANT_A pseudowire TEN_A_site3_site5_eline_vlan_based_10
   !
```

# Multicast

## IP IGMP Snooping

### IP IGMP Snooping Summary

| IGMP Snooping | Fast Leave | Interface Restart Query | Proxy | Restart Query Interval | Robustness Variable |
| ------------- | ---------- | ----------------------- | ----- | ---------------------- | ------------------- |
| Enabled | - | - | - | - | - |

### IP IGMP Snooping Device Configuration

```eos
```

# Filters

## Route-maps

### Route-maps Summary

#### RM-TENANT_B_INTRA-10.1.255.4-SET-NEXT-HOP-OUT

| Sequence | Type | Match and/or Set |
| -------- | ---- | ---------------- |
| 10 | permit | set ip next-hop 10.1.255.1 |

### Route-maps Device Configuration

```eos
!
route-map RM-TENANT_B_INTRA-10.1.255.4-SET-NEXT-HOP-OUT permit 10
   set ip next-hop 10.1.255.1
```

# ACL

# VRF Instances

## VRF Instances Summary

| VRF Name | IP Routing |
| -------- | ---------- |
| INTERNET | enabled |
| MGMT | disabled |
| TENANT_B_INTRA | enabled |

## VRF Instances Device Configuration

```eos
!
vrf instance INTERNET
!
vrf instance MGMT
!
vrf instance TENANT_B_INTRA
```

# Quality Of Service

# EOS CLI

```eos
!
management security
   password encryption-key common

```
