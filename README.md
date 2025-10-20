# nmap-task1
A learning project containing the results and sanitized summaries of my first authorized Nmap scan. Includes anonymized host and port data,  and Markdown summaries, and scripts to process and sanitize scan outputs. Designed for educational purposes and safe sharing.
Here, what i learned, the open ports are 135, 139, and 445.
What the ports are used for
Port 135 (RPC): Used by the Microsoft Remote Procedure Call (RPC) service to manage communication between different processes on a network. If exploited, this can allow an attacker to execute arbitrary code or gain unauthorized access.
Port 139 (NetBIOS): Used by older Windows versions for file and printer sharing over the NetBIOS protocol. The modern alternative, Server Message Block (SMB), uses port 445.
Port 445 (SMB): Used by modern versions of Windows for Server Message Block (SMB) file and printer sharing. This port was famously exploited during the WannaCry ransomware attacks.
Risks of keeping these ports open
WannaCry vulnerability: Outdated versions of the SMB protocol (SMBv1) that operate on these ports were exploited by ransomware like WannaCry to spread rapidly across networks. While Microsoft has patched these vulnerabilities, the risk remains if you have an unpatched system or a service still using SMBv1.
Network reconnaissance: Attackers can use these ports to perform network enumeration to gather information about your device, which they can then use to plan an attack.
Lateral movement: Malicious software that gains a foothold on one machine can use these open SMB ports to move laterally and infect other devices on the same network.
Exposure to the internet: While they might be open on your local network for file sharing, they should never be exposed to the public internet.
Measures to secure your device
Block the ports with Windows Firewall. The most important step is to create an inbound rule in Windows Defender Firewall to explicitly block connections on ports 135, 139, and 445. You can do this by following these steps:
Open Control Panel and go to Windows Defender Firewall.
Click on Advanced Settings.
Click Inbound Rules and then New Rule.
Choose Port and enter the specific ports: 135, 139, 445.
Select Block the connection as the action and apply the rule to all network profiles (Domain, Private, and Public).
Disable NetBIOS over TCP/IP. This is recommended for modern home networks that do not rely on older file-sharing methods.
Go to Control Panel > Network and Sharing Center.
Click on your connection (e.g., "Ethernet" or "Wi-Fi"), then Properties.
Select Internet Protocol Version 4 (TCP/IPv4) and click Properties.
Click the Advanced button and navigate to the WINS tab.
Select Disable NetBIOS over TCP/IP and click OK.
Disable SMBv1. For maximum security, you can turn off the outdated SMBv1 feature in Windows, as modern file-sharing uses SMBv3.
Press the Windows Key + R to open the Run dialog.
Type optionalfeatures.exe and press Enter.
In the list, find and uncheck the box for "SMB 1.0/CIFS File Sharing Support
Use a firewall on your router. For an extra layer of protection, ensure that your router's firewall is blocking these ports from the public internet. The scan from your VirtualBox can reach your host device because they are on the same local network, but it is critical that outside attackers cannot.

