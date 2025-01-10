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

