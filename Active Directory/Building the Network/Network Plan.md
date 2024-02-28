# Network plan

In this section of the knowledge base I am going to be planning out the network and how I want each device to be configured in the network.

## Server & Computer Names

**SRV01-AD** - This server is going to host the following services for the network.

- **Active Directory Domain Services (AD DS)** - For authentication and autherization to the network resources. It is also going to be used to link group policies to OUs.

- **Dynamic Host Configuration Protocol (DHCP)** - Used to dynamically assign Internet Protocol addresses to clients on the network to allow them to access the network.

- **Domain Name System (DNS)** - This is going to be used to translate domain names into IP addresses on the network.

**SRV02-FS** - This server is going to host the **Network File Share (NFS)** for clients to access and have restrictions to what files they are **allowed to access**.

**PC01-UBTU** - This computer is going to be using **Ubuntu** to connect to the Active Directory Domain to allow user to log into system and access their files, which are stored on a seperate drive.

# 
