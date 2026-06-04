# Attack 3 – Modbus Traffic Interception (Man-in-the-Middle)

## Objective

The goal of this attack was to demonstrate how an attacker on the same network can observe Modbus TCP communications between an HMI and PLC. This attack highlights the lack of encryption and authentication within the Modbus protocol and shows how process data can be exposed when network traffic is intercepted.

## Attack Overview

In the previous attacks, direct communication with the PLC was demonstrated through Modbus register reads and writes. For this attack, the focus shifted to observing communications exchanged between the HMI and PLC.

The Kali Linux system was placed on the same network segment as the Windows HMI and Ubuntu PLC. Ettercap was used to discover hosts and establish a man-in-the-middle position between the communicating systems. Wireshark was then used to inspect the resulting Modbus traffic.

---

## Host Discovery

Ettercap was used to identify active hosts on the network. After starting network scanning, the host list displayed all detected systems on the subnet.

The network gateway was selected as Target 1 and the PLC device was selected as Target 2. This configuration allowed traffic between the systems to be routed through the attacker machine for observation.

### Figure 1 – Host Discovery and Target Selection

![Figure 1](screenshots/attack3-host-discovery.png)

*Ettercap identifying hosts and selecting targets for interception.*

---

## Traffic Interception

After configuring the interception environment, the Kali VM was positioned between the Windows HMI and Ubuntu PLC. Traffic flowing between the two systems could then be observed using Wireshark.

During testing, the operator modified the simulated water level from the HMI interface. The resulting Modbus communications were captured and analyzed.

### Figure 2 – Traffic Interception Setup

![Figure 2](screenshots/attack3-mitm-setup.png)

*Attacker system positioned between the HMI and PLC to observe network traffic.*

---

## Packet Analysis

Wireshark was configured to monitor Modbus TCP traffic on port 502. Inspection of the captured packets revealed Modbus function code activity associated with reading holding registers.

One captured packet showed Register 0 containing a value of 25, which corresponded directly to the water level displayed on the HMI. This demonstrated that process values were transmitted across the network in clear text and could be observed by an attacker with network access.

### Figure 3 – Captured Modbus Packet

![Figure 3](screenshots/attack3-modbus-packet.png)

*Wireshark displaying Modbus traffic containing process values from Register 0.*

---

## HMI Correlation

The value observed within the captured Modbus packet matched the value displayed on the HMI interface. Register 0 contained the value 25, and the HMI simultaneously displayed a water level of 25%.

This correlation confirmed that operational process data could be extracted directly from network traffic without requiring authentication or privileged access to the PLC.

### Figure 4 – HMI Display Showing Water Level

![Figure 4](screenshots/attack3-hmi-water-level.png)

*AdvancedHMI displaying a water level value that matches the intercepted Modbus traffic.*

---

## Security Impact

This attack demonstrates a significant weakness in Modbus TCP communications. Because Modbus does not provide encryption, authentication, or integrity protection, an attacker with network access can observe industrial process data in transit.

Potential impacts include:

- Monitoring operational process values
- Identifying PLC register mappings
- Gathering information for future attacks
- Manipulating process data if additional access is obtained
- Disrupting industrial operations through unauthorized control actions

---

## Conclusion

