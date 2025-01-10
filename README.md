# Building Active Directory Infastructure Azure
![image](https://github.com/user-attachments/assets/efc5aa46-d767-4837-804d-c24e1e0a55ed)

# <b>Description<b/>
In this project I will create two Virtual Machines. The first one running Windows Server to act as a Domain Controller. The second Virtual Machine will act as a client that will be running Windows 10 that will join the Domain Controller. In later projects I will deploy Active Directory and run a script that will create users in the domain, which I can log into from the client VM, then manage the accounts and update the group policies. All to simulate a real life IT environment.
# <b>Envioronments and Utilites Used<b/>
 - Microsoft Azure
 - Virtual Machines
 - Remote Desktop Connection
# <b>Operating Systems Used<b/>
 - Windows Server
 - Windows 10
# <b>Project Walk-through<b>
To build the foundation first we need to log into Azure, go to Resource Group, Create new. We will name it "Active_Directory_Lab" and for the Region I use Canada Central as it allows me to make a VM later on with out a issue. So use whatever works best for you.
![image](https://github.com/user-attachments/assets/60fd095d-4179-4d6f-88bb-4e1169699920)
![image](https://github.com/user-attachments/assets/c04b82e4-ca7b-4f23-94dd-50f2e81f4f95)

Our next step is to search Virtual Networks in Azure and go here to set up our network next. Click create new. We are putting it under our Active_Directory_Lab Resource Group. The Virtual Network Name will be set to "Active_Directory_VNet". Make sure your region is set to the excat same as your Resource Group. Then Create it.
![image](https://github.com/user-attachments/assets/e373c8e6-db23-45d0-a719-46407b646ba0)

Now to make a Virtual Machine we can navigate there through the Azure search bar. We are going to create a new VM. MAKE SURE YOU ENTER ALL THIS CORRECT. Resource group is our Active_Directory_Lab. Virtual Machine name will be "dc-1". My Region is Canada Central yours may be different. The Image will be "Windows Server 2022 Datacenter: Azure Edtion - x64 Gen2. For the Size we want at least 2 vcpus and 8 GiB. For our username we will use "labuser" and password will be "Cyberlab123!". From here we will click next to Networking and make sure the Virtual network is set to Active_Directory_VNet. Then Review + Create.
![image](https://github.com/user-attachments/assets/d6660d41-1564-4b5d-aa40-df399f1ab2e7)
![image](https://github.com/user-attachments/assets/8c0b287a-322a-41f5-aa34-b6ff83d3a493)
![image](https://github.com/user-attachments/assets/df565138-46fa-456a-b81b-2daeea74a476)

Now we will go back to the VM tab and set up a second VM for us to use. Create new. Again set the Resource group to Active_Directory_Lab. The VM name will be "client-1". Region will be the same a everything else you have setup so far. The Image will change to "Windows 10 Pro, version 22H2 x64 Gen2". Size 2 vcpus, 8 GiB. We will use the labuser and Cyberlab123! user name and password. If there is a Licensing box at the bottom be sure to check it. Then we wil hit next till we get to the Networking tab and make sure Virtual network is set to Active_Directory_VNet and then Review + Create.
![image](https://github.com/user-attachments/assets/21467c3c-af21-4d04-b004-f6907aa069d4)
![image](https://github.com/user-attachments/assets/dd76e4fd-f232-49af-ad95-2cea94831aaf)
![image](https://github.com/user-attachments/assets/2649c617-08be-4772-8902-bc679a2e309c)

We now need to set our DC (Domain Controller) private IP address to "static" as by default it is set to "dynamic". I want this to be static because this DC will double as a DNS (Domain Name System) server which I will tell our client to use as a DNS server later. If the IP allocation setting were set to dynamic the IP address could change leaving the DNS configuration of our client invalid. So I'll go to the network settings of the DC and switch the IP allocation to static.

Now we will go to the VM tab on Azure and click the dc-1 VM to open it and click Network settings. We are going to click the Network interface/ IP configuration at the top. In here we will click ipconfig1 at the bottom and in this window we can see the Private IP address settings with Allocation under it. Here we can set it to Static and Save it.
![image](https://github.com/user-attachments/assets/20119468-bf0a-4b7c-baff-43b11ae0eece)
![image](https://github.com/user-attachments/assets/10b31a1b-0a12-429e-8168-c8d24c6dfd50)

Our next step is to login to dc-1 VM. Back on the VM tab on Azure grab the dc-1 VM public IP address and use the remote desktop to log in.
![image](https://github.com/user-attachments/assets/c9c75717-9ffa-412f-9691-3552090f8a12)

Once loged in if you do not see the Server Manager Dashboard there is a chance you used the wrong IP or a setting got skipped or messed up in the VM.
![image](https://github.com/user-attachments/assets/b81dffc6-9c10-473d-ae47-5e1a837bbd30)

Inside the Domain Controller right click the start button and select run. In the Run box we will type wf.msc. This will bring up the Windows Defender Firewall window. In here we will be disabling the fire wall (I wouldnt reccomend this in real life. This is just for practice on a machine with no personal data on it).
![image](https://github.com/user-attachments/assets/dfd3229c-3df7-40d1-964b-362583ffa04c)

To turn the firewall of click Windows Defender Firewall Properties button. On the Domain, Private, Public Profile tabs switch Firewall state to off then Apply and OK
![image](https://github.com/user-attachments/assets/97065283-121b-415f-b552-0e27a730e90c)

Now we need to set Clients-1's DNS settings to dc-1's private IP address. In order to do this go back to the VM tab on Azure, open dc-1 VM and highlight and copy the Private IP Address. Go to Client-1 VM, Networking, Network Settings and open the Network Interface/ IP configuration.
![image](https://github.com/user-attachments/assets/c656e79a-9a3e-42de-aae0-df97cefab5dd)
![image](https://github.com/user-attachments/assets/f0250edd-2081-48db-b405-c7babb41e17f)

Inside of Client-1's IP configurations look for DNS Servers on the left hand side. In here we will change it from Inherit from virtual network to Custom. Once we change it to custom you will paste your Private IP from dc-1 into here. Make sure there is no space at the start or end or it will not work. Click Save at the top and it will update.
![image](https://github.com/user-attachments/assets/ff0749e7-a6b9-4230-b3db-3433bb0b5be7)

Now we can go back to the VM page in Azure and Restart Client-1 VM. Check the box next to Client-1 and hit Restart at the top. Once the VM Restarts we can take the Public IP Addrress and use Remote Desktop again to now log into Client-1.
![image](https://github.com/user-attachments/assets/d5165e68-1623-4160-a28d-154f3523699c)

As the VM loads uncheck everything. Now we will attempt to ping dc-1's private address. Tab back to Azure and grab it if you dont remember it. At the bottom of our Client-1 VM typer "Powershell" in the search bar and open it.
![image](https://github.com/user-attachments/assets/996443a4-aa26-431b-af59-4b5f056f8d8e)

Inside PowerShell type "ping" then paste or type dc-1's Private IP Address and hit enter. If it times out and you do not get a response double check that both VM's are on the same Virtual Network. If they are not on the same Virtual Network you will need to re-setup the VM's and make sure they are so this works.
![image](https://github.com/user-attachments/assets/79d50746-fde7-457a-a70b-1c1a67ea140c)

While doing this we can double check that the DNS server is pointing to dc-1 buy running "ipconfig /all". If we have done this properly DNS Servers should have the IP Address for our dc-1 VM.
![image](https://github.com/user-attachments/assets/4b455474-3241-4937-b7f5-7d99619c1d33)

# <b>Building Active Directory Infastructure Finished<b/>
We've successfully created two Virtual Machines, one running Windows Server to act as a Domain Controller. The other VM as a client running Windows 10. In later projects we will deploy AD and run a script that will create users in the domain. Then we can log in from the client VM, then manage the accounts and update the group policies, all to simulate a real life environment. 
