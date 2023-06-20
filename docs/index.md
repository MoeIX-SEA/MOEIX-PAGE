# MoeIX
Moe Internet Exchanges

* A non-commercial Internet exchange point
* Operated by MoeQing Network

## Introduction

MoeIX is a non-commercial Internet Exchange Point (IXP) established in 2020. It provides traffic exchange services mainly for small ISPs, private networks. MoeIX is for learning and experimentation only and is not allowed to be used for commercial services and has no SLA.

## Current Location

* Seattle, Washington, USA

## Join

1. Join via VM
2. Join via tunnel

## Requirement

* Has a valid Public ASN
* Has at least /48 IPv6 address
* Have up-to-date PeeringDB information (preferably)
* Have up-to-date RIR Whois information
* Only send traffic to destinations advertised by BGP on the Peering LAN
* Does not send any multicast (except ARP/IPv6 ND) packets
* Prohibition of commercial service and abuse
* Have a active intranet, and running iBGP in it.
* Must have your own intranet (tunnel-based is acceptable) and include the provided VM in the network.
* Your intranet must have IGP and iBGP routing protocols running in it and be able to differentiate between peer and transit tables.
* The network interface attached on the IX VM is only used for constructing an internal network tunnel and not for any other services.

## Configure
We have three route servers, with 3 different policies  

**If you don't know what this is, please establish sessions to `RS Regular` only**  

* RS1, RS2
    * AS210979
    * A regular route server
    * [Filtering Policy](\RS#default-filtering-policy)
    * [Communities](\RS#announcement-control-via-bgp-communities)
    * In a nutshell: **Config the RS session as peering session**
    * You can connect to this RS without any concern, we will do IRR and RPKI validation for you.
    * A BGP connection with `RS1` is mandatory and you must **announce at least one IPv6 route from your own network**.
    * RS1: IP Address: `2a0a:280:f000:3::1`
    * RS2: IP Address: `2a0a:280:f000:3::2`

RS3:
    * AS210979
    * Transit route server
    * Your route will be transit to limewave via MoeQing Network
    * [Filtering Policy](\RS#default-filtering-policy)
    * [Communities](\RS#announcement-control-via-bgp-communities)
    * In a nutshell: **Config the RS session as upstream**
    * IP Address: `2a0a:280:f000:3::3`

## Members

See members list: [Members](\members)

## Limitations

### IX LAN
There are some security regulations for the IX peering LAN and the IX access port (usually eth1 for the IX VM).  

* Only permitted MAC addresses will be allowed
* arp-proxy and ndp-proxy must be disabled on the IX port. You can only respond the Neighbor Discovery packet that was sent to the Poema IX allocated `IX LAN` IP.
* L3 joining only. Bridging our port to other switches are not allowed.
* Participants must not announce ("leak") Poema IX peering LAN to other networks to reduce the potential attack surface.
* MOE IX does NOT support trunk port or VLAN mapping to our switches.
* Ethertypes: All forwarded frames must have one of the following ether types:
    * 0x0806 - ARP
    * 0x0800 - IPv4
    * 0x86dd - IPv6
* Link-local traffic: 
    * Only the following link-local traffic is allowed:
        * ICMPv6 Neighbor Solicitation / Advertisement
        * BGP session over link-local address in the IX peering LAN.
    * All other types of link-local traffic are prohibited, including but not limited to:
        * IGP traffic (e.g. OSPF, ISIS, IGRP, EIGRP)
        * BOOTP/DHCP
        * ICMPv6 Router Advertisement
        * ICMP redirects
        * Discovery Protocol：CDP, EDP
        * VLAN/trunking protocols：VTP, DTP
* Unicast/Multicast/Broadcast:
    * Only unicast traffic is allowed.
    * Frames forwarded must not be addressed to a multicast or broadcast MAC destination address except as follows:
        * ICMPv6 Neighbor Solicitation / Advertisement
    * Multicast/broadcast packet traffic must not exceed 1kbps
* Abuse on network infrastructure of IXP members is not allowed. Including but not limited to the following acts:
    *  Setting up default route or unauthorized routes to IXP member is prohibited.
    *  Sending routes that has malformed nexthop attribute such as point to other member is prohibited.
    *  Sending ICMP redirects packets to redirect your traffic to other members is prohibited.
    *  BGP hijacking without the authorization of the resource owner is prohibited. Including but not limited to the following behaviors
        * Prefix hijacking
        * ASN origin spoofing
        * AS path manipulation


## Special Thanks

* AS203472 KSKB for Technical support