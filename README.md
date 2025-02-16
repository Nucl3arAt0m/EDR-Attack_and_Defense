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

## Screenshots & Logs

![Detection Alert]()  
(*Replace with actual screenshots/logs*)

---

> *"Detection is the first step. Response makes the difference."* 🔐
