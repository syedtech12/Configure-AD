<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" height="40%" width="70%"alt="Microsoft Active Directory Logo"/>
</p>

<h1>Configuring Active Directory (On-Premises) Within Azure</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />
<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10

<h2>High-Level Deployment and Configuration Steps</h2>

- Create Resources
- Ensure Connectivity between the client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in AD
- Join Client-1 to your domain (myadproject.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create additional users and attempt to log into client-1 with one of the users

<h2>Deployment and Configuration Steps</h2>
<br />
<br />
<h3 align="center">Setup Resources in Azure</h3>
<br />
<p>
  <img src="https://i.imgur.com/iidunqP.png" height="75%" width="100%" alt="resource group"/>
<p>
  Create a Virtual Network and Subnet:
<p>
  <img src="https://i.imgur.com/LXthkle.png" height="75%" width="100%" alt="Create a Virtual Network and Subnet"/>
</p>
  Create the Domain Controller VM (Windows Server 2022) named “DC-1”:
</p>
<p>
  <img src="https://i.imgur.com/Ix3dxoo.png" height="75%" width="100%" alt="vm ms server"/>
</p>
<p>
  Create the Client VM (Windows 10) named “Client-1”. Use the same Resource Group and Vnet that was created in previous step:
</p>
<p>
  <img src="https://i.imgur.com/hNxnYar.png" height="75%" width="100%" alt="vm windows"/>
</p>
<p>
  Set Domain Controller’s NIC Private IP address to be static:
</p>
<p>
  <img src="https://i.imgur.com/G5vNOfj.png" height="75%" width="100%" alt="static ip"/>
</p>
<br />
<br />
<h3 align="center">Ensure Connectivity between the client and Domain Controller</h3>
<br />
<p>
  Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping):
</p>
<p>
  <img src="https://i.imgur.com/bnPM9tX.png" height="75%" width="100%" alt="perpetual ping"/>
</p>
<p>
  Login to the Domain Controller and enable ICMPv4 in on the local windows firewall:
</p>
<p>
  <img src="https://i.imgur.com/ZpPyEkt.png" height="75%" width="100%" alt="enable ICMPv4"/>
</p>
<p>
  Check back at Client-1 to see the ping succeed:
</p>
<p>
  <img src="https://i.imgur.com/8o3OfjY.png" height="75%" width="100%" alt="ping success"/>
</p>
<br />
<br />
<h3 align="center">Install Active Directory</h3>
<br />
<p>
  Login to DC-1 and install Active Directory Domain Services:
</p>
<p>
  <img src="https://i.imgur.com/fFs1goD.png" height="75%" width="100%" alt="active directory install"/>
</p>
 Promote as a Domain Controller:
</p>
<p>
  <img src="https://i.imgur.com/XYbVzqg.png" height="75%" width="100%" alt="domain controller promotion"/>
</p>
<p>
Setup a new forest as (can be anything, just remember what it is) I set it up as syedsactivedirectory.com:
</p>
<p>
  <img src="https://i.imgur.com/NTcBfbt.png" height="75%" width="100%" alt="set new forest"/>
</p>
<p>
  Restart and then log back into DC-1 as user: myadproject.com\labuser:
</p>
<p>
  <img src="" height="75%" width="100%" alt="fqdn login"/>
</p>
<br />
