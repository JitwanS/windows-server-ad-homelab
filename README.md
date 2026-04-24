# windows-server-ad-homelab
Windows Server 2022 Active Directory home lab with AD DS, Group Policy, file shares, and delegated administration


Windows Server 2022 Active Directory Home Lab
A self-directed lab project documenting the design and build of a functional Windows Server 2022 Active Directory environment, deployed on VMware Workstation Pro. The objective was to develop hands-on experience with the core components of enterprise IT infrastructure: identity, access, policy, and shared services.

Environment
ComponentDetailsHypervisorVMware Workstation ProDomain ControllerWindows Server 2022 Standard Evaluation (Desktop Experience)ClientWindows 10 Pro EvaluationDomainlab.localNetworkIsolated VMware LAN Segment, 192.168.10.0/24
Topology
    ┌─────────────────────────┐          ┌──────────────────────────┐
    │  DC01                   │          │  CLIENT01                │
    │  Windows Server 2022    │◄────────►│  Windows 10 Pro          │
    │  192.168.10.10          │  labnet  │  192.168.10.50           │
    │  AD DS / DNS            │          │  Domain-joined           │
    └─────────────────────────┘          └──────────────────────────┘

Components Implemented
Active Directory

Forest and domain (lab.local) created from scratch, including AD DS and DNS
Static IP addressing scheme across Domain Controller and clients
Hierarchical Organizational Unit structure separating users by department (IT, Finance, HR)
Security groups (GG-Finance, GG-HR, GG-IT, GG-Helpdesk) for role-based access
Client workstation joined to the domain with a custom computer OU (Workstations)

Group Policy

Control Panel access restrictions targeted at the Finance OU
Desktop wallpaper standardization applied domain-wide through the Departments OU
Automated Z: drive mapping via Group Policy Preferences, replacing manual drive mapping
Policies scoped by both user and computer configuration as appropriate

File Services

Shared folder \\DC01\CompanyFiles hosted on the Domain Controller
Layered permissions using Share and NTFS controls:

Finance folder accessible only to GG-Finance
HR folder accessible only to GG-HR
Public folder accessible to all Domain Users


Drive mapping automatically applied at login through Group Policy

Delegated Administration

GG-Helpdesk security group delegated password reset and account unlock rights on the HR OU
Custom delegation on the lockoutTime property for unlock permissions
RSAT (Remote Server Administration Tools) installed on CLIENT01 to perform delegated administration from the workstation, matching a real helpdesk operational workflow
Delegation verified against the principle of least privilege: helpdesk users can perform authorized tasks on the HR OU but cannot modify OUs, reset passwords outside their delegated scope, or access Domain Admin functions


Tools and Technologies

VMware Workstation Pro
Windows Server 2022 (AD DS, DNS)
Windows 10 Pro
Active Directory Users and Computers (ADUC)
Group Policy Management Console (GPMC)
Remote Server Administration Tools (RSAT)
PowerShell with the ActiveDirectory module
Command-line utilities: gpresult, gpupdate, nslookup, ipconfig, net use


Status
Initial build is complete. The environment is functional and has been used to validate each component end-to-end, including domain join, GPO application, permission enforcement, and delegated administration from the client.
