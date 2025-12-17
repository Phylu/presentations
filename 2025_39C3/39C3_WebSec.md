---
marp: true
theme: janosch-braukmann
paginate: true
---

<!-- _class: lead -->
<!-- _paginate: false -->
<!-- _footer: 09. December 2025 -->

# Pwn Basics
## Hacking Web Applications for Beginners

---

# Today's Agenda

- Introduction
- “Hack Me If You Can” – Virtual - Escape Game
- OWASP Top 10
- Hacking a Vulnerable Web Application


---

<!-- _class: chapter -->

# Introduction

---

# Who am I?

- Hi 👋, I'm Janosch
- Playing around reading passwords through JavaScript when ~16 years old
- Founded Security Startup in 2017
- Worked with and contributed to several OSS security tools
- Working as Infrastructure Team Lead & Information Security Officer for an insurance

## Contact
[https://github.com/Phylu](https://github.com/Phylu)

---

# Disclaimer

## Hacking is like Sex…

- Exciting
- Needs some Stamina
- Few people talk about it openly
- There are many variations
- More fun if not done alone

## But most importantly:
* **You need consent! 🤝**

---

<!-- _class: chapter -->

# Hack Me If You Can

---

<!-- _class: cta -->

# Hack Me If You Can

https://janosch-braukmann.de:8000

---

<!-- _class: chapter -->

# OWASP Top 10 2025-RC1

---

# OWASP Top Ten

> The OWASP Top Ten lists are awareness documents, meant to bring awareness to the most critical risks of whichever topic they cover. They are not meant to be a complete list, only a starting place.

---

# Information Security Goals

```
    Confidentiality
          / \
         /   \
        /     \
       /       \
      /   CIA   \
     /___________\
Integrity     Availability
```

## The CIA Triad
- **Confidentiality:**  Data is only accessible to authorized parties
- **Integrity:**  Data remains accurate and unaltered
- **Availability:**  Systems and data are accessible when needed

---

# What\'s New in OWASP Top 10 2025?

![OWASP Top 10 2025 Mappings](assets/owsap_top10_2025_mappings.png)

## 🆕 Two New Categories
- **A03: Software Supply Chain Failures** (expanded from Vulnerable Components)
- **A10: Mishandling of Exceptional Conditions** (completely new)

---

# What\'s New in OWASP Top 10 2025?

![OWASP Top 10 2025 Mappings](assets/owsap_top10_2025_mappings.png)

## 📊 Major Position Changes
- **Security Misconfiguration**: #5 → #2 (⬆️ 3 positions)
- **Cryptographic Failures**: #2 → #4 (⬇️ 2 positions)
- **Injection**: #3 → #5 (⬇️ 2 positions)

---

# What\'s New in OWASP Top 10 2025?

![OWASP Top 10 2025 Mappings](assets/owsap_top10_2025_mappings.png)

## 🔄 Consolidations
- **Vulnerable and Outdated Components** merged into new Software Supply Chain Failures (#3)
- **SSRF** merged into Broken Access Control (#1)

---

# A01:2025 – Broken Access Control
**➡️ Remains #1** | SSRF merged into this category

Access control enforces policy such that users cannot act outside of their intended permissions. Failures typically lead to unauthorized information disclosure, modification or destruction of all data, or performing a business function outside the user's limits.

## Do's
- **Deny by Default:**  Except for public resources, deny by default
- **Server-Side Enforcement:**  Implement access control in trusted server-side code
- **Log & Rate Limit:**  Log failures, alert on repeated attempts, and rate limit API access

---

# A01:2025 – Broken Access Control

| Date | Issue | Problem | Solution |
|------|-------|---------|----------|
| 2022 | [**Optus API**](https://www.authgear.com/post/what-is-broken-access-control-vulnerability-and-how-to-prevent-it) | Legacy API with missing authorization checks exposed millions of customer records | Object-level authorization on API calls, retire legacy endpoints, rate limiting |
| 2023 | [**Confluence**](https://confluence.atlassian.com/security/cve-2023-22515-broken-access-control-vulnerability-in-confluence-data-center-and-server-1295682276.html) | Setup endpoints allowed unauthenticated attackers to create new admin accounts | Restrict admin functions, disable exposed setup endpoints |
| 2024 | [**Kia Connected Cars**](https://www.authgear.com/post/what-is-broken-access-control-vulnerability-and-how-to-prevent-it) | Weak authorization between user accounts and vehicles allowed remote car control using only a license plate | Bind vehicles to authenticated owners, server-side authorization for vehicle actions |

<!-- 
- Many attacks are chained using different attack vectors. So don't be surprised if you think that an example fits into multiple categories
-->

---

# A02:2025 – Security Misconfiguration
**⬆️ #5 → #2** | Increasing as software becomes more configuration-driven

Security misconfiguration is when a system, application, or cloud service is set up incorrectly from a security perspective, creating vulnerabilities.

## Do's
- **Repeatable Hardening Process:**  Automate secure deployment with identical configuration across all environments
- **Minimal Platform:**  Remove unused features, components, permissions and samples
- **Automated Verification:**  Continuously verify configurations across all environments

---

# A02:2025 – Security Misconfiguration

| Date | Issue | Problem | Solution |
|------|-------|---------|----------|
| 2024 | [**Football Australia**](https://cloudsecurityalliance.org/blog/2025/06/09/the-2024-football-australia-data-breach-a-case-of-misconfiguration-and-inadequate-change-control) | AWS access keys embedded in website source code, 127 S3 buckets publicly accessible | Never hardcode credentials, use secrets management, block public S3 access |
| 2024 | [**Dell Partner Portal**](https://x-phy.com/what-we-can-learn-from-the-massive-dell-data-breach-that-exposed-49-million-records/) | Unsecured API allowed 5,000+ requests/min, exposing 49M customer records | Implement rate limiting, API authentication, anomaly detection |
| 2024 | [**Volkswagen EV Cloud**](https://www.computing.co.uk/news/2025/security/volkswagen-leak-exposes-personal-info) | Misconfigured S3 bucket left data for ~800k car owners publicly accessible | Secure S3 by default, enforce least‑privilege IAM |

---

# A03:2025 – Software Supply Chain Failures
**🆕 NEW at #3** | Expansion of A06:2025 Vulnerable and Outdated Components

Software supply chain failures are breakdowns or other compromises in the process of building, distributing, or updating software. They are caused by vulnerabilities or malicious changes in third-party code, tools, or other dependencies that the system relies on.

## Do's
- **Maintain Software Bill of Materials (SBOM):**  Track and manage all dependencies
- **Continuous Monitoring:**  Automate vulnerability scanning
- **Trusted Sources Only:**  Obtain signed components from official sources

---

# A03:2025 – Software Supply Chain Failures

| Date | Issue | Problem | Solution |
|------|-------|---------|----------|
| 2025 | [**Nx npm Packages**](https://www.theregister.com/2025/08/27/nx_npm_supply_chain_attack/) | Compromised npm token published malware stealing GitHub/SSH keys, 1,000+ tokens leaked | Require 2FA for publishing, monitor package provenance, rotate credentials |
| 2025 | [**npm Phishing Attack**](https://www.paloaltonetworks.com/blog/cloud-security/npm-supply-chain-attack/) | Phishing compromised maintainer account, 18 packages with 2.6B weekly downloads poisoned | Enable 2FA, verify npm communications, use package lock files |
| 2025 | [**Shai-Hulud Worm**](https://www.cisa.gov/news-events/alerts/2025/09/23/widespread-supply-chain-compromise-impacting-npm-ecosystem) | Self-replicating worm compromised 500+ npm packages via stolen credentials | Pin dependency versions, scan for malicious code, monitor SBOM changes |

---

# A04:2025 – Cryptographic Failures
**⬇️ #2 → #4**

All data in transit should be encrypted at the transport layer (OSI layer 4). Beyond securing the transport layer, it is important to determine what data needs encryption at rest as well as what data needs extra encryption in transit (at the application layer, OSI layer 7).

## Do's
- **Classify Encrypt Data:**  Label sensitive data, encrypt at rest and in transit
- **Strong Key Management:**  Use hardware security modules for sensitive keys
- **Strong Encryption:**  Use strong standard alogrithms and avoid deprecated cryptographic functions

---

# A04:2025 – Cryptographic Failures

| Date | Issue | Problem | Solution |
|------|-------|---------|----------|
| 2021 | [**RockYou2021 Password Dump**](https://www.authgear.com/post/cryptographic-failures-owasp) | Compilation of passwords in plaintext or with weak hashing | Always hash passwords with modern KDFs (bcrypt/Argon2/PBKDF2), enforce strong password policies |
| 2022 | [**Toyota GitHub Key Exposure**](https://www.authgear.com/post/cryptographic-failures-owasp) | Uploaded private keys and access tokens to a public GitHub repo | Centralize secret management, prevent committing secrets, enforce least-privilege access |
| 2025 | [**LastPass Vault Cracking**](https://krebsonsecurity.com/2025/03/feds-link-150m-cyberheist-to-2022-lastpass-hacks/) | Offline vault cracking due to weak master passwords and few hashing iterations | Enforce strong master passwords, increase hashing iterations, hardware-backed key storage |

---

# A05:2025 – Injection
**⬇️ #3 → #5**

An injection vulnerability is a system flaw that allows an attacker to insert malicious code or commands into a program’s input fields, tricking the system into executing the code or commands as if it were part of the system. This can lead to truly dire consequences.

## Do's
- **Use Safe APIs:**  Prefer parameterized interfaces or ORMs that avoid interpreters
- **Separate Data from Commands:**  Never concatenate user input into queries
- **Positive Server-Side Validation:**  Validate input against allowed patterns, escape special characters when needed

---

# A05:2025 – Injection

| Year | Issue | Problem | Solution |
|------|-------|---------|----------|
| 2023 | [**MOVEit Transfer SQLi**](https://unit42.paloaltonetworks.com/threat-brief-moveit-cve-2023-34362/) | Critical SQL injection exploited by Cl0p ransomware gang, 2,674+ servers exposed, mass data theft | Apply patches immediately, use parameterized queries, monitor for web shells |
| 2023 | [**Atlassian Confluence**](https://confluence.atlassian.com/security/cve-2023-22527-rce-remote-code-execution-vulnerability-in-confluence-data-center-and-confluence-server-1333990257.html) | Template injection RCE (CVSS 10), unauthenticated attacker achieves RCE | Update to patched versions, disable public access, use template sandboxing |
| 2021 | [**Log4Shell**](https://www.dynatrace.com/news/blog/what-is-log4shell/) | JNDI lookup command injection, millions of exploit attempts, still targeted in 2024 | Update Log4j, disable JNDI lookups, implement WAF rules |

---

# A06:2025 – Insecure Design
**⬇️ #4 → #6**

Insecure design represents different weaknesses, expressed as "missing or ineffective control design." An insecure design cannot be fixed by a perfect implementation as needed security controls were never created to defend against specific attacks.

## Do's
- **Secure Development Lifecycle:**  Involve security in feature planning and user stories
- **Threat Modeling & Testing:**  Model critical flows (authentication, access control, business logic) and write tests validating threat resistance
- **Architectural Segregation:**  Separate system/network tiers and isolate tenants

---

# A06:2025 – Insecure Design

| Year | Issue | Problem | Solution |
|------|-------|---------|----------|
| 2022 | [**Optus API**](https://www.upguard.com/blog/how-did-the-optus-data-breach-happen) | Public-facing API with no authentication + sequential customer IDs exposed 9.8M records | Design APIs to require authentication, use non-sequential UUIDs, isolate sensitive data access |
| 2022 | [**Kia Connected Cars**](https://samcurry.net/web-hackers-vs-the-auto-industry/) | VIN-based access control allowed remote unlock/start/location tracking of any vehicle | Design authorization to verify ownership, no predictable identifiers for access control |
| 2020 | [**Zoom Waiting Room**](https://citizenlab.ca/2020/04/zooms-waiting-room-vulnerability/) | Unapproved users received live video stream + encryption keys while in "waiting room" | Design security features to enforce isolation, don't send data before authorization is granted |

<!--
Optus / Kia - Already explained as Broken Access Control
-->

---

# A07:2025 – Authentication Failures
**➡️ Remains #7** | Previously "Identification and Authentication Failures"

When an attacker is able to trick a system into recognizing an invalid or incorrect user as legitimate, this vulnerability is present.

## Do's
- **Implement MFA & Strong Passwords:**  Enforce MFA, check for breached credentials
- **Rate Limiting & Attack Detection:**  Limit failed attempts, log all failures, prevent account enumeration with consistent error messages
- **Secure Session Management:**  Use a premade, well-trusted system to handle authentication, identity, and session management

---

# A07:2025 – Authentication Failures

| Year | Issue | Problem | Solution |
|------|-------|---------|----------|
| 2024 | [**Okta Password Bypass**](https://www.theverge.com/2024/11/1/24285874/okta-52-character-login-password-authentication-bypass) | Authentication bug allowed login without password verification for long usernames | Implement comprehensive authentication testing, monitor for anomalous login patterns |
| 2023 | [**MGM Resorts Social Engineering**](https://specopssoft.com/blog/mgm-resorts-service-desk-hack/) | Attackers  called service desk, gained admin access, deployed ransomware | Enforce identity verification at service desk, implement callback procedures, train staff on vishing |
| 2022 | [**Uber MFA Fatigue Attack**](https://www.upguard.com/blog/what-caused-the-uber-data-breach) | Attacker spammed contractor with MFA push notifications until accepted, gained full admin access | Use number-matching MFA, implement push notification rate limiting, train users on MFA fatigue attacks |

---

# A08:2025 – Software or Data Integrity Failures
**➡️ Remains #8**

Software and data integrity failures relate to code and infrastructure that does not protect against integrity violations. Examples include relying on plugins, libraries, or modules from untrusted sources without sufficient integrity verification during runtime (CDNs) or at build time (CI/CD).

## Do's
- **Verify Integrity with Digital Signatures:**  Use digital signatures to verify software/data is from expected source and unaltered
- **Trusted Dependencies & Internal Repositories:**  Use internal and trusted sources
- **Secure CI/CD Pipeline:**  Ensure segregation/access control in CI/CD

---

# A08:2025 – Software or Data Integrity Failures

| Year | Issue | Problem | Solution |
|------|-------|---------|----------|
| 2020 | [**SolarWinds Orion**](https://www.techtarget.com/whatis/feature/SolarWinds-hack-explained-Everything-you-need-to-know) | Backdor in Orion software updates, compromised 30,000+ orgs including US government | Implement code signing, verify build integrity, use Software Bill of Materials (SBOM) |
| 2023 | [**3CX Desktop App Double-Linked Attack**](https://www.wired.com/story/3cx-supply-chain-attack-times-two/) | Attack on Trading Technologies software, backdooring into 3CX VoIP app | Verify third-party software integrity, monitor workstations, supply chain security |
| 2024 | [**XZ Utils Backdoor**](https://www.crowdstrike.com/en-us/blog/cve-2024-3094-xz-upstream-supply-chain-attack/) | Trusted maintainer inserted backdoor into XZ compression library via obfuscated test files (CVSS 10) | Vet maintainers, review build processes, use reproducible builds, monitor for suspicious commits |

---

# A09:2025 – Logging & Alerting Failures
**➡️ Remains #9** | Previously "Security Logging and Monitoring Failures"

Without logging and monitoring, attacks and breaches cannot be detected, and without alerting it is very difficult to respond quickly and effectively during a security incident.

## Do's
- **Comprehensive Security Logging:** Log all login, access control, input validation failures with user context, ensure sufficient retention for forensic analysis
- **Effective Alerting:**  Alert on suspicious behavior and security events and ensure alerts trigger appropriate action
- **Incident Response Plan:**  Follow incident response process, train developers to recognize attacks, ensure quick detection and response

---

# A09:2025 – Logging & Alerting Failures

| Year | Issue | Problem | Solution |
|------|-------|---------|----------|
| 2018 | [**Marriott**](https://www.huntress.com/threat-library/data-breach/marriott-data-breach) | Attackers in  reservation system for 4 years undetected, 500M guest records stolen | Continuous monitoring, alert on anomalous database access |
| 2017 | [**Equifax**](https://www.breachsense.com/blog/equifax-data-breach/) | Expired TLS certificate disabled network monitoring for 76 days, attackers exfiltrated 147M records | Monitor certificate expiration, alert on (encrypted) traffic anomalies |
| 2020 | [**SolarWinds**](https://www.techtarget.com/whatis/feature/SolarWinds-hack-explained-Everything-you-need-to-know) | Backdoor remained undetected for 8+ months, attackers had access to 18,000+ organizations | Behavioral analytics, monitor for unusual network patterns, correlate logs across systems |

<!-- SolarWinds also mentioned before already -->

---

# A10:2025 – Mishandling of Exceptional Conditions
**🆕 NEW at #10**

Mishandling exceptional conditions in software happens when programs fail to prevent, detect, and respond to unusual and unpredictable situations, which leads to crashes, unexpected behavior, and sometimes vulnerabilities.

## Do's
- **Fail Closed & Centralized Exception Handling:**  Catch all exceptions globally and roll back transactions
- **Rate Limiting & Resource Quotas:**  Throttle and limit to prevent denial of service
- **Secure Error Responses & Monitoring:**  Display generic and log detailed errors

---

# A10:2025 – Mishandling of Exceptional Conditions

| Year | Issue | Problem | Solution |
|------|-------|---------|----------|
| 2024 | [**Apache Tomcat Auth Bypass**](https://nvd.nist.gov/vuln/detail/CVE-2024-52316) | Exception during authentication without explicit HTTP status set allowed bypass | Always set explicit failure status on exceptions, fail closed, validate all error paths |
| 2024 | [**OpenSSH Race Condition**](https://blog.qualys.com/vulnerabilities-threat-research/2024/07/01/regresshion-remote-unauthenticated-code-execution-vulnerability-in-openssh-server) | Race condition in signal handler allowed RCE | Use signal-safe functions only, implement proper synchronization |
| 2024 | [**WordPress Really Simple Security**](https://www.sitelock.com/blog/really-simple-security-plugin-exploit/) | Improper error handling in WP_REST_Response allowed authentication bypass | Validate error responses, fail closed, don't trust clients |

<!-- Again several issues mentioned before -->

---

<!-- _class: chapter -->

# Further OWASP Projects

---

# OWASP Mobile Top 10 (2024)

### M1: Improper Credential Usage (See: A02 & A04)
Hardcoded API keys, passwords, or tokens in app code/config files, or insecure credential storage on device (plaintext, weak encryption). 

### M2: Inadequate Supply Chain Security (See: A03)
Compromised third-party SDKs, libraries, or development tools in the mobile app supply chain.

### M3: Insecure Authentication/Authorization (See: A07)
Weak password policies, missing MFA, insecure session management, or client-side authorization checks.

---

# OWASP API Security Top 10 (2023)

### API1: Broken Object Level Authorization (BOLA) (See: A01)
APIs fail to validate that users can only access their own objects. 

### API2: Broken Authentication (See: A07)
Weak authentication mechanisms in APIs allow credential stuffing, brute force attacks, and token theft.

### API3: Broken Object Property Level Authorization (See: A01)
APIs expose more object properties than users should access, leading to mass assignment vulnerabilities and excessive data exposure.

---

# OWASP Top 10 for LLM Applications (2025)

### LLM01: Prompt Injection (See: A05)
Malicious prompts manipulate LLM behavior to bypass restrictions. Directly via user prompts or indirectly through external sources (documents, websites).

### LLM02: Sensitive Information Disclosure (See: A04)
LLMs inadvertently reveal sensitive data in responses such as training data, PII, credentials, and proprietary information.

### LLM03: Supply Chain Vulnerabilities (See: A03)
Risks from third-party models, datasets, and plugins. Compromised pre-trained models or poisoned datasets. Malicious plugins or extensions.

---

# Potential Attacks from the wild

**[LLM01: Prompt Injection](https://www.golem.de/news/prompt-injection-mehrere-ki-browser-mit-nur-einem-zeichen-ueberlistet-2511-202610.html)** (25.11.2025)

> HashJack is a newly discovered indirect prompt injection technique that conceals malicious instructions after the # in legitimate URLs. When AI browsers send the full URL [...] to their AI assistants, those hidden prompts get executed.

**[LLM09:2025 Misinformation](https://genai.owasp.org/llmrisk/llm092025-misinformation/)**
> Attackers experiment with popular coding assistants to find commonly hallucinated package names. Once they identify these frequently suggested but nonexistent libraries, they publish malicious packages with those names to widely used repositories. Developers, relying on the coding assistant's suggestions, unknowingly integrate these poised packages into their software. 

---

# Security of LLMs

## Groundhog Day?

- **Injections:** LLMs are susceptible to injection attacks
- **Filtering & Santization:** Allow-listing tools like `find` may allow attacks using the option `-xargs`
- **Interesting Design Decisions:** YOLO-mode in Google Gemini-CLI
- **Issues in generated Code:** Suggestion to store session tokens in shared preferences which does not offer secure storage, even as storing was not necessary as all information was already (securely) stored by the used library (personal experience)
- **Hallucinated Package Names:** Manually check your code!

---

<!-- _class: chapter -->

# OWASP Top 10 Summary

---

# OWASP Top 10 Summary

## Key Takeaways

- **Broken Access Control** remains the #1 threat
- **Supply chain security** is now a top-3 priority
- **Logging without alerting** is insufficient

## Sources & Further Reading: 
- [OWASP Top 10 2025](https://owasp.org/Top10)
- [OWASP Mobile Top 10 2024](https://owasp.org/www-project-mobile-top-10/)
- [OWASP API Security Top 10 2023](https://owasp.org/API-Security/editions/2023/en/0x11-t10/)
- [OWASP Top 10 for LLM Applications 2025](https://genai.owasp.org/llm-top-10/)

---

<!-- _class: chapter -->

# Hacking a Vulnerable Web Application

---

<!-- _class: cta -->

# Hacking a Vulnerable Web Application

[http://janosch-braukmann.de:8080](http://janosch-braukmann.de:8080
)

---

# How do I Play?

1. Log in & Play a game
2. Check out the highscore
3. See what you can break
4. Remember the OWASP Top 10

**SQL Injection:**
```
' OR '1' = '1
```

**Cros-Site Scripting:**
```
<script>alert("You got hacked!")</script>
````

---

# Stay Secure!

Source Code: https://github.com/Phylu/vulnerable-click-game

https://owasp.org, licensed under a Creative Commons Attribution 3.0 Unported License
