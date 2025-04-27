# The Basics About DNS Records

## Basics - Definitions

**Domain Name System (DNS)**: Translates human-readable domain names (e.g., `example.com`) into machine-readable IP addresses.

**A Record**: Maps a domain name to an IPv4 address.

**AAAA Record**: Maps a domain name to an IPv6 address.

**CNAME Record (Canonical Name)**: An alias that points one domain to another. For example, `blog.example.com` might point to `example.com`.

**MX Record (Mail Exchange)**: Specifies the mail server responsible for receiving emails for a domain.

**TXT Record (Text Record)**: Stores text-based information, often used for SPF, DKIM, and DMARC configurations to enhance email security.

**NS Record (Name Server)**: Defines which servers are authoritative for a domain’s DNS zone.

## Basics - DNS Record Example

### Example - A Record
`example.com. 3600 IN A 93.184.216.34`
- `example.com`: The domain name.
- `3600`: Time to live (TTL), in seconds.
- `IN`: Class of the record (always "IN" for internet).
- `A`: Record type, mapping to an IPv4 address.
- `93.184.216.34`: The IP address.

### Example - MX Record
`example.com. 3600 IN MX 10 mail.example.com.`
- `example.com`: The domain name.
- `3600`: TTL.
- `MX`: Record type, for mail servers.
- `10`: Priority (lower values indicate higher priority).
- `mail.example.com`: The mail server’s domain name.

### Example - CNAME Record
`www.example.com. 3600 IN CNAME example.com.`
- `www.example.com`: Alias for `example.com`.
- `3600`: TTL.
- `CNAME`: Canonical name record type.
- `example.com`: The domain being aliased.

### Example - TXT Record (SPF)
`example.com. 3600 IN TXT "v=spf1 ip4:192.0.2.0/24 -all"`
- `v=spf1`: SPF version.
- `ip4:192.0.2.0/24`: Allowed IP range.
- `-all`: Policy for unauthenticated IPs (fail).

## Advanced - DNS Record TTL

**Time to Live (TTL)**: Defines how long DNS information is cached before refreshing. Short TTL values (e.g., 300 seconds) are used for frequently changing records, while longer TTLs (e.g., 86400 seconds) reduce DNS query traffic for static records.

## Frequently Asked Questions (FAQs)

### What happens if a DNS record is missing?
If an essential record, like an `A` or `MX` record, is missing, services (such as your website or email) associated with the domain may become unreachable.

### How can I update a DNS record?
You can update your DNS records via your domain registrar or DNS hosting provider’s control panel.

### How long does it take for DNS changes to propagate?
It depends on the TTL value and global DNS cache propagation. Changes usually propagate within a few minutes to 48 hours.



