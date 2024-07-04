<h1>Azure Project - Creating and deploying a virtual machine on a web server </h1>

<h2>Description</h2>
This is an entry-level/beginner project to introduce familiarity with Azure, starting with deploying a VM and web server on Azure. I'll be creating a resource group, virtual network/subnet, employing Bastion and more. 

<img src="https://imgur.com/D77oxIh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<h2>Lab walk-through/details:</h2>

<p align="center">

<b> Getting Started - Creating the Resource Group (RG):

- <b> Establish Azure Account (Use Free Tier and within its limits to avoid being billed)
- <b> On dashboard, Create new -> Search Resource Group -> Create a Resource Group
- <b> Use your subscription, set the resource group as RG-USE-Nextcloud (for the server)
- <b> Leave region as US East (just where metadata resources will be stored)
- <b> Review and create and make sure validation passes; if so, Create. If not, review details and adjust as necessary.
- <b> Notification should appear on your dashboard after; head over there and review your Resource Group creation.

<img src="https://imgur.com/a350C1v.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<b> Creating a Virtual Network inside the Resource Group:

- <b> A virtual network is a logical, segregated isolated network that enables different resources to securely communicate and interact with one another as if it were doing so physically connected. It also acts a filter between internal resources and the internet.
- <b> In the resource group itself, click create, search virtual network and create virtual network

<img src="https://imgur.com/on7L7En.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- <b> Everything should be pre-selected unless you have other resources previously created. If so, select the proper one that matches the lab.
- <b> Name the Instance Detail as "VNET-USE-Nextcloud" (The VM has to be in the same region as the virtual network or it won't work.)
- <b> Click next, and click the IP addresses tab. Delete the address space and create your own below using the following:

<img src="https://imgur.com/NtBXy9B.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- <b> Afterwards, hit Review and Create and check to make sure everything passes/looks good.

<img src="https://imgur.com/xO0L8U9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- <b> The virtual network will be deployed and will take a moment.
- <b> After it is done, go back to the Resource Group. Refresh the browser when you get there to see it update.
- <b> The virtual network should populate under the Resource Group.

<img src="https://imgur.com/dE9JMqU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- <b> Take a moment to check the Address range and subnet information (left hand side of the dashboard, under settings, with "Address space" and "Subnets"
- <b> Head to Monitoring, expand it and click on Diagram. You'll be able to see a topology of everything so far.

<b> Creating a Network Security Group (NSG) to protect a subnet:

- <b> An NSG acts a logical filter for traffic to and from Azure resources on the virtual network. It can be set as an allow or deny inbound/outbound traffic to and from different Azure resources, and also the Internet on the outside.
- <b> Go back to your RG, click Create, and search "Network Security Group." Click Create for the NSG.
- <b> The RG should be assigned, just like when setting up the virtual network. Name the resource for the NSG as NSG-USE-Nextcloud.
- <b> Click on Review and Create and check/verify the settings are good.

<img src="https://imgur.com/6kSDlKC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>  

- <b> Go to the NSG.
- <b> You'll see that Azure Bastion has been created by default, with inbound and outbound rules set. Within Azure, data/network traffic can go in and out by default. Nothing can come in from outside of the virtual network, however, hence acting as virtual firewall, unless modifications were to be made.

<img src="https://imgur.com/b8G7MZd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>  

- <b> Next, we will needto assign the similar rules to the our subnets.
- <b> Head back to the RG. You will see the NSG is now there under your RG.
- <b> Head to your VNET, click subnets, and click on the subnet previously created earlier.
- <b> Scroll down and find Security, and look for Network Security Group. From the dropdown, assign the NSG you created.

<img src="https://imgur.com/b8G7MZd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 

<b> Deploy a Bastion instance to connect to the VM:

- <b> Go back to Subnets while on VNET
- <b> Click add +Subnet to add a new one
- <b> Enter the settings as shown below:

<img src="https://imgur.com/zjkas38.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- <b> After adding it, you'll see Bastion as part of the resource group.
- <b> Head back to RG and search for Bastion.
- <b> Enter in the following items and review before creating:

<img src="https://imgur.com/md7ZVgh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- <b> Bastion group will be created.

<img src="https://imgur.com/md7ZVgh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<b> Create an Ubuntu server VM:

- <b> On your RG, click Create, search Ubuntu Server 18.04 LTS
- <b> Create, and apply the following:
- <b> VM-USE-Nextcloud, leave availability zone to zone 1, and B1 for basic (free at the first 750s and enough for this project).
- <b> SSH Key, make a username, and label the key pair name as VM-USE-Nextcloud_SSHkey (to be clear and distinct).
- <b> Change the inbound ports to None (keeping it away for the internet and working internally for this project).
- <b> Next (Disks) -> Leave 30 GB on premium SSD and others default, then next
- <b> Next (Networking) -> Switch public IP and replace with None.
- <b> REVIEW AND CREATE; double check all selections/parameters first then create.

<img src="https://imgur.com/SuLev8A.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- <b> Download the virtual key. As soon as you do, the VM will begin deploying.

<img src="https://imgur.com/t77FeZQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<b> Install Nextcloud via SSH with Bastion:

- <b> Go to your VM as soon as it's done deploying.
- <b> Find connect and connect via Bastion.
- <b> Enter and connect via the following details (using your username key you downloaded previously)
- <b> Connect

<img src="https://imgur.com/j09BQLD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- <b> You will be on a CLI.
- <b> Enter: sudo snap install nextcloud
- <b> Hit enter and it'll download the appropriate packages.

<img src="https://imgur.com/zpptxYN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- <b> Next we will create a simple admin username and password.
- <b> Enter: sudo nextcloud.manual-install admin your name (password). (Don't do this in a real production environment).
- <b> You'll see your name added to the CLI
- <b> Enter: sudo nextcloud.enable-https self-signed
- <b> After the installs, type exit and enter to leave the cli.

<img src="https://imgur.com/G5Wn1Ha.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<b> Publish an IP address:

- <b> Go to VM-USE-Nextcloud, Network settings, vm-use-nextcloudxxx_xx network interface
- <b> Under settings, click IP configurations. Find ipconfig1 and click on it.
- <b> Check Associate public IP address and create a public IP address, naming it VMIP-USE-Nextcloud
- <b> Save the configuration.
- <b> After it's done, head back to overview for VM-USE-Nextcloud. It should now have a public IP address.

<img src="https://imgur.com/5rcrTNI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- <b> Copy the IP address. Go to your web browser and try to go to the IP address. It should not work and that's due to not having a rule to allow any traffic anything to come inbound.
- <b> Go to www.whatsmyip.com. Copy the IP you have. Head back to Azure.
- <b> VM-USE-Nextcloud, Network, network settings, create port rule, inbound port rule.

<img src="https://imgur.com/a/IClmaPj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- <b> ALLOW, Priority 100, Name: HTTPS_Nextcloud
- <b> Once rule is created, copy that public IP adress again and attempt to go there. It should be responding with a warning.

<img src="https://imgur.com/nOS2km6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- <b> Proceed through by Advanced and you'll be at the nextcloud server.

<img src="https://imgur.com/p6qGUnD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- <b> No entry should be shown. Next is to create a DNS entry to allow access.

<b> Creating DNS label: 

- <b> Go to VMIP-USE-Nextcloud, Settings, Configuration.
- <b> On DNS Label option, give it a name and save afterwards.

<img src="https://imgur.com/JBSvjde.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- <b> Head back to VM-USE-Nextcloud.
- <b> Connect via Bastion
- <b> Enter: sudo nextcloud.occ config:system:set trust_domains 1 --value= your dns label you set.eastus.cloudapp.azure.com then enter the command. Afterwards, type exit and enter to leave the ssh connection.

<img src="https://imgur.com/nj4NDs7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- <b> Go back to your web browswer and type in your full DNS label and try to go it. ie: https://brandonnextcloud.eastus.cloudapp.azure.com/

<img src="https://imgur.com/FluYXz5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- <b> Enter your admin credentials (for simplicity, earlier in the lab, it was admin yourname)

<img src="https://imgur.com/rHjimEN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- <b> In the end, we should have successfully deployed a virtual machine on a web server through Microsoft Azure. It's all experimentation and sandboxing from there.
- <b> Remember to stop and/or delete your VM instance or disconnect Bastion to prevent getting billed.
