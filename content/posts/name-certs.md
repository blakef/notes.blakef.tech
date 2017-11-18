---
title: "Name Certs"
date: 2017-11-08T21:39:11+02:00
draft: true
---

- [plex nuclear option](https://blog.filippo.io/how-plex-is-doing-https-for-all-its-users/)
- [CoreDNS](https://coredns.io/) 

# Reading

## Pro DNS and BIND 10

### Chpt. 1: DNS Introductino

- Primary and Secondary
- RFC 1034 & 1035
- TLD & SLD -> `foo{SLD}.com{TLD}.{root}`
    - gTLD & ccTLD
- Authority <-> Delegation
- ICANN
    - Registry Operators: operator authoritative gTLD DNS servers
    - Registrars: allow public to register gTLDs

**Resolvers** issue queries to (cache, proxy, etc...) that eventually will have recieved and **authoritative answer** from an **authoritative name server**.

- DNS Resolver: Reads 1..n **zone files**, responds to queries from local / remote clients in a configured manner.

- Zone Files
    - Set of Resource Records (RR):
        - [Req] Start of Authority (SOA)
        - A / AAAA Record (IPv4/6)
        - MX - mail server
        - NS Authoritative name severs for the domain (can be for subdomain delegation):
            - Glue Record (1..n A/AAAA records).

    ```
    ; IPv4 zone file for example.com
    $TTL 2d    ; default TTL for zone
    $ORIGIN example.com.
    ; Start of Authority record defining the key characteristics of the zone (domain)
    @         IN      SOA   ns1.example.com. hostmaster.example.com. (
                            2003080800 ; sn = serial number
                            12h        ; refresh
                            15m        ; retry = refresh retry
                            3w         ; expiry
                            2h         ; nx = nxdomain ttl
                            )
    ; name servers Resource Records for the domain
                  IN      NS      ns1.example.com.
    ; the second name servers is
    ; external to this zone (domain).
                  IN      NS      ns2.example.net.
    ; mail server Resource Records for the zone (domain)
    3w     IN      MX  10  mail.example.com.
    ; the second  mail servers is
    ; external to the zone (domain)
                  IN      MX  20  mail.anotherdomain.com.
    ; domain hosts includes NS and MX records defined above
    ; plus any others required
    ns1           IN      A       192.168.254.2
    mail          IN      A       192.168.254.4
    joe           IN      A       192.168.254.6
    www           IN      A       192.168.254.7
    ```

    - Master & Slave DNS Server: _master_ allows _zone transfers_ to _slaves_.  Both are authoritative.

### Chpt. 2: Zone files and Resource Records

- Comments: `; Foobar`
- Directives: `$ORIGIN blakef.tech`
- Resource Records (RR): single line, but '(' ')' can span multiple lines
- Mandatory:
    - $TTL: default TTL of RR if not specified
    - SOA, NS (>=2), 
- Optional: $ORIGIN, MX, A (host ip), AAAA, CNAME (alias)

### Chpt. 3: DNS Operation
### Chpt. 4: DNS Type
### Chpt. 5: DNS & IPv6
### Chpt. 9: DNS Diagnostics and Tools
### Chpt. 11: DNSSEC
