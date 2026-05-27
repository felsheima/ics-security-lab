# ics-security-lab
Graduate ethical hacking project focused on offensive security analysis of simulated SCADA/ICS environments using Modbus, OpenPLC, and MITM attack techniques. 

# Overview 
This project demonstrates common security weaknesses in Industrial Control Systems (ICS) and SCADA environments through a controlled virtual lab setup. The lab simulates a Modbus-based industrial network using OpenPLC, a Human Machine Interface (HMI), and an attacker system running Kali Linux.

The purpose of this project is educational and research-oriented only. All testing is performed in an isolated lab environment.

# Objectives 
- Build a simulated SCADA/ICS environment
- Deploy and configure a Modbus PLC using OpenPLC
- Analyze Modbus TCP communications
- Demonstrate Man-in-the-Middle (MITM) attacks
- Simulate unauthorized PLC control and command injection
- Evaluate security weaknesses in industrial protocols
- Document offensive techniques and defensive recommendations

# Lab Architecture 
The environment consists of three virtual machines:

# VM & Purpose
Kali Linux	> Attacker system used for reconnaissance, packet capture, MITM attacks, and exploitation
OpenPLC	Simulated > PLC running Modbus TCP services
Modbus HMI	> Human Machine Interface used to monitor and control PLC operations

# Authors 
- Allison Felsheim
- Morgan Felsheim
