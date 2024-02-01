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


![7](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/2f6c1dde-28f9-4131-a2b6-a9c8b46ce500)

let's proceed with identifying and labeling the network adapters:
- __Identify the Main Network (External-Facing NIC):__ Check the IP address associated with this network adapter. It should be obtained dynamically from your home router.Rename this network connection to "Internet" to clearly indicate its role as the connection to the external network. <br>
- __Identify the Internal Network (Internal-Facing NIC):__ Confirm that this network adapter is set up with a static IP address for the internal network.Rename this network connection to "Intranet" to signify its function as the internal communication channel within your network. <br>

By labeling the network adapters as "Internet" and "Intranet," you're providing a clear and intuitive representation of their respective roles in connecting to the broader internet and facilitating internal network communication.<br>

![8](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/e1a38ee1-b808-4d40-9df2-0cd07f1a0fed)

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

![9](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/285d9beb-eb4b-42d3-893e-e7efd0fbe5e9)

continue the setup by selecting "Add a new forest" and follow these steps: <br>
- In the wizard, choose "Add a new forest." <br>
- Specify a generic root domain name; for instance, use "mydomain.com." <br>
- Proceed to the next step by clicking "Next." <br>
- This configuration will set up a new forest with the specified root domain name. Following these instructions will help establish the foundation for your Active Directory environment. <br>

![10](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/c93b911c-0261-43fe-b885-aad6dad9541e)

After a quick restart, I accessed the newly created Active Directory to set up a new Organizational Unit (OU), which we named "_ADMINS." Following the creation of this OU, a new user was added under this specific OU. This step ensures a well-organized structure within Active Directory, making user management more efficient and structured. <br>

![12](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/dd4099cb-bc6c-40e1-a76c-122449708b92)

You will add your user to the admin group. Click on "Admin," then go to "New" and select "User." Enter the desired username and password. After setting up the user account, log out of the current user and attempt to log in with the newly created credentials. <br>
Now that the first Domain Admin user is established, log out and log into the server using this new user account. This user will have administrative privileges within the Active Directory domain.<br>

![13](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/25b2aee7-b06b-4308-aa8d-0aa9ca2d0464)

#### This should be Steve rogers i accidentally took screenshot of this 

The next crucial step is to promote the Active Directory (AD) to a Domain Controller. This action transforms the server into a central hub that all client computers will access to connect to the internet. This promotion establishes a hierarchical and organized structure within the network, ensuring efficient communication and access for all connected devices.<br>
![14](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/ce9bb0ab-e0a6-4e26-ad77-1382689507f4)

## Now to the Second Part of RAS / NAT / DHCP

![15](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/3ef9f94d-c803-4991-b49a-b5ddb2e759f8)

Following that, the next step involves setting up the Remote Access Server (RAS) and Network Address Translator (NAT). This configuration empowers the client computer, once it's configured, to access the internet through the Domain Controller. By implementing RAS and NAT, you establish a seamless connection for client devices to utilize the internet resources while maintaining a secure and centralized network environment through the Domain Controller.

![16](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/8306b7f7-1195-43bc-9fd5-801f381eb51c)

To set up the Remote Access Server (RAS) and Network Address Translator (NAT), follow these steps: <br>
1. Open "Add Roles & Features" and proceed by selecting "Next." <br>
2. In the "Roles" section, check "Remote Access" and continue with "Next." <br>
3. On the "Select Role Services" page, check "Routing," and additional features, such as "Remote Access Service (RAS)," will automatically be selected. Click "Next" to proceed. <br>
4. Follow the prompts until the installation is complete and then close the wizard. <br>
Now, access the tools by going to "Routing and Remote Access": <br>
1. Right-click on the Domain Controller. <br>
2. Choose "Configure and Enable Routing and Remote Access." <br>
3. In the configuration wizard, select NAT (Network Address Translator). <br>
4. If no network interfaces show up, close the window and open it again. <br>
5. Choose the "INTERNET" interface and complete the configuration. <br>
By following these steps, you enable remote access and NAT, allowing client computers to access the internet through the Domain Controller. <br>

![17](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/8d2d34d2-32be-4ba3-ad50-5b044362449a)

To set up the Remote Access Server (RAS) and Network Address Translator (NAT), follow these steps: <br>
1. Navigate to "Add Roles & Features" and proceed to the next steps in the wizard until you reach the "Roles" section. <br>
2. In the "Roles" section, check "Remote Access" and proceed to the next steps in the wizard. <br>
3. On the "Select Role Services" page, check "Routing," and additional features such as "Remote Access Service (RAS)" will be automatically selected. Click "Next" to proceed. <br>
4. Follow the prompts until the installation is complete, and then close the wizard. <br>
Now, go to "Tools" and select "Routing and Remote Access." <br>
1. Right-click on the Domain Controller. <br>
2. Choose "Configure and Enable Routing and Remote Access." <br>
3. In the configuration wizard, select NAT (Network Address Translator). <br>
4. If no network interfaces show up, close the window and open it again. <br>
5. Select the "INTERNET" interface and complete the configuration. <br>
By following these steps, you enable remote access and NAT, allowing the client computer, once set up, to access the internet through the Domain Controller. <br>

![18](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/c5ed141a-f522-42ec-8e53-501da0bf8c1b)

Now, proceed to configure DHCP (Dynamic Host Configuration Protocol) by following these steps: <br>
1. Click on "dc.mydomain" and check "IPv4." <br>
2. In the DHCP management console, create an IP address scope for the users. <br>
3. Set the DHCP IP address scope to 172.16.0.100-200. This range will allow for the assignment of new IP addresses to devices within your network. <br>
By establishing this DHCP IP address scope, you ensure that devices connecting to your network will be dynamically assigned IP addresses within the specified range, facilitating efficient and automated network configuration. <br>

![19](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/071be4af-89e9-4e9c-8458-73f183a655c4)

![20](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/aafd4c75-e5bc-4e95-8412-a67f56d3d007)

Now, disable the Enhanced Security Configuration and download the PowerShell script for creating 1000 users from the GitHub repository. <br>
1. __Disable Enhanced Security Configuration:__ <br>
 - Depending on your browser, go to the settings or options. <br>
 - Find and disable Enhanced Security Configuration. <br>
 - Save changes and restart the browser. <br>
2. __Download PowerShell Script:__ <br>
 - Visit the GitHub repository containing the PowerShell script. <br>
 - Click on the provided link, and the script will automatically download. <br>
3. __Extract Files:__ <br>
 - Once downloaded, extract the contents of the file. You should now have two files: a PowerShell script for creating users and a "names.txt" file containing a list of names.
4. __Modify Names.txt:__ <br>
 - Open the "names.txt" file. <br>
 - Add your first name to the list, ensuring it's in a format compatible with the script. <br>
Now, you're ready to execute the PowerShell script, creating users in your Active Directory based on the names in the modified "names.txt" file. <br>

![21](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/d3f12dfc-9664-472c-a65f-e12993c403a4)

Now, open PowerShell as an administrator and execute the script: <br>
- Right-click on the PowerShell icon. <br>
- Select "Run as Administrator" to open PowerShell with elevated privileges. <br>
- Once PowerShell is open, navigate to the directory where you saved the PowerShell script. Execute the script by typing its name and pressing Enter. <br>
![23](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/77797e82-ba28-4e14-9c79-8a3efb999f74)

 now we have to run the script but we have to make sure the names.txt file is in the same place as the code so now <br>
- Use the cd command to change the directory to where the script is located. Replace "C:\Path\To\Your\Script\Directory" with the actual path where your script is located <br>

![24](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/5cdfebc6-f622-4f95-a343-ec8faaf4814f)

Voila! Running the script successfully creates the 1000 users in your Active Directory. The PowerShell script has processed the information from the "names.txt" file, and the users are now set up and ready for use 

![25](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/30e30e63-1d52-418d-87cd-71292dbc2914)

Now to Check the users <br>
- __Open Server Manager:__ Launch Server Manager on your Windows Server. <br>
- __Access Local Server Information:__ In Server Manager, look for the "Local Server" tab on the left side. <br>
- __Check Active Directory Users:__ Within the "Local Server" information, there should be a section related to Active Directory. Click on the task link that typically says "Tools" or "Manage." <br>
- __Open Active Directory Users and Computers:__ In the "Tools" or "Manage" section, look for "Active Directory Users and Computers" and open it. <br>
- __Verify User Creation:__ Navigate to the Organizational Unit (OU) where you created the users, such as "_ADMINS."Check if the users have been successfully created. You should see the 1000 users listed in this OU. <br>

By going through these steps, you can confirm that the script has effectively created the users within your Active Directory. If you encounter any issues or have further questions, feel free to ask! <br>


![26](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/ce7cfb85-fbfd-4373-aa99-68d6e07c4984)

### Now we need to change to Windows 10
- __Open Windows 10 VM:__ Launch your Windows 10 Enterprise VM in Oracle VirtualBox. <br>
- __Join the Domain:__ Navigate to "System" settings on the Windows 10 VM.Join the Windows 10 VM to the domain you set up earlier. Use the domain credentials to complete the joining process. <br>
- __Log in with New User:__ After joining the domain, log out or restart the Windows 10 VM.Log back in using the credentials of one of the newly created users. <br>
- __Verify User Access:__ Check if the user can successfully log in and access the resources within the domain. <br>

![27](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/4879cb43-b720-4285-8d43-7f2ed5503b6a)

__Now to change the Computer Name:__
- __Change the Computer Name:__ On the Windows 10 VM, right-click on the "This PC" icon on the desktop or in File Explorer. Select "Properties" to open the System properties. Click on the "Change settings" link next to the computer name. Click the "Change" button, enter the new computer name "CLIENT," and click "OK." <br>
- __Restart the VM:__ You may be prompted to restart the VM. If not, go ahead and restart it manually. <br>
- __Join the Domain Again (if needed):__ After restarting, you might need to join the domain again with the updated computer name. Follow the steps mentioned earlier for joining the domain.  <br>
- __Log in with New User:__ Log in to the "CLIENT" VM using the credentials of one of the newly created users.  <br>

![28](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/1cd045b2-1bc8-48b0-86ec-77cee2508e90)

#### click on you don't have product key and proceed with the next steps.

![29](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/8914b4fb-73a4-47a5-a127-aa743b130fd8)

- __Check Network Configuration on Windows 10 CLIENT VM:__ Open a Command Prompt on the CLIENT VM.Type the following command and press Enter:cmdCopy codeipconfigThis will display the network configuration details, including IP address, subnet mask, and default gateway. <br>
- __Change DHCP Server Options - Router (Option 003):__ Open the DHCP management console on your Windows Server.Navigate to the DHCP server and expand it.Right-click on "Server Options" and select "Configure Options."Look for "003 Router" in the list of options.Change the value to the desired default gateway IP address. Click "Apply" or "OK" to save the changes. <br>

By checking the network configuration on the CLIENT VM, you can verify that it has received the correct IP address and gateway information from the DHCP server. Changing the DHCP server options ensures that the correct default gateway is assigned to the connected devices on the network. <br>

![30](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/0886524d-6228-43e6-94fc-ad5037d20b15)

Let's change the computer name and join the Windows 10 CLIENT VM to the domain "mydomain. com". Follow these steps:
1. __Change Computer Name:__ Right-click on the "This PC" icon on the desktop or in File Explorer. Select "Properties" to open the System properties. Click on the "Change settings" link next to the computer name. Click the "Change" button, enter the new computer name (e.g., "CLIENT"), and click "OK."You may be prompted to restart the computer. If not, restart the VM manually.
2. __Join the Domain:__ After restarting, go back to the System properties. Click on the "Change" button next to the domain settings.Enter "mydomain. com" in the "Member of" field. Click "OK" and provide domain credentials when prompted.Restart the VM if required.
3. __Verify Domain Join:__ After restarting, log in to the Windows 10 CLIENT VM using domain credentials.Verify that the computer is now a member of the. "mydomain. com" domain.

![31](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/3ab9a491-5c24-4c52-94d8-c9bc72fe1e14)

Let's verify that the IP address assigned to the Windows 10 CLIENT VM matches the one listed in the DHCP address leases on the Domain Controller. Here are the steps: <br>
1. __Go to DHCP Address Leases on DC:__ On the Domain Controller, open the DHCP management console.Navigate to the DHCP server, expand it, and click on "Address Leases." <br>
2. __Check Assigned IP Address:__ Look for the lease assigned to the Windows 10 CLIENT VM. The hostname or IP address should match the one you configured or received dynamically. <br>
3. __Verify IP Address on Windows 10 CLIENT VM:__ On the Windows 10 CLIENT VM, open a Command Prompt.IPCONFIG <br>
4.Check the "IPv4 Address" in the output to ensure it matches the IP address listed in the DHCP address leases on the DC. <br>

By comparing the DHCP address leases on the DC with the actual IP address assigned to the Windows 10 CLIENT VM, you can verify that the DHCP server is correctly assigning IP addresses to devices on the network. If there's a match, it confirms successful communication and configuration <br>


![32](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/912665a9-669c-4bb9-b4c2-d179b24a97fb)

Let's check the username on the Windows 10 CLIENT VM using the whoami command. Follow these steps: <br>
1. __Open Command Prompt on CLIENT VM:__ On the Windows 10 CLIENT VM, open a Command Prompt. <br>
2. __Run whoami Command:__ Type the following command and press Enter: whoami <br>
3. __Verify Username:__ Check the output to verify that the username matches the ones you added using the PowerShell script. <br>

By running whoami, you can confirm the username associated with the current user context on the Windows 10 CLIENT VM. If everything is configured correctly, it should display the username you created using the PowerShell script. <br>

![33](https://github.com/Jaswanthbommi/Active-Directory/assets/62924828/597c7a43-38e0-4bbf-bf51-dda5ea203f8d)

And there we have it, folks! That wraps up our lab session. We've successfully gone through the entire process – from setting up Active Directory on our Domain Controller to creating 1000 users using PowerShell. Now, as we check for other users on our Windows 10 CLIENT machine, we can confidently say that this lab is complete. If you have any questions or want to delve into more exciting IT adventures, feel free to ask. Happy exploring! <br>

__Key take aways :__ 
1. __Network Customization:__ Navigated through various settings, customizing IP addresses, and configuring network adapters to establish a well-structured network environment. <br>
2. __Domain Setup:__ Successfully set up a domain, providing a centralized and organized platform for managing network resources. <br>
3. __RAS/NAT Configuration:__ Configured the Remote Access Server (RAS) and Network Address Translator (NAT), enabling client computers to access the internet through the Domain Controller. <br>
4. __PowerShell Scripting for User Creation:__ Actively utilized PowerShell scripting to create 1000 users, demonstrating proficiency in automating and optimizing user management tasks. <br>
5. __Educational Journey:__ Engaged in a comprehensive learning journey, from downloading and setting up VMs to troubleshooting and optimizing user management in Active Directory. <br>
6. __Skill Enhancement:__ Enhanced technical expertise by understanding the nuances of Active Directory, honing troubleshooting skills, and gaining hands-on experience in optimizing user management. <br>
7. __Hands-on Troubleshooting:__ Applied a hands-on approach to troubleshooting, gaining valuable insights into resolving issues and optimizing network configurations. <br>
8. __Continuous Learning:__ Recognized the project as a continuous learning experience, solidifying knowledge and skills in IT infrastructure and network administration. <br>

Overall, this project has been a valuable journey in technology, providing practical insights into network administration, server configuration, and efficient user management. <br>



