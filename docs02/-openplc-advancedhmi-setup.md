# OpenPLC + AdvancedHMI Setup

## Objective

The goal of this setup was to establish communication between OpenPLC Runtime and AdvancedHMI using Modbus TCP.

The final environment allowed:

* OpenPLC Runtime to host PLC variables
* AdvancedHMI to monitor and modify PLC states
* Communication over Modbus TCP on port 502

---

# Environment

## Linux VM

* Ubuntu Linux
* OpenPLC Runtime V3
* Python 3

## Windows VM

* AdvancedHMI
* Visual Studio

---

# OpenPLC Runtime Setup

OpenPLC Runtime V3 was installed and configured on the Linux VM.

The runtime was configured to:

* Compile Structured Text programs
* Host Modbus TCP services
* Listen on port 502

Several runtime dependencies and build issues required troubleshooting during setup.

---

# PLC Program

```pascal
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

# Modbus TCP Configuration

The OpenPLC runtime was configured to listen on:

```text
Port 502
```

The following command was used to allow the runtime to bind to the privileged Modbus port:

```bash
sudo setcap 'cap_net_bind_service=+ep' ~/OpenPLC_v3/webserver/core/openplc
```

---

# AdvancedHMI Configuration

## ModbusTCPCom

```text
IPAddress = <PLC_IP>
Port = 502
```

## Button Configuration

```text
PLCAddressClick = 00001
OutputType = Toggle
```

## Pilot Light Configuration

```text
PLCAddressValue = 00001
```

---

# Final Result

The final environment successfully demonstrated:

* OpenPLC Runtime communication
* Modbus TCP connectivity
* HMI button interaction
* Real-time pilot light state updates
* Successful PLC/HMI integration
