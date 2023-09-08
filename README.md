# Configuring-On-premises-Active-Directory-within-Azure-VMs
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>
<p align="center">
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/7f432c24-4e30-498f-bc8d-c356b9c88f59"/>
</p>
<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: Lab 5 :  Configuring On premises Active Directory within Azure VMs](https://youtu.be/PJnGEWljhkc)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create Resource Group
- Create Virtual Machine Windows Server Datacenter
- Create Virtual Machine Windows 
- Use Remote Dektop Connection to log into Cilent-1 VM
- Grab the Private IP of DC-1 to do a endless ping on Cilent-1 VM in Command Prompt
- Go to DC-1 to load wf.msc to allow the ping to occur in inbound rules
- Go to Server Manager to add roles and features
- Create a Active Directory Domain Services
- Promote the server to a domain controller and create a new forest
- Log back into DC-1 VM by using mydomian.com\labuser
- In DC-1 go to tools, and go to Active Directory Users and Computers
- Create a new organizational unit folder called _EMPLOYEES
- Create another new organizational unit folder called _ADMINS
- Create new user in ADMINS folder
- Put new user in Domain Admins then logoff of DC-1
- Log back into DC-1 under Admin account
- Go back to Cilent-1 and rename this pc under a new domain, but will recieve an error
- Copy DC-1 Privite NIC IP then paste in Cilent-1 DNS Servers
- Restart Cilent-1 VM
- Log into Cilent-1 VM using Remote Desktop Connection
- Rename this PC again in Cilent-1 VM
- Change the Domain name to user Admins
- Restart VM again
- Log into Cilent-1 VM under admin account using Remote Desktop Connection
- Use Remote Desktop to let Domain Users log into the account
- Go back to DC-1 VM and go to the Users folder to see both labuser and admin account in Domain Users
- Run Windows Powershell ISE as administrator
- Create a new file and run script for creating 2000 users
- Go to _EMPLOYEES folder and grab one's display name
- Logoff of Cilent-1 VM then log back into Cilent-1 VM under user you picked
- Logoff Cilent-1 as random user
- Grab another random user Display name
- Log back into Cilent-1 VM with new user but mistype password to get kicked out of account
- Go to DC-1 VM and manually reset the password or unlock the account

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/2ab35262-3971-4727-a542-e245a44edd3b"/>
</p>
<p>
First go to Microsoft Azure and type Resource Group 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/bbaa41e2-d3fb-4479-a90c-f4462759f6ea"/>
</p>
<p>
Next click create to create the Resource Group
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/7d172964-31b9-4803-a324-ad768c70c8c5"/>
</p>
<p>
Now for the name type AD-LAb and the region under US West US 3 then go to the review and create tab 
</p>
<br />


<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/20b91653-279e-4a5d-9731-4ed229abd1ce"/>
</p>
<p>
Next the validation pass through 
</p>
<br />


<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/423985b6-0399-48c6-b659-14f64e9f8c89"/>
</p>
<p>
Now once the process is done you will see the Resource Group was created 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/ad25a52e-2b2c-444d-b1e9-5be18b516090"/>
</p>
<p>
Type Virtual Machine in the search bar 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/cfa8962d-0b01-4711-b314-dbd18edc04d5"/>
</p>
<p>
Next click Azure Virtual Machine to create the VM
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/21a7d91a-4c51-46cd-9361-784fea32dc2c"/>
</p>
<p>
Now for the resource group click AD-LAb, and the virtual machine name type DC-1. The region put under US West US 3 and the image under Windows Server
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/3bb65ff1-041d-4d79-8484-bf9405119a99"/>
</p>
<p>
Next the size needs to be under Standard E2 and teh username under labuser and the password under your own unique password. Remember to open a notepad and type all your info out so you dont lose it.
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/9319be66-069e-4170-8aca-5498bc8b12e2"/>
</p>
<p>
Next click the box in the Licensing section and then click th econfirm box. Then click review and create 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/2ae3c544-c562-4247-84f1-878b68045f24"/>
</p>
<p>
Now go to the networking tab and make sure the virtual network, subnet, and the public IP all says (new)
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/40e5830a-4e4a-47ef-873a-d178b6592834"/>
</p>
<p>
Now go to the review and create section 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/d001f26b-93b9-4f36-b146-23d5bcc06528"/>
</p>
<p>
Next let the deployment progess load 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/a4017821-7d27-4ab7-91a6-b04fa467f625"/>
</p>
<p>
Now the process will be complete when there is a green check 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/80d04256-ffcb-4d47-a93a-de6f38304d29"/>
</p>
<p>
Next type virtual machine and you will see DC-1 VM was created
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/04c3a764-33ce-462f-a1f7-6b01300f4a3e"/>
</p>
<p>
Next click create and then go to Azure Virtual Machine 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/69a42173-e8e8-4b79-9fd1-b2fdd064445c"/>
</p>
<p>
Next in the subscriiption section make sure the same subscription that you used for the resource group is selected. Then in Resource Group click AD-Lab then for the name type Cilent-1 and the region click US West US 3
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/7e636d9a-cbdc-4eeb-8e27-99d34d345dce"/>
</p>
<p>
Now for the Image click Windows 10 pro version and the size click Standard E2
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/f8993172-9c42-482e-8a3e-f831c32acf9b"/>
</p>
<p>
Next for the username type labuser and the password the same as DC-1 VM. Then click the Licensing tab then click review and create 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/b5335eee-d6c4-4d58-ae9e-5c4896c93117"/>
</p>
<p>
Now the deployment will be done when a green check appears next to the deployment
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/8cf04195-6679-428e-a77f-06899ae7dc06"/>
</p>
<p>
Next type virtual machines in the search bar 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/f0ed0801-4d05-4531-96e9-054f6d9d1800"/>
</p>
<p>
Next you will see that DC-1 and Cilent-1 was created 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/0f5791a0-296f-40a0-9d8d-4dd40f783b0c"/>
</p>
<p>
Now click DC-1 and click networkng 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/667a5e43-913b-4276-9f10-d2fff584106b"/>
</p>
<p>
Next click on the Network Interface 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/6217f4e0-7135-4bcb-8605-cd54b8b86943"/>
</p>
<p>
Next click on IP Configurations 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/5de5cb97-2158-411d-9b7f-51363d08152b"/>
</p>
<p>
Now click ipconfig1
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/3f192efc-718d-42e4-bdf1-086e76260773"/>
</p>
<p>
We are editing the IP Configurations in the allocation section click Static instead of Dynamic then click save.
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/0bc6094c-bb28-41e7-91ee-bdc940843048"/>
</p>
<p>
Now we are going to log into Cilent-1 VM copy the public IP address
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/7cee9a52-24e3-4a47-b743-fda018088b52"/>
</p>
<p>
Next type Remote Desktop Connection and click to open the app
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/8fb28bb8-9e13-4115-8900-2cf8a338ca3b"/>
</p>
<p>
Next paste the IP of Cilent-1 in the computer section 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/56423833-9ca1-4e30-bdde-24c5508c152d"/>
</p>
<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/714f1e25-9e0b-431f-8d73-1da1908ee50e"/>
</p>
<p>
Now tpye for the username type labuser and the password type the password you made for the VM, then click ok
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/06d7c39a-e864-4cfe-9905-a7121d9d2457"/>
</p>
<p>
Next click yes to open the VM
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/9f693248-c914-46ab-aa8e-80bed6da0a67"/>
</p>
<p>
Now you should see the VM loading under the name labuser 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/c70b82b7-4382-47ae-ae0e-d782e8dc8a31"/>
</p>
<p>
Next click no to the following image above 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/b085de07-1e8f-45ff-b7d6-88412bb08c5d"/>
</p>
<p>
Once networks load click yes 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/8b6d5ae6-5c7d-44e4-a20c-05647d3a9a85"/>
</p>
<p>
Now open up command prompt 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/2b4973a6-77b0-4bae-9a9b-d1f225fe96d4"/>
</p>
<p>
Next go back to Azure and copy the Private IP of DC-1
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/32f7e581-f58d-4483-8743-b067b24a708f"/>
</p>
<p>
Go back to Cilent-1 VM and type ping -t the the private IP of DC-1. We are doing a endless ping to see the traffic 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/55e8a294-7e44-44ad-9824-1a41a465ea68"/>
</p>
<p>
Then go to Azure and grab the Public IP of DC-1 VM then load Remote Desktop Connection and open the app  
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/4583ff7e-e4c9-4eb5-88be-fc3c4c4f9995"/>
</p>
<p>
Paste the IP of DC-1 in the computer section then click connect 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/dc52a45a-6782-4d7b-8180-214ce6158c52"/>
</p>
<p>
Next type the username labuser and the password you made for DC-1 VM then click ok 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/1b17a0c4-24af-4d5a-b4e8-15c9408a123f"/>
</p>
<p>
Next click yes to log into the VM
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/36f616fd-8423-4235-a9e2-da570f213cf3"/>
</p>
<p>
Once the VM loads let Server Manager load as well. Next once networks load click yes 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/a23e9065-4bde-41be-976a-a044e726775d"/>
</p>
<p>
Next type wf.msc in the search bar of DC-1 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/32520177-a2ef-4f9e-8d4d-9c193d8e8baa"/>
</p>
<p>
Next click on Inbound Rules 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/b27bb6cc-7d6a-493b-8079-b38d1ee2f302"/>
</p>
<p>
Next click the protocol, then look for ICMPv4 protcol
</p>
<br />


<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/6d53aec3-cff6-4b4d-9363-b9040e8577bb"/>
</p>
<p>
Next right click then enable rule for the following in the image above 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/660351d4-7b2b-472e-b355-12f21025cc9e"/>
</p>
<p>
Go back to Cilent-1 VM and you wil see the constant pinging click Ctrl + C then go back to the directory
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/a885a1a1-7ae2-4eac-bb37-66ee8bb7a36b"/>
</p>
<p>
Next go to DC-1 and click add roles and features 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/099486a7-ce1f-4732-b82b-add2bf2fcdb4"/>
</p>
<p>
Click next 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/75a51ee8-5dd7-4805-8f84-42a1d0191e06"/>
</p>
<p>
Click next 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/b88aa771-41fb-4283-af7f-d75a598b6bba"/>
</p>
<p>
Click next 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/3c5e8364-49fd-4a87-91c2-46563e4efb1e"/>
</p>
<p>
Click the box for Active Directory Domain Services 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/5cfef78a-1dc7-4f99-a8dc-88831af6e9c7"/>
</p>
<p>
Click the add features 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/a904d8e1-623f-4df7-adeb-007268c39667"/>
</p>
<p>
Click next 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/8dce276a-20ca-4919-a1b7-bad2b1f4e1d2"/>
</p>
<p>
Click next 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/984ab1ef-fb8b-4c3b-b05c-095b5d3ddcca"/>
</p>
<p>
Click next 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/2696ccd0-c159-48bd-ba14-077cf9e40b64"/>
</p>
<p>
Click Install 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/108624e0-9e54-476f-9c69-ab78f1ce4ed4"/>
</p>
<p>
Next let the installation process start
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/567aa4b3-d65a-4dac-9151-87c2d9f72e71"/>
</p>
<p>
Once the process finishes click close 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/fcf1593b-917c-4d7b-9f44-381e937562e6"/>
</p>
<p>
Next click the caution symbol near manage on the top right 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/067a661f-29a8-471c-a362-82202bb2f9f0"/>
</p>
<p>
Next click Promote this server to a domain controller 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/c709abb1-f85a-46d6-8552-bdb246034825"/>
</p>
<p>
Click add a new forest then type mydomain.com then click next. {NOTE} you can type anything you want just have a .com at the end of it please copy it down to your notepad to not forget 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/f4d0e028-a2fa-442d-8316-ee45eaf005b6"/>
</p>
<p>
Next type the password in for this my password will be Password1 then click next 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/ed56b7fe-3dd9-4a4a-80d0-3732919bff90"/>
</p>
<p>
Next click next
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/16fed491-7bf9-45b0-984c-97b5e5f769c8"/>
</p>
<p>
Next click next
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/0789fc2f-61fd-458f-b1ab-0c4aad4da4b1"/>
</p>
<p>
Next click next
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/b69dff26-9ddd-4e9d-8aa3-bebb91b9dce0"/>
</p>
<p>
Next click next
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/2dff13dc-20a0-4c9b-97f8-a96fe1b753a1"/>
</p>
<p>
Next click install to finish creating the domain controller 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/851bac16-2857-49a4-97f2-718b3a4470ed"/>
</p>
<p>
Then let the installation process finish 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/88a0dbde-5c1c-48f9-8cbe-5fe5ff4a1cb9"/>
</p>
<p>
You might see the image above for Reconnecting dont click cancel let the VM bandwidth connect back only if it doesnt kick you out properly then click cancel 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/9018461c-8592-46d2-ab77-a721142545c3"/>
</p>
<p>
Go back to Azure and click DC-1 copy the public IP 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/ef0abb63-54b6-420a-97bb-4fed450a9871"/>
</p>
<p>
Next type Remote Desktop Conenction and open the app 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/922279f1-9ef3-47ad-a3f8-3d85294b2e80"/>
</p>
<p>
Now since we made DC-1 under another name click more choices then click use a different account 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/a03503ad-020a-4d26-ad3e-df3ff017c439"/>
</p>
<p>
Next tpye in mydomain.com\labuser for the username and the password is Password1 then click ok 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/cbbfdea3-7b3a-4483-925d-c33f49d4c9ce"/>
</p>
<p>
Next click yes to log into the VM {NOTE} if it doesnt work the first time try again to log in. If it still doesn't let you then close Remote Desktop Connection and do the process again 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/d8131e1f-b25f-4d04-b65b-3a53905c75fb"/>
</p>
<p>
Now once you are in the DC-1 VM let Server Manager load on the screen 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/bf8ab7eb-20cd-4f00-9b75-d8a30c299d4f"/>
</p>
<p>
Next click Tools on the top right then go to Active Directory Users and Computers 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/9e37bf8b-9612-411c-b3e4-bce96821898e"/>
</p>
<p>
Next click on mydomain.com folder on the left side 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/aa9f7abb-1250-475c-aa8b-0df5dde626af"/>
</p>
<p>
Next right click anywhere and go to new then to organizational unit 
</p>
<br />


<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/2da9a029-87ec-4608-a92a-275ac7cc3cd5"/>
</p>
<p>
Next type _EMPLOYEES then click ok 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/7563f4fb-a7c8-4bd4-9f52-0d527c214e4a"/>
</p>
<p>
Now go back to mydomain.com and right click anywhere again, go to new then to organizational unit 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/1d9d210a-741a-440d-a029-7af26c750663"/>
</p>
<p>
Next type ADMINS then click ok 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/43d15d55-415b-4fee-b2ad-36282f6704bc"/>
</p>
<p>
In ADMINS right click then go to new then to user
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/5ecc8a96-b727-41fa-a0bf-0c41169302d4"/>
</p>
<p>
For the first name type jane and the intials can be doe or the last name can be doe. For the user logon name type jane_admin then click next 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/74600f4d-1c15-438b-8364-b4d81b28df2d"/>
</p>
<p>
Next for the password type Password1 then uncheck user must change password at next login  
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/406d7077-f41f-4503-8e0f-5ecf613a367e"/>
</p>
<p>
Next check the box for Password never expires then click next
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/9e6cc56e-cebc-4e35-a847-f869bae00e60"/>
</p>
<p>
Then finish to create the user 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/49a3edab-3467-48d3-857f-f62363bb08ef"/>
</p>
<p>
Now you should see jane doe account in the ADMINS folder if not right click then go to refresh 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/d1fda67c-04db-4a7d-a961-56175140c792"/>
</p>
<p>
Next right click the account and go to properties 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/91b3bde9-8ee8-4d35-b5fa-190dc8850201"/>
</p>
<p>
Next the member of tab then click add 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/43587478-a918-4390-9c7a-a41ad4a8c0b6"/>
</p>
<p>
Next in the enter section type domain then click check names 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/9db1856c-35a1-4321-b1e5-f3ab287927e1"/>
</p>
<p>
Next double click on Domain Admins then click ok 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/b0b4fa87-f1a4-4199-938d-cf7359b4e7eb"/>
</p>
<p>
Then click ok 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/08e5dea4-a552-4c81-aa08-bfc48793c0cd"/>
</p>
<p>
Then click apply to finish 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/6fa7ba5c-4236-4e03-9f61-7619eb62df9e"/>
</p>
<p>
Next open command prompt then type whoami you will see we are still under labuser and not jane doe next type logoff 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/702a31f2-03ee-4e18-9701-8981a64ba60c"/>
</p>
<p>
Go back to Azure and click DC-1 and copy the Public IP
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/e8e29ad0-2aa7-4b18-8f2a-a582e23980f6"/>
</p>
<p>
Next type Remote Desktop Connection and open the app
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/7d700907-3cc5-431b-98f0-a37d65e1b3ec"/>
</p>
<p>
Next paste DC-1 VM public IP then click connect 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/5f10add9-bf30-4aa7-81ab-d83b1000d0b2"/>
</p>
<p>
Next click more choices then click use a different account
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/9c0046b0-84ef-47c0-a14f-1337cac6fdeb"/>
</p>
<p>
Next type mydomain.com\jane_admin in the username then the password is still Passsword1 then click ok 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/08c70bdd-4da0-414e-be79-d51b57e51b9e"/>
</p>
<p>
Next click yes to log into DC-1 VM
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/2b3e72ea-0ceb-453a-8012-d66c78df24c8"/>
</p>
<p>
DC-1 VM should load and you will see the name jane doe.
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/e1872b43-6a00-4378-895a-ef730ced9b33"/>
</p>
<p>
Open command line then type whoami and you will see you are logged in as jane_admin 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/991eb684-0118-4420-b7d8-46c8c5b62477"/>
</p>
<p>
Next right click the windows icon on the bottom left then click the system file 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/ca7edc7e-f5a5-4e71-9271-95a201e7bde7"/>
</p>
<p>
Now click Rename this PC (advanced)
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/167d7c20-efb0-4122-b11b-9e0537d4b2b7"/>
</p>
<p>
Next click change 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/09893ccd-1680-437c-87e2-ddcfe9aa58d4"/>
</p>
<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/b149e245-84ee-4bf8-8a37-c8b48eefa62e"/>
</p>
<p>
Next click member of and click the domain circle, then type domain.com then click ok 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/fcdd96ce-0d3b-4e59-919b-9c0fa77da602"/>
</p>
<p>
Now you will see an error displyed on the screen click ok this is because we have to change the NIC in azure for Cilent-1
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/1dc42180-09dc-4ea2-a91e-ee0533ec444a"/>
</p>
<p>
Now go to the Azure portal and go to Virtual Machine then click DC-1, copy the NIC Private IP
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/c56d3f3c-21ea-4519-bbd1-54138e525937"/>
</p>
<p>
Next click Cilent-1 and go to Network Interface and click on cilent 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/d441f8cb-4e31-46e1-b26f-73320b72ed2b"/>
</p>
<p>
Next click DNS servers then click custom 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/940c1feb-2931-4d21-9a39-313d1dd21af7"/>
</p>
<p>
Now paste the NIC Private IP of DC-1 then click save 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/320e0df8-7201-47b9-8416-e845374097ac"/>
</p>
<p>
Next let the process change the NIC
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/cb2f13af-e7ea-4643-8356-9e5ebd18eeb3"/>
</p>
<p>
Once its done you will see a green check you can click the bell icon to see the prcess load 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/48480f92-8917-4975-9a22-81918bac31cb"/>
</p>
<p>
Next go back to Virtual Machine adn click restart then click yes to restart Cilent-1 VM
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/e6ad8434-0787-4c5b-93f0-51adf131fd56"/>
</p>
<p>
You can click the bell icon and see the process restart the VM
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/60639df1-158c-49cf-9178-85a4b3fef1fd"/>
</p>
<p>
Once its done you will see a green check mark icon 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/afeca4be-57a5-4fb5-afbf-15b572a4495d"/>
</p>
<p>
Next click Cilent-1 then copy the public IP 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/a89632c4-19c5-4687-88c3-b5fde7acd026"/>
</p>
<p>
Type Remote Desktop Connection and load the app 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/e7db9734-b39f-48d6-8ddd-df988a842c36"/>
</p>
<p>
Next paste the Public IP in the computer section and then click connect 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/4658286d-46a4-407a-b067-6ec97cdb16b0"/>
</p>
<p>
Now type labuser for the username and the original password you made for Cilent-1 then click ok 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/4df21922-1a88-49a2-88f6-a6b9c1fd1de4"/>
</p>
<p>
Next press yes to log into the VM
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/32ee1ac3-c0c7-4d4b-8a83-ae2c9e3d3be1"/>
</p>
<p>
Now you will see Cilent-1 VM load under labuser 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/878b7f3d-c799-49c8-9911-15925544646b"/>
</p>
<p>
We are going to do the same process as before right click the windows icon then click on system 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/258597d2-6ac4-41e3-8ef5-b45e44a7ab37"/>
</p>
<p>
Next click Rename this PC (advanced)
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/6d5b289e-811b-4a1e-bfc3-a1cf01118036"/>
</p>
<p>
Now click change 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/b80a520f-fde4-4826-9ebc-c7ab1d78faec"/>
</p>
<p>
Now click domain and type mydomain.com then click ok 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/ebd2a07f-2250-4a7f-a7a8-cefe6c867cca"/>
</p>
<p>
Now Computer Name / Domain Changes should load on your screen 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/b0ef21c9-fb5c-4d48-8b4b-bd6715bc372b"/>
</p>
<p>
Next type mydomain.com\jane_admin then the password is Password1 then click ok 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/9d50d6f6-eb5a-464a-8b81-4f3fa4ae482e"/>
</p>
<p>
You will see the VM is trying to reconnect dont click cancel let the bandwidth conenct back to the VM
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/257c9513-176f-4a61-953d-5117e3c0a1c7"/>
</p>
<p>
Next you will see a Please wait page 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/f0fd0c40-631a-4cc2-abcd-46a6891be72b"/>
</p>
<p>
Close out of everything, but you wil see a tab that says You must restart your computer to apply these changes then click ok 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/eca341c4-0cd2-4648-afd3-76a1dd18c603"/>
</p>
<p>
Then click Restart Now to restart the VM
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/79dac041-0092-49d6-b7ac-6d65e855b887"/>
</p>
<p>
Next you will see a Restarting Screen load 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/f014446b-69f3-4b2a-8e94-29566fd6b64a"/>
</p>
<p>
It will kick you out of Cilent-1 VM now go back to get the Public IP then type Remote Desktop Connection and open the app 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/18513efd-bad4-4501-9805-fbad9aff8315"/>
</p>
<p>
Next paste the public IP in the computer section then click connect 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/979b19d5-09c7-40c9-8a0f-5e8e090fad45"/>
</p>
<p>
Click more choices then click use a different account 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/3e1dce01-7608-47e6-bdf9-e48a73acd8f4"/>
</p>
<p>
Now type mydomain.com\jane_admin then the password is Password1 then click ok 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/bc113c76-8db9-4504-9b7a-dc1e3918b5ae"/>
</p>
<p>
Next click yes to connect to the VM
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/85e0f5b0-72b5-49c4-9eaf-489d53e09d45"/>
</p>
<p>
Now you will see the Cilent-1 VM loading as jane doe 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/88f0493d-c56e-4fd2-b13a-6a12170c3e64"/>
</p>
<p>
Next right click the windows icon then click system 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/6407b46d-9953-456f-ad88-cb61bb9bf7f2"/>
</p>
<p>
Next click Remote Desktop 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/83179131-dce0-42b4-aa5f-ab239c64e11a"/>
</p>
<p>
Now click Select users that can remotely access this PC
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/756760a0-9da9-4b38-bb5b-442fa24ff787"/>
</p>
<p>
Next click add 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/80910d23-635e-4f77-8bf5-9217a6db30b9"/>
</p>
<p>
Type domain users then click check names 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/1fd5e59e-34b0-4fc2-bb12-a76c9338ef3d"/>
</p>
<p>
You will see the name changed to CAPS with a underscore then click ok 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/50bd24fb-9321-4000-8890-afe5ae5962f9"/>
</p>
<p>
Next click ok 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/9daedf6e-ae64-4cd5-bf3d-95d27e2e0f4e"/>
</p>
<p>
Go back to DC-1, another way to get to Users and Computers is to click the windows icon on the bottom left. Next click Windows Administrative Tools then click Active Directory Users and Computers
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/8d0091c5-b02b-48c1-94fb-8df23a4f8f01"/>
</p>
<p>
Next click users then click Domain Users
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/4fc4f2f5-d1d6-43b5-b4fb-982249ecdb8e"/>
</p>
<p>
Now you will see jane doe and labuser are under the Domain Users
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/f00e2f1b-0b58-4ff2-a436-d7a84178cab3"/>
</p>
<p>
Next type Windows Powershell ISE right click and run as administrator
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/52731396-42b2-4752-80a3-65fa335d9b64"/>
</p>
<p>
Now click yes to run the software 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/4e1022f8-6bd3-44d2-9b44-eee5d0883904"/>
</p>
<p>
Click file then click new 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/d3281cb9-e79d-4f93-8a18-7bdb24f3fbf2"/>
</p>
<p>
Go to the Link and copy the code this code will create 2000 users https://github.com/Jacobvillagomez1/Generate-Names-Create-Users.ps1/blob/main/README.md
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/3206dc71-8055-419f-b903-e807c7b92ca8"/>
</p>
<p>
Now paste the code in the white blank page section 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/526b4bd7-d087-4be2-ba06-e5e000c79cb1"/>
</p>
<p>
Now click the green play icon to run the script 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/0899eab8-7d9a-4c5c-b4e2-700f827fa5db"/>
</p>
<p>
Now in the blue section you will see the 2000 users being created in a ligth blue color 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/850e7ff4-196d-4a84-b359-a3565bbf9651"/>
</p>
<p>
Next click on the _EMPLOYEES folder then right click and click refresh 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/3d794795-61d7-4b97-b2c7-8a6ff1283ccb"/>
</p>
<p>
Now you will see the current users that have been created 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/937a3c25-6aee-4bf4-bc18-0100f4f2442a"/>
</p>
<p>
Next go to Cilent-1 open up the command line then type logoff, then press enter 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/d62f1456-4352-4ce0-9d78-a574356f218d"/>
</p>
<p>
Now that we logged out of Cilent-1 we are going to go to DC-1 VM and pick a user then copy the display name. 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/92106042-1475-4cb6-aafb-34b80df93203"/>
</p>
<p>
Open up your notepad and paste or type the display name of the account you want to log into  
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/db198ef9-536f-4a39-b9a2-5baf68143dc4"/>
</p>
<p>
Now type Remote Desktop Connection and open the app
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/0b5b7ff7-afce-42a4-8058-4fe3aff29ba8"/>
</p>
<p>
Next paste the public IP of Cilent-1 VM then click connect
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/075247fe-f3ea-49b9-8109-64249c551e44"/>
</p>
<p>
Next click more choices and click use a different account 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/809a2320-5074-46da-a0e6-7ce3e6984b1e"/>
</p>
<p>
Now type mydomain.com\ then your username. Next for the password type Password1 refer to the image above then press ok
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/d681a6c7-f783-42d1-be11-baaa5ede25a0"/>
</p>
<p>
Next press yes to connect to the VM
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/38251e25-e471-464f-a9d2-c7f7e1858c3a"/>
</p>
<p>
Now you will see the username display on the screen of the loading screen of Cilent-1 VM
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/43d5f06e-cac1-436e-bfe0-d93f94b641fd"/>
</p>
<p>
Open commandline and type whoami and you will see we are logged in as the user you picked. Type hostname and you will see you are still under Cilent-1 then type logoff 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/f83f4694-e231-473f-9e34-8741b13b0a2e"/>
</p>
<p>
Go back to DC-1 VM and pick another user, then copy the display name 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/a0857ddd-8fcd-4bad-8a24-a712a754db5d"/>
</p>
<p>
Type Remote Desktop Connection and load the app 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/4d1f40ee-b93e-4741-83a1-68fceac33c77"/>
</p>
<p>
Next paste the Public IP of Cilent-1 then click connect 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/66242ef0-4145-454b-a85e-cc5a253ee98c"/>
</p>
<p>
Click more choices then click use a different account 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/164e4d51-a623-48ee-8983-8a480d4e0829"/>
</p>
<p>
Now type mydomain.com\ then the username, but for the password type the password incorrectly ten times to lock you out of your account refer to the image above 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/63f27065-9e25-42fb-969b-57824e9cff63"/>
</p>
<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/686606a1-4259-41a9-a12d-843ef254a1d1"/>
</p>
<p>
Next go back to DC-1 VM and go to the account tab of the user you picked. Click th box Unlock account then click ok 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/8a06ac57-d4bc-4478-8ce2-ee345b4e45e1"/>
</p>
<p>
You can also right click the user you picked and click reset password, or even disable the account 
</p>
<br />

<p>
<img src="https://github.com/Jacobvillagomez1/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/143027686/39a34abc-ab16-4bb4-a6d7-f668f6662af6"/>
</p>
<p>
Now to see Lab 6 https://github.com/Jacobvillagomez1/Create-Inspect-and-Delete-DNS-A-Records-and-CNAME and Lab 7 https://github.com/Jacobvillagomez1/Network-File-Shares-and-Permissions 
</p>
<br />
