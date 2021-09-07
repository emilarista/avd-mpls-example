# dc1-spine1
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
- [Interfaces](#interfaces)
  - [Ethernet Interfaces](#ethernet-interfaces)
  - [Loopback Interfaces](#loopback-interfaces)
- [Routing](#routing)
  - [Service Routing Protocols Model](#service-routing-protocols-model)
  - [IP Routing](#ip-routing)
  - [IPv6 Routing](#ipv6-routing)
  - [Static Routes](#static-routes)
  - [Router BGP](#router-bgp)
- [Multicast](#multicast)
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
| Management1 | oob_management | oob | MGMT | 10.30.30.112/24 | 10.30.30.1 |

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
   ip address 10.30.30.112/24
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
| Ethernet1 | P2P_LINK_TO_DC1-SERVERLEAF1A_Ethernet1 | routed | - | 100.64.10.0/31 | default | 9214 | false | - | - |
| Ethernet2 | P2P_LINK_TO_DC1-SERVERLEAF1B_Ethernet1 | routed | - | 100.64.10.6/31 | default | 9214 | false | - | - |
| Ethernet3 | P2P_LINK_TO_DC1-BORDERLEAF1A_Ethernet1 | routed | - | 100.64.10.12/31 | default | 9214 | false | - | - |
| Ethernet4 | P2P_LINK_TO_DC1-BORDERLEAF1B_Ethernet1 | routed | - | 100.64.10.18/31 | default | 9214 | false | - | - |

### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   description P2P_LINK_TO_DC1-SERVERLEAF1A_Ethernet1
   no shutdown
   mtu 9214
   no switchport
   ip address 100.64.10.0/31
!
interface Ethernet2
   description P2P_LINK_TO_DC1-SERVERLEAF1B_Ethernet1
   no shutdown
   mtu 9214
   no switchport
   ip address 100.64.10.6/31
!
interface Ethernet3
   description P2P_LINK_TO_DC1-BORDERLEAF1A_Ethernet1
   no shutdown
   mtu 9214
   no switchport
   ip address 100.64.10.12/31
!
interface Ethernet4
   description P2P_LINK_TO_DC1-BORDERLEAF1B_Ethernet1
   no shutdown
   mtu 9214
   no switchport
   ip address 100.64.10.18/31
```

## Loopback Interfaces

### Loopback Interfaces Summary

#### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | EVPN_Overlay_Peering | default | 100.64.11.1/32 |

#### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | EVPN_Overlay_Peering | default | - |


### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description EVPN_Overlay_Peering
   no shutdown
   ip address 100.64.11.1/32
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
| default | false || MGMT | false |


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
| 65000.100|  100.64.11.1 |

| BGP Tuning |
| ---------- |
| no bgp default ipv4-unicast |
| distance bgp 20 200 200 |
| graceful-restart restart-time 300 |
| graceful-restart |
| bgp asn notation asdot |
| maximum-paths 4 ecmp 4 |

### Router BGP Peer Groups

#### IPv4-UNDERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | ipv4 |
| Send community | all |
| Maximum routes | 12000 |

### BGP Neighbors

| Neighbor | Remote AS | VRF |
| -------- | --------- | --- |
| 100.64.10.1 | 65000.110 | default |
| 100.64.10.7 | 65000.110 | default |
| 100.64.10.13 | 65000.111 | default |
| 100.64.10.19 | 65000.111 | default |

### Router BGP EVPN Address Family

#### Router BGP EVPN MAC-VRFs

#### Router BGP EVPN VRFs

### Router BGP Device Configuration

```eos
!
router bgp 65000.100
   router-id 100.64.11.1
   no bgp default ipv4-unicast
   distance bgp 20 200 200
   graceful-restart restart-time 300
   graceful-restart
   bgp asn notation asdot
   maximum-paths 4 ecmp 4
   neighbor IPv4-UNDERLAY-PEERS peer group
   neighbor IPv4-UNDERLAY-PEERS password 7 $1c$U4tL2vQP9QwZlxIV1K3/pw==
   neighbor IPv4-UNDERLAY-PEERS send-community
   neighbor IPv4-UNDERLAY-PEERS maximum-routes 12000
   neighbor 100.64.10.1 peer group IPv4-UNDERLAY-PEERS
   neighbor 100.64.10.1 remote-as 65000.110
   neighbor 100.64.10.1 description dc1-serverleaf1a_Ethernet1
   neighbor 100.64.10.7 peer group IPv4-UNDERLAY-PEERS
   neighbor 100.64.10.7 remote-as 65000.110
   neighbor 100.64.10.7 description dc1-serverleaf1b_Ethernet1
   neighbor 100.64.10.13 peer group IPv4-UNDERLAY-PEERS
   neighbor 100.64.10.13 remote-as 65000.111
   neighbor 100.64.10.13 description dc1-borderleaf1a_Ethernet1
   neighbor 100.64.10.19 peer group IPv4-UNDERLAY-PEERS
   neighbor 100.64.10.19 remote-as 65000.111
   neighbor 100.64.10.19 description dc1-borderleaf1b_Ethernet1
   redistribute connected route-map RM-CONN-2-BGP
   !
   address-family ipv4
      neighbor IPv4-UNDERLAY-PEERS activate
```

# Multicast

# Filters

## Prefix-lists

### Prefix-lists Summary

#### PL-LOOPBACKS-EVPN-OVERLAY

| Sequence | Action |
| -------- | ------ |
| 10 | permit 100.64.11.0/24 eq 32 |

### Prefix-lists Device Configuration

```eos
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 100.64.11.0/24 eq 32
```

## Route-maps

### Route-maps Summary

#### RM-CONN-2-BGP

| Sequence | Type | Match and/or Set |
| -------- | ---- | ---------------- |
| 10 | permit | match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY |

### Route-maps Device Configuration

```eos
!
route-map RM-CONN-2-BGP permit 10
   match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY
```

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
