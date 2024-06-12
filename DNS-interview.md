## DNS


### What is DNS? What is it used for?

- DNS (Domain Name Systems) is a protocol used for converting domain names into IP addresses.
- computer networking (at layer 3 of the OSP model) is done with IP addresses but for as humans it's hard to remember IP addresses, it's much easier to remember names. 
- This why we need something such as DNS to convert any domain name we type into an IP address. 
- You can think on DNS as a huge phonebook or database where each corresponding name has an IP.



### What is DNS resolution?
- The process of translating IP addresses to domain names.

### What is a name server?
- A server which is responsible for resolving DNS queries.

### What is the resolution sequence of: www.site.com
It's resolved in this order:

1) .
2) .com
3) site.com
4) www.site.com

### What is a domain name registrar?
-  "A domain name registrar provides domain name registrations to the general public. 
- A common misconception is that registrars sell domain names; these domain names are actually owned by registries and can only be leased by users."

### Given the following fqdn, <code>www.blipblop.com</code>, what is the root?

- `.` is the root


### Given the following fqdn, <code>www.blipblop.com</code>, what is the top level domain?

- `.com.` is the top level domain

### Given the following fqdn, <code>www.blipblop.com</code>, what is the second level domain?

- `blipblop.com.` is the second level domain


###  Given the following fqdn, <code>www.blipblop.com</code>, what is the domain?

- `www.blipblop.com.` is the domain


###  Describe DNS resolution workflow in high-level

In general the process is as follows:

  * The user types an address in the web browser (some_site.com)
  * The operating system gets a request from the browser to translate the address the user entered
  * A query created to check if a local entry of the address exists in the system. In case it doesn't, the request is forwarded to the DNS resolver
  * The Resolver is a server, usually configured by your ISP when you connect to the internet, that responsible for resolving your query by contacting other DNS servers
  * The Resolver contacts the root nameserver (aka as .)
  * The root nameserver either responds with the address you are looking for or it responds with the address of the relevant Top Level Domain DNS server (if your address ends with org then the org TLD)
  * The Resolver then contacts the TLD DNS. TLD DNS might respond with the address you are looking for. If it doesn't has the information, it will provide the address of SLD DNS server
  * SLD DNS server will reply with the address to the resolver
  * The Resolver passes this information to the browser while your OS also stores this information in the cache
  * The user cab browse the website with happiness and joy :D

---
## DNS - Records

###  What is a DNS record?
- A mapping between domain name and an IP address.

### What types of DNS records are there?

* A — IPv4 address
* AAAA — IPv6 address
* CNAME — Canonical name
* MX — Mail exchange
* NS — Name server
* TXT — Human-readable text
* SOA — Start of authority
  ...

A more detailed list, can be found [here](https://www.nslookup.io/learning/dns-record-types)


### What is a A record?

- A (Address): Maps a host name to an IPv4 address.

- When a computer has multiple adapter cards and IP addresses, it should have multiple address records.


### What is a AAAA record?

- An AAAA Record performs the same function as an A Record, but for an IPv6 Address.

### What is a CNAME record?

- CNAME: maps a hostname to another hostname.

- The target should be a domain name which must have an A or AAAA record. Think of it as an alias record.

### What is a PTR record?

- While an A record points a domain name to an IP address, a PTR record does the opposite and resolves the IP address to a domain name.

### What is a MX record?

- MX (Mail Exchange) Specifies a mail exchange server for the domain, which allows mail to be delivered to the correct mail servers in the domain.


### What is a NS record?

- NS: name servers that can respond to DNS queries

---
## DNS - TTL

### Explain DNS Records TTL

- [varonis.com](https://www.varonis.com/blog/dns-ttl): "DNS TTL (time to live) is a setting that tells the DNS resolver how long to cache a query before requesting a new one. 
- The information gathered is then stored in the cache of the recursive or local resolver for the TTL before it reaches back out to collect new, updated details."

--------------

###  Is DNS using TCP or UDP?

DNS uses UDP port 53 for resolving queries either regular or reverse. DNS uses TCP for zone transfer.


###  What is a zone? What types of zones are there?

- Forward and Reverse lookup zone