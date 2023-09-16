<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Protocols and Traffic</h1>

In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups.

<p></p>

<h2>Environments and Technologies Used</h2>

- Microsoft Azure Virtual Machines
- Microsoft Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDP, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Step 1: Create Virtual Machines and Download Wireshark
- Step 2: Observe ICMP Traffic
- Step 3: Observe SSH Traffic
- Step 4: Observe DHCP Traffic
- Step 5: Observe DNS Traffic
- Step 6: Observe RDP Traffic

<h2>Actions and Observations</h2>

<h3>Step 1: Create Virtual Machines</h3>

The first step is to create two virtual machines (VMs) in Azure. One VM will be running Windows 10 and the other will be running Linux Ubuntu Server. 


Once you have created your VMs, log into the Windows VM via Microsoft Remote Desktop. From within the VM, download [Wireshark](https://www.wireshark.org/download.html).

![image](https://github.com/mathew-perez/azure-network-protocols/assets/144407220/ea51d2df-0617-4e9f-85c8-4e94ae4d7157)
![image](https://github.com/mathew-perez/azure-network-protocols/assets/144407220/189bdb4a-ea1b-4bc4-9de8-4c521c70c98e)


<h3>Step 2: Observe ICMP Traffic</h3>
Next, we'll begin to use Wireshark. Wireshark is a network protocol analyzer and you can use it to observe the capturing of packets from a network connection. Before starting, grab the private Internet Protocol (IP) address of the Linux VM first.

![image](https://github.com/mathew-perez/azure-network-protocols/assets/144407220/285f3a88-612c-4bbe-9d3c-014982aaf983)

Internet Control Message Proctol or ICMP is a network protocol that determines if there is communication issues. It is primarily used to report errors. 

<p></p>

Next, open up Wireshark and Windows Powershell. In Wireshark, type in "icmp" in the green bar. In Powershell ping the Linux VM's private IP address (10.0.0.5 in my example). Then ping a public website (Google). Observe the network traffic in both Wireshark and Powershell. Then setup a perpetual ping using "ping -t" + Linux VM's private IP in Powershell. 

![image](https://github.com/mathew-perez/azure-network-protocols/assets/144407220/812f16fb-6b44-4f19-86d8-865948232485)


Next, we'll observe what happens when we block the ICMP traffic. Go back to the Linux VM's Azure Portal, then click on Networking. From Networking, click "Add inbound port rule" -> check ICMP -> check Deny, then click "Add". 

<p></p>
This area of Azure is known as Network Security Groups (NSGs). It is basically a firewall in Azure as you can set security rules for your resources. 

![image](https://github.com/mathew-perez/azure-network-protocols/assets/144407220/bcaa9376-0649-4956-be02-59eecab3ad28)

</p>

Once this is done, go back into the Windows VM and observe the changes in Wireshark and Powershell. Since ICMP traffic is being denied, the requests to are timing out and are showing no response.

![image](https://github.com/mathew-perez/azure-network-protocols/assets/144407220/8abd21b0-3a4c-45f2-9f33-39b8a7079e9f)


Next, we'll go back to the Azure Portal and set allow ICMP traffic again. You can either delete the rule or set it to allow. Observe the changes in Wireshark and Powershell again. To stop the perpetual ping, just press "Control" + "C". 

![image](https://github.com/mathew-perez/azure-network-protocols/assets/144407220/d4ca3ee2-318c-46c3-9592-4bd8f416adc4)

![image](https://github.com/mathew-perez/azure-network-protocols/assets/144407220/99823a42-9493-4d8f-8a1a-9480e7d95c1a)


<h3>Step 3: Observe SSH Traffic</h3>
Next, we'll observe SSH traffic. Secure Shell Protocol or SSH is a network protocol which allows a secure connection to another machines Command Line Interface (CLI). 

<p> </p>
Filter ssh traffic in Wireshark. Then type "ssh" + the Linux VM's private IP address. Powershell will prompt you to login, so use the Linux VM's login credentials. Once you are logged in via SSH, you can begin to play around with it by using Linux commands such as "cd", "pwd", etc. To exit SSH just type "exit". 

<p>
<img src="https://i.imgur.com/2hRFoSS.png" height="80%" width="80%" alt="15."/>
</p>

<p>
<img src="https://i.imgur.com/sa57YlF.png" height="80%" width="80%" alt="16."/>
</p>

<h3>Step 4: Observe DHCP Traffic</h3>
Next, we'll observe DHCP traffic. Dynamic Host Configuration Protocol or DHCP is the network protocol responsible for automatically assigning IP addresses.

<p></p>
Filter DHCP traffic in Wireshark. In Powershell, type the command "ipconfig /renew" and observe the changes. 

<p>
<img src="https://i.imgur.com/DI56TjI.png" height="80%" width="80%" alt="17."/>
</p>

<h3>Step 5: Observe DNS Traffic</h3>
Next, we'll observe DNS traffic. Domain Name System or DNS is the network protocol that transforms Fully Qualified Domain Names (FQDNs) into their assigned IP addresses. Type DNS in Wireshark and the command nslookup. I used Google and Disney in this example. 

<p></p>

If you want to learn about DNS, please see my lab on it [here](https://github.com/klcarpio/Understanding-DNS).

<p>
<img src="https://i.imgur.com/vnVMyIj.png" height="80%" width="80%" alt="18."/>
</p>

<h3>Step 6: Observe RDP Traffic</h3>
Finally, we'll observe RDP traffic. Remote Desktop Protoctol or RDP is the protocol that allows the remote connection to another computer and complete control of the Graphical User Interface (GUI). Type RDP in Wireshark and observe the traffic. Since it is a VM, you can see there is a lot of RDP traffic. 

<p>
<img src="https://i.imgur.com/7IuT1yZ.png" height="80%" width="80%" alt="19."/>
</p>

Thank you for checking out this tutorial. It should have helped you gain a better understanding of network protocols and how network traffic works. 


**REMEMBER TO DELETE YOUR RESOURCES ONCE YOU ARE DONE WITH THE LAB!**
