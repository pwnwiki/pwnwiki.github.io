DNS Configuration Issues

### Cache snooping
host -r www.google.com <nameserverIP>

### Open DNS resolution against a DNS server.
Supply a hostname not cached or inside a company owned domain.

nslookup www.nsa.gov <nameserverIP>
