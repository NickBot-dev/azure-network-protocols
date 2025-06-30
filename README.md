
<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Network Protocols Using Wireshark</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop Connection
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Observe ICMP Traffic (Internet Control Message Protocol)
- Configure a Firewall (Network Security Group)
- Observe SSH Traffic (Secure Shell)
- Observe DHCP Traffic (Dynamic Host Configuration Protocol)
- Observe DNS Traffic (Domain Name System)
- Observe RDP Traffic (Remote Desktop Protocol)

<h2>Actions and Observations</h2>

<p>

 ![Screenshot 2025-06-27 122056](https://github.com/user-attachments/assets/56c42ac0-9ee8-43c4-8c9e-7e1b0becaf8f) ![Screenshot 2025-06-27 122135](https://github.com/user-attachments/assets/b9549912-ceeb-422f-ad4d-6562dcab6179)

</p>
<p>
Make sure that both of the VMs are running. Start with logging into the Windows Virtual Machine (VM) using Remote Desktop Connection. Copy and paste the public IP address of the Windows VM, followed by supplying the credentials to successfully log in.   
</p>
<br />

<p>

 ![icmp blank](https://github.com/user-attachments/assets/ff33d217-d311-4fb1-a99c-8883e03ac2d1)

</p>
<p>
Observing ICMP Traffic. We start by typing icmp in the green search bar followed by clicking start capture, which is the green shark fin icon above. This tells Wireshark to filter out all inbound and outbound traffic except for ICMP Traffic.    
</p>
<br />

<p>

 ![scrnshot 4](https://github.com/user-attachments/assets/669542ad-ab27-4552-be8f-492a8d172798) ![scrnshot 2](https://github.com/user-attachments/assets/696e0039-4969-4f3c-a611-d29a7a222546)

</p>
<p>
After opening Powershell, we will run the Ping Command, followed by the Private IP Address of the Linux Virtual Machine (VM), ping 10.0.0.5... This will allow Wirshark to capture and display the ICMP traffic that we're looking for. 
</p>
<br />

<p>
 
![scrnshot 5](https://github.com/user-attachments/assets/60e648db-e41f-44b8-8b6c-330d41155ea1)

</p>
<p>
Back in Wireshark, we see the requests from the Linux VM, as well as the replies from the Windows VM. This shows that the Windows and Linux VMs both have a successful connection.   
</p>
<br />

<p>

![scrnshot nsg ping -t command](https://github.com/user-attachments/assets/89734012-8624-47d8-b752-387347858629) ![scrn shot ping -t](https://github.com/user-attachments/assets/9f21bc81-f5a9-4bd3-b2e8-242f5c0929e5)

</p>
<p>
Configure a Firewall (Network Security Group). To start, we initiate a perpetual/non-stop ping from the Windows 10 VM to the Linux VM by running the command... "ping 10.0.0.5 -t". We will notice that Wireshark starts to non-stop ping ICMP Traffic.  
</p>
<br />

<p>

 ![Screenshot 2025-06-27 123217](https://github.com/user-attachments/assets/3c2eb432-f097-491b-9251-0b5806fb68e4) ![Screenshot 2025-06-27 123335](https://github.com/user-attachments/assets/0954a7a5-88ec-43b1-ae39-eab6201d33c8) ![Screenshot 2025-06-27 123636](https://github.com/user-attachments/assets/6534b649-10cb-4e3d-8302-b193515ec215) ![image](https://github.com/user-attachments/assets/3eeeba3d-9429-4cf5-83df-698c97fe1b33)


</p>
<p>
Back in Microsoft Azure, open the Network Security Group for the Linux VM and disable incoming (inbound) ICMPv4 traffic, this is the traffic that the Ping command captures. Click on Network Settings, open the Network Security Group settings for the Linux VM, click inbound rules, and click add new inbound rule. Source/Destination Ports have the (*) symbol, which means any port, this is because ICMP Protocol does not use any specific ports. Finally we click add. We can see that our new inbound rule was successfully created.   
</p>
<br />

<p>

  ![ggugyu](https://github.com/user-attachments/assets/e7b2b22d-3cbb-4dd4-a94d-73b6bf8eb604) ![Untitled](https://github.com/user-attachments/assets/0833ad3a-25d8-4486-8ce8-f566a05c7527)

</p>
<p>
After enabling our new Inbound Security Rule, we now only see the requests from the Windows VM and "no response found" from the Linux VM. This shows that our new Inbound Security Rule working and we have successfully configured a Network Security Group (NSG).  
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
