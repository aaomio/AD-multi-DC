# Active Directory Replication Validation

This document validates Active Directory replication between:

- DC-01 (192.168.1.199)
- DC-02 (192.168.1.200)

Both domain controllers operate within the `matrix.local` domain and maintain synchronized directory data through multi-master replication.

---

## Replication Concept

Active Directory uses multi-master replication.

This means:

- Both DC-01 and DC-02 can process changes
- Changes are automatically replicated between domain controllers
- No single server acts as a permanent primary controller

---

## Validation Objective

This test confirms:

- Directory objects created on DC-01 replicate to DC-02
- Directory objects created on DC-02 replicate to DC-01
- DNS resolution remains consistent across both servers

---

## Step 1: Create OU on DC01

On DC-01 (192.168.1.199):

- Open Active Directory Users and Computers
- Navigate to domain: `matrix.local`
- Create Organizational Unit:
  - Name: ReplicationTest

---

## Step 2: Create User in OU

Inside `ReplicationTest` on DC01:

- Create user account:
  - Username: test.user

---

## Step 3: Verify on DC02

On DC-02 (192.168.1.200):

- Open Active Directory Users and Computers
- Navigate to domain: `matrix.local`

Validation:

- ReplicationTest OU exists
- test.user exists inside OU

---

## Step 4: Replication Commands (Optional)

Run on either DC:

```cmd id="rep02x1"
repadmin /replsummary