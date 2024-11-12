# What is Active Directory (AD)?

Active Directory (AD) is a system created by Microsoft to manage networks in a Windows environment. It keeps track of important information about objects like computers, users, and printers, similar to how a phone book stores contact details. When users log in or access resources, AD verifies their identity using a process called **Kerberos**. Non-Windows devices, such as Linux computers or network devices like firewalls, can also connect to Active Directory through methods like **RADIUS** or **LDAP**.

## AD DS Data Store

The **Active Directory Domain Services (AD DS)** data store is a special database that holds all the directory information about users, services, and applications in a network. It’s stored in a file called `Ntds.dit` and by default, it is located in the `%SystemRoot%\NTDS` folder on domain controllers. Only domain controller systems can access and manage this data.

## Domains

Domains are used to organize and manage objects (like users and computers) in a network. A **domain**:

- Acts as an administrative boundary, meaning you can apply rules and policies to all objects within the domain.
- Is a replication boundary, meaning data between domain controllers is synchronized within the domain.
- Controls access, ensuring only authorized users can access certain resources.

## Trees

A **domain tree** is a collection of domains connected in a hierarchy. In a domain tree:

- All domains share a naming structure with the parent domain.
- A parent domain can have several child domains.
- Domains automatically trust each other for easier management of resources.

## Forests

A **forest** is a larger structure that can contain multiple domain trees. A forest:

- Shares the same technical setup, like the schema (blueprints for the directory) and configuration.
- Has a global catalog, which helps in searching for information across the entire forest.
- Connects all domains within the forest with trust relationships.
- Includes special admin groups like **Enterprise Admins** and **Schema Admins**.

## Organizational Units (OUs)

**Organizational Units (OUs)** are containers inside Active Directory that can hold users, groups, computers, and other OUs. They are used to:

- Organize your network in a logical, hierarchical way, reflecting your company's structure.
- Simplify the management of objects by grouping them together.
- Assign administrative tasks and apply policies to these groups.

## Types of Objects in Active Directory

- **User**: Represents a person or entity that needs access to the network resources.
- **InetOrgPerson**: Similar to a user, but designed for compatibility with other directory systems.
- **Contact**: Primarily used for storing external email addresses (doesn't grant network access).
- **Group**: Helps manage user permissions and access in bulk, making administration easier.
- **Computer**: Represents a computer on the network, allowing it to be authenticated and tracked for resource access.
- **Printer**: Stores information about printers, making it easier for users to find and connect to them.
- **Shared Folder**: Used for managing shared files and folders, making them searchable based on specific properties.

## Domain Controllers

A **domain controller** is a server that manages and controls access to a network. It runs Active Directory and is set up to handle domain tasks. Domain controllers:

- Store the network's important data (like user accounts and computer information).
- Check usernames and passwords to grant access to the network.
- Share updates with other domain controllers to keep everything up to date.
- Allow admins to manage user accounts and network resources.
