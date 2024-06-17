# Domain Name Server

## Core Function

Translate human friendly domain names (like google.com) into IP addresses (eg 123.45.67.89) which computers understand.

**Super important** as who remembers ip addresses now a days : )

If DNS server would be a large index in a single machine, this would be super risky! That's why the whole process of DNS resolution has been given to something called DNS resolvers which has step by step distributes processes to fetch an IP address.

DNS servers can be your ISP, your router, google ([8.8.8.8](8.8.8.8)), cloudflare ([1.1.1.1](1.1.1.1)) and can also be configured on your OS. In these

**Root Nameservers**: are the backbone! There are a total of 13 [root nameservers](https://www.iana.org/domains/root/servers) named `a.root-servers.com`, `b.root-servers.com`, ... upto `m.root-servers.com`. These server's ip addressed are literally **hard coded**.

## Are there 13 root nameservers?

**No!**

There are 13 ip addresses by these ip addresses are carry forwarded to a distributed system by levaraging something known as [Anycast](https://www.cloudflare.com/en-gb/learning/cdn/glossary/anycast-network/).

## How DNS Resolver works?

- Client types a domain name: `www.google.com`
- Computer asks your DNS resolver for the IP address.
- *Hierarchial Search begins!*
    - Request goes to nearest **root nameserver** asking for the IP address of the TLD nameserver for this domain name (which is `.com`)
    - Request goes to the TLD (Top Level Domain) server asking for the IP address for the **Authoritative Nameserver** responsible for holding the entry for this domain name.
    - Request foes to the Authoritative Nameserver and this returns the actual IP of the load balancer serving `www.google.com`.
- DNS resolver caches the IP address and returns to the client.

## Key Features of DNS

- **Distributed**: No single server hold everything => resilience, highly available
- **Caching**: Commonly request domain names are caches to reduce DNS lookup.
