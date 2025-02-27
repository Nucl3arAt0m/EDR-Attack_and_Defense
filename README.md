# EDR Attack & Defense

## Overview

This lab is dedicated to simulating a real cyber attack and endpoint detection and response. I will be using virtual machines to simulate the threat & victim machines. The attack machine will utilize 'Sliver' as a C2 framework to attack a Windows endpoint machine, which will be running 'LimaCharlie' as an EDR solution. The goal is to simulate real-world attack scenarios, observe detection capabilities, and enhance defenses using **LimaCharlie D&R rules**.

## Environment Setup

- **EDR Solution:** LimaCharlie
- **Operating System:** Windows 11 VM, Ubuntu-server VM
- **Attack Tools Used:** Sliver
- **Defense Mechanism:** LimaCharlie D&R rules

## Attack Simulation

### ✅ Credential Access Techniques Tested
- Dumping credentials using Sliver
- LSASS memory dump analysis
- Extracting NTLM hashes

## Defense Implementation

### ✅ Detection & Response (D&R) Rules
- **Process monitoring:** Detect suspicious vssadmin.exe
- **Memory analysis:** Identify unauthorized memory dumps
- **Behavior-based detection:** Flag known credential dumping patterns

## Results

- **Successful detection of credential dumping attempts** 🔍
- **D&R rules triggered alerts and mitigated threats** ✅
- **SIEM logs captured attack activity** 📊

## Setup

#### The first step to the lab is setting up both machines. The attack machine will run on Ubuntu Server, and the endpoint will be running Windows 11. In order for this lab to work smoothly Microsoft Defender should be turned off (along with other settings). I am also going to be installing Sliver on the Ubuntu machine as my primary attack tool, and setting up LimaCharlie on the Windows machine as an EDR solution. LimaCharlie will have a sensor linked to the windows machine, and will be importing sysmon logs.

#### Windows 11 machine :
![Detection Alert](screenshots/win_initial.png)  
![Detection Alert](screenshots/LC_Sensor.png)
![Detection Alert](screenshots/LC_Sensor_artifact_collection_rule.png)

#### Ubuntu machine :
![Detection Alert](screenshots/ubuntu__machine.png)
![Detection Alert](screenshots/ubuntu_terminal.png)

## Attack and the Defense

#### The first step is to generate our payload on Sliver, and implant the malware into the Windows host machine. Then we can create a command and control session after the malware is executed on the endpoint.

![Sliver](screenshots/sliver.png)
![C2](screenshots/CmdandCont2.png)

#### Now that we have a live session between the two machines, the attack machine can begin peeking around, checking priveleges, getting host information, and checking what type of security the host has.

![sliver_cmds](screenshots/sliver_commands.png)
![sliver_cmds](screenshots/C2_cmd3.png)

#### On the host machine we can look inside our LimaCharlie SIEM and see telemetry from the attacker. We can identify the payload thats running and see the IP its connected to.

![LC_timeline](screenshots/LC_Sensor_timeline.png)
![LC_detection](screenshots/detection_proc.png)

#### We can also use LimaCharlie to scan the hash of the payload through VirusTotal; however, it will be clean since we just created the payload ourselves.

![VT_scan](screenshots/VirusTotal_scan.png)


#### I wrote a custom rule under D&R rules, that will detect and block the attacks coming from the Sliver server. On the Ubuntu machine we can simulate parts of a ransomware attack, by attempting to delete the volume shadow copies. In LimaCharlie we can view the telemetry and then write a rule that will block the attack entirely. After we create the rule in our SIEM, the Ubuntu machine will have no luck trying the same attack again.

![shell_cmd](screenshots/sliver_shell.png)

#### In the detections tab, the "Whoami utility Execution" is detected.
![shell_cmd](screenshots/Shell_detection.png)
![shell_cmd](screenshots/shell_vssadmin.png)

#### "vssadmin delete shadows" command is detected
![shell_cmd](screenshots/C2_detection.png)
![shell_cmd](screenshots/vssAdmin_rule.png)
![shell_cmd](screenshots/D&R_rule_trigger.png)

---

> *"Detection is the first step. Response makes the difference."* 🔐
