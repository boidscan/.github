# Boidscan

Boidscan is a free and open source index of publicly reachable services, in the spirit of Shodan and Censys, run by its community instead of a company.

## Goal

Knowing what is exposed on the internet should not depend on a commercial subscription. Boidscan aims to build that index as a shared public resource: anyone can run a node, anyone can query the results, and anyone can opt out.

The name comes from [Boids](https://en.wikipedia.org/wiki/Boids), Craig Reynolds' 1986 flocking simulation, where many simple agents following a few local rules behave like one flock. Boidscan nodes ("boids") are meant to work the same way: independent nodes, each following the same rules, that together cover more than any single one could. The current release is a single node. Federation between nodes is the next milestone.

## How a node works

1. [ZMap](https://github.com/zmap/zmap) finds open TCP ports.
2. [ZGrab2](https://github.com/zmap/zgrab2) records what each service announces during a normal handshake: banners, HTTP responses, TLS certificates, SSH and similar.
3. Results are stored in PostgreSQL and published through a public JSON API.

## Scanning in the open

Boidscan never tries credentials, never exploits vulnerabilities and never hides who is scanning. Every node enforces the same rules:

- **Identity.** A node refuses to scan without an abuse contact. The contact and project URL are sent in the User-Agent and shown on the node's public info page.
- **Rate ceiling.** 10,000 packets per second at most.
- **Exclusions.** IANA reserved ranges are always excluded.
- **Opt-out.** Anyone can opt out a range through the node's info page. The range is excluded from future scans and its stored results are deleted.

## Repositories

- [boidscan/boidscan](https://github.com/boidscan/boidscan): the node, search API and Go client

## License

[AGPL-3.0](https://github.com/boidscan/boidscan/blob/main/LICENSE).
