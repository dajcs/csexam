# Authentication vs Authorization

## General Concepts


**01. What is the purpose of authentication in computer security**

The purpose of authentication in computer security is to verify the identity of a user, device, or system. It ensures that the entity requesting access is exactly who or what they claim to be, acting as the first line of defense against unauthorized access.

**02. What is the purpose of authorization in access control systems**

The purpose of authorization is to determine what an authenticated user, device, or system is allowed to do. Once an identity is verified, authorization dictates the specific resources, files, data, or applications the entity is permitted to access or modify based on predefined rules and policies.

**03. What are the fundamental differences between authentication and authorization**

The fundamental difference is their primary function: authentication is about *identity* ("Who are you?"), whereas authorization is about *permissions* ("What are you allowed to do?"). Authentication challenges the user to prove their identity, while authorization checks the system's rules to grant or deny access to a specific resource.

**04. What is the correct sequence of authentication and authorization in security systems**

Authentication must always precede authorization. A system must first confirm the identity of the user (authentication) before it can evaluate what permissions and access rights that specific identity possesses (authorization).

## Authentication

**05. What are the three main authentication factors**

The three main authentication factors are:
1. **Knowledge Factor**: Something you know (e.g., a password, passphrase, or PIN (Personal Identification Number)).
2. **Possession Factor**: Something you have (e.g., a smartphone, a hardware token, or a smart card).
3. **Inherence Factor**: Something you are (e.g., biometric markers like a fingerprint, retina scan, or facial recognition).

**06. How does the authentication process work**

The process typically begins with a user presenting an identifier (like a username). The user then provides a credential (like a password) to prove they own that identifier. The system transmits this credential to an IdP (Identity Provider) or checks it against a secure local database. If the provided credential matches the stored credential, the system verifies the identity and the authentication process is successful.

**07. What are the main authentication protocols**

The main authentication protocols include:
* **SAML (Security Assertion Markup Language)**: Used primarily for web-based single sign-on.
* **OIDC (OpenID Connect)**: A modern identity layer built on top of the OAuth (Open Authorization) framework.
* **Kerberos**: A network authentication protocol that uses tickets to allow nodes to prove their identity securely.
* **LDAP (Lightweight Directory Access Protocol)**: Used to authenticate against directory services.
* **RADIUS (Remote Authentication Dial-In User Service)**: Used for network access and remote user authentication.

**08. What is the difference between single-factor and multi-factor authentication**

SFA (Single-Factor Authentication) requires only one form of verification to verify an identity (typically just a username and password). MFA (Multi-Factor Authentication) requires two or more pieces of evidence from different factor categories (e.g., a password combined with a fingerprint, or a PIN (Personal Identification Number) combined with a code sent to a mobile device). MFA is significantly more secure than SFA.

**09. What HTTP status code indicates authentication failure**

The HTTP (Hypertext Transfer Protocol) status code that indicates authentication failure is **401 Unauthorized**. This means the client must authenticate itself to get the requested response.

## Authorization

**10. What are the main authorization models**

The main authorization models include:
* **RBAC (Role-Based Access Control)**
* **ABAC (Attribute-Based Access Control)**
* **MAC (Mandatory Access Control)**
* **DAC (Discretionary Access Control)**

**11. How does Role-Based Access Control (RBAC) work**

In an RBAC (Role-Based Access Control) system, access permissions are assigned to specific roles within an organization rather than to individual users. Users are then assigned to one or more roles. For example, a user assigned the "Administrator" role will inherit all the read, write, and delete permissions associated with that role, while someone with a "Viewer" role will only inherit read permissions.

**12. How does Attribute-Based Access Control (ABAC) differ from RBAC**

While RBAC (Role-Based Access Control) grants access based solely on static, predefined roles, ABAC (Attribute-Based Access Control) makes dynamic access decisions based on a combination of multiple attributes. These can include user attributes (e.g., department, security clearance), resource attributes (e.g., data sensitivity), and environmental attributes (e.g., time of day, geographic location, or IP address). This makes ABAC much more granular and flexible than RBAC.

**13. What are the components of authorization**

Authorization typically involves several core components:
* **Subject**: The user, device, or API (Application Programming Interface) requesting access.
* **Object/Resource**: The file, database, or system endpoint being accessed.
* **Action**: The operation being attempted (e.g., read, write, execute, delete).
* **Policy**: The set of rules dictating whether the action should be allowed.
In modern architectures, this is often managed by a PEP (Policy Enforcement Point) which intercepts the request, and a PDP (Policy Decision Point) which evaluates the policy to grant or deny access.

**14. What HTTP status code indicates authorization failure**

The HTTP (Hypertext Transfer Protocol) status code that indicates authorization failure is **403 Forbidden**. This means the client's identity is known (they are authenticated), but they do not have the required permissions to access the specific resource.

## Security Best Practices

**15. What are the advantages of implementing both authentication and authorization**

Implementing both ensures a robust "Defense in Depth" strategy. It enforces the Principle of Least Privilege, ensuring users are who they say they are, and that they can only access the exact data necessary to do their jobs. This minimizes the impact of insider threats, protects sensitive data, ensures regulatory compliance, and provides clear accountability and traceability in audit logs.

**16. What are the security risks of skipping authentication or authorization**

If you skip authentication, your system is entirely public; anyone, including malicious actors, can enter and act anonymously. If you skip authorization, an authenticated user (such as an entry-level employee or a compromised standard account) would have unrestricted access to everything in the system, leading to privilege escalation, unauthorized data modification, and severe data breaches.

**17. How do authentication and authorization work together to protect systems**

They work together as a two-step gatekeeping mechanism. Think of a secure corporate building: Authentication is the front door security guard checking your ID badge to ensure you work for the company and can enter the lobby. Authorization is the electronic lock on the server room door that checks your badge again and ensures you have the specific clearance to enter that restricted room. Together, they keep outsiders out and ensure insiders stay in their permitted lanes.

**18. What is the difference between a username/password and biometric authentication**

A username/password combination relies on a knowledge factor (something you know). It can easily be forgotten, guessed, phished, or shared with unauthorized individuals. Biometric authentication relies on an inherence factor (something you are), utilizing unique physical or behavioral traits like a fingerprint, voiceprint, or facial structure. Biometrics are tied directly to the physical person, making them much harder to steal, share, or duplicate compared to passwords.
