# SECURITY ONION SOC LAB

A virtualized Security Operations Center lab built with Security Onion for practicing network security monitoring, alert triage, threat hunting, packet analysis, and incident investigation.

The project is designed as a reusable Blue Team environment for SOC Intern / SOC Analyst L1 practice and future security monitoring projects.

## Objectives

The main objectives of this project are to:

- Build an isolated and reusable SOC lab using VMware Workstation.
- Collect and analyze network security telemetry.
- Investigate alerts generated from controlled attack simulations.
- Practice threat hunting using network metadata and packet captures.
- Correlate events across multiple data sources.
- Reconstruct incident timelines.
- Map observed attacker behavior to MITRE ATT&CK.
- Document investigation findings using structured incident reports.

## Architecture

The lab runs entirely inside VMware Workstation.

```text
                         Windows Host
                              │
                       VMware Workstation
                              │
              ┌───────────────┴───────────────┐
              │                               │
        Management Network               SOC Network
              │                               │
       Security Onion                 ┌───────┼───────┐
       Management NIC                 │       │       │
                                      │       │       │
                                    Kali   Windows  Ubuntu
                                      │       │       │
                                      └───────┼───────┘
                                              │
                                      Security Onion
                                       Monitoring NIC
```

Traffic generated between lab systems is monitored by Security Onion through the dedicated monitoring interface.

## Lab Systems

| System | Role |
|---|---|
| Security Onion | SOC monitoring and investigation platform |
| Kali Linux | Controlled attack simulation and traffic generation |
| Ubuntu | Linux server and target system |
| Windows 10 | Windows endpoint and target system |
| Windows Host | VMware host and SOC console access |

## Technologies

### Security Monitoring

- Security Onion
- Suricata
- Zeek
- PCAP

### Analysis

- Security Onion Alerts
- Security Onion Hunt
- Security Onion Cases
- Wireshark
- MITRE ATT&CK

### Infrastructure

- VMware Workstation
- Kali Linux
- Ubuntu
- Windows 10

## SOC Workflow

The project follows a typical SOC investigation workflow:

```text
Traffic
   ↓
Telemetry
   ↓
Detection
   ↓
Alert
   ↓
Triage
   ↓
Pivot
   ↓
Threat Hunt
   ↓
PCAP Analysis
   ↓
Timeline Reconstruction
   ↓
MITRE ATT&CK Mapping
   ↓
Incident Case
```

## Detection and Investigation Scenarios

The lab is designed to support controlled scenarios such as:

- Network port scanning
- SSH brute-force activity
- Suspicious DNS activity
- Suspicious HTTP traffic
- Reverse-shell-like communication
- C2-like beaconing
- Web attack traffic
- Multi-stage incident reconstruction

Each scenario should include:

1. Scenario objective
2. Traffic source and target
3. Expected telemetry
4. Detection or alert
5. Investigation steps
6. Threat hunting queries
7. PCAP evidence when available
8. MITRE ATT&CK mapping
9. Analyst conclusion

## Repository Structure

```text
security-onion-soc-lab/
├── docs/
│   ├── architecture/
│   ├── installation/
│   └── methodology/
│
├── detections/
│
├── hunts/
│
├── incidents/
│
├── queries/
│
├── screenshots/
│
├── samples/
│
├── lab/
│   ├── ISO/
│   ├── VMware/
│   ├── PCAP/
│   └── Backups/
│
├── README.md
└── .gitignore
```

Local lab resources such as virtual machines, ISO images, backups, and large packet captures are excluded from Git history.

## Project Phases

The project is implemented incrementally.

### Phase 1 — Reusable VM Infrastructure

- Configure isolated VMware networking
- Create reusable base virtual machines
- Create project-specific clones
- Validate connectivity

### Phase 2 — Security Onion Deployment

- Create the Security Onion VM
- Configure management and monitoring interfaces
- Install and configure Security Onion
- Validate SOC console access

### Phase 3 — Network Visibility

- Generate normal lab traffic
- Verify Zeek telemetry
- Verify Suricata events
- Validate packet capture visibility

### Phase 4 — Baseline Traffic

Establish normal traffic patterns for:

- ICMP
- DNS
- HTTP
- SSH
- TCP connections

### Phase 5 — Detection Scenarios

Execute controlled attack simulations and analyze the resulting telemetry.

### Phase 6 — Threat Hunting

Develop reusable hunting procedures and investigation queries.

### Phase 7 — Incident Investigation

Create structured investigation reports and reconstruct attack timelines.

### Phase 8 — Portfolio Documentation

Prepare:

- Architecture documentation
- Investigation reports
- Screenshots
- Queries
- Detection notes
- Project findings

## Investigation Reports

Incident reports are stored under:

```text
incidents/
```

A report may include:

- Incident ID
- Alert information
- Affected asset
- Source and destination
- Relevant telemetry
- Timeline
- Indicators
- MITRE ATT&CK mapping
- Investigation findings
- Analyst conclusion

## Threat Hunting

Reusable hunting procedures and queries are maintained under:

```text
hunts/
queries/
```

Typical hunting dimensions include:

- Source IP
- Destination IP
- Ports
- DNS queries
- HTTP activity
- Connection frequency
- Time ranges
- Repeated or periodic network behavior

## Safety

All attack simulations are performed only inside the isolated virtual lab.

The project does not intentionally target:

- The physical host
- Home network devices
- Public Internet systems
- Third-party systems

Bridged networking is not used for attack simulation traffic.

## Current Status

The project is being implemented incrementally.

Current development focuses on building the reusable VMware lab infrastructure before deploying Security Onion and running detection scenarios.

## Future Work

Possible extensions include:

- Windows endpoint telemetry
- Sysmon integration
- Detection engineering
- Additional Suricata rules
- Active Directory monitoring
- Automated IOC enrichment
- Additional threat hunting scenarios
- Integration with future IDS/IPS labs

## Disclaimer

This project is intended for defensive security education and controlled laboratory use only.