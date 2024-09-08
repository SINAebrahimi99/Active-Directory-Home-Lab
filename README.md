# AD-LAB
Setup a basic AD on virtual home network

## Introduction

The main aim of this project is to form a domain and join our guest PC into that domain. after setting up, we create user accounts using a PowerShell script. in the end, we do a bruteforce attack on the domain to check for any obtainable passwords. 

## Lab Set-up and Tools

1 - Windows Server 2019 (AD DS)

2 - Windows 10 (guest)

3 - Ubunto (attacker)

4 - Windows 11 (HOST Machine + SIEM)

# Creating DC

After installing VMs, we will set up Windows Server 2019 to act as our domain controller. To do this, the server needs two network adapters:

External Network(_INTERNET_): This adapter connects to the internet, getting its IP address from the hosts network and the home router.

Internal Network(_INTERNAL_): This adapter allows communication between Windows Server 2019 and the Windows 10 VMs over a private network.


the INTERNET uses the default NAT configuration and INTERNAL will get its IP address manually


## Creating Users

After creating our domain, the next step is to add users via a PowerShell script and a text file with the usernames. The text file is called [names.txt](names.txt), and the PowerShell script is named [CreateUser.ps](CreateUser.ps). 

The `CreateUser.ps` script functions:

1. **Get Names** : It begins by fetching about 1000 names from the `names.txt` file.
2. **Set Const Password** : All users are assigned the password "Password1".
3. **Create Organizational Unit** : The script creates an Active Directory Organizational Unit (OU) named `_USERS`.
4. **Create and Enable Users** : at the end it uses a foreach loop to create the users in `_USERS` and ensures they are enabled.
