# IAM-Active-Directory-RBAC
Active Directory IAM Lab: RBAC & File Share Access

## Overview
This lab simulates a small enterprise Active Directory environment focused on Identity and Access Management (IAM) principles. The goal was to design and implement role-based access control (RBAC), enforce least privilege, and manage the user lifecycle while troubleshooting real-world authentication and authorization issues.

The environment includes:

Active Directory Domain Services
Structured Organizational Units (OUs)
Security groups for RBAC
Network file shares with NTFS + share permissions
Remote Desktop access controls

## Environment

Domain: helpdesk.local
Domain Controller: Windows Server (AD DS, DNS)
Client: Windows 10 (domain-joined)
Tools: Active Directory Users & Computers, NTFS, SMB, Remote Desktop

## Organizational Unit (OU) Design
Custom OUs were created to avoid using default AD containers and to support scalable identity management. This structure supports clean onboarding, role changes, and deprovisioning.

## User & Group Strategy (RBAC)

Users were created using a consistent naming convention and placed in department-specific OUs.
### Security Groups
Access is granted only through groups, never directly to users.
HR_Read / HR_Modify
Finance_Read / Finance_Modify
Sales_Read
IT_Admin
Remote_Desktop_Users
This implements Role-Based Access Control (RBAC) and simplifies access management.

## Access Control Design
### Network File Share

A centralized file share was created on the server:

\\server-dc01\CompanyShares

### Share Permissions (SMB)

Broad access at the share level (Everyone = Full Control)
Least privilege enforced via NTFS permissions
### NTFS Permissions
Root Folder (CompanyShares):
Authenticated Users → Read & List (folder traversal only)

Department Folders:

HR folder → HR_Read (Read), HR_Modify (Modify)
Finance folder → Finance_Read / Finance_Modify
Sales folder → Sales_Read

This ensures users can only access resources relevant to their role.


## Remote Desktop Access
Remote access was restricted using a dedicated security group:
Remote_Desktop_Users
Users can RDP into domain-joined client machines, while administrative access to the Domain Controller remains restricted to privileged accounts.

## Validation & Testing

Access was tested by logging in as different users and verifying:

Successful access to authorized folders

Access denied to unauthorized folders

Correct behavior across NTFS, SMB, and RDP layers


## Skills Demonstrated

Active Directory administration

Identity and Access Management (IAM)

Role-Based Access Control (RBAC)

Least privilege enforcement

Windows file sharing (SMB, NTFS)

Remote Desktop authorization

Troubleshooting authentication and authorization issues

Built and documented as part of hands-on IAM skill development.
