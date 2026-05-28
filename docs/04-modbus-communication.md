# Modbus TCP Communication

## Overview

This lab used Modbus TCP as the communication protocol between OpenPLC Runtime and AdvancedHMI.

Modbus TCP is commonly used in industrial environments for communication between:

* PLCs
* HMIs
* SCADA systems
* Industrial controllers

---

# Port Usage

The OpenPLC runtime listened on:

```text
Port 502
```

Port 502 is the default Modbus TCP port.

---

# PLC Variable Mapping

The PLC BOOL variable:

```text
%QX0.0
```

mapped to:

```text
Coil 00001
```

within Modbus TCP.

---

# HMI Interaction

AdvancedHMI communicated with the PLC by:

* Writing to Modbus coils
* Reading Modbus coil states
* Reflecting state changes through HMI indicators

---

# Security Observations

During testing, it became clear that:

* Modbus TCP does not provide authentication
* Modbus traffic is unencrypted
* PLCs may trust any reachable host
* HMI systems rely heavily on trusted network communication

These weaknesses make Modbus environments vulnerable to:

* Unauthorized writes
* Traffic interception
* MITM attacks
* False operator visibility
