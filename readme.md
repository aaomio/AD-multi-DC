# Active Directory Multi-Domain Controller Lab

This project demonstrates a Windows Server Active Directory environment using multiple domain controllers to provide redundancy, replication, and centralized identity management.

The lab simulates a small enterprise setup where Active Directory data is shared across multiple servers to ensure availability and consistency.

---

## Follow-on

This lab builds upon an earlier implementation covering Windows Server setup and Active Directory Domain Services (AD DS) deployment:

[win-server-AD](https://github.com/aaomio/win-server-AD)

---

## Domain Overview

Domain: `matrix.local`

Domain Controllers:
- DC-01: Primary Domain Controller
- DC-02: Secondary Domain Controller

Both domain controllers participate in the same Active Directory forest and maintain synchronized directory data through replication.

---

## Key Concepts Demonstrated

- Active Directory forest and domain creation
- Multi-domain controller architecture
- DNS integration with Active Directory
- Automatic replication between domain controllers
- Organizational Unit (OU) management
- Directory consistency validation across servers

---

## Lab Structure

- [DC-01 Setup](DC-01-setup.md)
- [DC-02 Setup](DC-02-setup.md)
- [Active Directory Replication Test](AD-replication-validate.md)

---

## Validation Overview

This lab confirms:

- DC02 successfully joins the existing domain
- Active Directory objects replicate between controllers
- Organizational Units are synchronized across both DCs
- Changes made on one DC appear on the other without manual intervention