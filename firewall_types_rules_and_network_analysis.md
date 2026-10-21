# Firewall Types, Firewall Rules, and Network Analysis

## Table of Contents

1. [Introduction to Firewalls](#1-introduction-to-firewalls)
2. [Types of Firewalls](#2-types-of-firewalls)
3. [Firewall Rules and Policies](#3-firewall-rules-and-policies)
4. [Understanding Rule Processing](#4-understanding-rule-processing)
5. [Firewall Threats and Limitations](#5-firewall-threats-and-limitations)
6. [Network Analysis and Threat Detection](#6-network-analysis-and-threat-detection)
7. [Firewall Change Control](#7-firewall-change-control)
8. [Practical Examples](#8-practical-examples)
9. [Security Best Practices](#9-security-best-practices)
10. [Knowledge Check](#10-knowledge-check)
11. [Key Takeaways](#11-key-takeaways)
12. [Glossary](#12-glossary)

---

# 1. Introduction to Firewalls

A **firewall** is a security control that monitors and controls incoming and outgoing network traffic according to predefined security rules.

Firewalls help protect networks, servers, computers, and applications from unauthorized access and malicious traffic.

They can be implemented as:

- Hardware appliances.
- Software applications.
- Cloud-based services.
- Virtual network appliances.
- Built-in operating system features.

## 1.1 Why Are Firewalls Necessary?

Firewalls help organizations:

- Block unauthorized network connections.
- Restrict access to sensitive services.
- Control inbound and outbound traffic.
- Reduce exposure to network-based attacks.
- Enforce network segmentation.
- Log suspicious connections.
- Support security monitoring and incident investigation.

**Important:** A firewall is only one layer of security. It cannot independently prevent every attack, especially those involving compromised accounts, malicious insiders, vulnerable applications, or traffic that appears legitimate.

---

# 2. Types of Firewalls

Firewall technologies have evolved as network threats have become more sophisticated.

## 2.1 Packet-Filtering Firewalls

A **packet-filtering firewall** evaluates packets using network-layer and transport-layer information.

Typical inspection fields include:

- Source IP address.
- Destination IP address.
- IP protocol.
- Source port.
- Destination port.
- Interface and traffic direction.

The firewall compares these fields against configured rules and permits or denies the packet.

### Example

Suppose a firewall has the following rule:

| Source | Destination | Protocol | Destination Port | Action |
|---|---|---|---|---|
| Any | Web server | TCP | 443 | Allow |

This rule permits matching TCP traffic to the web server on port 443, commonly used for HTTPS.

### Advantages

- Fast packet processing.
- Relatively simple configuration.
- Low resource requirements.
- Useful for basic network access control.

### Limitations

- Traditional packet filtering does not fully inspect application content.
- It may not recognize malicious payloads inside permitted traffic.
- Stateless filtering does not inherently understand whether a packet belongs to an established connection.

## 2.2 Application-Layer Firewalls

An **application-layer firewall** examines application-level traffic, such as HTTP requests.

It may inspect:

- HTTP methods and headers.
- URLs and request parameters.
- Application protocols.
- Suspicious request patterns.
- Known application attack signatures.

A specialized example is a **Web Application Firewall (WAF)**, which protects web applications against certain HTTP-based attacks.

### Example

A web server receives an unusually large number of suspicious HTTP requests. A suitably configured WAF may detect and block the requests based on rate limits, signatures, or application-specific security rules.

### Advantages

- More detailed application-level inspection.
- Can detect some attacks that basic packet filters cannot identify.
- Can enforce application-specific policies.

### Limitations

- Requires appropriate application-aware configuration.
- Can introduce latency and consume additional resources.
- Cannot guarantee protection against every application vulnerability.

**Note:** Application-layer firewalls and WAFs are related but not identical. A WAF specifically focuses on HTTP-based web applications, while application-aware firewall capabilities can cover a broader range of protocols.

## 2.3 Circuit-Level Gateways

A **circuit-level gateway** evaluates connection establishment and session-related information.

Depending on its implementation, it may check:

- Whether a connection follows expected setup procedures.
- Source and destination information.
- Whether a session meets configured policy.
- Connection-related state.

Once a connection is approved, the gateway may allow the session to proceed without deeply inspecting every application payload.

### Advantages

- Can control session establishment.
- Can reduce exposure to unauthorized connections.
- May require fewer resources than extensive application inspection.

### Limitations

- Does not necessarily inspect application payloads.
- May not detect malicious content inside an otherwise permitted session.

## 2.4 Proxy Firewalls

A **proxy firewall** acts as an intermediary between a client and a destination server.

Instead of allowing a direct client-to-server connection, the client communicates through the proxy. The proxy establishes or manages the corresponding connection to the destination.

### Basic communication flow

```text
Client
  |
  | Request
  v
Proxy Firewall
  |
  | Inspected and authorized request
  v
Internet Server
  |
  | Response
  v
Proxy Firewall
  |
  | Response returned to client
  v
Client
```

### Common functions

- Request filtering.
- User-based access control.
- Content inspection.
- Logging.
- Caching.
- Hiding internal client addresses from destination servers.

### Advantages

- Centralized control of client requests.
- Can enforce detailed access policies.
- Can provide additional application-level inspection.

### Limitations

- Can introduce latency.
- May become a performance bottleneck.
- Requires careful configuration and maintenance.

## 2.5 Stateful Inspection Firewalls

A **stateful firewall** tracks the state of network connections.

It maintains a connection or state table containing information such as:

- Source and destination IP addresses.
- Source and destination ports.
- Protocol.
- Connection state and relevant timers.

When a client inside a network initiates an allowed connection, the firewall records the connection state. It can then recognize legitimate response traffic associated with that connection.

### Example

A user inside a business network initiates an HTTPS connection to a website.

1. The outbound connection is evaluated against the firewall policy.
2. If permitted, the firewall records its state.
3. The website sends response packets.
4. The firewall checks whether the packets match the tracked connection.
5. Legitimate response traffic can be permitted according to the firewall's policy.

### Advantages

- Understands connection context.
- Allows legitimate return traffic without requiring a separate broad inbound rule for every response packet.
- Provides more protection than basic stateless filtering.

### Limitations

- State tables consume memory and processing resources.
- Resource exhaustion can affect firewall availability.
- Stateful inspection alone does not provide comprehensive application or malware detection.

## 2.6 Next-Generation Firewalls (NGFWs)

A **Next-Generation Firewall (NGFW)** combines traditional firewall capabilities with additional security functions.

Depending on the product and configuration, an NGFW may provide:

- Stateful inspection.
- Application identification and control.
- Deep packet inspection.
- Intrusion prevention system (IPS) capabilities.
- Malware detection or integration with threat intelligence.
- VPN support.
- User-identity-based policies.
- Security logging and reporting.

### Deep Packet Inspection (DPI)

Deep packet inspection examines packet contents beyond basic IP addresses, ports, and protocols, subject to the available visibility and encryption.

DPI can help identify application behavior and suspicious content. However, encrypted traffic generally requires suitable decryption or other visibility mechanisms for inspection of its protected payload.

### Advantages

- Consolidates several security capabilities.
