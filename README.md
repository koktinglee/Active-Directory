![image](https://github.com/user-attachments/assets/ad20a776-c332-406b-9074-653fc6a59a9d)![image](https://github.com/user-attachments/assets/f07f9140-c171-41b3-ba00-319d96dd98e3)<p align="center">
<img src="https://i.imgur.com/pU5A58S.png)" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Set up Active Directory home lab with VMware Workstation</h1>
For the Active Directory (AD) Lab we are going to configure three VMs. The first VM will be the Domain Controller (DC) of the environment. We will use Windows Server 2022 for this machine. The other two VMs will be the clients that use this environment. For the client VMs, we will use Windows 10 Enterprise.

Microsoft provided Evaluation copies for both of them. Windows Server 2019 has a license of 180 days while Windows 10 Enterprise has a license of 90 days. They should function just fine even after the evaluation period expires. After setting up the lab we will create snapshots for the VMs. The snapshots can also be used to roll back to the start of the evaluation period once it expires.

<h2>Environments and Technologies Used</h2>
<img src="https://github.com/koktinglee/Active-Directory/blob/main/activedirectory.png" alt="Microsoft Active Directory Logo"/>

- VMware Workstation Pro
- Windows 2022 Server
- Windows 10 Enterprise
- WIndows 10 Enterprise

<h2>Download Windows Server 2022 ISO file</h2>
You can search on the Internet and click download 



<h2>Creating the VM</h2>

-Open VMware Workstation Pro

-Choose for Create a New Virtual Machine

![image](https://github.com/user-attachments/assets/958d7c9c-cbd2-4373-9640-93845e69a3df)

-browse for the Windows Server ISO file

![image](https://github.com/user-attachments/assets/13e864fb-7d3a-480e-8968-fda466ccdce7)

-All the way next until you see this page

![image](https://github.com/user-attachments/assets/3d3ff36e-6b99-40fc-bb30-5061585c20d1)

-You can see the VM in the Workstation. Edit the virtual machine and remove the floppy drive (floppy drive will effect the VM OS boot up

![image](https://github.com/user-attachments/assets/23dd7f5e-a103-44af-b9f0-abb5838203ae)

<h2>OS Installation</h2>
-Click power on this virtual machine

-click next

![image](https://github.com/user-attachments/assets/c6923435-25b6-419f-b1c1-451ccab7a99f)

-click install

![image](https://github.com/user-attachments/assets/dfdf3fc7-5523-431e-8919-d0e5c5fc3370)

-Select Windows Server 2019 Standalone Evaluation (Desktop Experience) and click on Next.

![image](https://github.com/user-attachments/assets/65d970b1-ac76-4424-98ac-0ee0ad5b1a4a)

-Accept the agreement and click on Next.

![image](https://github.com/user-attachments/assets/ff6c1252-5cfe-416a-be77-bb8c2851f864)

-Select Custom: Install Windows only (Advanced).

![image](https://github.com/user-attachments/assets/3389e16d-691c-4996-8249-a4df4a36f29a)

-Select Disk 0 and click on Next.

![image](https://github.com/user-attachments/assets/3f34bcf3-f43b-4a75-91c0-e360a1c3cf8a)

-The VM will restart a couple of times during the installation process.

![image](https://github.com/user-attachments/assets/70d29ea9-5a43-421b-92b0-d3d4a561d79c)

<h2>OS Setup & Configuration</h2>

-Once the installation is complete we will be asked to set the password for the Administrator account. Once set click on Finish. ID: Administrator, PS:Admin123#

![image](https://github.com/user-attachments/assets/e1c03524-632f-4efc-bc42-098fc4198cb4)

-Use the shortcut Right Ctrl+Delete to access the login screen. Enter the configured password to access the VM.

![image](https://github.com/user-attachments/assets/39705f35-c251-44ce-bc4f-8575237fa1bb)

-Once we log in. Server Manager will automatically open. A popup will also open asking us to try Windows Admin Center. Click on Don't show this message again and then click on X to close the popup.

![image](https://github.com/user-attachments/assets/c24bf794-9c8e-45e8-a992-2d781a766620)

<h2>Network Configuration</h2>

-From the taskbar right-click on the network icon and select Open Network & Internet settings.
![image](https://github.com/user-attachments/assets/849afbbc-d3e9-442f-907e-223948deb257)

-Click on “Change adapter options”.
![image](https://github.com/user-attachments/assets/31228db5-26b9-4975-ac63-ce58e2bce4ee)

-On the Network Connections page, we should see the Ethernet adapter. Right-click on the adapter and select Properties.
![image](https://github.com/user-attachments/assets/2edbb55e-9419-432d-ab59-d1c99552961f)

-Select Internet Protocol Version 4 (TCP/IPv4) and click on Properties.
![image](https://github.com/user-attachments/assets/69e6e899-57a0-4b76-a3c7-ed72387e76f4)

-Enter the details as shown below and then click on OK. Click on OK again to close the Ethernet Properties menu.

IP address: 192.168.40.131
Subnet mask: 255.255.255.0
Default gateway: 192.168.40.2
Preferred DNS Server: 192.168.40.131

![image](https://github.com/user-attachments/assets/36abb0aa-c560-4712-b6cb-8ae7a3c4c520)

-In the Settings app click on the Home button (above search bar).
-Before we can set up the machine to be a Domain Controller let us rename the PC. Select “System”.

![image](https://github.com/user-attachments/assets/49206363-a96d-4b36-8f1e-e17138724c50)

-Click on About on the sidebar and then click on the “Rename this PC” button. Give the PC an easy-to-remember name and then click on Next.

![image](https://github.com/user-attachments/assets/2b48cc70-6935-4919-8bf6-c8c7bd37c564)

Click on “Restart now” for the changes to take effect.

![image](https://github.com/user-attachments/assets/b8a1ab1f-744c-4b6a-ae8d-e5622d29164e)

-Once installation done, you can check the updated hostname in cmd. Open cmd in searh bar and type "hostname"

![image](https://github.com/user-attachments/assets/dd766295-6dee-4ac9-b882-0c3162e9bb99)

<h2>Active Directory & DNS Installation</h2>
-After login wait for Server Manager to load. Click on the Manage button from the top right corner and select “Add Roles and Features”.

![image](https://github.com/user-attachments/assets/491392a7-fc03-4322-90fe-cecd9a2cad17)

-Click on Next till you reach the Server Roles page.
![image](https://github.com/user-attachments/assets/8d3f1946-cec0-439d-9b74-3b3dbec94824)

On this page enable “Active Directory Domain Services” and “DNS Server”.
![image](https://github.com/user-attachments/assets/0ebee882-27cc-4dfb-809e-28cb0549e946)

When you enable a feature the “Add Roles and Features Wizard” will open click on “Add Features” to confirm the selection.
![image](https://github.com/user-attachments/assets/bdc01663-8e92-438e-ab15-50241ed267c7)

![image](https://github.com/user-attachments/assets/b211e35c-65b2-426a-8301-a8e98d94dd7a)

Once both the features are selected click on Next to proceed with installation.
![image](https://github.com/user-attachments/assets/61e3c852-03b3-4087-b0a7-c7e5b255f478)

Click Next till you reach the Confirmation page. Here click on Install to start the installation of the selected features.
![image](https://github.com/user-attachments/assets/a0490935-fec1-4cd7-b381-7ac3aa36f0b6)

![image](https://github.com/user-attachments/assets/f2d5dac9-c381-4483-baeb-6b1235bd2d9d)
Once the installation is complete click on Close to exit the Wizard.

<h2>Active Directory configuration</h2>
Click on the Flag icon present in the top right of the toolbar in Server Manager. From the dropdown click on “Promote this server to a domain controller”.
![image](https://github.com/user-attachments/assets/eead07fb-355f-4b0c-b3af-6769c8a127cf)

The AD Domain Servers Configuration Wizard will open. For deployment operation select Add a new Forest. Give the domain a name. For my setup, I will be using the domain name ad.lab. After selecting the name click on Next.
![image](https://github.com/user-attachments/assets/bb9c4727-e7cf-4ab0-b229-5244cfc299cd)

On this page enter a password to use for using the AD Restore feature.
![image](https://github.com/user-attachments/assets/966d8831-289e-4b25-ad60-f500f0fb2f67)

Ignore the warning that is shown and click on Next.
![image](https://github.com/user-attachments/assets/d2360912-6ac8-42d4-b9f3-7a63194a50a7)

The NetBIOS name should automatically be filled. It will be the first part of the domain name. Click on Next to continue.
![image](https://github.com/user-attachments/assets/8bba87d5-6e29-4ead-962d-60e91e44a011)

Click on Next.
![image](https://github.com/user-attachments/assets/bafb2095-24df-4576-867d-dc0cb155dab7)

Click on Next.
![image](https://github.com/user-attachments/assets/48c5de15-1567-450b-b7f4-68ed09068077)

Click on Install to start the Domain Services setup process.
![image](https://github.com/user-attachments/assets/cb23409b-2473-4a7f-b7cc-d1bf1babdeea)

Once the install process is complete the machine will need to restart. Click on Close to reboot the system.
![image](https://github.com/user-attachments/assets/6730203a-15ae-48c2-87dc-2c80d69c49b8)

Once restart, you will notice that the name that is shown on the login page has changed. The first part of the domain name is prepended to the username. This means the machine has successfully been configured as the domain controller. Log in using the Administrator password.
![image](https://github.com/user-attachments/assets/6fe9ae9e-678a-47f9-88d6-3b6691643fa8)

<h3>DNS Configuration</h3>
Since we enabled DNS on this machine (Domain Controller). This machine (DC) will act as the DNS server for devices that are connected to the ad.lab environment. For the DNS service to function properly we need to configure a Forwarder. Forwarder is the device to which the DNS queries will be sent when the DC cannot resolve it. In our case, we need to forward the request to pfSense. The DNS service of pfSense will then perform the lookup.

Open the Start menu expand the “Windows Administrative Tools” folder and select DNS.
![image](https://github.com/user-attachments/assets/ba88f5e8-d6bf-405e-bec7-c487e5723d5b)

In the sidebar select the Domain Controller (in my case DC1) and from the right menu double-click on “Forwarders”.
![image](https://github.com/user-attachments/assets/15fdb829-c69d-4ca0-86c3-a32c72f246dc)

Go to Forwarders -> Edit

![image](https://github.com/user-attachments/assets/0643cbcd-e6e8-41fc-b0b1-0bfca23c9daf)

This will open the Forwarder configuration page. Enter the IP address of the AD_LAB interface (10.80.80.1) and press Enter.

![image](https://github.com/user-attachments/assets/8a46e860-4bf0-4345-ac7a-fc2031ed3a18)

Once added. Click on OK to confirm the change.

![image](https://github.com/user-attachments/assets/e8301e37-1c43-47c1-8122-e217b8c31b5e)

Click on Apply then OK to save the changes.

![image](https://github.com/user-attachments/assets/0eea9b81-dc27-4d25-9ed6-936a953004d6)

<h3>DHCP Installation</h3>

Since DHCP is disabled on the AD_LAB interface when new devices are added they will not be assigned an IP address. We will enable the DHCP service on the DC. Once set devices that connect to the AD_LAB network will be automatically assigned an IP address by the Domain Controller DHCP server.

Click on Manage from the toolbar in Server Manager. Then choose “Add Roles and Features”.

![image](https://github.com/user-attachments/assets/a15d503f-2929-48a6-a699-45ee6a8ab946)

Keep clicking Next till you reach the “Server Roles” page. Enable “DHCP Server” then click on “Add Features”.

![image](https://github.com/user-attachments/assets/3f9497ff-c02f-432f-96c4-cc431dcbea41)

![image](https://github.com/user-attachments/assets/b55587f0-ba46-40db-ad50-57a8cd360344)

Keep clicking Next till you reach the Confirmation page. Click Install to enable DHCP.

![image](https://github.com/user-attachments/assets/b4f06598-47e5-4a46-97ec-5fe521ec47bb)

After the installation is complete click on the Flag present in the toolbar of Server Manager and click on “Complete DHCP configuration”.

![image](https://github.com/user-attachments/assets/3d6ea7ab-6a10-4bb5-a9da-549a68435c35)

Click on Commit.

![image](https://github.com/user-attachments/assets/8747b1e9-e9b6-4c39-a32a-2214b7e8ce8e)

Click on Close to complete the installation.

![image](https://github.com/user-attachments/assets/f23fe1c0-9188-4970-b029-c751e9710b21)

From the Start menu click on “Windows Administrative Tools” and then choose DHCP.

![image](https://github.com/user-attachments/assets/ce0d377e-dfd1-43df-9893-b81637fdea07)

Expand the DHCP server (in my case dc1.ad.lab) dropdown on the left side of the window.

![image](https://github.com/user-attachments/assets/1b49ef25-b8fa-42d2-9451-5fd4baeeff43)

Right-click on IPv4. Then select “New Scope”. The scope defines the range of IP addresses that can be assigned to devices by the DHCP server.

![image](https://github.com/user-attachments/assets/3fffc986-9432-4af3-88db-af011c679725)

Enter a Name and Description for the new scope.

![image](https://github.com/user-attachments/assets/6fc61c2b-5aab-4e6d-a912-381e36311906)

![image](https://github.com/user-attachments/assets/167dde19-8210-4023-8e36-1604bbc2420e)

You can chose the Start IP address to be 10.80.80.3. I have purposely left the starting IP addresses out of the DHCP scope. In the future if the need arises I can use these IPs for static IP assignment.

We don’t have any Exclusions (static IP assignment). Leave all the options empty and click on Next.

![image](https://github.com/user-attachments/assets/cde2649d-36fe-4c55-8648-96bfe9d5a8db)

Increase the lease time to 365 days and click on Next.

![image](https://github.com/user-attachments/assets/cf2414cc-bfc6-47d5-9939-169a96fd6755)

Select “Yes, I want to configure these options now” and click on Next.

![image](https://github.com/user-attachments/assets/d66ac755-ad37-42ac-90ec-f2a85def6923)

In the IP address field enter the default gateway for the AD_LAB interface (10.80.80.1) and then click on Add. Once added click on Next.

![image](https://github.com/user-attachments/assets/5c3c6855-5056-4752-8c8c-f6f3febfd0ee)

Click on Next.

![image](https://github.com/user-attachments/assets/a629ae84-6898-442e-ad4c-a166feecb183)

We are not configuring a WINS Server for our environment so click on Next.

![image](https://github.com/user-attachments/assets/a567e5e9-dd86-4a36-9296-a8c4cbd0ab7e)

Select “Yes, I want to activate this scope now” and click on Next.

![image](https://github.com/user-attachments/assets/6b518c74-b175-4c4d-9970-295273c6f9ab)

So far we have installed Windows Server 2019, installed Guest Additions, configured the VM to be the Domain Controller (DC), set up a DNS Forwarder and configured DHCP. We still need to create users in the DC and set up client machines to use the AD environment.

