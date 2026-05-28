# ICS Security Lab

## Overview

This project demonstrates offensive security analysis against a simulated SCADA/ICS environment using **OpenPLC**, **AdvancedHMI**, **Modbus TCP**, and Kali Linux tooling.

The lab demonstrates three attack phases:

* **Attack 1:** PLC discovery and Modbus enumeration
* **Attack 2:** Unauthorized Modbus register manipulation
* **Attack 3:** Man-in-the-Middle interception and traffic manipulation

---

# Repository Layout

```text
ics-security-lab/
│
├── README.md
│
├── docs/
│   ├── 00-lab-overview.md
│   ├── 01-network-topology.md
│   ├── 02-openplc-advancedhmi-setup.md
│   ├── 03-troubleshooting-notes.md
│   └── 04-lessons-learned.md
│
├── attacks/
│   ├── attack-1-discovery-enumeration.md
│   ├── attack-2-register-manipulation.md
│   └── attack-3-mitm-modbus-interception.md
│
├── screenshots/
│   ├── setup/
│   ├── attack-1-discovery/
│   ├── attack-2-register-change/
│   └── attack-3-mitm/
│
├── pcaps/
│   ├── baseline-traffic/
│   ├── attack-2-register-write/
│   └── attack-3-mitm/
│
├── scripts/
│   ├── modbus-read/
│   ├── modbus-write/
│   └── mitm/
│
└── configs/
    ├── openplc/
    └── advancedhmi/
```

---

# README.md Outline

## Project Summary

This lab simulates a small industrial control system using OpenPLC as the PLC runtime and AdvancedHMI as the operator interface. Kali Linux is used as the attacker machine to perform discovery, enumeration, unauthorized Modbus interaction, and MITM traffic manipulation.

## Lab Components

| Component       | Purpose                           |
| --------------- | --------------------------------- |
| OpenPLC Runtime | Simulated PLC                     |
| AdvancedHMI     | Operator HMI                      |
| Kali Linux      | Attacker system                   |
| Modbus TCP      | Industrial communication protocol |

## Attack Demonstrations

### Attack 1: PLC Discovery and Enumeration

Goal:

* Discover the PLC
* Identify open ICS ports
* Enumerate Modbus registers/coils

Evidence to include:

* Nmap scan output
* Modbus scanner results
* Screenshots of open port 502
* Register/coil enumeration results

---

### Attack 2: Unauthorized Register Manipulation

Goal:

* Simulate an attacker changing a PLC value
* Demonstrate how unauthorized writes can affect HMI readings

Example scenario:

* PLC represents a water level system
* HMI displays normal/high/low level
* Attacker changes Modbus coil/register values
* HMI reflects manipulated state

Evidence to include:

* Before/after HMI screenshots
* Register write command output
* Wireshark capture of Modbus write traffic

---

### Attack 3: MITM Modbus Traffic Manipulation

Goal:

* Intercept Modbus traffic between HMI and PLC
* Demonstrate how traffic can be observed or altered in transit

Example scenario:

* Operator sees normal process values
* PLC receives altered values
* Attacker manipulates Modbus traffic using MITM tooling

Evidence to include:

* ARP spoofing/MITM setup screenshot
* Wireshark capture of intercepted Modbus traffic
* Before/after PLC/HMI behavior
* Notes explaining impact

---

# Documentation Files

## docs/00-lab-overview.md

Include:

* Project purpose
* What ICS/SCADA means
* Why Modbus is insecure by default
* Lab safety/authorization note

## docs/01-network-topology.md

Include:

```text
Kali Attacker VM
        |
        | same virtual network
        |
OpenPLC VM  <---- Modbus TCP ---->  Windows AdvancedHMI VM
```

Include IP table:

| System     | Role     |
| ---------- | -------- |
| Kali       | Attacker |
| OpenPLC    | PLC      |
| Windows VM | HMI      |

## docs/02-openplc-advancedhmi-setup.md

Include:

* OpenPLC installation notes
* AdvancedHMI configuration
* ModbusTCPCom settings
* Button and pilot light settings

## docs/03-troubleshooting-notes.md

Include:

* OpenPLC v4 issues
* Why v3 was selected
* Python dependency fixes
* Port 502 permission issue
* Final successful configuration

## docs/04-lessons-learned.md

Include:

* Modbus has no built-in authentication
* PLCs can trust unauthorized writes
* HMI values can be manipulated
* Network segmentation and monitoring are important

---

# Attack Note Template

Use this format for each attack file:

```markdown
# Attack X: Title

## Objective
What this attack demonstrates.

## Tools Used
- Tool 1
- Tool 2
- Tool 3

## Lab Setup
- PLC IP:
- HMI IP:
- Attacker IP:

## Steps Performed
1. Step one
2. Step two
3. Step three

## Results
Explain what happened.

## Evidence
- Screenshot filename
- PCAP filename
- Command output

## Security Impact
Explain why this matters in ICS environments.

## Defensive Recommendations
- Network segmentation
- Disable unnecessary services
- Monitor Modbus traffic
- Restrict access to PLC ports
```

---

# Final Result

By the end of the lab, the environment demonstrates:

* A working OpenPLC and AdvancedHMI setup
* Modbus TCP communication on port 502
* PLC discovery using network scanning
* Register/coil enumeration
* Unauthorized Modbus manipulation
* MITM-based traffic interception
* Practical ICS security risks and mitigations

---

# Key Takeaways

* Modbus TCP is easy to inspect because it is unencrypted.
* PLCs may accept commands from unauthorized systems if network access is not restricted.
* HMI displays can be influenced by manipulated process values.
* ICS environments require strong segmentation, monitoring, and access control.
* Offensive testing in a lab helps demonstrate why industrial protocols need layered defenses.
