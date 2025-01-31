<p align="center">
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

<h5>Create a virtual machine called DC-1</h5>
<p>
<img src="images/1 - createVm.PNG" alt="createVm" width="50%" height="50%">
<img src="images/2 - vmData.PNG" alt="vmData" width="50%" height="50%">
<img src="images/3 - vmBottomData.PNG" alt="vmBottomData" width="50%" height="50%">
<br />
<br />
<br />
  
<h5>Create a virtual machine called Client-1</h5>
<img src="images/4 - vmClient1DataTop.PNG" alt="vmClient1DataTop" width="50%" height="50%">
<img src="images/5 - vmClient1DataBottom.PNG" alt="vmClient1DataBottom" width="50%" height="50%">
<img src="images/6 - skipDisks.PNG" alt="skipDisks" width="50%" height="50%">
<img src="images/7 - networkingOptions.PNG" alt="networkingOptions" width="50%" height="50%">
<img src="images/8 - createVmTwo.PNG" alt="createVmTwo" width="50%" height="50%">
<br />
<br />
<br />

<h5>Network Settings</h5>
<img src="images/9 - networkSettings.PNG" alt="networkSettings" width="50%" height="50%">
<img src="images/10 - clickTheNic.PNG" alt="clickTheNic" width="50%" height="50%">
<h5>Set Domain Controller’s NIC Private IP address to be static</h5>
<img src="images/11 - configStatic.PNG" alt="configStatic" width="50%" height="50%">
<br />
<br />
<br />


<h5>Login into VM DC-1</h5>
<img src="images/12 - accessClientVm.PNG" alt="accessClientVm" width="50%" height="50%">
<img src="images/13 - login.PNG" alt="login" width="50%" height="50%">
<img src="images/15 - openWfmsc.PNG" alt="openWfmsc" width="50%" height="50%">
<img src="images/16 - enableCoreNetworking.PNG" alt="enableCoreNetworking" width="50%" height="50%">
<h5>Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t (ip address) (perpetual ping)</h5>
<img src="images/17 - SuccessfulPing.PNG" alt="SuccessfulPing" width="50%" height="50%">
<br />
<br />
<br />


<h5>Install Active Directory</h5>
<img src="images/18 - part2AddRoles.PNG" alt="part2AddRoles" width="50%" height="50%">
<h5>Login to DC-1 and install Active Directory Domain Services</h5>

<img src="images/19 - aDServices.PNG" alt="aDServices" width="50%" height="50%">
<img src="images/20 - finishInstall.PNG" alt="finishInstall" width="50%" height="50%">
<h5>Promote as a DC: Setup a new forest as mydomain.com </h5>
<img src="images/21 - selectDomain.PNG" alt="selectDomain" width="50%" height="50%">

<h5>Make sure Create DNS Delegation box is unchecked</h5>
<img src="images/22 - uncheckBox.PNG" alt="uncheckBox" width="50%" height="50%">
<br />
<br />
<br />


<h5>Login as admin_Jane</h5>
<img src="images/24 - gotToActiveDirectory.PNG" alt="gotToActiveDirectory" width="50%" height="50%">
<img src="images/24 - janeHomeScreen.PNG" alt="janeHomeScreen" width="50%" height="50%">
<img src="images/25 - newOrganization.PNG" alt="newOrganization" width="50%" height="50%">
<br />
<br />
<br />


<h5>Add EMPLOYEE and ADMIN FolderS</h5>
<img src="images/26 - EMPLOYEES.PNG" alt="EMPLOYEES" width="50%" height="50%">
<img src="images/27 - newFolders.PNG" alt="newFolders" width="50%" height="50%">
<br />
<br />
<br />


<h5>Add new admin</h5>
<img src="images/28 - newAdmin.PNG" alt="newAdmin" width="50%" height="50%">
<img src="images/29 - janeAdmin.PNG" alt="janeAdmin" width="50%" height="50%">
<br />
<br />
<br />


<h5>Add admin Jane to domain admins</h5>
<img src="images/30 - addJaneToDomain.PNG" alt="addJaneToDomain" width="50%" height="50%">
<img src="images/31 - whoAmIOne.PNG" alt="whoAmIOne" width="50%" height="50%">
<img src="images/32 - logOff.PNG" alt="logOff" width="50%" height="50%">
<br />
<br />
<br />


<h5>Login as Admin Jane</h5>
<img src="images/33 - loginAsJane.PNG" alt="loginAsJane" width="50%" height="50%">
<img src="images/34 - goToSystem.PNG" alt="goToSystem" width="50%" height="50%">
<img src="images/35 - renameThisPc.PNG" alt="renameThisPc" width="50%" height="50%">
<br />
<br />
<br />


<h5>Connect DC-1 to Client-1</h5>
<img src="images/36 - networkSettings.PNG" alt="networkSettings" width="50%" height="50%">
<img src="images/37 - setDnsServer.PNG" alt="setDnsServer" width="50%" height="50%">
<br />
<br />
<br />


<h5>Restart Client-1</h5>
<img src="images/38 - restartClient1.PNG" alt="restartClient1" width="50%" height="50%">
<img src="images/39 - goToStystem.PNG" alt="goToStystem" width="50%" height="50%">
<br />
<br />
<br />


<h5>Rename this PC</h5>
<img src="images/40 - renameThisPc.PNG" alt="renameThisPc" width="50%" height="50%">
<img src="images/41 - nyDomain.PNG" alt="nyDomain" width="50%" height="50%">
<img src="images/42 - newJaneLogin.PNG" alt="newJaneLogin" width="50%" height="50%">
<img src="images/43 - remoteDesktop.PNG" alt="remoteDesktop" width="50%" height="50%">
<br />
<br />
<br />


<h5>Add Jane to Domain Users</h5>
<img src="images/44 - remoteDesktopAdd.PNG" alt="remoteDesktopAdd" width="50%" height="50%">
<img src="images/45 - domainUsers.PNG" alt="domainUsers" width="50%" height="50%">
<img src="images/46 - users.PNG" alt="users" width="50%" height="50%">
<br />
<br />
<br />

<h5>Generate users to work with</h5>
<img src="images/47 - psIseAdmin.PNG" alt="psIseAdmin" width="50%" height="50%">
<img src="images/48 - addScript.PNG" alt="addScript" width="50%" height="50%">
<img src="images/49 - createRandomUsers.PNG" alt="createRandomUsers" width="50%" height="50%">
<img src="images/50 - employeeGenResult.PNG" alt="employeeGenResult" width="50%" height="50%">

<h5>Login as random new user</h5>
<img src="images/51 - randomUserLogin.PNG" alt="randomUserLogin" width="50%" height="50%">
<img src="images/52 - loginScreen.PNG" alt="loginScreen" width="50%" height="50%">

<h5>This new user has locked themselves out</h5>
<img src="images/53 - loginFail.PNG" alt="loginFail" width="50%" height="50%">

<h5>Unlock User's Account</h5>
<img src="images/54 - accountUnlock.PNG" alt="accountUnlock" width="50%" height="50%">

<h5>Reset the user's password</h5>
<img src="images/55 - passwordReset.PNG" alt="passwordReset" width="50%" height="50%">
</br>



