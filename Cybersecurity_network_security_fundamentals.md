# Cybersecurity Fundamentals: Authorization, Network Types, Wi-Fi Security, and Network Attacks

> **Level:** Beginner to Intermediate  
> **Domain:** Cybersecurity and Network Security  
> **Purpose:** Study notes, GitHub portfolio, and practical revision

## Table of Contents

1. [Authorization](#1-authorization)
2. [Internet, Intranet, and Extranet](#2-internet-intranet-and-extranet)
3. [Wi-Fi Router Security Protocols](#3-wi-fi-router-security-protocols)
4. [Network Attacks](#4-network-attacks)
5. [Defensive Security Controls](#5-defensive-security-controls)
6. [Practical Security Labs](#6-practical-security-labs)
7. [Knowledge Check](#7-knowledge-check)
8. [Key Takeaways](#8-key-takeaways)
9. [Glossary](#9-glossary)

---

# 1. Authorization

## 1.1 Authentication vs. Authorization

Authentication verifies the identity of a user, device, or system. Authorization determines which resources and actions that identity is permitted to access.

Imagine an office building that uses electronic keycards:

- **Authentication:** Verifies that the person has a valid identity.
- **Authorization:** Determines which rooms the person is allowed to enter.

Successfully logging in does not automatically grant unrestricted access to every resource.

| Feature | Authentication | Authorization |
|---|---|---|
| Main question | Who are you? | What are you allowed to do? |
| Purpose | Verify identity | Determine permissions |
| Examples | Passwords, biometrics, certificates, MFA | Roles, policies, access permissions |
| Typical sequence | Usually precedes access evaluation | Evaluated when access is requested |
| Failure | Identity verification fails | Requested access is denied |

### Example

A university application has three user roles:

| Resource | Student | Lecturer | Administrator |
|---|---|---|---|
| View course material | Allowed | Allowed | Allowed |
| Submit assignments | Allowed | Not normally required | Depends on policy |
| Enter grades | Denied | Allowed for assigned courses | Allowed if authorized |
| Create accounts | Denied | Denied | Allowed |
| Change security settings | Denied | Denied | Restricted to designated administrators |

These permissions are illustrative and depend on the institution's access policies.

## 1.2 Authorization as an Ongoing Process

Authorization requires continuous management as users, responsibilities, resources, and organizational requirements change.

Important activities include:

1. **Provisioning:** Grant appropriate permissions.
2. **Modification:** Update permissions when responsibilities change.
3. **Revocation:** Remove unnecessary or expired permissions.
4. **Access reviews:** Verify that existing permissions remain appropriate.
5. **Monitoring:** Investigate suspicious access and policy violations.
6. **Compliance:** Update policies to meet applicable legal and organizational requirements.

For example, when an employee leaves an organization, administrators should disable the account, revoke active sessions and tokens where applicable, remove group memberships, and review access to connected applications.

## 1.3 Authorization Models

### Role-Based Access Control (RBAC)

RBAC assigns permissions based on predefined organizational roles.

**Example:** Doctors can access assigned patient records, receptionists can manage appointments, and designated administrators can manage approved system settings.

Advantages:
- Simplifies permission management.
- Supports consistent access policies.
- Makes onboarding and role changes easier.

Limitations:
- Poorly designed roles can grant excessive permissions.
- Complex organizations may require many roles.

### Attribute-Based Access Control (ABAC)

ABAC evaluates attributes related to the user, resource, requested action, and environment.

Attributes may include:
- Department or job role.
- Resource classification.
- Device compliance.
- Time of access.
- Network location.

**Example:** A doctor can access a patient's record only when the doctor is assigned to that patient and the request satisfies the hospital's access policies.

### Mandatory Access Control (MAC)

MAC enforces centrally defined policies, often based on security labels and clearance levels.

**Example:** A classified information system permits access only when a user's clearance and the applicable security rules allow it.

### Discretionary Access Control (DAC)

DAC allows resource owners or authorized users to grant permissions to others, subject to system restrictions.

**Example:** A file owner grants a colleague read-only access to a document.

A limitation is that owners may accidentally grant access too broadly.

### Rule-Based Access Control (RuBAC)

Rule-based access control uses predefined rules to allow, deny, or restrict access.

**Example:** Administrative changes are permitted only from an approved management network during an authorized maintenance window.

The exact meaning and implementation of RuBAC can vary. Rule-based controls can coexist with RBAC and ABAC.

### Federated Identity

Federation enables an organization to trust identity assertions from another identity provider.

Common technologies include:

- **SAML 2.0:** Widely used for enterprise single sign-on.
- **OpenID Connect (OIDC):** An identity layer built on OAuth 2.0.
- **OAuth 2.0:** An authorization framework for delegated access.

Federation does not automatically grant access to every resource. The receiving application still evaluates its own authorization policies.

### Comparison of Authorization Models

| Feature | RBAC | ABAC | MAC | DAC | Rule-Based |
|---|---|---|---|---|---|
| Main basis | Roles | Attributes and context | Security labels and policies | Ownership and permissions | Defined rules |
| Flexibility | Moderate | High | Restrictive by design | High | Depends on rule design |
| Complexity | Low to high | Often high | High | Moderate | Moderate to high |
| Example | Department permissions | Context-sensitive patient access | Classified information | Shared file permissions | Time-based access |

## 1.4 Principle of Least Privilege

The principle of least privilege requires users, applications, and services to receive only the permissions necessary to perform their tasks.

Best practices:
- Assign permissions according to responsibilities.
- Separate administrative and ordinary accounts.
- Review access regularly.
- Remove unused accounts and permissions.
- Protect privileged accounts with MFA.
- Log sensitive administrative actions.

Least privilege reduces the potential impact of compromised accounts and accidental or malicious changes.

---

# 2. Internet, Intranet, and Extranet

## 2.1 Internet

The internet is a global interconnection of networks that communicate using standardized protocols such as IP and TCP.

Examples of internet services include:
- Websites and web applications.
- Email.
- Online education.
- Cloud computing.
- Video conferencing.

The internet is generally publicly accessible, but individual services may require authentication, payment, or authorization.

## 2.2 Intranet

An intranet is a private organizational network or collection of internal services intended for authorized users.

Common uses include:
- Internal announcements.
- Employee portals.
- HR and payroll systems.
- Document sharing.
- Project management.
- Organizational training resources.

Remote employees may access intranet services through a VPN, zero-trust access gateway, or another approved secure access mechanism.

## 2.3 Extranet

An extranet provides controlled access to selected organizational resources for authorized external parties, including suppliers, customers, contractors, and research partners.

Common uses include:
- Supplier portals.
- Customer support systems.
- Shared project workspaces.
- Partner collaboration.
- Order tracking.

An extranet may use a protected web portal, cloud services, or dedicated network connections.

## 2.4 Comparison

| Feature | Internet | Intranet | Extranet |
|---|---|---|---|
| Audience | General public and authorized service users | Authorized organizational users | Authorized internal and external users |
| Purpose | Global communication and services | Internal operations | Controlled external collaboration |
| Access control | Varies by service | Organization-defined | Organization-defined, including partner access |
| Example | Public university website | Employee portal | Supplier portal |

### Conceptual Diagram

```text
GLOBAL NETWORK ENVIRONMENT
|
+-- Internet
|   +-- Public websites
|   +-- Online services
|
+-- Intranet
|   +-- Internal organizational resources
|
+-- Extranet
    +-- Selected resources for approved external parties
```

**Note:** This is a conceptual illustration, not a literal physical topology. Intranets and extranets are not necessarily physically nested within the internet.

---

# 3. Wi-Fi Router Security Protocols

Wireless networks transmit data over radio waves. Appropriate security mechanisms protect network access and communications against unauthorized use.

## 3.1 WEP, WPA, WPA2, and WPA3

### WEP — Wired Equivalent Privacy

WEP is an obsolete wireless security protocol with serious cryptographic weaknesses.

**Recommendation:** Never use WEP.

### WPA — Wi-Fi Protected Access

The original WPA improved on WEP but commonly used TKIP, which is now obsolete.

**Recommendation:** Do not use the original WPA/TKIP for new deployments.

### WPA2 — Wi-Fi Protected Access 2

WPA2 commonly uses AES-CCMP to protect wireless communications.

Its main deployment modes are:

- **WPA2-Personal:** Uses a shared passphrase or pre-shared key.
- **WPA2-Enterprise:** Commonly uses IEEE 802.1X and EAP-based authentication.

WPA2 remains widely supported. Its security depends on correct configuration, credential strength, and device maintenance.

### WPA3 — Wi-Fi Protected Access 3

WPA3 improves wireless security compared with older protocols.

Key features include:
- WPA3-Personal uses Simultaneous Authentication of Equals (SAE).
- SAE improves resistance to offline password guessing compared with the traditional WPA2-Personal handshake.
- WPA3 requires Protected Management Frames for WPA3 connections.
- WPA3-Enterprise supports enhanced security options, including a 192-bit security mode.

**Recommendation:** Prefer WPA3 for compatible new deployments. Use securely configured WPA2-AES when compatibility requires it.

### Comparison

| Feature | WEP | WPA | WPA2 | WPA3 |
|---|---|---|---|---|
| Security status | Broken and obsolete | Obsolete | Still widely supported | Preferred for compatible new deployments |
| Common mechanism | RC4-based WEP | TKIP | AES-CCMP | SAE in Personal mode |
| New deployment | Never use | Never use | Compatibility alternative | Preferred where supported |

## 3.2 Enterprise Authentication and EAP-TLS

IEEE 802.1X provides port-based network access control and is commonly used with enterprise Wi-Fi.

EAP-TLS is an authentication method that uses digital certificates. When correctly configured, it supports mutual authentication between the client and authentication server.

### Authentication Flow

```text
Wireless Client
      |
      v
Wi-Fi Access Point
      |
      v
RADIUS Authentication Server
      |
      v
Certificate and Policy Validation
      |
      v
Access Granted or Denied
```

Benefits include:
- Certificate-based authentication.
- Centralized access management.
- Reduced dependence on a shared Wi-Fi password.
- Support for individual user or device credentials.

Security requirements:
- Protect private keys.
- Validate server certificates.
- Monitor certificate expiration.
- Revoke compromised certificates.
- Configure clients correctly.

## 3.3 MAC Address Filtering

A MAC address identifies a network interface at the data-link layer.

Some routers allow administrators to permit only listed MAC addresses.

However, MAC addresses can often be observed and spoofed. MAC filtering is therefore a supplementary control, not a substitute for strong wireless authentication and encryption.

## 3.4 Wireless Network Hardening

- [ ] Change default router administrator credentials.
- [ ] Enable WPA3 where supported.
- [ ] Use WPA2-AES if WPA3 is unavailable.
- [ ] Choose a long, unique Wi-Fi passphrase.
- [ ] Update router firmware.
- [ ] Disable WPS if unnecessary.
- [ ] Disable unnecessary remote administration.
- [ ] Configure a guest network.
- [ ] Isolate guest devices from internal resources.
- [ ] Use a separate IoT network where practical.
- [ ] Review connected devices and authentication logs.
- [ ] Replace routers that no longer receive security updates.

Different SSIDs do not guarantee network isolation. Isolation must be enforced through the actual network configuration.

---

# 4. Network Attacks

Network attacks may compromise confidentiality, integrity, or availability.

Understanding attack behavior helps security professionals detect suspicious activity and implement appropriate defenses.

## 4.1 Sniffing

Sniffing is the capture and inspection of network traffic.

Administrators use packet capture for troubleshooting and incident investigation. Attackers may use similar techniques to observe unauthorized communications.

### Types

**Passive sniffing:** Observes traffic without deliberately altering or redirecting it.

**Active interception:** Manipulates network behavior or traffic paths to gain access to communications.

### Common Tools

- **Wireshark:** Graphical packet analysis.
- **tcpdump:** Command-line packet capture and filtering.

### Risks

- Exposure of unencrypted credentials.
- Disclosure of sensitive information.
- Identification of network services.
- Analysis of communication patterns.

### Defenses

- Use HTTPS and other secure protocols.
- Avoid transmitting credentials in plaintext.
- Secure wireless networks.
- Protect physical network access.
- Apply network segmentation.
- Monitor suspicious traffic.
- Use VPNs where appropriate for protecting traffic over untrusted networks.

Encryption can protect application content even when packets are captured, although some metadata may remain visible.

## 4.2 Spoofing

Spoofing involves falsifying identifying information to impersonate another system, device, user, or service.

### IP Spoofing

An attacker falsifies the source IP address in a packet.

Possible impacts:
- Concealing the apparent packet source.
- Supporting certain denial-of-service attacks.
- Exploiting systems that incorrectly trust source addresses.

Defenses:
- Ingress and egress filtering.
- Source-address validation.
- Stateful firewall controls where appropriate.
- Avoiding IP addresses as the sole authentication mechanism.

Changing an IP source address does not automatically establish a TCP session or grant access to a service.

### ARP Spoofing

ARP maps IPv4 addresses to MAC addresses on a local network.

ARP spoofing involves sending misleading ARP messages that associate an IP address with an incorrect MAC address.

Possible impacts:
- Local traffic interception.
- Traffic manipulation.
- Communication disruption.

Defenses:
- Dynamic ARP Inspection where supported.
- DHCP snooping as part of a compatible switch configuration.
- Network segmentation.
- Monitoring unexpected IP-to-MAC changes.

### DNS Spoofing

DNS translates domain names into information such as IP addresses.

DNS spoofing involves providing false DNS information or manipulating DNS resolution, potentially redirecting users to malicious infrastructure.

Defenses:
- Use trusted DNS resolvers.
- Protect DNS administration.
- Apply DNSSEC validation where appropriate.
- Monitor unexpected DNS changes.
- Validate HTTPS certificates.
- Investigate certificate warnings.

DNSSEC authenticates DNS data but does not encrypt DNS queries.

### TLS and Certificate Impersonation

TLS protects communications and authenticates servers through certificates.

An attacker may attempt to impersonate a server, exploit compromised trust, or persuade users to accept an untrusted certificate.

Defenses:
- Validate certificates and hostnames.
- Keep software updated.
- Avoid bypassing certificate warnings.
- Protect certificate private keys.
- Use secure TLS configurations.

### Spoofing Comparison

| Type | Information manipulated | Possible impact | Defensive focus |
|---|---|---|---|
| IP spoofing | Source IP address | Evasion or traffic abuse | Source validation |
| ARP spoofing | IP-to-MAC mapping | Local interception | Switch protections |
| DNS spoofing | DNS data or configuration | Malicious redirection | DNS security |
| Certificate impersonation | Server identity or trust | Deceptive connections | Certificate validation |

## 4.3 Man-in-the-Middle (MITM) Attacks

A MITM attack occurs when an attacker intercepts communication between two parties and may observe or modify it without their knowledge.

### Conceptual Diagram

```text
Normal Communication:

Client <--------------------> Server


Potential MITM:

Client <------> Attacker <------> Server
```

### Typical stages

1. **Positioning:** The attacker gains a position where communications can be intercepted.
2. **Interception:** Traffic is observed or relayed.
3. **Analysis:** The attacker searches for information or opportunities.
4. **Possible manipulation:** Traffic may be modified if the necessary protections can be bypassed.

### Potential impact

- Credential theft.
- Exposure of sensitive data.
- Modification of transactions.
- Session compromise.
- Redirection to malicious services.

### Defenses

- Use correctly configured HTTPS/TLS.
- Validate certificates.
- Keep browsers and operating systems updated.
- Avoid untrusted wireless networks for sensitive activities.
- Use MFA and phishing-resistant authentication where possible.
- Protect network infrastructure.
- Monitor suspicious certificate and network configuration changes.

Correctly configured TLS protects application content against ordinary interception. A VPN does not automatically protect compromised endpoints or malicious destinations.

## 4.4 Denial-of-Service (DoS) and Distributed Denial-of-Service (DDoS)

A denial-of-service attack attempts to make a system or service unavailable to legitimate users.

A distributed denial-of-service attack uses multiple sources to overwhelm or disrupt a target.

### Comparison

| Feature | DoS | DDoS |
|---|---|---|
| Traffic sources | Commonly one source | Multiple distributed sources |
| Coordination | Often simpler | Often coordinated across many sources |
| Mitigation | May be easier to isolate | Can be more difficult to filter |
| Impact | Service disruption | Potentially large-scale service disruption |

### Major categories

**Volumetric attacks:** Attempt to consume available network bandwidth.

**Protocol attacks:** Attempt to exhaust resources used to process network protocols or maintain network state.

**Application-layer attacks:** Target application functions and consume resources such as CPU, memory, or database connections.

### Botnets

A botnet is a collection of compromised devices controlled or coordinated by an attacker.

Devices may be compromised through malware, vulnerabilities, or other methods. Command-and-control (C2/C&C) infrastructure may coordinate their activity.

### Defenses

- Rate limiting and traffic filtering.
- DDoS protection services.
- Load balancing and capacity planning.
- Content delivery networks where appropriate.
- Web application firewalls for relevant threats.
- Traffic and resource monitoring.
- Incident response planning.

A traffic spike alone does not prove a DDoS attack. Investigators should compare observed traffic with normal baselines and examine application, network, and infrastructure logs.

## 4.5 Wi-Fi Password Attacks

Wi-Fi password attacks attempt to guess or recover credentials used to access a wireless network.

Testing must be limited to networks for which explicit authorization has been obtained.

### Dictionary Attack

A dictionary attack tests candidate passwords from a prepared list.

**Defense:** Use a long, unique passphrase and avoid predictable personal information.

### Brute-Force Attack

A brute-force attack systematically tests possible password combinations.

Its feasibility depends on password length, character diversity, guessing speed, and the protocol's protections.

**Defense:** Use strong credentials and modern wireless security.

### Offline Password Guessing

In some circumstances, an attacker who obtains relevant authentication material can test password guesses offline.

This differs from repeatedly attempting to log in to a live service.

WPA2-Personal security depends significantly on passphrase strength. WPA3-Personal's SAE mechanism improves resistance to offline dictionary attacks compared with the traditional WPA2-Personal handshake.

### Rainbow Tables

Rainbow tables are precomputed structures used to accelerate the recovery of certain plaintext values from password hashes.

Their usefulness depends on the hashing scheme and available data. They are not automatically applicable to every Wi-Fi password attack.

**Important:** Hashing is not encryption. Encryption is designed to be reversible using an appropriate key, whereas secure password hashing is designed to make recovery computationally difficult.

### Wi-Fi Security Checklist

- Use WPA3 where supported.
- Otherwise use properly configured WPA2-AES.
- Choose a long, unique passphrase.
- Disable WEP and obsolete WPA/TKIP configurations.
- Update access point firmware.
- Disable WPS when unnecessary.
- Review connected devices.
- Use enterprise authentication where appropriate.

## 4.6 Port Scanning

Port scanning checks network ports to identify reachable services on a host.

Security professionals use port scanning for authorized asset discovery, attack-surface assessment, and firewall verification. Attackers may use it during reconnaissance.

### Common Ports

| Port | Common service | Security consideration |
|---|---|---|
| 21/TCP | FTP control | Traditional FTP does not protect credentials and data in transit by default |
| 22/TCP | SSH | Protect administrative access and keys |
| 25/TCP | SMTP | Secure and restrict mail-server functions |
| 53/TCP or UDP | DNS | Protect resolver and authoritative DNS services |
| 80/TCP | HTTP | Prefer HTTPS for sensitive communications |
| 443/TCP | HTTPS | Maintain secure TLS and application configuration |
| 3389/TCP | RDP | Restrict exposure and enforce strong authentication |

These are conventional port assignments. Services may use different ports, and an open port does not prove which application is running.

### Common Port States

- **Open:** A service is accepting connections or responding in a way that indicates an open port.
- **Closed:** The host is reachable, but no service is listening on that port according to the observed response.
- **Filtered:** Filtering or network conditions prevent the scanner from determining the state reliably.

### Port Scanning vs. Vulnerability Assessment

Port scanning identifies reachable ports and possible services. It does not prove that a service is vulnerable.

A fuller assessment involves:

1. Asset identification.
2. Port and service discovery.
3. Service and version verification.
4. Configuration review.
5. Vulnerability assessment.
6. Risk prioritization.
7. Remediation and retesting.

### Defenses

- Disable unnecessary services.
- Restrict management interfaces.
- Apply appropriate firewall rules.
- Patch exposed services.
- Monitor unusual connection attempts.
- Segment networks.
- Review externally exposed assets regularly.

An open port is not automatically a vulnerability. Risk depends on the service, exposure, configuration, authentication, and known weaknesses.

---

# 5. Defensive Security Controls

| Threat | Preventive controls | Detective controls | Response priorities |
|---|---|---|---|
| Unauthorized access | MFA, least privilege, access policies | Authentication logs and access reviews | Revoke compromised access |
| Sniffing | Encryption, secure Wi-Fi, segmentation | Packet analysis and network monitoring | Assess exposure and rotate affected credentials |
| Spoofing | Source validation, secure DNS, network controls | Address-change alerts and DNS logs | Correct trust settings and isolate affected systems |
| MITM | TLS validation, secure endpoints | Certificate and network anomaly monitoring | Remove interception and assess data exposure |
| DoS/DDoS | Rate limits, protective services, capacity planning | Traffic and resource monitoring | Mitigate traffic and restore availability |
| Wi-Fi password attacks | Strong credentials, WPA3/WPA2-AES | Authentication failure monitoring | Change compromised credentials |
| Unnecessary open ports | Firewalls, service minimization, patching | Asset and port monitoring | Restrict exposure and remediate weaknesses |

### Security Workflow

```text
Identify Assets
      |
      v
Identify Threats and Risks
      |
      v
Select Security Controls
      |
      v
Implement Controls
      |
      v
Validate and Monitor
      |
      v
Investigate Findings
      |
      v
Remediate and Retest
      |
      v
Continuous Improvement
```

Effective security combines prevention, detection, response, recovery, and regular review.

---

# 6. Practical Security Labs

Perform practical testing only on systems you own or are explicitly authorized to assess.

## Lab 1: Authorization and Access Control

**Objective:** Demonstrate role-based permissions.

Tasks:
1. Define student, lecturer, and administrator roles.
2. Create a permission matrix.
3. Assign permissions.
4. Test allowed and denied operations.
5. Verify that the server enforces permissions.
6. Record the results.

**Expected result:** Each role can perform only permitted operations.

## Lab 2: Wireless Security Audit

**Objective:** Review your own router's security configuration.

Tasks:
1. Identify the router model and firmware version.
2. Check the wireless security mode.
3. Verify administrator credentials.
4. Review WPS and remote-management settings.
5. Check guest-network isolation.
6. Document firmware status.
7. Recommend improvements.

**Expected result:** A documented wireless security baseline.

## Lab 3: Packet Analysis with Wireshark

**Objective:** Understand network packets and encryption.

Tasks:
1. Capture traffic from your own device or an authorized lab.
2. Identify source and destination IP addresses.
3. Examine DNS queries and responses.
4. Identify TCP connections where visible.
5. Compare observable HTTP and HTTPS traffic.
6. Document which information is visible and which is protected by encryption.
7. Save sanitized screenshots and findings.

**Expected result:** A short packet-analysis report.

Avoid capturing unrelated users' traffic or collecting credentials and personal information.

## Lab 4: Network Exposure Assessment

**Objective:** Identify services exposed by an authorized system.

Tasks:
1. Define the approved target and scope.
2. Identify the target IP address.
3. Use an appropriate scanning tool within the approved scope.
4. Record observed port states.
5. Identify expected services.
6. Compare findings with the intended configuration.
7. Restrict unnecessary services and retest.

**Expected result:** A validated report of exposed services and remediation.

## Lab 5: Network Incident Analysis

**Objective:** Investigate a simulated suspicious network event.

Scenario: A web application experiences unusual traffic and repeated authentication failures.

Tasks:
1. Record the event timeline.
2. Identify affected assets.
3. Review available authentication, web-server, and firewall logs.
4. Separate confirmed facts from hypotheses.
5. Assess confidentiality, integrity, and availability impacts.
6. Recommend containment and recovery actions.
7. Document evidence and limitations.

**Expected result:** A concise incident report.

### Lab Report Template

```markdown
# Security Lab Report

## 1. Objective
Describe the security question being investigated.

## 2. Scope and Authorization
List approved systems, addresses, and testing boundaries.

## 3. Environment
Record operating system, tool versions, and relevant configuration.

## 4. Methodology
Explain the steps performed.

## 5. Observations
Record evidence and measured results.

## 6. Findings
Describe confirmed weaknesses or behaviors.

## 7. Risk Assessment
Explain likelihood, impact, and affected assets.

## 8. Remediation
List corrective actions.

## 9. Validation
Repeat relevant tests and document results.

## 10. Limitations
Describe untested areas and uncertainties.

## 11. Conclusion
Summarize results and remaining risks.
```

---

# 7. Knowledge Check

Answer the following questions before checking the answer key.

### Questions

**1. What is the primary difference between authentication and authorization?**

A. Authentication encrypts data.  
B. Authentication verifies identity, while authorization determines permitted actions.  
C. They are identical.  
D. Authorization verifies passwords.

**2. Which model assigns permissions according to roles?**

A. DAC  
B. MAC  
C. RBAC  
D. DNS

**3. What is an intranet?**

A. A network accessible to everyone.  
B. A private organizational environment for authorized users.  
C. A type of encryption.  
D. A password management protocol.

**4. Which wireless security protocol is generally preferred for compatible new deployments?**

A. WEP  
B. WPA-TKIP  
C. WPA3  
D. Open Wi-Fi

**5. What is a key limitation of MAC filtering?**

A. MAC addresses cannot change.  
B. It encrypts all application traffic.  
C. MAC addresses can often be observed and spoofed.  
D. It replaces wireless authentication.

**6. What is the primary purpose of network sniffing?**

A. Capture and inspect network traffic.  
B. Assign IP addresses.  
C. Encrypt files.  
D. Replace DNS.

**7. What distinguishes a DDoS attack?**

A. It never uses network traffic.  
B. It commonly involves multiple distributed sources.  
C. It affects only wireless networks.  
D. It is an authentication method.

**8. What does an open TCP port generally indicate?**

A. The system is definitely compromised.  
B. A service may be accepting connections.  
C. The service is necessarily vulnerable.  
D. The network is unencrypted.

**9. What does correctly configured TLS help provide?**

A. Protected communications and endpoint authentication.  
B. Automatic protection against all endpoint compromises.  
C. Automatic prevention of all DDoS attacks.  
D. Universal authorization.

**10. Which practice demonstrates least privilege?**

A. Giving everyone administrator access.  
B. Sharing one administrator password.  
C. Granting only the permissions required for assigned work.  
D. Disabling security logs.

## Answer Key

| Question | Answer | Explanation |
|---|---|---|
| 1 | B | Authentication verifies identity; authorization evaluates permissions. |
| 2 | C | RBAC associates permissions with roles. |
| 3 | B | An intranet provides restricted organizational resources. |
| 4 | C | WPA3 is generally preferred for compatible new deployments. |
| 5 | C | MAC addresses can be observed and spoofed. |
| 6 | A | Sniffing captures and analyzes traffic. |
| 7 | B | DDoS commonly uses multiple distributed sources. |
| 8 | B | An open port indicates reachability or a listening service, not necessarily a vulnerability. |
| 9 | A | Correctly configured TLS protects communications and authenticates endpoints. |
| 10 | C | Least privilege limits access to what is necessary. |

---

# 8. Key Takeaways

1. Authentication verifies identity; authorization determines permitted actions.
2. Authorization requires continuous management and access reviews.
3. RBAC, ABAC, MAC, DAC, and rule-based controls serve different purposes.
4. Internet, intranet, and extranet differ in their intended audiences and access policies.
5. WPA3 is preferred for compatible new wireless deployments; securely configured WPA2-AES remains a compatibility alternative.
6. MAC filtering is supplementary and does not replace strong wireless security.
7. Sniffing, spoofing, and MITM attacks are distinct but can overlap.
8. DoS and DDoS attacks threaten service availability.
9. Strong Wi-Fi credentials and modern security protocols reduce unauthorized access risks.
10. Port scanning identifies exposed services but does not prove that a vulnerability exists.
11. Effective security combines prevention, detection, response, recovery, and validation.
12. Practical cybersecurity testing must be authorized, scoped, and documented.

---

# 9. Glossary

| Term | Definition |
|---|---|
| Access Control | Mechanisms that determine who or what can access resources. |
| Authentication | Verification of an identity. |
| Authorization | Evaluation of permissions for a requested action or resource. |
| ABAC | Attribute-Based Access Control. |
| RBAC | Role-Based Access Control. |
| MAC | Mandatory Access Control; also means Media Access Control in networking. |
| DAC | Discretionary Access Control. |
| RuBAC | Rule-Based Access Control. |
| IAM | Identity and Access Management. |
| MFA | Multi-Factor Authentication. |
| Internet | Global interconnection of networks. |
| Intranet | Private organizational network or internal services. |
| Extranet | Controlled access to selected resources for external parties. |
| VPN | Virtual Private Network. |
| WEP | Wired Equivalent Privacy; obsolete wireless security. |
| WPA2 | Wi-Fi Protected Access 2. |
| WPA3 | Wi-Fi Protected Access 3. |
| EAP-TLS | EAP method using TLS and certificates. |
| RADIUS | Protocol commonly used for centralized network access authentication. |
| Sniffing | Capturing and inspecting network traffic. |
| Spoofing | Falsifying identifying information. |
| ARP | Address Resolution Protocol. |
| DNS | Domain Name System. |
| TLS | Transport Layer Security. |
| MITM | Man-in-the-Middle attack. |
| DoS | Denial-of-Service attack. |
| DDoS | Distributed Denial-of-Service attack. |
| Botnet | Collection of compromised devices controlled or coordinated by an attacker. |
| C2/C&C | Command-and-control infrastructure or communications. |
| Port | A transport-layer endpoint identified by a port number. |
| Port Scanning | Checking ports to discover reachable services and apparent states. |
| Least Privilege | Granting only the permissions necessary for assigned tasks. |
| Network Segmentation | Dividing a network into controlled security zones. |
| Incident Response | A structured process for investigating and handling security incidents. |

---

**End of Document**
