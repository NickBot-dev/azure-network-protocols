
<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Network Protocols Using Wireshark</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- Network Security Groups and Inspecting Network Protocols with Wireshark https://www.youtube.com/watch?v=w8H5fWBHddA&t=24s

<h2>Environments and Technologies Used</h2>

- Microsoft Azure Windows and Linux Virtual Machines
- Remote Desktop Connection
- Powershell and Various Command-Line Tools
- Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (packet analyzer or network sniffer)

<h2>Operating Systems Used </h2>

- Windows 10 Pro
- Linux Ubuntu

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
Make sure that both of the Virtual machines are running. Start with logging into the Windows Virtual Machine using Remote Desktop Connection. Copy and paste the public IP address of the Windows Virtual Machine and supply the credentials to log in.   
</p>
<br />

<p>

![icmp blank](https://github.com/user-attachments/assets/4244d588-b51d-40ed-9596-ac959cde6fac)

</p>
<p>
Observing ICMP Traffic. We start by typing icmp all lower case in the green search bar and pressing "Enter". This tells Wireshark to filter out all inbound and outbound traffic except for ICMP Traffic. We can now see all of the packets that were captured.    
</p>
<br />

<p>

 ![scrnshot 4](https://github.com/user-attachments/assets/669542ad-ab27-4552-be8f-492a8d172798) ![scrnshot 2](https://github.com/user-attachments/assets/696e0039-4969-4f3c-a611-d29a7a222546)

</p>
<p>
After opening Powershell, we will run the Ping Command, followed by the Private IP Address of the Linux Virtual Machine , "ping 10.0.0.5".  This will allow Wirshark to capture and display the ICMP traffic that we're looking for. 
</p>
<br />

<p>
 
![scrnshot 5](https://github.com/user-attachments/assets/60e648db-e41f-44b8-8b6c-330d41155ea1)

</p>
<p>
Back in Wireshark, we see the packets, which are requests from the Linux Virtual Machine, as well as the replies from the Windows Virtual Machine. This shows that the Windows and Linux Virtual Machines both have a successful connection.   
</p>
<br />

<p>

![scrnshot nsg ping -t command](https://github.com/user-attachments/assets/89734012-8624-47d8-b752-387347858629) ![scrn shot ping -t](https://github.com/user-attachments/assets/9f21bc81-f5a9-4bd3-b2e8-242f5c0929e5)

</p>
<p>
Configuring a Firewall (Network Security Group). To start, we initiate a perpetual/non-stop ping from the Windows 10 Virtual Machine to the Linux Virtual Machine by running the command... "ping 10.0.0.5 -t". We will notice that Wireshark starts to non-stop ping ICMP Traffic.  
</p>
<br />

<p>

 ![Screenshot 2025-06-27 123217](https://github.com/user-attachments/assets/3c2eb432-f097-491b-9251-0b5806fb68e4) ![Screenshot 2025-06-27 123636](https://github.com/user-attachments/assets/6534b649-10cb-4e3d-8302-b193515ec215) ![image](https://github.com/user-attachments/assets/3eeeba3d-9429-4cf5-83df-698c97fe1b33)


</p>
<p>
Back in Microsoft Azure, open the Network Security Group for the Linux Virtual Machine and disable incoming or inbound ICMPv4 traffic, this is the traffic that appears in Wireshark after running the "Ping" command . Click on Network Settings, open the Network Security Group settings for the Linux Virtual Machine, click inbound rules, and click add new inbound rule. Source/Destination Ports have the (*) symbol, which means any port, this is because ICMP Protocol does not use any specific ports. Finally we click "add". We can see that our new inbound rule was successfully created.   
</p>
<br />

<p>

  ![ggugyu](https://github.com/user-attachments/assets/e7b2b22d-3cbb-4dd4-a94d-73b6bf8eb604) ![Untitled](https://github.com/user-attachments/assets/0833ad3a-25d8-4486-8ce8-f566a05c7527)

</p>
<p>
After enabling our new Inbound Security Rule, we now only see "Request timed out". This shows that our new Inbound Security Rule is working and we now have successfully configured a Network Security Group (NSG). We can delete the rule if we want to revert the changes.  
</p>
<br />

<p>

![ssh command](https://github.com/user-attachments/assets/319c15ea-f8f8-4a97-9f11-e3fb4c458967) ![scrn shot 20](https://github.com/user-attachments/assets/6c67eb14-4893-4050-abfc-56bbcf2f19e6) ![ssh filter after connection](https://github.com/user-attachments/assets/3bf8af52-487e-41a7-a594-136d0e7295d7)

</p>
<p>
Observe SSH Traffic. Secure Shell (SSH) is used to make a secure connection from one computer to another, this ebables all communication to be encrypted or hidden. In the Windows Virtual Machine, open WireShark and start a packet capture. Filter for SSH traffic only. Next, open PowerShell and run the command  "ssh labuser@10.0.0.5", this tells the Windows Virtual Machine that we want to Secure Shell (SSH) connect to the Linux Virtual Machine from the Windows Virtual Machine. We specified the username and private IP Address of the Linux Virtual Machine after the SSH command in order to connect our Windows Virtual Machine to the Linux Virtual Machine via Secure Shell (SSH) connection. Say "yes" to fingerprint and provide the Linux Virtual Machine Credentials to successfully connect via Secure Shell (SSH). Secure Shell uses TCP Port: 22.
 </p>
<br />

<p>
 
 ![ffgyghjgjghjgjkj](https://github.com/user-attachments/assets/155fc27c-3b79-4013-a274-e670ae6c1973)

</p>
<p> 
 We can see that the connection to the Linux VM was successful.
</p>
<br />

<p>
 
 ![ipconfig renew](https://github.com/user-attachments/assets/1a132272-1cd5-4682-be5c-3444ae7bf8db) ![dhcp filtered](https://github.com/user-attachments/assets/b27ee957-a8fa-4c16-a915-efdf3de05fd3)

</p>
<p>
Observe DHCP Traffic. This protocol is used to assign an IP Address to devices when they are first connected to the network. DHCP uses UDP Ports: 67 and 68. Back in Wireshark, filter for DHCP traffic only From your Windows 10 Virtual Machine, attempt to issue a new IP address from the command line. Open PowerShell as an adminintrator and run the command "ipconfig /renew". We will see the DHCP traffic appearing in WireShark

</p>
<br />


<p>

 ![nslookup google and disney](https://github.com/user-attachments/assets/920d1a05-8b0f-4dec-ab8c-5fde4d49f706) ![dns traffic disney and goog;e](https://github.com/user-attachments/assets/8d5bdcab-dade-4462-894c-492b16f7c9e4)

</p>
<p>
Observe DNS Traffic. DNS, or Domain Name System, uses TCP/UDP Port: 53. From Powershell in the Windows VM, run the command "nslookup" followed by the URL of "google.com" and "disney.com" to see what the IP addresses are. In Wireshark, filter for DNS traffic only. Observe the DNS traffic being show in WireShark

</p>
<br />

<p>

 ![rdp filtered](https://github.com/user-attachments/assets/51b30648-4333-4b4e-a984-705db01039a6)

</p>
<p>
Observe RDP Traffic (Remote Desktop Protocol). In Wireshark, we type "rdp" in the search bar, followed by pressing "enter", in order to filter for RDP traffic only. RDP or Remote Desktop Protocol, is used for remotely connecting from one computer to another, gaining a Remote Desktop Graphical User Interface (GUI). RDP uses TCP Port: 3389
</p>
<br />
