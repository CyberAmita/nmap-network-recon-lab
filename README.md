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
