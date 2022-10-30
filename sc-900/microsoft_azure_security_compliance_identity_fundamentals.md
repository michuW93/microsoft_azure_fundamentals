microsoft_azure_security_compliance_identity_fundamentals SC-900

# SC-900
Tutorial based on Vlad Catrinescu tutorial

![alt text](https://github.com/michuW93/microsoft_azure_fundamentals/blob/master/sc-900/images/security_cloud.png?raw=true)


Some responsibilities are always retained by the customer!
* information and data,
* devices
* accounts and identities

# Spear phishing
Spear phishing is like phising but targeted. Spear phishing is an email or electronic communications scam <b>targeted towards a specific individual, organization or business</b>. Often intended to steal data for malicious purposes. </br>
This is how it works: <b>An email arrives, apparently from a trustworthy source, but instead it leads the unknowing recipient to a bogus website full of malware (or website with login page which looks exactly the same as real website e.g Facebook)</b>. These emails often use clever tactics to get victims' attention. For example, the FBI has warned of spear phishing scams where the emails appeared to be from the National Center for Missing and Exploited Children.

# Dictionary attack - brute force attack
A dictionary attack is a method of breaking into a password-protected computer, network or other IT resource by <b>systematically entering every word in a dictionary as a password</b>. A dictionary attack can also be used in an attempt to find the key necessary to decrypt an encrypted message or document.

# password spraying
Password Spraying is a variant of what is known as a brute force attack. In a traditional brute force attack, the perpetrator attempts to gain unauthorized access to a single account by guessing the password repeatedly in a very short period of time. Most organizations have employed countermeasures, commonly a lock-out after three to five attempts. In a Password Spraying attack, the attacker circumvents common countermeasures (e.g., account lock out) by “spraying” the same password across many accounts before trying another password. <b>so here instead of using milions of passwords for single account we try small batch of passwords for multiple accounts</b>

# Coin miners (cryptojacking)
affected computer mines for Cryptocurrency for the hacker, affected computers only notice a decrease in performance

# Zero trust methodology
Zero Trust is a security framework requiring all users, whether in or outside the organization’s network, to be authenticated, authorized, and continuously validated for security configuration and posture before being granted or keeping access to applications and data. Zero Trust assumes that there is no traditional network edge; networks can be local, in the cloud, or a combination or hybrid with resources anywhere as well as workers in any location.

The main concept behind the zero trust security model is <b>"never trust, always verify,”</b> which means that devices should not be trusted by default, even if they are connected to a permissioned network such as a corporate LAN and even if they were previously verified. ZTNA is implemented by establishing <b>strong identity verification, validating device compliance prior to granting access, and ensuring least privilege access to only explicitly authorized resources.</b>

# Defence in depth
in army:
Defence in depth (also known as deep defence or elastic defence) is a military strategy that seeks to delay rather than prevent the advance of an attacker, buying time and causing additional casualties by yielding space. Rather than defeating an attacker with a single, strong defensive line, defence in depth relies on the tendency of an attack to lose momentum over time or as it covers a larger area. 

but quite similar in IT:
The idea behind the defense in depth approach is to defend a system against any particular attack using several independent methods. <b>It is a layering tactic (eg. physical control, compute control, network control etc.),</b> conceived by the National Security Agency (NSA) as a comprehensive approach to information and electronic security. The term defense in depth in computing is inspired by a military strategy of the same name, but is quite different in concept. The military strategy revolves around having a weaker perimeter defense and intentionally yielding space to buy time, envelop, and ultimately counter-attack an opponent, whereas the information security strategy simply involves multiple layers of controls, but not intentionally ceding ground (cf. honeypot.)

# Modern authentication
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals/blob/master/sc-900/images/modern_authentication.png?raw=true)

a modern Identity Provider offers Single Sign On(<b>SSO</b>)

# Six Key privacy principles
* control - we will put you in control of your privacy with easy-to-use tools and clear choices
* transparency - we will be transparent about data collection and use
* security - string security and encryption
* strong legal protections - we will respect your local privacy laws
* no content-based targeting - we will not use your email, chat, files, etc to target ads to you
* benefits to you - when we do collect data, we will use it to benefit you and to make your experiences better

In <b>Service Trust Portal</b> you can find Audit Reports, Security Assessments, Pen test results etc and more informations on how 
Microsoft manages security, privacy and compliance

![alt text](https://github.com/michuW93/microsoft_azure_fundamentals/blob/master/sc-900/images/auth_methods.png?raw=true)

# Azure AD B2B
Azure Active Directory (Azure AD) B2B collaboration is a feature within External Identities that lets you invite guest users to collaborate with your organization.
With B2B collaboration, you can securely share your company's applications and services with external users, while maintaining control over your own corporate data.
Work safely and securely with external partners, large or small, even if they don't have Azure AD or an IT department.

# Azure AD B2C
Azure Active Directory B2C provides business-to-customer identity as a service. 
Your customers use their preferred social, enterprise, or local account identities to get single sign-on access to your applications and APIs.
It's for custom apps when you let customer to log into your app via google, facebook etc.

# Multi-Factor Authentication (MFA)
MFA requires more than one form of verification sth you know or sth you have or biometrics.
Passwords, SMS and Voice calls are considered the least secure MFA methods but still better then no MFA!

# Azure AD Password Protection
It automatically blocks <b>global banned password list (e.g P@$$w0rd)</b> and <b>custom banned password list</b> so you are not allow to set password from lists because they are weak

# Azure AD Self service password reset (SSPR)
you can reset password without any contact with helpdesk etc.

# Azure AD Access Reviews
used to remove permissions of users who no longer need access to a resource

# Azure AD Entitlement Management
it lets to create a catalog of permissions so e.g when new team join into project they don't need to find one by one permission

Azure Active Directory (Azure AD) entitlement management is an identity governance feature that enables organizations to manage
identity and access lifecycle at scale, by automating access request workflows, access assignments, reviews, and expiration.

Employees in organizations need access to various groups, applications, and SharePoint Online sites to perform their job. 
Managing this access is challenging, as requirements change. New applications are added or users need more access rights. 
This scenario gets more complicated when you collaborate with outside organizations. 
You may not know who in the other organization needs access to your organization's resources,
and they won't know what applications, groups, or sites your organization is using.

Azure AD entitlement management can help you more efficiently manage access to groups, applications, and SharePoint Online sites 
for internal users, and also for users outside your organization who need access to those resources.

# Azure AD Privileged Identity
Privileged Identity Management (PIM) is a service in Azure Active Directory (Azure AD) that enables you to manage, control, and monitor access
to important resources in your organization. These resources include resources in Azure AD, Azure, and other Microsoft Online Services 
such as Microsoft 365 or Microsoft Intune.

E.g when someone request admin permission then mail is send to some list of users so it increases visibility

# Azure AD Identity Protection
Identity Protection uses the learnings Microsoft has acquired from their position in organizations with Azure Active Directory,
the consumer space with Microsoft Accounts, and in gaming with Xbox to protect your users. 
Microsoft analyses trillions of signals per day to identify and protect customers from threats. 
Identity Protection allows organizations to accomplish three key tasks:

* Automate the detection and remediation of identity-based risks.
* Investigate risks using data in the portal.
* Export risk detection data to other tools.

The signals generated by and fed to Identity Protection, can be further fed into tools like Conditional Access to make access decisions,
or fed back to a security information and event management (SIEM) tool for further investigation.

# Azure Network Security Groups (NSG)
filter network traffic to/from Azure resources in an Azure Virtual Network
(Azure Firewall is working on other layers (3-7) so between internet and Azure Virtual Network)

# Azure Bastion
When you connect from Azure Portal to VM then you can choose RDP, SSH or Bastion.
PaaS managed service, provides secure and seamless RDP/SSH connectivity to your VM directly from the Azure Portal (over TLS).
No public IP or special tool needed on your virtual machines. It guarantees protection against port scanning protects against zero-day exploits

# Azure Key Vault
Could service for securely storing and accessing secrets.
All secrets are encrypted, so when you put sth inside it's encrypted, when you take it out it's decrypted. Key is generated per Key Vault

# Cloud Security Posture Management (CSPM)
Cloud Security Posture Management (CSPM) is a market segment for IT security tools that are designed to identify misconfiguration issues and compliance risks
in the cloud. An important purpose of CSPM programming is to continuously monitor cloud infrastructure for gaps in security policy enforcement.

# SIEM (Azure Sentinel)
Security information and event management (SIEM) is a set of tools and services that combine security events management (SEM)
and security information management (SIM) capabilities to enable analysts to review log and event data, understand and prepare for threats,
and retrieve and report on log data.

# SOAR (Azure Sentinel)
Security orchestration, automation and response (SOAR) is a collection of software programs developed to bolster an organization’s cybersecurity posture.
A SOAR platform enables a security analyst team to monitor security data from a variety of sources, 
including security information and management systems and threat intelligence platforms.

# XDR (Microsoft 356 Defender and Azure Defender)
Extended Detection and Response (XDR) is the next evolution of endpoint detection and response (EDR).
XDR takes a holistic approach to threat detection and response that streamlines security data ingestion, analysis, and prevention and remediation workflows 
across an organization’s entire security stack. 
With a single console to view and act on threat data, XDR enables security teams to effortlessly uncover hidden and advanced threats, 
and automate even complex, multi-step responses across their security technology stacks. XDR is often categorized into two types, open XDR and native XDR.



# Q&A
1. <b>The Microsoft Cloud Adoption Framework for Azure</b> provides best practices from Microsoft employees, partners, and customers, including tools and guidanace to assist in an Azure deployment.
2. <b>Customer Lockbox</b> is used to identify, hold, and export electronic information that might be used in an investigation.
3. You can manage Microsoft Intune by using the <b>Microsoft Endpoint Manager admin center</b>
4. Which score measures an organization's progress in completing actions that help reduce risks associated to data protection and regulatory standards? <b>Compliance score</b>
5. What do you use to provide real-time integration between Azure Sentinel and another security source? <b>a connector</b>
6. Which Microsoft portal provides information about how Microsoft cloud services comply with regulatory standard, such as International Organization for
Standardization (ISO)?  Microsoft Service Trust Portal 
7. In the shared responsibility model for an Azure deployment, what is Microsoft solely responsible for managing? the management of the physical hardware
8. <b>Control and Transparency</b> are the keys privacy principles of Microsoft
9. In the Microsoft Cloud Adoption Framework for Azure, which two phases are addressed before the Ready phase? Plan and Define Strategy
10. <b>Security baselines for Azure</b> provides benchmark recomendations and guidenance for protecting Azure services.
11. Which three statements accurately describe the guiding principles of Zero Trust? Use identity as the primary security boundary, Always verify the permissions of a user explicitly and Always assume that the user system can be breached. 
12. What can you use to provide a user with a two-hour window to complete an administrative task in Azure? conditional access policies
13. Azure AD Password Protection detects and blocks known weak passwords and their variants, and can also block additional weak terms that are specific to your organization.
With Azure AD Password Protection, default global banned password lists are automatically applied to all users in an Azure AD tenant. To support your own business and security needs, you can define entries in a custom banned password list.
14. Azure Active Directory (Azure AD) access reviews enable organizations to efficiently manage group memberships, access to enterprise applications, and role assignments.
15. Conditional Access policies are enforced after first-factor authentication is completed.
16. Microsoft Defender for Identity is a cloud-based security solution that leverages your on-premises Active Directory signals to identify, detect, and investigate advanced threats, compromised identities, and malicious insider actions directed at your organization.
17. Which Azure Active Directory (Azure AD) feature can you use to provide just-in-time (JIT) access to manage Azure resources? Azure AD Privileged Identity Management (PIM) 
18. Which Microsoft 365 feature can you use to restrict communication and the sharing of information between members of two departments at your organization?
 information barriers
19. When you register an application through the Azure portal, an application object and service principal are automatically created in your home directory or tenant.
20. MFA is enabled in security defaults in Azure Active Directory
21. You have an Azure subscription.
You need to implement approval-based, time-bound role activation.
What should you use? Azure Active Directory (Azure AD) Privileged Identity Management (PIM)
22. When security defaults are enabled for an Azure Active Directory (Azure AD) tenant, which two requirements are enforced? Each correct answer presents a complete solution.
    Administrators must always use Azure Multi-Factor Authentication (MFA) and Azure Multi-Factor Authentication (MFA) registration is required for all users.
23. Which three tasks can be performed by using Azure Active Directory (Azure AD) Identity Protection?
    Automate the detection and remediation of identity based-risks, Investigate risks that relate to user authentication, Create and automatically assign sensitivity labels to data.
24. What are two capabilities of Microsoft Defender for Endpoint? automated investigation and remediation and attack surface reduction
25. Security defaults make it easy to protect your organization with the following preconfigured security settings:
    *Requiring all users to register for Azure AD Multi-Factor Authentication.
    * Requiring administrators to do multi-factor authentication.
    * Blocking legacy authentication protocols.
    * Requiring users to do multi-factor authentication when necessary.
    * Protecting privileged activities like access to the Azure portal.
26. Which Microsoft portal provides information about how Microsoft cloud services comply with regulatory standard, such as International Organization for
    Standardization (ISO)? <b>Microsoft Service Trust Portal</b>
