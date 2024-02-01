# Active-Directory
![first ](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/d0e4fdd8-2952-47d4-af28-1d5db9d0232a)
## Active Directory - Home Lab
Hello everyone, before we delve into this lab, we need to understand what Active Directory is.<br>

Active Directory is like a master organizer created by Microsoft for computer networks. It serves as a central hub that keeps track of crucial information in a network, such as who is using it, available resources, and how to maintain overall security. Think of it as a giant digital filing cabinet that stores details about users (individuals utilizing the network), groups (clusters of users with similar access), and the rules ensuring everything stays secure.<br>

In simpler terms, it's the system boss that helps manage who can do what on a network, ensuring everything remains organized, secure, and user-friendly.<br>

Now that we have an understanding of Active Directory, let's proceed to the next steps. These are the main tasks we'll tackle in the lab: <br>
- Active Directory & VM Installation <br>
- Remote Access Server (RAS) & Network Services <br>
- Dynamic Host Configuration Protocol (DHCP) <br>
- User Account Management via PowerShell <br>
- Understanding Active Directory’s Core <br>
- Create a Windows 10 Enterprise VM, Rename, and Join the Domain <br>
- Verify Login Credentials <br>
- the lab was made by [Josh Madakor](https://www.linkedin.com/in/joshmadakor/) the click on the [Video](https://www.youtube.com/watch?v=MHsI8hJmggI&ab_channel=JoshMadakor) for detail response. <br>

![123](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/dd33b6bd-329d-4581-b3e5-08fb9b879707)

In line with the diagram provided, we're setting up a Domain Controller with two network adapters. The first one links to the internet through the host computer, grabbing an IP dynamically or using a set static IP. The second adapter sticks to a static IP and is exclusively for our internal network. This internal setup paves the way for Network Address Translation (NAT) on the Domain Controller, letting client computers hop onto the internet using a specific range of IPs. For the clients, we're keeping it straightforward with a single Network Interface Card (NIC) that solely connects to the internal network—no mingling with the host computer's NIC. This setup ensures the Domain Controller acts like a secure gateway, allowing clients to reach the internet via NAT while keeping our internal network in its own bubble.<br>

## First we need to Download [Virtual Box](https://www.virtualbox.org/wiki/Downloads) 
 ![1](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/70e7e572-4088-4ba9-aa65-deabdbccfa5c)

## Next we need to download [windows server 2019](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019) 

![2](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/152e326e-9be7-4503-8d74-4357804d6550)

## And last we have to download [windows 10](https://www.microsoft.com/en-us/software-download/windows10ISO)
![3](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/f929b69e-6f5d-4b10-8e53-4bb24fdacbb8)

##  Now we need to add server 2019 to the virtual machine 
![4](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/954102c0-1a0b-44cd-974f-a8bca1f4ea9d)

- After configuring all components, it's time to designate the system as the Domain Controller (DC). Let's navigate to the settings and make adjustments. Enable two network adapters: one for internet connectivity and the other for the internal network to establish a connection with the Windows 10 virtual machine.<br>
- For the external-facing NIC, ensure it acquires its IP address from your home router. This establishes the connection to the broader internet. Meanwhile, the internal NIC requires a specific setup to connect with the Windows 10 virtual machine within the internal network.<br>
- By configuring these network settings, you create a dual-network environment, allowing your Domain Controller to efficiently manage both internet connectivity and internal network communication with the Windows 10 VM.<br>

![5](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/61ba058f-f4b1-41a8-b7b8-5d3516e2356b)

- Now, open the "Network & Internet" settings, navigate to "Ethernet," and click on "Change adapter settings." In this section, you will find your two network interface cards (NICs). <br>
- One of these NICs is designated for the internet connection, while the other is for the internal network. Identify and review these adapters to ensure they correspond to the intended configurations. This step allows you to verify that both network adapters are recognized by the system and are ready for further configuration. <br>
- Remember, the external-facing NIC should be associated with your home router to access the internet, while the internal NIC is set up for communication within the internal network, particularly with the Windows 10 virtual machine. <br>

![6](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/bc183ad0-1968-491b-b3e2-27567b266523)

let's proceed with identifying and labeling the network adapters:
- __Identify the Main Network (External-Facing NIC):__ Check the IP address associated with this network adapter. It should be obtained dynamically from your home router.Rename this network connection to "Internet" to clearly indicate its role as the connection to the external network. <br>
- __Identify the Internal Network (Internal-Facing NIC):__ Confirm that this network adapter is set up with a static IP address for the internal network.Rename this network connection to "Intranet" to signify its function as the internal communication channel within your network. <br>

By labeling the network adapters as "Internet" and "Intranet," you're providing a clear and intuitive representation of their respective roles in connecting to the broader internet and facilitating internal network communication.<br>

![7](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/2f6c1dde-28f9-4131-a2b6-a9c8b46ce500)

Once that is complete, the next step is to add Active Directory Domain Services as a feature to the server through the Server Manager. <br>
1. Open Server Manager. <br>
2. Navigate to "Add Roles and Features." <br>
3. Proceed with the on-screen instructions by selecting "Next" and "Next" again. <br>
__Server Selection:__
4. Choose your server for the installation. <br>
5. Select "Active Directory Domain Services" as the Role. <br>
6. Continue with "Next," "Next," and "Next." <br>
__Finally:__
7. Click on "Install" to initiate the installation process. <br>
By following these steps, you'll seamlessly integrate Active Directory Domain Services into the server configuration. <br>

![8](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/e1a38ee1-b808-4d40-9df2-0cd07f1a0fed)

continue the setup by selecting "Add a new forest" and follow these steps: <br>
- In the wizard, choose "Add a new forest." <br>
- Specify a generic root domain name; for instance, use "mydomain.com." <br>
- Proceed to the next step by clicking "Next." <br>
- This configuration will set up a new forest with the specified root domain name. Following these instructions will help establish the foundation for your Active Directory environment. <br>



















