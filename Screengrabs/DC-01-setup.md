# DC-01 Setup (Primary Domain Controller)

Before proceeding with this guide, ensure:

1. VMware Workstation or VMware Player is installed.
2. Windows Server virtual machine is created and configured.
3. Windows Server is installed and set up.
4. A static IP address is assigned to the server.

A detailed walkthrough covering VMware setup, Windows Server installation, and Active Directory Domain Services (AD DS) deployment can be found here:

[win-server-AD](https://github.com/aaomio/win-server-AD)

---

## Server Rename

Before any domain configuration, rename the server to match its role.

1. Press **Windows + R**
2. Type:

```text
sysdm.cpl
```

3. Press **Enter**
4. Go to **Computer Name** tab and click **Change**
5. Set the name to:

```text
DC-01
```

6. Click **OK**
7. Restart the server when prompted

---

## Server Role Overview

**DC-01** serves as the primary Domain Controller for the lab environment and is responsible for:

- Creating and managing the Active Directory forest.
- Hosting the `matrix.local` domain.
- Providing DNS services for name resolution.
- Handling user authentication and authorization.
- Managing Group Policy and directory services.

---

## Network Configuration

Configure the server with the following static network settings:

```text
IP Address:      192.168.1.199
Subnet Mask:     255.255.255.0
Default Gateway: 192.168.1.254
Preferred DNS:   192.168.1.199
```

> **Note:** Once DNS is installed, the server should point to itself for DNS to ensure proper AD resolution.

---

## Active Directory Domain Services Installation

1. Open **Server Manager**
2. Select **Manage** anf go to **Add Roles and Features**.
3. Choose **Role-based or feature-based installation**
4. Select the local server (`DC-01`)
5. Install **Active Directory Domain Services**
6. Add required features when prompted
7. Complete the wizard and install

---

## Promote Server to Domain Controller

After AD DS installation:

1. In **Server Manager**, click the notification flag
2. Select **Promote this server to a domain controller**
3. Choose **Add a new forest**
4. Enter:

```text
matrix.local
```

5. Set the DSRM password
6. Continue through defaults and install
7. Server will restart automatically

---

## Verification

After restart:

- Sign in with domain administrator account
- Open **Active Directory Users and Computers** and confirm domain exists
- Open **DNS Manager** and verify `matrix.local` zone
- Run in PowerShell:

```powershell
Get-ADDomain
```

Expected output:

```text
DNSRoot : matrix.local
```