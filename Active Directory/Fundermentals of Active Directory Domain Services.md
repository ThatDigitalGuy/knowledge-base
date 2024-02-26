# Fundermentals of Active Directory Domain Services

*All information is from [Microsoft Learn Training - Active Directory Domain Services](https://learn.microsoft.com/en-us/training/modules/introduction-to-ad-ds/1-introduction?ns-enrollment-type=learningpath&ns-enrollment-id=learn.wwl.active-directory-domain-services)*

## Prerequisites
- Windows Server
- Core Networking Technologies

## Learning Objectives
- Describe AD DS.
- Describe users, groups, and computers.
- Identify ad describe AD DS forests and domains.
- Describe OUs.
- Manage objects and their properties in AD DS.

## What is AD DS?
Active Directory Domain Services (**AD DS**) and its related services form the foundation for enterprise networks that run the Windows Operating System (**OS**). The AD DS database is the central store of all the domain objects, such as user accounts, computer accounts, groups. It allows for a searchable, hierarchical directory and is a method on applying configuration and security settings.

> **Hierarchical** is defined as by [Cambridge Dictionary](https://dictionary.cambridge.org/dictionary/english/hierarchical)...
> 	*"arranged according to people's or things' level of importance, or relating to such a system."*

AD DS includes both logical and physical components, you should understand how AD DS components work together so that you can manage your infrastructure efficiently. 

**You can also use AD DS options to preform the following actions:**
- Installing, configuring, and updating applications.
- Managing the security infrastructure.
- Enabling Remote Access Service and DirectAccess.
- Issuing and managing digital certificates.

### What are the Logical Components?
AD DS logical components are structures that you can use to implement an AD DS design that is appropriate for an organisation. The logical components are as follows, according to Microsoft Learn (n.d.):

| Logical Component         | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Partition                 | A partition, or naming context, is a portion of the AD DS database. Although the database consists of one file named Ntds.dit, different partitions contain different data. For example, the schema partition contains a copy of the Active Directory schema. The configuration partition contains the configuration objects for the forest, and the domain partition contains the users, computers, groups, and other objects specific to the domain. Active Directory stores copies of partitions on multiple domain controllers and updates them through directory replication. |
| Schema                    | A schema is the set of definitions of the object types and attributes that you use to define the objects created in AD DS.                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Domain                    | A domain is a logical administrative container for objects such as users and computers. A domain maps to a specific partition, and you can organise the domain with parent-child relationships to other domains.                                                                                                                                                                                                                                                                                                                                                                   |
| Domain Tree               | A domain tree is a hierarchical collection of domains that share a common root domain and a contiguous Domain Name System (DNS) namespace.                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Forest                    | A forest is a collection of one or more domains that have a common AD DS root, a common schema, and a common global catalogue.                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Organisational Unit (OUs) | An OU is a container object for users, groups, and computers that provides a framework for delegating administrative rights and administration by linking Group Policy Objects (GPOs).                                                                                                                                                                                                                                                                                                                                                                                             |
| Containers                | A container is an object that provides an organisational framework for use in AD DS. You can use the default containers, or you can create custom containers. You can't link GPOs to containers.                                                                                                                                                                                                                                                                                                                                                                                   |

### What are the physical components?

> According to Microsoft Learn (n.d.), **physical components** can be described as...
> 	*"Physical components in AD DS are those objects that are tangible, or that described tangible components in the real world."*

Below is the following physical components, according to Microsoft Learn (n.d.):

| Physical Component                 | Description                                                                                                                                                                                                                                                                                          |
| ---------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Domain controller                  | A domain controller contains a copy of the AD DS database. For most operations, each domain controller can process changes and replicate the changes to all the other domain controllers in the domain.                                                                                              |
| Data Store                         | A copy of the data store exists on each domain controller. The AD DS database uses Microsoft Jet database technology and stores the directory information in the Ntds.dit file and associated log files. The C:\\Windows\\NTDS folder stores these files by default.                                 |
| Global Catalog Server              | A global catalog server is a domain controller that hosts the global catalogue, which is a partial, read-only copy of all the objects in a multiple-domain forest. A global catalogue speeds up searches for objects that might be stored on domain controllers in a different domain in the forest. |
| Read-only domain controller (RODC) | An RODC is a special, read only installation of AD DS. RODCs are common in branch offices where physical security is not optimal, IT support is less advanced than in the main corporate centres, or line-of-business applications need to run on a domain controller.                               |
| Site                               | A site is a container for AD DS objects, such as computers and services that are specific to a physical location. This is in comparison to a domain, which represents the logical structure of objects, such as users and groups, in addition to computers.                                          |
| Subnet                             | A subnet is a portion of the network IP addresses of an organization assigned to computers in a site. A site can have more than one subnet.                                                                                                                                                          |
## Defining Users, groups, and Computers
*All information is from [Microsoft Learn - AD DS Training](https://learn.microsoft.com/en-us/training/modules/introduction-to-ad-ds/3-define-users-groups-computers)*

In AD DS, every user that requires access to the network **requires a user account**. With the AD DS account they can access the network and resources. In Windows Server, a user account is an object that contains all the information that defines a user. The user account includes:

- The username
- A user password
- Group Memberships

The user account can contain setting that can be configured based on the requirements of the business.
![Example User Configuration in AD DS](https://learn.microsoft.com/en-us/training/wwl-windows-server/introduction-to-ad-ds/media/m6-user-89703b1f.png)
*Photo from [Microsoft Learn AD DS Training](https://learn.microsoft.com/en-us/training/modules/introduction-to-ad-ds/3-define-users-groups-computers)*

The username and password of a user account serve as the user's sign in credentials. A user object also includes several other attributes that describe and manage the user. You can use the following to create and manage a user object in **AD DS**:

- Active Directory Administrative Centre.
- Active Directory Users and Computers.
- Windows Admin Centre.
- Windows Powershell.
- The `dsadd` command-line tool. 

### Managed Service accounts
A managed service account can run in the background  and doesn't require user interaction. The service account can be local to the computer, a Network Service, or a Local System accounts. You also can configure a service account to use a domain-based account located in **AD DS**.

Centralised administration and to meet program requirements, business' can use a domain-based account to run program services. There are benefits to this, however there are the following challenges with this approach.

- Extra administration effort might be necessary to manage the service account password securely.
- It can be difficult to determine where a domain-based account is being used as a service account.
- Extra administration effort might be necessary to manage the service principal name (SPN).

> According to [Microsoft Learn (n.d.)](https://learn.microsoft.com/en-us/windows/win32/ad/service-principal-names), **Service Principal Name** can be defined as...
> 	*A service principal name (SPN) is a unique identifier of a service instance.*

Windows Server supports an AD DS object, named a managed service account, which you can use to facilitate service-account management. A managed service account enables:

- Simplified password management
- Simplified Service Principal Name (**SPN**) management


### What are group objects?
Whilst practical to assign users in a small business permissions per user, it becomes impractical to do so in a large business, it will also be inefficient. Before you implement groups in your organisation, you must understand the scope of various AD DS group types. In addition, you must understand how to use group types to manage access to resources or to assign management rights and responsibilities.

> According to Cambridge Dictionary (2019), **scope** can be defined as...
> 	*"the range of a subject covered by a book, programme, discussion, class, etc."*

![Groups Management](https://learn.microsoft.com/en-us/training/wwl-windows-server/introduction-to-ad-ds/media/m6-group-39cc1f7d.png)
*Photo from [Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/introduction-to-ad-ds/3-define-users-groups-computers)*
### Group types
There are two types of groups, as described below.

| Group Type   | Description                                                                                                                                                                                                                                                                                                       |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Security     | Security groups are security-enabled, and you use them to assign permissions to various resources. You can use security groups in permission entries in access control lists (ACLs) to help control security for resource access. If you want to use a group to manage security, it must be a security group. |
| Distribution | Email applications typically use distribution groups, which are not security-enabled. You also can use security groups as a means of distribution for email applications.                                                                                                                                         |

### Group Scopes
The scope of a group determines both the range of group's abilities or permissions and the group membership. There are four groups.

##### Local
You can use this type of group for standalone servers or workstations, on domain-member servers that are not domain controllers, or on domain-member workstations. Local groups are available only on the computer where they exist.

- **Standalone servers or workstations** - Individual computers that are not part of a network domain. They manage their own users and resources independently.
- **Domain-member servers that are not Domain Controllers** - Computers that are part of the network domain but don't control the domain itself. They might host applications or data but don't manage user accounts or security policies.
- **Domain-member workstations** - Computers connected to a network domain and rely on the domain controller for the user accounts, security policies, and other resources.

**Characteristics of local group are**...
- You can assign abilities and permissions on local resources only, meaning on the local computer.
- Members can be from anywhere in the AD DS forest.

##### Domain-local
You use this type of group primarily to manage access to resources or to assign management rights and responsibilities. Domain-local groups exist on domain controllers in an AD DS domain, and so, the group’s scope is local to the domain in which it resides. The important characteristics of domain-local groups are:

- You can assign abilities and permissions on domain-local resources only, which means on all computers in the local domain.
- Members can be from anywhere in the AD DS forest.

##### Global
You use this type of group primarily to consolidate users who have similar characteristics. For example, you might use global groups to join users who are part of a department or a geographic location. The important characteristics of global groups are:

- You can assign abilities and permissions anywhere in the forest.
- Members can be from the local domain only and can include users, computers, and global groups from the local domain.

##### Universal
You use this type of group most often in multidomain networks because it combines the characteristics of both domain-local groups and global groups. Specifically, the important characteristics of universal groups are:

- You can assign abilities and permissions anywhere in the forest similar to how you assign them for global groups.
- Members can be from anywhere in the AD DS forest.

### What are computer objects?
*All information is from [Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/introduction-to-ad-ds/3-define-users-groups-computers)*

Computers, like users, are security principals, in that:

- They have an account with a sign-in name and password that Windows changes automatically on a periodic basis.
- They authenticate with the domain.
- They can belong to groups and have access to resources, and you can configure them by using Group Policy.

A computer account begins its lifecycle when you create the computer object and join it to your domain. After you join the computer account to your domain, day-to-day administrative tasks include:

- Configuring computer properties.
- Moving the computer between Organisational Unit OUs.
- Managing the computer itself.
- Renaming, resetting, disabling, enabling, and eventually deleting the computer object.

![Create Computer Configuration](https://learn.microsoft.com/en-us/training/wwl-windows-server/introduction-to-ad-ds/media/m6-computer-c09654bd.png)
*Photo from [Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/introduction-to-ad-ds/3-define-users-groups-computers)*

### Computer Containers
*All information is from [Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/introduction-to-ad-ds/3-define-users-groups-computers)*

Before you create a computer object in AD DS, you must have a place to put it. The Computers container is a built-in container in an AD DS domain. This container is the default location for the computer accounts when a computer joins the domain.

This container is not an OU. Instead, it is an object of the Container class. Its common name is CN=Computers. There are subtle but important differences between a container and an OU. You cannot create an OU within a container, so you cannot subdivide the Computers container. You also cannot link a Group Policy Object to a container. Therefore, we recommend that you create custom OUs to host computer objects, instead of using the Computers container.

## Define AD DS forest and domains
*All information is from [Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/introduction-to-ad-ds/4-define-forests-domains)*

According to Microsoft Learn (n.d.)...

An AD DS forest is a collection of one or more AD DS trees that contain one or more AD DS domains. Domains in a forest share:

- A common root.
- A common schema.
- A global catalog.

An AD DS domain is a logical administrative container for objects such as:

- Users
- Groups
- Computers

### What is an AD DS Forest?
*All information is from [Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/introduction-to-ad-ds/4-define-forests-domains)*

A forest is a top-level container in AD DS. Each forest is a collection of one or more domain trees that share a common directory schema and a global catalog. A domain tree is a collection of one or more domains that share a contiguous namespace. The forest root domain is the first domain that you create in the forest.

Personally I can't understand this however I asked Gemini AI from Google to explain this to me and this is what it responded with.

---

**Forest:**

- **Top-level container:** Imagine a large box holding everything in your AD DS environment.
- **Collection of domain trees:** Think of these as smaller boxes representing different administrative units within the forest, like colleges in a university.
- **Shared directory schema and global catalog:** These define the structure and location of objects like users and computers, and a searchable index across all domains, akin to a university library catalog.

**Domain tree:**

- **Collection of domains:** Even smaller boxes within a domain tree, like departments within a college, managing specific groups of users and resources.
- **Contiguous namespace:** Ensures unique user names across the tree, preventing confusion, like having one central naming system for all departments.

**Forest root domain:**

- **First domain created:** The foundation of the forest, like the main administration building in a university.
- **Special role:** Holds critical settings and objects shared across the forest, such as the central directory structure and searchable index.

**Analogy:**

Think of a university with colleges (domain trees) and departments (domains). The entire university system represents the forest, housing all colleges and departments. The main administration building could be the forest root domain, containing central resources and governing rules.

**Key points:**

- Forests organize large AD DS deployments with multiple administrative units.
- Domain trees offer further division within a forest for specific needs.
- The forest root domain holds vital configuration information for the entire AD DS environment.


---

The forest root domain contains objects that don't exist in other domains in the forest. Because you always create these objects on the first domain controller, a forest can consist of as few as one domain with a single domain controller, or it can consist of several domains across multiple domain trees.

The following graphic displays `Contoso.com` as the forest root domain. Beneath are two domains, `Adatum.com` in a separate tree, and `Seattle.Contoso.com` as a child of `Contoso.com`.

![Example of Forest's in Active Directory](https://learn.microsoft.com/en-us/training/wwl-windows-server/introduction-to-ad-ds/media/m6-forest-bc4595bc.png)
*Photo from [Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/introduction-to-ad-ds/4-define-forests-domains)*

The following objects exist in the forest root domain:

- The schema master role.
- The domain naming master role.
- The Enterprise Admins group.
- The Schema Admins group.

You may see **AD DS** be referred as the following:

- **A security boundary**. 
	- By default, no users from outside the forest can access any resources inside the forest. In addition, all the domains in a forest automatically trust the other domains in the forest. This makes it easy to enable access to resources for all the users in a forest, regardless of the domain to which they belong.
- **A replication boundary.** 
	- An AD DS forest is the replication boundary for the configuration and schema partitions in the AD DS database. Therefore, organizations that want to deploy applications with incompatible schemas must deploy additional forests. The forest is also the replication boundary for the global catalog. The global catalog makes it possible to find objects from any domain in the forest.

The following objects exist in each domain (including the forest root):

- The RID master role.
- The Infrastructure master role.
- The PDC emulator master role.
- The Domain Admins group.

### What is an AD DS domain?

An AD DS domain is a logical container for managing user, computer, group, and other objects. The AD DS database stores all domain objects, and each domain controller stores a copy of the database.

The following graphic displays an AD DS domain.
![AD DS Domain Example](https://learn.microsoft.com/en-us/training/wwl-windows-server/introduction-to-ad-ds/media/m6-domain-755853b7.png)
*Photo from [Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/introduction-to-ad-ds/4-define-forests-domains)*

**Below you will find the commonly used objects described.

| **Object**        | **Description**                                                                                                                                                        |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| User accounts     | User accounts contain information about users, including the information required to authenticate a user during the sign-in process and build the user's access token. |
| Computer accounts | Each domain-joined computer has an account in AD DS. You can use computer accounts for domain-joined computers in the same way that you use user accounts for users.   |
| Computer accounts | Groups organize users or computers to simplify the management of permissions and Group Policy Objects in the domain.                                                   |

*AD DS allows a single domain to contain nearly two billion objects.*

An AD DS domain is often described as:

- A replication boundary. When you make changes to any object in the domain, the domain controller where the change occurred replicates that change to all other domain controllers in the domain. If multiple domains exist in the forest, only subsets of the changes replicate to other domains. AD DS uses a multi-master replication model that allows every domain controller to make changes to objects in the domain.
- An administrative unit. The AD DS domain contains an Administrator account and a Domain Admins group. By default, the Administrator account is a member of the Domain Admins group, and the Domain Admins group is a member of every local Administrators group of domain-joined computers. Also, by default, the Domain Admins group members have full control over every object in the domain.

An AD DS domain provides:

- Authentication. Whenever a domain-joined computer starts or a user signs in to a domain-joined computer, AD DS authenticates it. Authentication verifies that computer or user has the proper identity in AD DS by verifying its credentials.
- Authorization. Windows uses authorization and access control technologies to determine whether to allow authenticated users to access resources.

### What are trust relationships?
According to Microsoft Learn (n.d.), "AD DS trusts enable access to resources in a complex AD DS environment."

***Below is the main trust types***

| **Trust Type**                 | **Description**              | **Direction**      | **Description**                                                                                                                                                                                                                           |
| ------------------------------ | ---------------------------- | ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Parent and child               | Transitive                   | Two-way            | When you add a new AD DS domain to an existing AD DS tree, you create new parent and child trusts.                                                                                                                                        |
| Tree-root                      | Transitive                   | Two-way            | When you create a new AD DS tree in an existing AD DS forest, you automatically create a new tree-root trust.                                                                                                                             |
| External                       | Nontransitive                | One-way or two-way | External trusts enable resource access with a Windows NT 4.0 domain or an AD DS domain in another forest. You also can set these up to provide a framework for a migration.                                                               |
| Realm                          | Transitive or non-transitive | One-way or two-way | Realm trusts establish an authentication path between a Windows Server AD DS domain and a Kerberos version 5 (v5) protocol realm that implements by using a directory service other than AD DS.                                           |
| Forest (complete or selective) | Transitive                   | One-way or two-way | Trusts between AD DS forests allow two forests to share resources.                                                                                                                                                                        |
| Shortcut                       | Non-transitive               | One-way or two-way | Configure shortcut trusts to reduce the time taken to authenticate between AD DS domains that are in different parts of an AD DS forest. No shortcut trusts exist by default, and an administrator must create them if they are required. |

## Defining OUs
*All information is from [Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/introduction-to-ad-ds/5-define-organizational-units)*

According to Microsoft Learn (n.d.), "An OU is a container object within a domain that you can use to consolidate users, computers, groups, and other objects. You can link Group Policy Objects (GPOs) directly to an OU to manage the users and computers contained in the OU. You can also assign an OU manager and associate a COM+ partition with an OU.".

You can create new OUs in AD DS by using:

- Active Directory Administrative Center.
- Active Directory Users and Computers.
- Windows Admin Center.
- Windows PowerShell with the Active Directory PowerShell module.

### Why Use Organisational Units?
There are two reasons to create an OU:

- To consolidate objects to make it easier to manage them by applying GPOs to the collective. When you assign GPOs to an OU, the settings apply to all the objects within the OU. GPOs are policies that administrators create to manage and configure settings for computers or users. You deploy the GPOs by linking them to OUs, domains, or sites.
- To delegate administrative control of objects within the OU. You can assign management permissions on an OU, thereby delegating control of that OU to a user or a group within AD DS, in addition to the Domain Admins group.

You can use OUs to represent the hierarchical, logical structures within your organization.

### Why & What are the generic containers?
AD DS has several built-in containers, or generic containers, such as Users and Computers. These containers store system objects or function as the default parent objects to new objects that you create. The primary difference between OUs and containers is the management capabilities. Containers have limited management capabilities. For example, you can't apply a GPO directly to a container.

![Container Overview](https://learn.microsoft.com/en-us/training/wwl-windows-server/introduction-to-ad-ds/media/m6-objects-4501913a.png)
*Photo by [Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/introduction-to-ad-ds/5-define-organizational-units)*

Installing AD DS creates the Domain Controllers OU and several generic container objects by default. AD DS primarily uses some of these default objects, which are also hidden by default. The following objects are displayed by default:

- Domain. The top level of the domain organizational hierarchy.
- Builtin container. A container that stores several default groups.
- Computers container. The default location for new computer accounts that you create in the domain.
- Foreign Security Principals container. The default location for trusted objects from domains outside the local AD DS domain that you add to a group in the local AD DS domain.
- Managed Service Accounts container. The default location for managed service accounts. AD DS provides automatic password management in managed service accounts.
- Users container. The default location for new user accounts and groups that you create in the domain. The Users container also holds the administrator, the guest accounts for the domain, and some default groups.
- Domain Controllers OU. The default location for domain controllers' computer accounts. This is the only OU that is present in a new installation of AD DS.

***Below is the hidden containers by default.***

| **Object**   | **Description**                                                                                                              |
| ------------ | ------------------------------------------------------------------------------ |
| LostAndFound | This container holds orphaned objects.|
| Program Data | This container holds Active Directory data for Microsoft applications, such as Active Directory Federation Services (AD FS). |
| System       | This container holds the built-in system settings.                                                                           |
| NTDS Quotas  | This container holds directory service quota data.                                                                           |
| TPM Devices  | This container stores the recovery information for Trusted Platform Module (TPM) devices.                                    |

> Containers in an AD DS domain cannot have GPOs linked to them. To link GPOs to apply configurations and restrictions, create a hierarchy of OUs and then link the GPOs to them.


### Hierarchical Design
According to Microsoft Learn (n.d.), "The administrative needs of the organisation dictate the design of an OU hierarchy. Geographic, functional, resource, or user classifications could all influence the design. Whatever the order, the hierarchy should make it possible to administer AD DS resources as effectively and flexibly as possible."

## Manage Objects and their properties in AD DS
*All information is from [Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/introduction-to-ad-ds/6-manage-objects-active-directory)*

There are several tools that you can use to manage AD DS.

### Active Directory Administrative Center
![Active Directory Administrative Center](https://learn.microsoft.com/en-us/training/wwl-windows-server/introduction-to-ad-ds/media/m6-administrative-center-195c7431.png)
*Photo from [Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/introduction-to-ad-ds/6-manage-objects-active-directory)*

**Summary**
The Active Directory Administrative Center is a graphical interface built on Windows PowerShell that simplifies managing objects in Active Directory. It offers a task-oriented approach and replaces the older Active Directory Users and Computers tool.

**Tasks that it can perform**

Tasks that you can perform by using the Active Directory Administrative Center include:

- Creating and managing user, computer, and group accounts.
- Creating and managing OUs.
- Connecting to and managing multiple domains within a single instance of the Active Directory Administrative Center.
- Searching and filtering AD DS data by building queries.
- Creating and managing fine-grained password policies.
- Recovering objects from the Active Directory Recycle Bin.
- Managing objects that the Dynamic Access Control feature requires.

### Windows Admin Center
![Window Admin Center](https://learn.microsoft.com/en-us/training/wwl-windows-server/introduction-to-ad-ds/media/m6-windows-admin-center-9057410f.png)
*Photo from [Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/introduction-to-ad-ds/6-manage-objects-active-directory)*

Windows Admin Center is a web-based console that you can use to manage server computers and computers that are running Windows 10. Typically, you use Windows Admin Center to manage servers instead of using Remote Server Administration Tools (RSAT).

### Remote Server Administration Tools (RSAT)
![Remote Server Administration Tools](https://learn.microsoft.com/en-us/training/wwl-windows-server/introduction-to-ad-ds/media/m6-add-optional-feature-dialog-box-cc4ed1ad.png)
*Photo from [Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/introduction-to-ad-ds/6-manage-objects-active-directory)*

You can install the consoles available within RSAT on computers running Windows 10 or on server computers that are running the Server with Desktop Experience option of a Windows Server installation. Until the introduction of Windows Admin Center, RSAT consoles were the primary graphical tools for administering the Windows Server operating system.

### Other AD DS management tools 

| **Management tool**                            | **Description**                                                                                                                                                                                                                                                                                                      |
| ---------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Active Directory module for Windows PowerShell | The Active Directory module for Windows PowerShell supports AD DS administration, and it's one of the most important management components. Server Manager and the Active Directory Administration Center are based on Windows PowerShell and use cmdlets to perform their tasks.                                    |
| Active Directory Users and Computers           | Active Directory Users and Computers is a Microsoft Management Console (MMC) snap-in that manages most common resources, including users, groups, and computers. Although many administrators are familiar with this snap-in, the Active Directory Administrative Center replaces it and provides more capabilities. |
| Active Directory Sites and Services            | The Active Directory Sites and Services MMC snap-in manages replication, network topology, and related services.                                                                                                                                                                                                     |
| Active Directory Domains and Trusts            | The Active Directory Domains and Trusts MMC snap-in configures and maintains trust relationships at the domain and forest functional levels.                                                                                                                                                                         |
| Active Directory Schema snap-in                | The Active Directory Schema MMC snap-in examines and modifies the definitions of AD DS attributes and object classes. You don't need to review or change it often. Therefore, by default, the Active Directory Schema snap-in is not registered.                                                                     |

# Reference list

Cambridge Dictionary (2019). _SCOPE | meaning in the Cambridge English Dictionary_. [online] Cambridge.org. Available at: https://dictionary.cambridge.org/dictionary/english/scope [Accessed 23 Feb. 2024].

Cambridge Dictionary (2022). _hierarchical_. [online] @CambridgeWords. Available at: https://dictionary.cambridge.org/dictionary/english/hierarchical.

Microsoft Learn (n.d.). _Define AD DS - Training_. [online] learn.microsoft.com. Available at: https://learn.microsoft.com/en-us/training/modules/introduction-to-ad-ds/2-define-ad-ds?source=learn [Accessed 23 Feb. 2024].

Microsoft Learn (n.d.). _Define AD DS forests and domains - Training_. [online] learn.microsoft.com. Available at: https://learn.microsoft.com/en-us/training/modules/introduction-to-ad-ds/4-define-forests-domains [Accessed 23 Feb. 2024].

Microsoft Learn (n.d.). _Define users, groups, and computers - Training_. [online] learn.microsoft.com. Available at: https://learn.microsoft.com/en-us/training/modules/introduction-to-ad-ds/3-define-users-groups-computers.

Microsoft Learn (2023). _Service principal names - Win32 apps_. [online] learn.microsoft.com. Available at: https://learn.microsoft.com/en-us/windows/win32/ad/service-principal-names [Accessed 23 Feb. 2024].
