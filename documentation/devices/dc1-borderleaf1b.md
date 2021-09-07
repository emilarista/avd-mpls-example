# dc1-borderleaf1b
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
- [MLAG](#mlag)
  - [MLAG Summary](#mlag-summary)
  - [MLAG Device Configuration](#mlag-device-configuration)
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
| Management1 | oob_management | oob | MGMT | 10.30.30.117/24 | 10.30.30.1 |

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
   ip address 10.30.30.117/24
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

# MLAG

## MLAG Summary

| Domain-id | Local-interface | Peer-address | Peer-link |
| --------- | --------------- | ------------ | --------- |
| dc1-borderleaf1 | Vlan4094 | 100.64.14.4 | Port-Channel3 |

Dual primary detection is disabled.

## MLAG Device Configuration

```eos
!
mlag configuration
   domain-id dc1-borderleaf1
   local-interface Vlan4094
   peer-address 100.64.14.4
   peer-link Port-Channel3
   reload-delay mlag 300
   reload-delay non-mlag 330
```

# Spanning Tree

## Spanning Tree Summary

STP mode: **mstp**

### MSTP Instance and Priority

| Instance(s) | Priority |
| -------- | -------- |
| 0 | 4096 |

### Global Spanning-Tree Settings

Spanning Tree disabled for VLANs: **4093-4094**

## Spanning Tree Device Configuration

```eos
!
spanning-tree mode mstp
no spanning-tree vlan-id 4093-4094
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
| 3009 | MLAG_iBGP_TENANT_A_INSIDE | LEAF_PEER_L3 |
| 3019 | MLAG_iBGP_TENANT_B_INSIDE | LEAF_PEER_L3 |
| 4093 | LEAF_PEER_L3 | LEAF_PEER_L3 |
| 4094 | MLAG_PEER | MLAG |

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
!
vlan 3009
   name MLAG_iBGP_TENANT_A_INSIDE
   trunk group LEAF_PEER_L3
!
vlan 3019
   name MLAG_iBGP_TENANT_B_INSIDE
   trunk group LEAF_PEER_L3
!
vlan 4093
   name LEAF_PEER_L3
   trunk group LEAF_PEER_L3
!
vlan 4094
   name MLAG_PEER
   trunk group MLAG
```

# Interfaces

## Ethernet Interfaces

### Ethernet Interfaces Summary

#### L2

| Interface | Description | Mode | VLANs | Native VLAN | Trunk Group | Channel-Group |
| --------- | ----------- | ---- | ----- | ----------- | ----------- | ------------- |
| Ethernet3 | MLAG_PEER_dc1-borderleaf1a_Ethernet3 | *trunk | *2-4094 | *- | *['LEAF_PEER_L3', 'MLAG'] | 3 |
| Ethernet4 | MLAG_PEER_dc1-borderleaf1a_Ethernet4 | *trunk | *2-4094 | *- | *['LEAF_PEER_L3', 'MLAG'] | 3 |

*Inherited from Port-Channel Interface

#### IPv4

| Interface | Description | Type | Channel Group | IP Address | VRF |  MTU | Shutdown | ACL In | ACL Out |
| --------- | ----------- | -----| ------------- | ---------- | ----| ---- | -------- | ------ | ------- |
| Ethernet1 | P2P_LINK_TO_DC1-SPINE1_Ethernet4 | routed | - | 100.64.10.19/31 | default | 9214 | false | - | - |
| Ethernet2 | P2P_LINK_TO_DC1-SPINE2_Ethernet4 | routed | - | 100.64.10.21/31 | default | 9214 | false | - | - |
| Ethernet5 | P2P_LINK_TO_dc2-borderleaf1_Ethernet5 | routed | - | 100.64.48.2/31 | default | 9214 | false | - | - |

### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   description P2P_LINK_TO_DC1-SPINE1_Ethernet4
   no shutdown
   mtu 9214
   no switchport
   ip address 100.64.10.19/31
!
interface Ethernet2
   description P2P_LINK_TO_DC1-SPINE2_Ethernet4
   no shutdown
   mtu 9214
   no switchport
   ip address 100.64.10.21/31
!
interface Ethernet3
   description MLAG_PEER_dc1-borderleaf1a_Ethernet3
   no shutdown
   channel-group 3 mode active
!
interface Ethernet4
   description MLAG_PEER_dc1-borderleaf1a_Ethernet4
   no shutdown
   channel-group 3 mode active
!
interface Ethernet5
   description P2P_LINK_TO_dc2-borderleaf1_Ethernet5
   no shutdown
   mtu 9214
   no switchport
   ip address 100.64.48.2/31
```

## Port-Channel Interfaces

### Port-Channel Interfaces Summary

#### L2

| Interface | Description | Type | Mode | VLANs | Native VLAN | Trunk Group | LACP Fallback Timeout | LACP Fallback Mode | MLAG ID | EVPN ESI |
| --------- | ----------- | ---- | ---- | ----- | ----------- | ------------| --------------------- | ------------------ | ------- | -------- |
| Port-Channel3 | MLAG_PEER_dc1-borderleaf1a_Po3 | switched | trunk | 2-4094 | - | ['LEAF_PEER_L3', 'MLAG'] | - | - | - | - |

### Port-Channel Interfaces Device Configuration

```eos
!
interface Port-Channel3
   description MLAG_PEER_dc1-borderleaf1a_Po3
   no shutdown
   switchport
   switchport trunk allowed vlan 2-4094
   switchport mode trunk
   switchport trunk group LEAF_PEER_L3
   switchport trunk group MLAG
```

## Loopback Interfaces

### Loopback Interfaces Summary

#### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | EVPN_Overlay_Peering | default | 100.64.11.7/32 |
| Loopback1 | VTEP_VXLAN_Tunnel_Source | default | 100.64.12.6/32 <br> 100.64.255.255/32 secondary |

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
   ip address 100.64.11.7/32
!
interface Loopback1
   description VTEP_VXLAN_Tunnel_Source
   no shutdown
   ip address 100.64.12.6/32
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
| Vlan3009 |  MLAG_PEER_L3_iBGP: vrf TENANT_A_INSIDE  |  TENANT_A_INSIDE  |  9214  |  false  |
| Vlan3019 |  MLAG_PEER_L3_iBGP: vrf TENANT_B_INSIDE  |  TENANT_B_INSIDE  |  9214  |  false  |
| Vlan4093 |  MLAG_PEER_L3_PEERING  |  default  |  9214  |  false  |
| Vlan4094 |  MLAG_PEER  |  default  |  9214  |  false  |

#### IPv4

| Interface | VRF | IP Address | IP Address Virtual | IP Router Virtual Address | VRRP | ACL In | ACL Out |
| --------- | --- | ---------- | ------------------ | ------------------------- | ---- | ------ | ------- |
| Vlan1 |  TENANT_A_INSIDE  |  -  |  10.0.1.1/24  |  -  |  -  |  -  |  -  |
| Vlan2 |  TENANT_A_INSIDE  |  -  |  10.0.2.1/24  |  -  |  -  |  -  |  -  |
| Vlan1275 |  TENANT_B_INSIDE  |  -  |  10.1.1.1/24  |  -  |  -  |  -  |  -  |
| Vlan1520 |  TENANT_B_INSIDE  |  -  |  10.1.246.1/24  |  -  |  -  |  -  |  -  |
| Vlan1521 |  TENANT_B_INSIDE  |  -  |  10.1.247.1/24  |  -  |  -  |  -  |  -  |
| Vlan3009 |  TENANT_A_INSIDE  |  100.64.13.5/31  |  -  |  -  |  -  |  -  |  -  |
| Vlan3019 |  TENANT_B_INSIDE  |  100.64.13.5/31  |  -  |  -  |  -  |  -  |  -  |
| Vlan4093 |  default  |  100.64.13.5/31  |  -  |  -  |  -  |  -  |  -  |
| Vlan4094 |  default  |  100.64.14.5/31  |  -  |  -  |  -  |  -  |  -  |


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
!
interface Vlan3009
   description MLAG_PEER_L3_iBGP: vrf TENANT_A_INSIDE
   no shutdown
   mtu 9214
   vrf TENANT_A_INSIDE
   ip address 100.64.13.5/31
!
interface Vlan3019
   description MLAG_PEER_L3_iBGP: vrf TENANT_B_INSIDE
   no shutdown
   mtu 9214
   vrf TENANT_B_INSIDE
   ip address 100.64.13.5/31
!
interface Vlan4093
   description MLAG_PEER_L3_PEERING
   no shutdown
   mtu 9214
   ip address 100.64.13.5/31
!
interface Vlan4094
   description MLAG_PEER
   no shutdown
   mtu 9214
   no autostate
   ip address 100.64.14.5/31
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
   vxlan virtual-router encapsulation mac-address mlag-system-id
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
| 65000.111|  100.64.11.7 |

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
| Next-hop unchanged | True |
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

#### MLAG-IPv4-UNDERLAY-PEER

| Settings | Value |
| -------- | ----- |
| Address Family | ipv4 |
| Remote AS | 65000.111 |
| Next-hop self | True |
| Send community | all |
| Maximum routes | 12000 |

### BGP Neighbors

| Neighbor | Remote AS | VRF |
| -------- | --------- | --- |
| 100.64.10.18 | 65000.100 | default |
| 100.64.10.20 | 65000.100 | default |
| 100.64.11.4 | 65000.110 | default |
| 100.64.11.5 | 65000.110 | default |
| 100.64.13.4 | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | default |
| 100.64.21.4 | 65000.210 | default |
| 100.64.48.3 | 65000.210 | default |
| 100.64.13.4 | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | TENANT_A_INSIDE |
| 100.64.13.4 | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | TENANT_B_INSIDE |

### Router BGP EVPN Address Family

#### Router BGP EVPN MAC-VRFs

##### VLAN Based

| VLAN | Route-Distinguisher | Both Route-Target | Import Route Target | Export Route-Target | Redistribute |
| ---- | ------------------- | ----------------- | ------------------- | ------------------- | ------------ |
| 1 | 100.64.11.7:10001 | 65000:10001 | - | - | learned |
| 2 | 100.64.11.7:10002 | 65000:10002 | - | - | learned |
| 1275 | 100.64.11.7:21275 | 65000:21275 | - | - | learned |
| 1520 | 100.64.11.7:21520 | 65000:21520 | - | - | learned |
| 1521 | 100.64.11.7:21521 | 65000:21521 | - | - | learned |

#### Router BGP EVPN VRFs

| VRF | Route-Distinguisher | Redistribute |
| --- | ------------------- | ------------ |
| TENANT_A_INSIDE | 100.64.11.7:10 | connected |
| TENANT_B_INSIDE | 100.64.11.7:20 | connected |

### Router BGP Device Configuration

```eos
!
router bgp 65000.111
   router-id 100.64.11.7
   no bgp default ipv4-unicast
   distance bgp 20 200 200
   graceful-restart restart-time 300
   graceful-restart
   bgp asn notation asdot
   maximum-paths 4 ecmp 4
   neighbor EVPN-OVERLAY-PEERS peer group
   neighbor EVPN-OVERLAY-PEERS next-hop-unchanged
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
   neighbor MLAG-IPv4-UNDERLAY-PEER peer group
   neighbor MLAG-IPv4-UNDERLAY-PEER remote-as 65000.111
   neighbor MLAG-IPv4-UNDERLAY-PEER next-hop-self
   neighbor MLAG-IPv4-UNDERLAY-PEER password 7 $1c$U4tL2vQP9QwZlxIV1K3/pw==
   neighbor MLAG-IPv4-UNDERLAY-PEER send-community
   neighbor MLAG-IPv4-UNDERLAY-PEER maximum-routes 12000
   neighbor MLAG-IPv4-UNDERLAY-PEER route-map RM-MLAG-PEER-IN in
   neighbor 100.64.10.18 peer group IPv4-UNDERLAY-PEERS
   neighbor 100.64.10.18 remote-as 65000.100
   neighbor 100.64.10.18 description dc1-spine1_Ethernet4
   neighbor 100.64.10.20 peer group IPv4-UNDERLAY-PEERS
   neighbor 100.64.10.20 remote-as 65000.100
   neighbor 100.64.10.20 description dc1-spine2_Ethernet4
   neighbor 100.64.11.4 peer group EVPN-OVERLAY-PEERS
   neighbor 100.64.11.4 remote-as 65000.110
   neighbor 100.64.11.4 description dc1-serverleaf1a
   neighbor 100.64.11.5 peer group EVPN-OVERLAY-PEERS
   neighbor 100.64.11.5 remote-as 65000.110
   neighbor 100.64.11.5 description dc1-serverleaf1b
   neighbor 100.64.13.4 peer group MLAG-IPv4-UNDERLAY-PEER
   neighbor 100.64.13.4 description dc1-borderleaf1a
   neighbor 100.64.21.4 peer group EVPN-OVERLAY-PEERS
   neighbor 100.64.21.4 remote-as 65000.210
   neighbor 100.64.21.4 description dc2-borderleaf1
   neighbor 100.64.21.4 route-map RM-EVPN-FILTER-AS65000.210 out
   neighbor 100.64.48.3 peer group IPv4-UNDERLAY-PEERS
   neighbor 100.64.48.3 remote-as 65000.210
   neighbor 100.64.48.3 description dc2-borderleaf1
   redistribute connected route-map RM-CONN-2-BGP
   !
   vlan 1
      rd 100.64.11.7:10001
      route-target both 65000:10001
      redistribute learned
   !
   vlan 2
      rd 100.64.11.7:10002
      route-target both 65000:10002
      redistribute learned
   !
   vlan 1275
      rd 100.64.11.7:21275
      route-target both 65000:21275
      redistribute learned
   !
   vlan 1520
      rd 100.64.11.7:21520
      route-target both 65000:21520
      redistribute learned
   !
   vlan 1521
      rd 100.64.11.7:21521
      route-target both 65000:21521
      redistribute learned
   !
   address-family evpn
      neighbor EVPN-OVERLAY-PEERS activate
   !
   address-family ipv4
      no neighbor EVPN-OVERLAY-PEERS activate
      neighbor IPv4-UNDERLAY-PEERS activate
      neighbor MLAG-IPv4-UNDERLAY-PEER activate
   !
   vrf TENANT_A_INSIDE
      rd 100.64.11.7:10
      route-target import evpn 65000:10
      route-target export evpn 65000:10
      router-id 100.64.11.7
      neighbor 100.64.13.4 peer group MLAG-IPv4-UNDERLAY-PEER
      redistribute connected
   !
   vrf TENANT_B_INSIDE
      rd 100.64.11.7:20
      route-target import evpn 65000:20
      route-target export evpn 65000:20
      router-id 100.64.11.7
      neighbor 100.64.13.4 peer group MLAG-IPv4-UNDERLAY-PEER
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
| 10 | permit 100.64.11.0/24 eq 32 |
| 20 | permit 100.64.12.0/24 eq 32 |
| 30 | permit 100.64.255.255/32 |

### Prefix-lists Device Configuration

```eos
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 100.64.11.0/24 eq 32
   seq 20 permit 100.64.12.0/24 eq 32
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

#### RM-MLAG-PEER-IN

| Sequence | Type | Match and/or Set |
| -------- | ---- | ---------------- |
| 10 | permit | set origin incomplete |

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
!
route-map RM-MLAG-PEER-IN permit 10
   description Make routes learned over MLAG Peer-link less preferred on spines to ensure optimal routing
   set origin incomplete
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
