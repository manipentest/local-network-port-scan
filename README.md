
# Local Network Port Scan using Zenmap

## Objective

This project involves scanning the local network `192.168.1.0/24` using Zenmap, the graphical interface for Nmap. The goal is to identify active hosts and open ports, and assess the potential security risks associated with exposed services. The task helps build a foundational understanding of internal network reconnaissance and service enumeration.

## Tools Used

- Zenmap (Nmap GUI)
- Windows 10 Operating System

## Scan Configuration

- **Scan Profile**: Intense Scan
- **Command Used**: `nmap -T4 -A -v 192.168.1.0/24`
- **Scan Options**:
  - OS Detection
  - Service Version Detection
  - Script Scanning
  - Traceroute

## Summary of Results

### Device 1 – 192.168.1.1 (TP-Link Router)

- **Open Ports**:
  - Port 80: HTTP (router web admin page)
  - Port 1900: UPnP (Universal Plug and Play)

- **Observations**:
  - The HTTP service likely hosts the TP-Link router’s configuration interface.
  - UPnP is enabled, which may expose internal services unnecessarily.

- **Risk**:
  - If the router's web interface uses default or weak credentials, it may be susceptible to unauthorized access.
  - UPnP should be reviewed and disabled if not required.

---

### Device 2 – 192.168.1.103 (Windows Host)

- **Open Ports**:
  - 135: Microsoft RPC
  - 139, 445: SMB (file sharing)
  - 3306: MySQL (unauthenticated access)
  - 902, 912: VMware-related services

- **Observations**:
  - MySQL is accessible over the network without authentication, which poses a clear security concern.
  - SMB ports are open, which could expose the host to vulnerabilities related to Windows file sharing and remote code execution if not properly secured.

- **Risk**:
  - Unauthorized access to MySQL could result in data leaks or remote attacks.
  - SMB-related ports are commonly targeted in lateral movement within networks.

## Recommendations

- Disable unnecessary services, especially MySQL and UPnP if not in use.
- Restrict access to the router interface from only trusted IPs.
- Apply firewall rules to limit access to services like SMB and MySQL to trusted devices only.
- Ensure all network devices use strong, unique administrative credentials.
- Keep software and firmware updated to minimize known vulnerabilities.

## Included File

- `regularscan1.xml`: Zenmap XML output containing detailed scan results, including hosts, services, ports, and potential vulnerabilities.

