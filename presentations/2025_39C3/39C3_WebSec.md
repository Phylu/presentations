---
marp: true
theme: 39c3
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

- Hi 👋, I'm Janosch, on Congress you can find me as **Dr. Affe**
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

# A02:2025 – Security Misconfiguration
**⬆️ #5 → #2** | Increasing as software becomes more configuration-driven

Security misconfiguration is when a system, application, or cloud service is set up incorrectly from a security perspective, creating vulnerabilities.

## Do's
- **Repeatable Hardening Process:**  Automate secure deployment with identical configuration across all environments
- **Minimal Platform:**  Remove unused features, components, permissions and samples
- **Automated Verification:**  Continuously verify configurations across all environments

---

# A03:2025 – Software Supply Chain Failures
**🆕 NEW at #3** | Expansion of A06:2025 Vulnerable and Outdated Components

Software supply chain failures are breakdowns or other compromises in the process of building, distributing, or updating software. They are caused by vulnerabilities or malicious changes in third-party code, tools, or other dependencies that the system relies on.

## Do's
- **Maintain Software Bill of Materials (SBOM):**  Track and manage all dependencies
- **Continuous Monitoring:**  Automate vulnerability scanning
- **Trusted Sources Only:**  Obtain signed components from official sources

---

# A04:2025 – Cryptographic Failures
**⬇️ #2 → #4**

All data in transit should be encrypted at the transport layer (OSI layer 4). Beyond securing the transport layer, it is important to determine what data needs encryption at rest as well as what data needs extra encryption in transit (at the application layer, OSI layer 7).

## Do's
- **Classify Encrypt Data:**  Label sensitive data, encrypt at rest and in transit
- **Strong Key Management:**  Use hardware security modules for sensitive keys
- **Strong Encryption:**  Use strong standard alogrithms and avoid deprecated cryptographic functions

---

# A05:2025 – Injection
**⬇️ #3 → #5**

An injection vulnerability is a system flaw that allows an attacker to insert malicious code or commands into a program’s input fields, tricking the system into executing the code or commands as if it were part of the system. This can lead to truly dire consequences.

<!--
Payloads:

SQLI:
' OR '1' = '1

XSS:
<script>alert('You got Hacked!')</script>

 -->

## Do's
- **Use Safe APIs:**  Prefer parameterized interfaces or ORMs that avoid interpreters
- **Separate Data from Commands:**  Never concatenate user input into queries
- **Positive Server-Side Validation:**  Validate input against allowed patterns, escape special characters when needed

---

# A06:2025 – Insecure Design
**⬇️ #4 → #6**

Insecure design represents different weaknesses, expressed as "missing or ineffective control design." An insecure design cannot be fixed by a perfect implementation as needed security controls were never created to defend against specific attacks.

## Do's
- **Secure Development Lifecycle:**  Involve security in feature planning and user stories
- **Threat Modeling & Testing:**  Model critical flows (authentication, access control, business logic) and write tests validating threat resistance
- **Architectural Segregation:**  Separate system/network tiers and isolate tenants

---

# A07:2025 – Authentication Failures
**➡️ Remains #7** | Previously "Identification and Authentication Failures"

When an attacker is able to trick a system into recognizing an invalid or incorrect user as legitimate, this vulnerability is present.

## Do's
- **Implement MFA & Strong Passwords:**  Enforce MFA, check for breached credentials
- **Rate Limiting & Attack Detection:**  Limit failed attempts, log all failures, prevent account enumeration with consistent error messages
- **Secure Session Management:**  Use a premade, well-trusted system to handle authentication, identity, and session management

---

# A08:2025 – Software or Data Integrity Failures
**➡️ Remains #8**

Software and data integrity failures relate to code and infrastructure that does not protect against integrity violations. Examples include relying on plugins, libraries, or modules from untrusted sources without sufficient integrity verification during runtime (CDNs) or at build time (CI/CD).

## Do's
- **Verify Integrity with Digital Signatures:**  Use digital signatures to verify software/data is from expected source and unaltered
- **Trusted Dependencies & Internal Repositories:**  Use internal and trusted sources
- **Secure CI/CD Pipeline:**  Ensure segregation/access control in CI/CD

---

# A09:2025 – Logging & Alerting Failures
**➡️ Remains #9** | Previously "Security Logging and Monitoring Failures"

Without logging and monitoring, attacks and breaches cannot be detected, and without alerting it is very difficult to respond quickly and effectively during a security incident.

## Do's
- **Comprehensive Security Logging:** Log all login, access control, input validation failures with user context, ensure sufficient retention for forensic analysis
- **Effective Alerting:**  Alert on suspicious behavior and security events and ensure alerts trigger appropriate action
- **Incident Response Plan:**  Follow incident response process, train developers to recognize attacks, ensure quick detection and response

---

# A10:2025 – Mishandling of Exceptional Conditions
**🆕 NEW at #10**

Mishandling exceptional conditions in software happens when programs fail to prevent, detect, and respond to unusual and unpredictable situations, which leads to crashes, unexpected behavior, and sometimes vulnerabilities.

## Do's
- **Fail Closed & Centralized Exception Handling:**  Catch all exceptions globally and roll back transactions
- **Rate Limiting & Resource Quotas:**  Throttle and limit to prevent denial of service
- **Secure Error Responses & Monitoring:**  Display generic and log detailed errors

---

<!-- _class: chapter -->

# More OWASP Top 10

<!--
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
-->
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
<!--
---

# Security of LLMs

## Groundhog Day?

- **Injections:** LLMs are susceptible to injection attacks
- **Filtering & Santization:** Allow-listing tools like `find` may allow attacks using the option `-xargs`
- **Interesting Design Decisions:** YOLO-mode in Google Gemini-CLI
- **Issues in generated Code:** Suggestion to store session tokens in shared preferences which does not offer secure storage, even as storing was not necessary as all information was already (securely) stored by the used library (personal experience)
- **Hallucinated Package Names:** Manually check your code!
-->
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

- **Connect at Congress:** DECT 5009
- **Source Code:** https://github.com/Phylu/vulnerable-click-game
- **Resources:** https://owasp.org, licensed under a Creative Commons Attribution 3.0 Unported License