# Snark Holding Corp. (Snark Networks) — IP Geofeeds

This repository publishes the IP geolocation feeds for all networks operated by
Snark Holding Corp. ("Snark Networks"), per
[RFC 8805](https://datatracker.ietf.org/doc/html/rfc8805). Feeds are organized
by autonomous system number (ASN): each AS we operate has its own directory
containing a `geofeed.csv`.

Repository: <https://github.com/as-snark/geofeed>

## Repository layout

```
geofeed/
├── AS62787/
│   └── geofeed.csv
├── AS218771/
│   └── geofeed.csv
└── AS402577/
    └── geofeed.csv
```

## Feed URLs

Each feed is available at its canonical URL:

| ASN | Canonical geofeed URL |
|---------|------------------------------------------------------------------------------------------|
| AS62787 | `https://raw.githubusercontent.com/as-snark/geofeed/main/AS62787/geofeed.csv` |
| AS218771 | `https://raw.githubusercontent.com/as-snark/geofeed/main/AS218771/geofeed.csv` |
| AS402577 | `https://raw.githubusercontent.com/as-snark/geofeed/main/AS402577/geofeed.csv` |

Each URL is published in the `geofeed:` attribute of the corresponding RIR
WHOIS objects (inetnum/inet6num) for that ASN's prefixes.

## Format

All feeds follow the RFC 8805 CSV format:

```
ip_prefix,alpha2code,region,city,postal_code
```

- `ip_prefix` — IPv4 or IPv6 prefix in CIDR notation (required)
- `alpha2code` — ISO 3166-1 alpha-2 country code (e.g., `US`)
- `region` — ISO 3166-2 subdivision code (e.g., `US-NC`)
- `city` — free-form UTF-8 city name (commas are not permitted)
- `postal_code` — postal/ZIP code; deprecated by RFC 8805 §2.1.1.5, but
  included deliberately in our feeds

Notes:

- Files are UTF-8 text with CRLF line endings (RFC 8805 §2.1).
- Each file begins with a `#` comment line identifying the feed and its
  `Last updated:` timestamp; RFC 8805 treats text from `#` to end-of-line
  as a comment.
- All five fields are populated in every record; there is exactly one row
  per prefix.

Example (using RFC 5737 / RFC 3849 documentation ranges):

```
192.0.2.0/24,US,US-CA,Los Angeles,90001
198.51.100.0/24,US,US-TX,Dallas,75202
2001:db8:aa::/48,US,US-NY,New York,10001
```

## Consumers

These feeds are public and may be fetched by anyone, including geolocation
database vendors. No authentication is required. In the absence of HTTP
caching headers, consumers should refresh no more often than weekly, per
RFC 8805 §3.4. Data is provided as-is, without warranty; corrections are
welcome (see Contact).

## Updates

Feeds are updated as prefixes are added, re-geolocated, or reassigned.
Changes typically propagate to major geolocation databases within days to
weeks.

## Contact

For corrections or questions about a specific feed, contact the NOC listed
in the WHOIS/RDAP records for the relevant ASN, or email
`tac@snarknetworks.net`.
