- [Errata Security: Falsehoods programmers believe about networks](https://web.archive.org/web/20210411013500/https://blog.erratasec.com/2012/06/falsehoods-programmers-believe-about.html#.YHJSSHnS9qs)
- [BBR: Congestion-Based Congestion Control - ACM Queue](https://queue.acm.org/detail.cfm?id=3022184)

## DNS

```
8.8.8.8
8.8.4.4
2001:4860:4860::8888
2001:4860:4860::8844
208.67.222.222
208.67.220.220
2620:0:ccc::2
2620:0:ccd::2
```

- [Get Started  |  Public DNS  |  Google Developers](https://developers.google.com/speed/public-dns/docs/using#google_public_dns_ip_addresses)
- [IPv6 | OpenDNS](https://www.opendns.com/about/innovations/ipv6/)
- [Use OpenDNS](https://use.opendns.com/)
- `cat /etc/resolv.conf`
- [Non-responsive DNS server or invalid DNS configuration can cause long delay before webpages load - Apple Support](https://support.apple.com/en-au/HT203244)
- [domain name system - dig works but ping does not resolve host - Server Fault](https://serverfault.com/questions/813158/dig-works-but-ping-does-not-resolve-host)
- [DNS Lecture Notes: contents](http://www-inf.int-evry.fr/~hennequi/CoursDNS/NOTES-COURS_eng/)

### DNS Record

```dns-zone
bar.example.com.        CNAME  foo.example.com.
foo.example.com.        A      192.0.2.23
@                  IN   TXT    "some text"
```

RR:
	DNS Resource Record

> A DNS zone file contains the list of all Resource Records in the DNS zone. Format is defined in RFC1035 page 33 with an addendum in RFC2308. A unique SOA RR and at least one NS RR for the zone name are required. A complete RR is a quintuplet {FQDN_NAME, TTL, CLASS, TYPE, RDATA} which can be in abbreviated form in some cases.
>
> - Comments start with a semicolon `;` and go to the end of line.
> - Empty lines are allowed; any combination of tabs and spaces acts as a delimiter.
> - RR are defined line by line as :
> - `[Name] [TTL] [CLASS] TYPE RDATA`
> 	- if no `Name`, the name is taken from the last stated RR
> 	- if `Name` exists, it starts at the first character of the line
> 	- if `Name` is not dot-terminated (non FQDN), the default domain name defined by `$ORIGIN` directives is concatenated to `Name`
> 	- if no `TTL`, the TTL is defined by `$TTL` directives.
> 	- if no `CLASS`, the CLASS is taken from the last stated RR
> 	- `TTL` and `CLASS` can be exchanged.
> - `$TTL integer_value` sets the default value of TTL for following RRs in file (RFC2308, bind>8.1)
> - `$ORIGIN fqdn_name` sets the default value of domain name for following RRs in file. Initially, in BIND, the value is set to the current zone name.
> - `$INCLUDE filename` inserts the named file into the current file. NB: be careful about value of `$TTL` or `$ORIGIN` after a `$INCLUDE`
> - `@` is used to denote the current default domain name.
> - `(` and `)` are used to group data that crosses a line boundary. Line terminations are not recognized within parentheses
> - `\` is used to quote special characters. Ex : `\.` can be used to place a dot character in a label; `\223` is the 8-bit character corresponding to decimal value 223.
>
> Stylistic hints:
>
> - Organize RR : Start with SOA, NS and MX of the zone, continue with delegation (NS) and glue. Group RR by names.
> - Comments are useful
> - Use spaces or tabulations for vertical alignment
> - Start file with a `$ORIGIN` and a `$TTL`
> - Try to avoid writing of the zone name in the file
> - Generate serial number in SOA as : year/month/day/version 4+2+2+2.
> - **BE CAREFUL**: Modify the serial number each time the master file is modified

`CNAME` can't be used for apex domain (aka bare domain or naked domain, ex: example.com):

- [networking - How to overcome root domain CNAME restrictions? - Stack Overflow](https://stackoverflow.com/questions/656009/how-to-overcome-root-domain-cname-restrictions)
- [Why a domain’s root can’t be a CNAME — and other tidbits about the DNS](https://www.freecodecamp.org/news/why-cant-a-domain-s-root-be-a-cname-8cbab38e5f5c/)

See also:

- [domain name system - What's the meaning of '@' in a DNS zone file? - Server Fault](https://serverfault.com/questions/83874/whats-the-meaning-of-in-a-dns-zone-file)
- [Zone file — Wikipedia](https://en.wikipedia.org/wiki/Zone_file)
- [List of DNS record types — Wikipedia](https://en.wikipedia.org/wiki/List_of_DNS_record_types)
- [Frequent Questions: DNS Records — Gandi Documentation documentation](https://docs.gandi.net/en/domain_names/faq/dns_records.html#do-you-have-examples-of-dns-records) - DNS records exampels

## Wake-on-LAN

- [Making a Linux home server sleep on idle and wake on demand — the simple way | Daniel P. Gross](https://web.archive.org/web/20230420192730/https://dgross.ca/blog/linux-home-server-auto-sleep/)
- [Wake-on-LAN - Wikipedia](https://en.wikipedia.org/wiki/Wake-on-LAN)

## IP address

- 0: 127.0.0.1 (or 0.0.0.0 on macOS)
- 10.50.1: 10.50.0.1
- 10.0.513: 10.0.2.1
- 167772673: 10.0.2.1
- A000201: 10.0.2.1
- 10.0.2.010: 10.0.2.8

- [There’s more than one way to write an IP address](https://web.archive.org/web/20230505170552/https://ma.ttias.be/theres-more-than-one-way-to-write-an-ip-address/)
