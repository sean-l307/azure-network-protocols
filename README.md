<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Step 1: Use Remote Desktop to connect to your Windows 10 Virtual Machine
- Step 2: Within your Windows 10 Virtual Machine, Install the WireShak application
- Step 3: Ping the Ubuntu Virtual Machine to observe ICMP traffic, disable and re-enable ICMP traffic through the Network Security Group
- Step 4: Observe SSH traffic on the Windows Virtual Machine
- Step 5: Observe DNS traffic on the Windows Virtual Machine
- Step 6: Observe RDP traffic on the Windows Virtual Machine
- Step 7: Clean up by deleting the resource groups to ensure we don't incur any charges

<h2>Actions and Observations</h2>

![Capture9(enterIP and usernameRDP)](https://github.com/user-attachments/assets/a4ecc67f-8177-4bdd-a793-440324ceb5cf)
</p>
<p>
First, access the Azure portal by navigating to https://portal.azure.com/. Once inside the portal, locate your Windows virtual machine (VM) and copy its public IP address. To connect to this VM, open Remote Desktop Connection (RDC) by typing "RDC" into the Windows search bar and selecting the first result. A dialog box will appear where you should enter the public IP address of the VM. After clicking Connect, you will be prompted to enter the username and password that were created earlier. Enter these credentials and click OK to log in.

</p>
<br />

![wire sc](https://github.com/user-attachments/assets/4de09c38-73d1-4c86-bf95-a3c902a5fb2f)
<p>
In the VM, open the Microsoft Edge browser and navigate to the Wireshark download page by copying and pasting this link: https://www.wireshark.org/download.html. Once on the page, download the Windows Installer (64-bit) version to proceed with the installation.
</p>
<br />

![Capture11(pingprivatenetwork)](https://github.com/user-attachments/assets/329409f5-0349-4897-a595-21615c3e9b23)
</p>
<p>
Launch the installer and proceed with the installation by clicking Next through each step, accepting the default settings. Once the installation is complete, open Wireshark. In Wireshark, set the filter to "icmp" to capture only ICMP packets. To begin monitoring traffic, click the blue shark fin icon at the top left of the window. This will start capturing network traffic through the VM.
</p>
<br />
