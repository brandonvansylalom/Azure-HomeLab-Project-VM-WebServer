<h1>Azure Project - Creating and deploying a virtual machine on a web server </h1>

<h2>Description</h2>
This is an entry-level/beginner project to introduce familiarity with Azure, starting with deploying a VM and web server on Azure. I'll be creating a resource group, virtual network/subnet, employing Bastion and more. 

<img src="https://imgur.com/gwOvDjt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<h2>Lab walk-through/details:</h2>

<p align="center">

<b> Getting Started - Creating the Resource Group:

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

<img src=https://imgur.com/on7L7En.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

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

-<b> 
