# DMARC, DKIM, and SPF

## Definitions

**Sender Policy Framework (SPF)**: Says what IPs are allowed to send for this domain.

**DomainKeys Identified Mail (DKIM)**: Verified the email came from domain specified using signatures.

**Domain-based Message Authentication, Reporting, and Conformance (DMARC)**: Says what to do with emails that fail the above checks.

## Diagram
![DMARC Flow](https://github.com/user-attachments/assets/19141c39-b3ba-43dd-a77a-bd65bcd87cd7)

*Access this link to see the most updated version: [Canva](https://www.canva.com/design/DAGS70X--Bs/DUmDxfXvxUq2B9UZrjnN1g/view?utm_content=DAGS70X--Bs&utm_campaign=designshare&utm_medium=link&utm_source=editor)*

## Terms
It may be useful to see the sample email headers below while viewing this.

1. **The Enveloper From Address:** The envelope from address is used in the SMTP transaction and not directly in the headers, but is usually written to the "Return-Path domain".
2. **The Return-Path domain:** In general, the Return-Path designates the email address where bounced messages and other feedback are sent.

### Sample Email Headers
![Email Headers](https://github.com/user-attachments/assets/82dc3d3c-8e6a-4801-9737-5b8d33da1812)

*Access this link to see the most updated version: [Canva](https://www.canva.com/design/DAGrwMkfaUo/S6fQtf5M2OVyYp2SnYzCzw/view?utm_content=DAGrwMkfaUo&utm_campaign=designshare&utm_medium=link2&utm_source=uniquelinks&utlId=h47ea67f1d8)*

## Authentication Check
So what exactly is the authentication check? 

To pass DMARC, either SPF or DKIM has to verify and pass alignment. 

1. SPF
- For SPF to verify, the sending IP must be listed in the SPF record of the envelope from address.
- For SPF to align, the header from address must match the envelope address (generally in the return path header). 

2. DKIM
- For DKIM to pass, the hash of the specified fields must match the hash that is decrypted from the DKIM signature using the public key of the domain. 
- For DKIM to align, the "d=" domain in the DKIM signature must match the header from address. 

# Advanced

## Alignment
There are generally two types of alignment set in the DMARC record.

Strict means the domains must match exactly.

Relaxed includes the exact domain as well as subdomains. 


### SPF Alignment
DMARC checks if the From domain aligns with the Return-Path domain.

### DKIM Alignment
DMARC checks if the domain in the From domain aligns with the DKIM Signature domain.

## Example Records

### Example DMARC Record
```
v=DMARC1; p=reject; rua=mailto:dmarc-reports@example.com; ruf=mailto:forensic-reports@example.com; fo=1; adkim=s; aspf=s; pct=100;
```
`v=DMARC1`: Specifies the DMARC version.

`p=reject`: Instructs the receiving server to reject emails that fail DMARC.

`rua`: Where aggregate reports should be sent.

`ruf`: Where forensic reports should be sent.

`fo=1`: Requests detailed forensic reports for every failed email.
- `fo=0`: Generate a report only if both SPF and DKIM fail (this is the default behavior).
- `fo=1`: Generate a report for every email that fails either SPF or DKIM.
- `fo=d`: Generate a report if DKIM fails, regardless of SPF results.
- `fo=s`: Generate a report if SPF fails, regardless of DKIM results.

`adkim=s`: Align DKIM checks strictly with the domain in the "From" header.

`aspf=s`: Align SPF checks strictly with the domain in the "From" header.

`pct=100`: Apply the DMARC policy to 100% of messages.

### Example DKIM Record
```
v=DKIM1; k=rsa; p=MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAzDOjHRhvPDAF...
```
`v=DKIM1`: Specifies the DKIM version.

`k=rsa`: Specifies the key type (RSA).

`p=<public key>`: The public key used for verification, in Base64 format.

The domain used in the Host field (default._domainkey.example.com) is a combination of:
- default: The selector you use in your DKIM setup.
- _domainkey: Specifies that this is a DKIM record.
- example.com: Your domain.

### Example SPF Record
```
v=spf1 ip4:192.0.2.0/24 ip6:2001:db8::/32 include:mailgun.org ~all
```
`v=spf1`: Specifies the SPF version.

`ip4:192.0.2.0/24`: Authorizes this IPv4 address range to send emails.

`ip6:2001:db8::/32`: Authorizes this IPv6 address range to send emails.

`include:mailgun.org`: Authorizes Mailgun (third-party email service) to send emails for this domain.

`~all`: Soft fail for any server not listed in the SPF record. Other options:
- `-all`: Hard fail (reject).
- `+all`: Allow any server (not recommended).

## More About DKIM

### DKIM Selectors

In the example email, you may recall the below line

```DKIM-Signature: v=1; a=rsa-sha256; c=relaxed/relaxed; d=dundermifflin.com; h=From:To:Subject:Date:Message-ID; s=default; bh=abc123...; b=def456...```

The selector in this example is default as designated by s=default, but you may see something like `s1` or a random alphanumeric string. 

This, combined with the d=dundermifflin.com attribute, is what is used to check the DKIM record. In this example, it would check default._domainkey.dundermufflin.com. 

# Frequently Asked Questions (FAQs)

## What happens if the SPF policy is not set but DMARC is p=quarantine or p=reject? 
If the email passes DKIM, then it should pass DMARC and be delivered.

IF the email fails DKIM, then the SPF will count as a fail and it will fail DMARC.

## What happens when spf=pass, dkim=pass but dmarc=fail? 
DMARC fails likely due to alignment. 

## What does neutral DKIM mean?
No signature in the email or the receiver did not do a lookup.

## What policy does a sub-subdomain inherit? 
It seems most internet sources say that subdomains inherit from their parent domains, however in my experience the sub-subdomains actually inherit from the organizational domain not their immediate parent domain. 

Example:
- company.org is set to `p=reject`
- subsidiary.company.org is set to `p=quarantine`
- Then comms.subsidiary.company.org will be set to `p=reject` according to my experience despite internet sources.

# Further Reading
[Dmarcly](https://dmarcly.com/blog/how-to-implement-dmarc-dkim-spf-to-stop-email-spoofing-phishing-the-definitive-guide#anatomy-of-an-email-message)
