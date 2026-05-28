# Troubleshooting Notes

## Overview

A significant portion of this lab involved troubleshooting OpenPLC Runtime dependencies, runtime configuration, Linux permissions, and Modbus communication.

The troubleshooting process provided hands-on experience working through real-world ICS deployment issues.

---

# Major Issues Encountered

## OpenPLC Runtime Dependencies

Several Python and runtime dependencies were missing or incompatible with the environment.

Additional configuration was required to:

* Install older package versions
* Configure runtime dependencies
* Restore OpenPLC compatibility

---

## Runtime Compilation Issues

OpenPLC attempted to compile optional industrial protocol modules that were not required for this lab.

Several build script modifications were performed to:

* Disable unnecessary industrial protocol support
* Simplify runtime compilation
* Restore successful runtime builds

---

## Linux Port Permissions

The Modbus service initially failed to bind to port 502 because Linux restricts privileged ports.

This was resolved using:

```bash
sudo setcap 'cap_net_bind_service=+ep' ~/OpenPLC_v3/webserver/core/openplc
```

This allowed OpenPLC Runtime to successfully listen on port 502.

---

## AdvancedHMI Communication

The HMI initially behaved as a momentary button instead of maintaining PLC state.

This was corrected by modifying the HMI button behavior to:

```text
OutputType = Toggle
```

---

# Key Lessons Learned

This troubleshooting process reinforced:

* Linux service management
* Runtime debugging
* Dependency troubleshooting
* Industrial protocol configuration
* Modbus TCP communication concepts
* PLC/HMI integration workflows
