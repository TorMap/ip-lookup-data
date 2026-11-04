# TorMap IP lookup data

Monthly snapshots of the free [DB-IP](https://db-ip.com) Lite databases used by [TorMap](https://github.com/TorMap/tormap)
to map Tor relay IP addresses to locations and autonomous systems. They live here, as release assets, so that the
TorMap repository does not grow with every update.

| Release asset | Source | Content |
| --- | --- | --- |
| `dbip-city-lite.mmdb.gz` | [IP to City Lite](https://db-ip.com/db/download/ip-to-city-lite) | City, coordinates and country per IP range |
| `dbip-asn-lite.mmdb.gz` | [IP to ASN Lite](https://db-ip.com/db/download/ip-to-asn-lite) | Autonomous system number and organization per IP range |
| `SHA256SUMS` | | SHA-256 checksums of both files |

Each release is named after the month of the DB-IP edition, for example `2026-11`. The files are copied unchanged in
the [MaxMind DB format](https://maxmind.github.io/MaxMind-DB/).

## How releases are made

The [release workflow](.github/workflows/release.yml) runs on the 2nd, 9th and 16th of each month. It downloads the
current month's files from `download.db-ip.com`, checks that they are valid gzip files with the expected MMDB database
type, and publishes them with their checksums. A run for a month that already has a release does nothing. It can also
be started by hand for a given month (DB-IP only keeps about the last two months).

Releases are immutable: once published, their assets and tag cannot be changed. TorMap pins a release by its name, and
its build verifies the downloaded files against `SHA256SUMS`. Renovate opens the TorMap PR for each new release.

Old releases are kept, so older TorMap versions stay buildable and past months can be looked up later.

## License

The data is provided by [DB-IP.com](https://db-ip.com) under the
[Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/). Anyone using it
must credit DB-IP.com, and web pages showing results must link to https://db-ip.com. The workflow and this README are
part of TorMap and licensed under GPL-3.0.
