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

# Azure AD has role based system control
role is pre-packaged permissions for one or multiple apps
