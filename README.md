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
* Identify PLC communication services

## Attack 2 – Unauthorized Register Manipulation

* Modify PLC register/coil values
* Demonstrate unauthorized process manipulation
* Show HMI state changes caused by attacker interaction

## Attack 3 – Modbus Traffic Interception (MITM)

* Intercept Modbus TCP traffic
* Manipulate traffic in transit
* Demonstrate how operators can receive misleading process data

---

# Lab Environment

| System          | Purpose                    |
| --------------- | -------------------------- |
| OpenPLC Runtime | Simulated PLC              |
| AdvancedHMI     | Operator HMI               |
| Kali Linux      | Attacker Machine           |
| Modbus TCP      | ICS Communication Protocol |

---

# Network Topology

```text id="b36i3y"
+-------------------+
|   Kali Linux VM   |
|    (Attacker)     |
+-------------------+
          |
          | Modbus TCP / MITM
          |
+-------------------+        +-------------------+
|   OpenPLC Runtime | <----> |   AdvancedHMI     |
|    Linux VM       |        |    Windows VM     |
+-------------------+        +-------------------+
```

---

# Technologies Used

## ICS / SCADA

* OpenPLC Runtime V3
* AdvancedHMI
* Modbus TCP

## Offensive Security Tools

* Nmap
* Modbus scanners
* Ettercap
* Bettercap
* Scapy
* Wireshark

## Operating Systems

* Ubuntu Linux
* Windows
* Kali Linux

---

# OpenPLC + HMI Configuration

## Modbus TCP

The OpenPLC runtime was configured to listen on:

```text id="42pkmf"
Port 502
```

AdvancedHMI connected using:

```text id="6t2k0h"
IPAddress = <PLC_IP>
Port = 502
```

---

# PLC Program

```pascal id="b3e4om"
PROGRAM PLC_PRG
VAR
    HMI_Button AT %QX0.0 : BOOL;
END_VAR

HMI_Button := HMI_Button;

END_PROGRAM

CONFIGURATION Config0
    RESOURCE Res0 ON PLC
        TASK Main(INTERVAL := T#100ms, PRIORITY := 0);
        PROGRAM Inst0 WITH Main : PLC_PRG;
    END_RESOURCE
END_CONFIGURATION
```

---

# Attack Demonstrations

# Attack 1 – PLC Discovery & Enumeration

## Goal

Identify the PLC on the network and enumerate Modbus information.

## Demonstrated Concepts

* ICS asset discovery
* Open Modbus TCP services
* Register/coils enumeration
* Industrial reconnaissance

## Tools Used

* Nmap
* Modbus scanners
* Wireshark

## Evidence

* Open port 502 discovery
* Modbus enumeration screenshots
* Register mapping results

---

# Attack 2 – Unauthorized Register Manipulation

## Goal

Demonstrate how attackers can modify PLC process values through Modbus writes.

## Scenario

A simulated water level process was represented through PLC variables and HMI indicators.

The attacker:

* Connected directly to the PLC
* Modified Modbus register/coil values
* Caused the HMI to display altered process conditions

## Demonstrated Concepts

* Lack of Modbus authentication
* Unauthorized PLC control
* HMI trust in PLC data

## Evidence

* Register write commands
* HMI state changes
* Packet captures of Modbus writes

---

# Attack 3 – Modbus MITM Traffic Manipulation

## Goal

Intercept and manipulate Modbus TCP traffic between the HMI and PLC.

## Scenario

Traffic between AdvancedHMI and OpenPLC was intercepted using MITM tooling.

The attacker:

* Positioned between the PLC and HMI
* Observed Modbus traffic
* Manipulated values in transit

## Demonstrated Concepts

* Unencrypted ICS traffic
* ARP spoofing/MITM attacks
* Traffic manipulation risks
* False operator visibility

## Tools Used

* Ettercap
* Bettercap
* Scapy
* Wireshark

## Evidence

* MITM packet captures
* Modified Modbus traffic
* PLC/HMI behavior differences

---

# Key Lessons Learned

## Industrial Protocol Security

* Modbus TCP does not provide encryption or authentication by default.
* PLCs may trust any host capable of reaching port 502.
* HMI systems can display manipulated values if network traffic is altered.

---

## Network Security

* Flat industrial networks increase attack surface.
* ICS protocols should be segmented and monitored.
* Unauthorized hosts should not have direct PLC access.

---

## Defensive Considerations

Potential mitigations include:

* Network segmentation
* Firewall restrictions
* Industrial IDS/IPS monitoring
* Protocol-aware monitoring
* VLAN separation
* Secure remote access controls

---

# Useful Commands

## Check Listening Ports

```bash id="9km6rm"
ss -tulpn | grep 502
```

## Start OpenPLC Runtime

```bash id="k3v8sh"
./openplc
```

## Kill Existing Runtime

```bash id="z9n3oq"
sudo pkill -f openplc
```

## Start OpenPLC Webserver

```bash id="e0nn9w"
python3 webserver.py
```

---

# Repository Structure

```text id="k4cmxw"
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

# Conclusion

This lab successfully demonstrated:

* PLC discovery and enumeration
* Modbus TCP communication analysis
* Unauthorized PLC manipulation
* MITM interception of industrial traffic
* Real-world weaknesses in ICS environments

The project provided hands-on experience with industrial protocols, HMI integration, offensive security tooling, and defensive considerations relevant to modern ICS/SCADA systems.
