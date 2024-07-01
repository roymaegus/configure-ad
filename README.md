<p>
<img src="images/msAzureBanner.PNG" alt="dndUploadFolder" width="50%" height="50%">
</p>

# On-premises Active Directory Deployed in the Cloud (Azure)

This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.

## Environments and Technologies Used
- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

## Operating Systems Used
- Windows Server 2022
- Windows 10 (21H2)

## High-Level Deployment and Configuration Steps
1. Create Two Virtual Machines
2. Ensure Connectivity between the client and Domain Controller
3. Install Active Directory
4. Create an Admin and Normal User Account in AD
5. Join Client-1 to your domain
6. Setup Remote Desktop for non-administrative users on Client-1
7. Create additional users and attempt to login Client-1 with one of the users

## Deployment and Configuration Steps

### Create Two Virtual Machines
To start, go to [portal.azure.com](https://portal.azure.com) and create a profile or login. Create a subscription name, create a resource group, create two virtual machines, create a domain controller using Windows Server, and a client PC using Windows 10 Pro.

### Ensure Connectivity between the client and Domain Controller
1. In Azure, click on Networking and change the private IP address from dynamic to static so the IP address will stay the same for the client's DNS to connect to the server.
2. From the networking screen, click on your Network interface name to open ipconfig from the menu.
3. Once your NIC settings are open, click on IP Configuration and the three dots for your private IP address at the bottom of the screen.
4. From the ipconfig1 screen, change the assignment of the private IP address from dynamic to static. Then click Save.
5. Login to the Domain Controller through the Remote Desktop Connection and enable ICMPv4 on the local Windows Firewall. To do this, go to Start, Windows Administrative Tools, Windows Defender Firewall with Advanced Security.
6. From the Windows Defender menu, click on Inbound Rules, click on Protocol to ascend the types, look for ICMPv4 protocol, right-click on echo requests and Enable Rule. This will now allow the client's DNS server to establish a connection with the server.
7. To confirm connectivity, open an instance of your client desktop and open your command prompt, type `ping -t [private IP address]` and press enter. If a connection has been established, this command will ping the specified host continuously until stopped. The host is replying, so we have established a successful connection between the client and the host.

### Install Active Directory
1. Open an instance of your Domain Controller from the Remote Desktop Connection and open the server manager. Click on Add roles and features. The following steps will install Active Directory on this server.
2. Click Add roles and features and the wizard will open. Click next continually until you see your destination server to connect. Click next a few times again until you see the Select server roles. Check the radio button Active Directory Domain Services. On that page, click on Add Features. Click next through the proceeding pages that install all of the dependencies and the final install button.
3. Once Active Directory is installed, the server still needs to be promoted as a domain server. In the upper right-hand corner, you will see a yellow caution sign next to the flag. Click on that flag and the drop-down menu will populate and select Promote the server to a domain controller.
4. In the Deployment Configuration dialog box, click on Add a new forest and give your DC a domain name and click on next.
5. Create a password for Directory Service Restoration Mode (DSRM), click Next until the domain controller finishes installing. It will automatically reboot, and you will need to log in with your domain name\username and password as the server has been promoted to a domain controller.

### Create an Admin and Normal User Account in AD
1. Go to your Remote Desktop Connection and log into your domain controller. In the Server Manager Menu, click on Tools, Active Directory Users and Computers and it will open its window.
2. In Active Directory, right-click on your domain name and move your mouse to hover new, Organizational Unit, and left-click to create folders for your AD. We will create employees, admins, and security groups.
3. After the Admins and Employees folder has been created, create an admin user for the admin folder. To create a user, right-click on the _ADMINS folder under your domain, hover over New, hover to User, and left-click User.
4. Once the user has been created, the account must be added as an admin to that folder. To add this user as an administrator, right-click on the name, hover to Properties, click on Properties, click on the Member Of tab, double-click on Domain Users to open the next window.
5. Once the group box is populated, type "domains" in the enter the object names to be selected box, click on Check Names to the right, select Domain Admins, click Ok, click on Apply, and click Ok. This will add your user as a domain admin to your active directory. Log out of the server and log back into the server as the admin.

### Join Client-1 to Your Domain
1. Go to Azure and go to Virtual Machines, click on DC-1, Networking and get the private IP address. You will need this IP address to connect Client-1's DNS server.
2. In Microsoft Azure, go to virtual machines and select Client-1, Networking, click on the Network interface, DNS servers, select the ratio button in DNS servers from Inherit from network to Custom, type in DC-1's private IP address in the bar, click Save. Once the settings are saved, you will restart Client-1 within the Azure portal, and it will flush the DNS cache.
3. Log into Client-1 using your login credentials from Microsoft Azure, go to Start, Settings, About, Rename this PC (advanced), click on Domain, type the name of your domain in the domain box, click OK.

### Setup Remote Desktop for non-administrative users on Client-1
1. Connect to your remote desktop now as the admin that you created in your _ADMINS folder in your active directory. Right-click on the start menu and click on system properties, click on Remote Desktop, click Select users that can remotely access this PC, type "domain" in the object names box, click on Check Names to the right, another dialog box will show the groups, select Domain Users, click ok.
2. Login to your domain controller (DC-1) as an admin. Go to your Server Manager, Tools, Active Directory Users and Computers to open your AD, click on Users, Domain Users. This will bring you to your domain users policy. This is where your non-admin users will show up. *Note: Group Policy will allow you to assign many users to many systems at once, but it's not covered in this session.

### Create additional users and attempt to login Client-1 with one of the users
**Note: This method will add 10,000 users using programming code in PowerShell.**
1. Log into your remote desktop Client-1 with your system admin credentials. Once Windows is open, type PowerShell ISE in your search bar, open as an administrator, click on the New File icon, paste the code, click on the Run icon that looks like a green play button and the users will load into the system. We will go back to DC-1 and choose a user, get credentials, and log into Client-1 with that user's credentials.
2. In your domain controller, go to your Server Manager, Tools, Active Directory Users and Computers, click on your domain, click on _EMPLOYEES folder that was created previously, double-click on a user and the Properties window will populate, click on the Account tab, type a login name in the box for your user, click Ok.
3. Log into your Remote Desktop Connection using the username and credentials from DC-1. You will need to use the domain\default username and default password. Open command prompt and confirm username by typing `whoami` and type `hostname` to verify the name of the computer.


