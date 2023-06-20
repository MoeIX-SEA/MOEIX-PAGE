# MOEIX POP List

## Node List

Limewave-SEA

Pop
    
* Physical Location: US Seattle
* No SLA guarantee

Access Method

=== "Tunnel"

    1. OpenVPN
    2. GRETAP
    3. VXLAN

=== "IX VM"
    |Virt| CPU| Mem| Disk| MRC    |
    |----|----|----|-----|--------|
    | LXC| 1C |0.5G| 8G  | Free   |

    ???+ "VM Access Requirements"
        1. You must have your own intranet (tunnel-based is fine) and include our provided VM in your network.
        2. The internal network must have IGP and iBGP routing protocols running and be able to separate between peer and transit routes.
        3. The network interface attached on the IX VM is only used for constructing and connecting your internal network tunnel and not for any other services.
        4. You must peering with Route Server 1 and announce at least one active routes. Otherwise your free VM will be reclaimed.
        5. Learning with a humble attitude and be nice.
    ???+ "Free IX VM Rules"
        * Comply with the laws of the United States.
        * Personal use only; transfer, rental, and commercial uses are prohibited.
        * Cyber attacks are not allowed, such as ARP attack, ARP hijacking, scanning weak passwords, malicious exhaustion, DDoS, Trojan horses, and interfering with the operation of other networks and servers.
        * Spamming emails, spamming messages, spreading Trojans, viruses (including referencing malicious files from other servers) are not allowed.
        * Committing copyright violations using Torrents, BitTorrent, etc., is not allowed.
        * Usage of net_speeder/finalspeed/kcptun, etc., and any form of packet multiplication tools that may interfere with our network is prohibited.
        * Fair use terms apply to all resources. It is forbidden to consume/occupy CPU/network/bandwidth and other resources for a long time, such as rclone transferring/crypto mining or any action that makes my network feel very laggy.
        * Using it as a crawler or for account registration, etc., which may cause my IP to be marked as a bot is not allowed.
        * You may not run resource-consuming programs, such as online games or crypto mining.
        * VMs are only allowed for intranet tunneling and network configuration purposes (such as OSPF/eBGP/iBGP/Route Reflector).
        * The network provided by VMs is only for member-to-member or intranet traffic exchange and should not be used as an external network.
            * The connected entities must meet the following criteria:
                1. Other nodes within your internal network
                2. Peering partners
                3. apt update/git clone traffic required for node maintenance
            * Long-time bandwidth occupation that affects others' usage is prohibited.
        * Prohibited use for other purposes such as proxy hosting, etc., including but not limited to:
            * Provision of public services or public connections is prohibited.
                * Looking glass or network configuration-related services are allowed.
            * File hosting, such as image hosting/file/web servers, is prohibited.
            * VPN egress is prohibited.
            
    ### VM Connectivity
    
    Network Connections
    
    All **outgoing** connections from the IX VM follow the routing policies outlined below:
    
    | Dst IP           | Dst port                | Connection         | Speed     | MTU  |
    |------------------|-------------------------|--------------------|-----------|------|
    | 0.0.0.0/0        | `0~9999`                | wgcf(Cloudflare)   | 250M/250M | 1440 |
    | 0.0.0.0/0        | `10000~65535`<br>ICMP   | Limewave           | 250M/250M | 1500 |
    | 0.0.0.0/0        | Any(Public IP)          | MoeQing Network    | 250M/250M | 1480 |
    
    Connection Service  
    
    * Port forward:
        * 🂠🂠🂠=**VMID**
        tcp/udp porforwarding, a total of 100 portsrt
            *For internal network tunnel setup  
            * 🂠🂠🂠00~🂠🂠🂠99
        * ssh port:
            Connect to port 22 of VMID machine
            * :7🂠🂠🂠 → :22

=== "Limewave VM"

    Please contact Limewave support
    
=== "Physical"

    Not implement yet


