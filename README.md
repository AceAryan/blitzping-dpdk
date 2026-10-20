# Blitzping DPDK

A DPDK-based extension of [Blitzping](https://github.com/Thraetaona/Blitzping) for high-speed packet processing and TTL-based network tracing with live hop and RTT results.

> **Status:** Early development. Hardware support, features, and benchmark results are still being validated.

## Goals

- Port selected Blitzping packet-crafting functionality to DPDK.
- Trace IPv4 network paths using TTL-limited probes and ICMP replies.
- Report hop addresses, probe RTTs, timeouts, and packet statistics.
- Display trace results as they arrive in a simple GUI.
- Compare DPDK and conventional networking paths in a reproducible lab.

## How it works

The DPDK application uses an Ethernet PMD to send and receive packets through NIC queues. DPDK manages packet buffers and memory used by those queues; on supported hardware, the NIC transfers packet data to and from those buffers.

Traceroute sends probes with increasing TTL values. Routers that expire a probe may reply with ICMP Time Exceeded. The tool matches replies to probes and reports elapsed round-trip time. RTT is not a direct one-way link-delay measurement.

## Requirements

- Linux
- A DPDK version supported by this project
- A NIC and PMD supported by that DPDK version, or a supported virtual/PCAP-backed device for development
- Hugepage configuration appropriate for the selected DPDK setup
- GCC or Clang
- Optional: Mininet for repeatable network experiments

The exact DPDK version, NICs, and setup steps will be documented here as the project is validated.

## Build

Build instructions are not yet finalized. They will include the supported DPDK version, required development packages, and the project’s Makefile targets.

## Usage

Command-line options and GUI launch instructions will be added after the initial DPDK transmit and traceroute milestones are complete.

## Development plan

1. Separate packet creation and parsing from the original raw-socket transport.
2. Initialize DPDK, configure a port, and verify basic packet transmission and reception.
3. Port selected packet-crafting features to DPDK.
4. Implement TTL-based probes, reply matching, RTT measurements, and timeouts.
5. Add structured output and a real-time GUI.
6. Validate behavior and benchmark in a controlled Mininet lab.

## Benchmarks

Performance claims will be published only with reproducible details, including hardware, NIC and PMD, DPDK version, CPU configuration, topology, packet size, and command line. Throughput and traceroute latency will be reported separately.

## Safety

Use this tool only on systems and networks you own or are explicitly authorized to test. Development and performance experiments should run in an isolated lab topology.

## License and attribution

Blitzping is licensed under GPL-3.0-or-later. This project should preserve applicable license notices and document its relationship to the upstream project. See [the upstream repository](https://github.com/Thraetaona/Blitzping) for the original license and source.

## References

- [Blitzping](https://github.com/Thraetaona/Blitzping)
- [DPDK documentation](https://doc.dpdk.org/guides/)
- Project reference DOI: [10.1016/j.comcom.2020.07.040](https://doi.org/10.1016/j.comcom.2020.07.040) 
