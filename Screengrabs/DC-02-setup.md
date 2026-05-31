# DC-02 Setup (Secondary Domain Controller)

DC-02 provides redundancy and resilience for the Active Directory environment by acting as an additional Domain Controller within the existing `matrix.local` domain.

---

## Server Role Overview

DC-02 is responsible for:

- Providing fault tolerance for authentication services.
- Maintaining a replicated copy of the Active Directory database.
- Hosting DNS services for name resolution redundancy.
- Supporting load distribution across Domain Controllers.
- Ensuring continued domain availability during maintenance or outages.

---

## Network Configuration

Configure the server with the following static network settings:

```text
IP Address:      192.168.1.200
Subnet Mask:     255.255.255.0
Default Gateway: 192.168.1.254
Preferred DNS:   192.168.1.199
Alternate DNS:   192.168.1.200
```

> **Note:** Configure DC-01 as the preferred DNS server to ensure successful domain discovery during the domain join and promotion process.

---

## Rename the Server and Join the Domain

Windows Server assigns a random computer name during installation. Before promoting the server to a Domain Controller, rename it and join the existing `matrix.local` domain.

1. Press **Windows + R**.
2. Type:

```text
sysdm.cpl
```

3. Press **Enter**.
4. In **System Properties**, select the **Computer Name** tab.
5. Click **Change**.
6. Enter the new computer name:

```text
DC-02
```

7. Under **Member of**, select **Domain**.
8. Enter the domain name:

```text
matrix.local
```

9. Click **OK**.
10. When prompted, provide Domain Administrator credentials.
11. After receiving the welcome message confirming the domain join, click **OK**.
12. Restart the server when prompted.

After the restart, sign in using a domain account and verify that the server is joined to the domain before continuing with the Domain Controller promotion process.

## Install Active Directory Domain Services

1. Open **Server Manager**.
2. Select **Manage** and go to **Add Roles and Features**.
3. Choose **Role-based or feature-based installation**.
4. Select the local server.
5. Install **Active Directory Domain Services**.
6. Complete the installation wizard.

---

## Promote DC-02 to a Domain Controller

After the AD DS role is installed:

1. Open **Server Manager**.
2. Click the notification flag and select **Promote this server to a domain controller**.
3. Choose:

```text
Add a domain controller to an existing domain
```

4. Specify the domain:

```text
matrix.local
```

5. Provide domain administrator credentials if required.
6. Enable the following options:
   - DNS Server
   - Global Catalog (GC)

7. Configure the Directory Services Restore Mode (DSRM) password.
8. Complete the wizard and click **Install**.
9. Allow the server to restart automatically.

---

## Verify Replication

After promotion, verify that Active Directory replication is functioning correctly.

Run the following command in PowerShell:

```powershell
repadmin /replsummary
```

Confirm that replication completes successfully without errors.

To view Domain Controllers within the domain:

```powershell
Get-ADDomainController -Filter *
```

Expected result:

```text
DC-01
DC-02
```

---

## DNS Validation

Open **DNS Manager** and verify that:

- The `matrix.local` zone exists.
- DNS records have replicated successfully.
- Both Domain Controllers are registered within DNS.

---

## Next Steps

With DC-02 operational, the environment now has:

- Redundant authentication services.
- Multi-master Active Directory replication.
- DNS failover capability.
- Improved resilience against Domain Controller outages.

The domain is now ready for additional infrastructure services such as DHCP, file servers, management servers, and domain-joined client systems.