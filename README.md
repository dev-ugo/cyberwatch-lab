# CyberWatch Lab

A personal network security lab built with Docker Compose,
tcpdump and Suricata.

## Objectives

- Understand HTTP communication over TCP.
- Capture network traffic in PCAP format.
- Analyze captures with Suricata.
- Write and validate detection rules.

## Environment

- Windows with Ubuntu on WSL.
- Nginx: HTTP server.
- curl: HTTP client.
- netshoot / tcpdump: server traffic capture.
- Suricata: offline PCAP analysis.

The client and server communicate over an internal Docker network.
The observer shares the server's network namespace.
Suricata analyzes recorded captures with networking disabled.

## First exercise: distinguish GET from HEAD

Local rule 1000001 matches requests whose HTTP method is
exactly GET.

| Capture | Traffic | Observed result |
|---|---|---|
| http-baseline.pcap | GET / — HTTP 200 | Alert 1000001 triggered |
| http-head.pcap | HEAD / — HTTP 200 | No alert |

In both cases, an HTTP event confirms that Suricata
successfully parsed the request.

## Limitations

This educational rule matches a normal HTTP method.
An alert therefore does not imply malicious activity.

Analysis runs against recorded captures.
No live traffic is blocked.

Checksum verification is disabled with -k none for these
exercises in a virtualized environment.