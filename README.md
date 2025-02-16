# EDR Attack & Defense

## Overview

This lab is dedicated to simulating a real cyber attack and endpoint detection and response. I will be using virtual machines to simulate the threat & victim machines. The attack machine will utilize 'Sliver' as a C2 framework to attack a Windows endpoint machine, which will be running 'LimaCharlie' as an EDR solution. The goal is to simulate real-world attack scenarios, observe detection capabilities, and enhance defenses using **LimaCharlie D&R rules**.

## Environment Setup

- **EDR Solution:** LimaCharlie
- **Operating System:** [Specify OS, e.g., Windows 10, Ubuntu]
- **Attack Tools Used:** [Mention tools, e.g., Mimikatz, Rubeus, etc.]
- **Defense Mechanism:** LimaCharlie D&R rules

## Attack Simulation

### ✅ Credential Access Techniques Tested
- Dumping credentials using Mimikatz
- LSASS memory dump analysis
- Extracting NTLM hashes

## Defense Implementation

### ✅ Detection & Response (D&R) Rules
- **Process monitoring:** Detect suspicious LSASS access
- **Memory analysis:** Identify unauthorized memory dumps
- **Behavior-based detection:** Flag known credential dumping patterns

## Results

- **Successful detection of credential dumping attempts** 🔍
- **D&R rules triggered alerts and mitigated threats** ✅
- **SIEM logs captured attack activity** 📊

## Setup

The first step to the lab is setting up both machines. The attack machine will run on Ubuntu Server, and the endpoint will be running Windows 11. In order for this lab to work smoothly Microsoft Defender should be turned off (along with other settings). I am also going to be installing Sliver on the Ubuntu machine as my primary attack tool, and setting up LimaCharlie on the Windows machine as an EDR solution. LimaCharlie will have a sensor linked to the windows machine, and will be importing sysmon logs.

#### Windows 11 machine :
![Detection Alert](win_initial.png)  
![Detection Alert](LC_Sensor.png)
![Detection Alert](LC_Sensor_artifact_collection_rule.png)

#### Ubuntu machine :
![Detection Alert](ubuntu__machine.png)
![Detection Alert](ubuntu_terminal.png)

## Attack and the Defense

The first step is to generate our payload on Sliver, and implant the malware into the Windows host machine. Then we can create a command and control session after the malware is executed on the endpoint.

![Sliver](sliver.png)
![C2](C2.png)

Now that we have a live session between the two machines, the attack machine can begin peeking around, checking priveleges, getting host information, and checking what type of security the host has.



---

> *"Detection is the first step. Response makes the difference."* 🔐
