<h1>On-Premises Active Directory Deployed in the Cloud (Azure)</h1>
This is an implemntation of on-premises Active Directory while using Azure Virtual Machines.

<h2>Materials Used</h2>

-  Microsoft Azure (Virtual Machines/Computer/Network)
-  Remote Desktop
-  Active Directory Domain Services
-  Powershell
-  Windows Server 2022
-  Windows 10 OS (Operating System)

<h2>Deployment and Configuration Process</h2>

-  Create the Azure Virtual Machines
-  Ensure that the virtual machines are communicating
-  Installing Active Directory
-  Configuring Accounts in Active Directory
-  Join the Client VM to the Domain
-  Setup Remote Desktop for non-administrative users

<h2>In depth Deployment and Configuration Process</h2>

Begin by creating a Resource Group within Azure

Create a Virtual Network and Subnet

Create a Domain Controller VM (Window Server 2022) for this instance it will be labeled DC-1

Create the Client VM (Windows 10)

Change the Domain Controller's NIC Private IP from Dynamic to Static



<h2>Ensure Connection Between the Virtual Machines</h2>

Login to the CLient VM through Remote Desktop and ping DC-1's IP address with ping -t (Command Line for a perpetual ping)

This ping should initially fail or time out within the Command Line Prompt

(Screenshot here)

Login to the Domain Controller with Remote Desktop and enable ICMPv4 on the local Windows Firewall

To navigate to the Firewall click in the windows search bar and type in Firewall and select the option "with Advanced Security

Select Inbound Rules then click to sort by Protocol

Once sorting by Protocol find ICMPv4 and Enable the Core Networking Echo Requests by right clicking on them

(Screenshot here)


Check CLient VM to see the ping succeed and in the Command Line Prompt hit the buttons Ctrl-C to stop the ping

(Screenshot here)

<h2>Installing Active Directory</h2>

Install Active Directory through the Server Manager software

Active Directory Domain Services

Click Yellow Flag up top to begin turning the VM into the Domain Controller

(Click through the process until it is all installed)

Once the installation process has been completed then it will automatically close the Remote Desktop session to restart as a Domain Controller

When logging in through Remote Desktop again a new login account name will be needed to login successfully



<h2>Configuring Accounts in Active Directory</h2>

Will create Organizational Units and setup an Administrator user

To access Active Directory click the Tools dropdown box in Server Manager

Create an Employees and Admins Organizational Units

Create an Admin account and right click on it to give it Domain Admins Group access 

Then logout of current Remote Desktop session

Remote Desktop back into the Domain Controller as the Admin Account that was created



<h2>Join the Client VM to the Domain</h2>

From the Azure portal take the Client VM's Private IP Address and alter it to match the Domain Controllers Private IP Address

Then restart the Client VM within the Azure portal

Remote Desktop back into the Client VM to join it to the Domain

When in the Client VM right click on the start button and select System and then click on "Rename this PC (advanced)"

(Screenshot the Domain Stuff)

Logout of Client VM

<h2>Setup Remote Desktop for non-administrative users on Client VM</h2>



