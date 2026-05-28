# ICS Security Lab – OpenPLC + AdvancedHMI + Modbus TCP

## Overview

This project demonstrates offensive security analysis against a simulated Industrial Control System (ICS) / SCADA environment using:

* OpenPLC Runtime V3
* AdvancedHMI
* Modbus TCP
* Kali Linux offensive tooling

The lab focuses on identifying and exploiting weaknesses commonly found in industrial environments, specifically around unauthenticated Modbus communication and insecure network trust relationships.

---

# Lab Objectives

This project demonstrates three primary attack scenarios:

## Attack 1 – PLC Discovery & Modbus Enumeration

* Discover ICS devices on the network
* Identify open industrial ports
* Enumerate Modbus coils/registers

## Attack 2 – Unauthorized Register Manipulation

* Modify PLC register/coil values
* Demonstrate unauthorized process manipulation
* Show HMI state changes caused by attacker interaction

## Attack 3 – Modbus Traffic Interception (MITM)

* Intercept Modbus TCP traffic
* Manipulate traffic in transit
* Demonstrate how operators can receive misleading process data

---

# Technologies Used

* OpenPLC Runtime V3
* AdvancedHMI
* Modbus TCP
* Nmap
* Wireshark
* Ettercap / Bettercap / Scapy
* Kali Linux
* Ubuntu Linux

---

# Repository Structure

```text
ics-security-lab/
│
├── README.md
├── docs/
├── attacks/
├── screenshots/
├── pcaps/
├── scripts/
└── configs/
```

---

# Final Result

The completed environment successfully demonstrated:

* PLC discovery and enumeration
* Modbus TCP communication analysis
* Unauthorized PLC manipulation
* HMI interaction with OpenPLC
* MITM interception of industrial traffic
* Real-world weaknesses in ICS environments
