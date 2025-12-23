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
<img width="949" height="673" alt="Domain   OU Structure" src="https://github.com/user-attachments/assets/894b9fe6-6ae8-4b15-acf3-62da7506dd99" />

## User & Group Strategy (RBAC)

Users were created and placed in department-specific OUs.
### Security Groups
Access wass granted only through groups, never directly to users.
HR_Read / HR_Modify
Finance_Read / Finance_Modify
Sales_Read
IT_Admin
Remote_Desktop_Users
This implements Role-Based Access Control (RBAC) and simplifies access management.
<img width="953" height="671" alt="Users in Correct OUs" src="https://github.com/user-attachments/assets/fa988a20-2de6-4eb9-8dac-471e16178bbe" />
<img width="950" height="672" alt="Security Groups" src="https://github.com/user-attachments/assets/24783097-0752-414c-99d1-e4a9779a7558" />

## Access Control Design
### Network File Share

A centralized file share was created on the server:

\\server-dc01\CompanyShares
<img width="1046" height="819" alt="File Share Existing" src="https://github.com/user-attachments/assets/ae8c7787-22d0-4fde-87b3-5933350f07e7" />

### Share Permissions (SMB)

Broad access at the share level (Everyone = Full Control)
Least privilege enforced via NTFS permissions
<img width="1058" height="845" alt="share permissions" src="https://github.com/user-attachments/assets/429f04e0-ebce-4e0e-95f0-9e708739dcef" />

### NTFS Permissions
Root Folder (CompanyShares):
Authenticated Users → Read & List (folder traversal only)

Department Folders:

HR folder → HR_Read (Read), HR_Modify (Modify)
Finance folder → Finance_Read / Finance_Modify
Sales folder → Sales_Read

This ensures users can only access resources relevant to their role.
<img width="1039" height="814" alt="NTFS Permissions - root folder" src="https://github.com/user-attachments/assets/88b457b7-1408-46f6-866c-dd6845daefc7" />
<img width="1145" height="782" alt="NTFS Permissions - Department Folder" src="https://github.com/user-attachments/assets/57dc3368-e232-4e4d-83f8-91c6b509f29b" />


## Remote Desktop Access
Remote access was restricted using a dedicated security group:
Remote_Desktop_Users
Users can RDP into domain-joined client machines, while administrative access to the Domain Controller remains restricted to privileged accounts.

## Validation & Testing

Access was tested by logging in as different users and verifying:

Successful access to authorized folders

Access denied to unauthorized folders

<img width="1058" height="802" alt="access success client B" src="https://github.com/user-attachments/assets/1bb1de66-bdab-48a3-9f54-227220c8f21d" />
<img width="1182" height="795" alt="access denied client" src="https://github.com/user-attachments/assets/409f24e0-5295-4337-856b-def3ecb746a5" />


## Skills Demonstrated

Active Directory administration

Identity and Access Management (IAM)

Role-Based Access Control (RBAC)

Least privilege enforcement

Windows file sharing (SMB, NTFS)

Remote Desktop authorization

Troubleshooting authentication and authorization issues

Built and documented as part of hands-on IAM skill development.
