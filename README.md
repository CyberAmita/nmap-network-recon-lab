# nmap-network-recon-lab
Hands-on Nmap lab demonstrating network discovery, port scanning, service enumeration, and security analysis in an authorized lab environment.
# Nmap Network Reconnaissance Lab

## Overview

This project documents my hands-on practice with Nmap in a Kali Linux lab environment. The goal is to practice network reconnaissance, identify active hosts, discover open ports, enumerate running services, and analyze scan results.

All scanning in this project is performed only in an authorized lab environment.

## Lab Environment

- Operating System: Kali Linux
- Nmap Version: 7.95
- Environment: Local lab
- Tool: Nmap

## Objectives

- Perform host discovery
- Identify open ports
- Enumerate running services and versions
- Analyze Nmap scan results
- Understand how network reconnaissance supports vulnerability assessment

## Nmap Version Verification
Before beginning reconnaissance, I verified that Nmap was installed and available in my Kali Linux environment.

Command:
```bash
nmap --version
```
Result:
```text
Nmap version 7.95
Platform: x86_64-pc-linux-gnu
```
## Network Identification
Before starting the scan, I identified the active network interface and local network configuration using:

Command:
```bash
ip addr
```
The active interface was `eth0` with the following IPv4 configuration:

Result:
```text
IPv4 Address: 10.0.2.15/24
Network: 10.0.2.0/24
```
The `/24` prefix indicates a subnet mask of `255.255.255.0`. This helped identify the local network range to use for host discovery.

## Host Discovery
The first reconnaissance step was to identify active hosts on the local network before performing any port scanning.

### Host Discovery with `-sn`

Command:
```bash
nmap -sn 10.0.2.0/24
```

Result:
```text
Nmap scan report for 10.0.2.2
Host is up.
Nmap scan report for 10.0.2.3
Host is up.
Nmap scan report for 10.0.2.15
Host is up.

Nmap done: 256 IP addresses (3 hosts up)
```
-sn performs host discovery without scanning ports. Without -sn, a standard Nmap scan typically scans the 1,000 most common TCP ports on active hosts.

### Understanding Why a Host Was Detected
I repeated the discovery scan with the `--reason` option:

Command:
```bash
nmap -sn 10.0.2.0/24 --reason
```
--reason shows why Nmap considers a host up. In this scan, hosts were detected through ARP responses, while the Kali host was detected through a localhost response.

### Privileged vs. Unprivileged Scanning
I also compared host discovery with and without `sudo`:

Command:
```bash
nmap -sn 10.0.2.0/24
```
Command:
```bash
sudo nmap -sn 10.0.2.0/24
```
Both commands identified the same three active hosts in this local lab environment.

`sudo` runs Nmap with elevated privileges. Some Nmap techniques require raw-packet access, which may require root privileges on Linux. However, elevated privileges are not required for every Nmap operation.

In this host-discovery test, using `sudo` did not change the discovered hosts. The importance of privileges becomes more apparent with scan types such as SYN scanning (`-sS`), which I explore later in this lab.

### Key Observation
Host discovery provides a useful first step in reconnaissance because it identifies active systems before more detailed port and service enumeration.
