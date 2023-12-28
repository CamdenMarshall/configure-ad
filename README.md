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

<h2>In Depth Deployment and Configuration Process</h2>

Begin by creating a Domain Controller VM (Window Server 2022) for this instance it will be labeled DC-1

![image](https://github.com/CamdenMarshall/configure-ad/assets/153537343/7fb71902-7e4f-4fba-ac71-62b2a9c98872)

While creating the Domain Controller set the Resource Group

During the setup of the Domain Controller create the Admin account and ensure that you can refer back to that information as needed

A Virtual Network and Subnet will be created during the creation of the Domain Controller

Change the Domain Controller's NIC Private IP from Dynamic to Static

-  Select DC-1 from Virtual Machines tab
-  Select Networking from the menu on the the right
-  Click on the Network Interface
![image](https://github.com/CamdenMarshall/configure-ad/assets/153537343/437ad667-099d-4ba2-87db-156e4c9ea293)
-  Go to IP configurations and select ipconfig
-  Turn the Private IP address to static
![image](https://github.com/CamdenMarshall/configure-ad/assets/153537343/35265b1f-7f75-4aeb-b9b9-4fdb3217f3ff)


Create the Client VM (Windows 10) on the created VNet



<h2>Ensure Connection Between the Virtual Machines</h2>

Login to the Client VM through Remote Desktop and ping DC-1's IP address with ping -t (Command Line for a perpetual ping)

This ping should initially fail or time out within the Command Line Prompt

![image](https://github.com/CamdenMarshall/configure-ad/assets/153537343/7d01c673-bd5f-4a10-9371-b5d477be9ce2)


Login to the Domain Controller with Remote Desktop and enable ICMPv4 on the local Windows Firewall

To navigate to the Firewall click in the windows search bar and type in Firewall and select the option "with Advanced Security

Select Inbound Rules then click to sort by Protocol

Once sorting by Protocol find ICMPv4 and Enable the Core Networking Echo Requests by right clicking on them

![image](https://github.com/CamdenMarshall/configure-ad/assets/153537343/2d6aa81d-22bd-4bcf-8728-d68f03e57b0b)


Check Client VM to see the ping succeed and in the Command Line Prompt hit the buttons Ctrl-C to stop the ping

![image](https://github.com/CamdenMarshall/configure-ad/assets/153537343/7577a43b-6872-40b0-a55f-87acaf100677)


<h2>Installing Active Directory</h2>

Install Active Directory through the Server Manager software

Active Directory Domain Services by clicking on Add roles and features

![image](https://github.com/CamdenMarshall/configure-ad/assets/153537343/f3a1e85e-12db-4819-9486-50936307a7d7)

![image](https://github.com/CamdenMarshall/configure-ad/assets/153537343/afa89a47-c688-4e57-bbb7-63fbb96334f4)


Click The Flag up top to begin turning the VM into the Domain Controller

![image](https://github.com/CamdenMarshall/configure-ad/assets/153537343/ccf925a2-8b5f-4e96-91c6-8c8e0ddaf06e)


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

Remote Desktop connect into the Client VM once again but login as the Admin account

Once logged in return to System and then click on "Remote Desktop" then access "Select users that can remotely access this PC"

Add "Domain Users" to the users allowing all users on the Domain to login through the Client VM

(Screenshot adding Domain Users)



