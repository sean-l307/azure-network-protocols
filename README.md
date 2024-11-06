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

![Capture10(filtureforICMP)](https://github.com/user-attachments/assets/ee367bae-add2-4a4a-9809-250356b0cc3b)
</p>
<p>
Launch the installer and proceed with the installation by clicking Next through each step, accepting the default settings. Once the installation is complete, open Wireshark. In Wireshark, set the filter to "icmp" to capture only ICMP packets. To begin monitoring traffic, click the blue shark fin icon at the top left of the window. This will start capturing network traffic through the VM.
</p>
<br />


![Capture8edited](https://github.com/user-attachments/assets/95c4801b-d87f-410a-8e27-ae33a1fc67d8)
</p>
<p>
Find your Linux VM's private IP and copy it, then connect using RDP.
</p>
<br />


![Capture11(pingprivatenetwork)](https://github.com/user-attachments/assets/132798c5-75c8-49c4-8b41-b9212c25c759)
</p>
<p>
Return to your VM and open Command Prompt or PowerShell by searching for it in the Windows search bar at the bottom left. Use the command ping -t [Linux VM's private IP address] to send continuous ICMP traffic, allowing you to observe this activity in Wireshark. You should see ICMP requests from the Linux VM's private IP and responses from the Windows VM's private IP.
</p>
<br />


![Capture12(on paper)](https://github.com/user-attachments/assets/0a6197fd-72e9-45b9-9b81-b7aee9f3e9b4)
</p>
<p>
To disable ICMP traffic from the Linux virtual machine's network security group (NSG) in the Azure portal, start by typing "NSG" in the search bar and selecting the Network security groups service. Locate the NSG associated with the Linux VM and open it. Once on the NSG page, go to Inbound security rules and add a new rule. Set ICMP as the protocol and choose Deny for the action. Adjust the priority to a number lower than the first rule in the list; a lower priority number will give this rule higher precedence. For example, setting the priority to 200 will make it take effect before a rule with a priority of 300.
</p>
<br />

![Capture13(new rule in effect)](https://github.com/user-attachments/assets/45373628-44cc-4e97-92ec-bcf08302831b)
</p>
<p>
After applying the rule, head back into the VM and observe how the ping to the private IP address will time out or fail.
</p>
<br />


![capture14 part 2(1of2)](https://github.com/user-attachments/assets/10dbaaa9-cb82-43cf-8e32-e24adfb5a55b)
![Capture14 part2(2of2)](https://github.com/user-attachments/assets/bc040de2-050b-4654-b1ac-f441d7b00d55)
</p>
<p>
We have now observed ICMP traffic between the two VMs through Remote Desktop Connection (RDC) and will proceed to connect to the Ubuntu VM via SSH (Secure Shell) using PowerShell. Begin by typing ssh <username>@<Ubuntu VM private IP address>. When prompted with the message:

"The authenticity of host '10.0.0.5 (10.0.0.5)' can't be established. ECDSA key fingerprint is SHA256
/JTv69D9C8feZvkyQAHgpvW5ZNdt2AvYfA. Are you sure you want to continue connecting (yes/no/[fingerprint])?"

Type yes to continue. After this, you will be asked for the password set when the VM was created. Note that the password will not appear as you type it, but it is still being entered even though it remains invisible on the screen.
</p>
<br />


![image](https://github.com/user-attachments/assets/90536140-d386-4e6c-8634-8582ae5189a8)
<p>
In wireshark, filter the traffic by "ssh" without saving. Within the SSH connection to the Ubuntu VM, enter any Linux shell commands (such as ls to list directory contents or uname -a to display system information) to generate SSH traffic. You should see the corresponding activity in your Wireshark capture. Once you're done, type exit in the command line to close the SSH connection.
</p>
<br />


---------
</p>
<p>
---------
</p>
<br />



