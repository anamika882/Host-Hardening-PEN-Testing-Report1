README Summary (GitHub)
Exploiting & Securing FUEL CMS (CVE-2018-16763) — Host Hardening + Penetration Test

This project demonstrates an end-to-end security assessment of FUEL CMS v1.4.1, focusing on CVE-2018-16763, a pre-auth Remote Code Execution (RCE) flaw caused by unsanitized input passed to eval() via the fuel/pages/select/?filter= endpoint. The work follows a realistic workflow: system hardening → vulnerability reintroduction → exploitation → post-exploitation → mitigations without patching.

Key Objectives

Harden a Linux web server to simulate a production-like baseline.

Reintroduce a known CVE for controlled security testing.

Exploit the CMS RCE remotely and demonstrate impact.

Perform post-exploitation discovery and privilege escalation chaining.

Propose defense-in-depth mitigations that do not rely on patching.

What We Did
1) System Hardening (CentOS + Apache + PHP)

Reduced attack surface (updates, remove/disable unnecessary services).

Firewall configured to allow only essential services.

Hardened SSH access (non-root login).

Apache hardening (directory listing off, security headers).

PHP hardening (disabled dangerous functions, restricted paths, hidden errors).

Application restrictions (reduced write permissions, removed defaults).

2) Recon & Enumeration

Network and service discovery using recon tooling.

Web directory enumeration identified sensitive endpoints.

robots.txt revealed /fuel, leading to confirmation of FUEL CMS deployment.

3) Exploitation: CVE-2018-16763 (Pre-auth RCE)

Leveraged the vulnerable filter parameter to execute arbitrary commands remotely.

Confirmed code execution and enumerated application directories and configs.

4) Credential Discovery → Lateral Access (SSH)

Retrieved database credentials from configuration artifacts and validated access.

Used the obtained credentials to gain SSH access as a low-privileged user.

5) Post-Exploitation: Pickle Deserialization RCE Chain

Discovered a local Python Flask service using unsafe pickle.loads() on user-controlled input.

Generated a malicious payload and achieved a reverse shell, demonstrating how insecure deserialization can be chained after initial compromise.

Mitigation Strategy (Without Patching)

A defense-in-depth approach to break the exploit chain even if the CMS remains vulnerable:

Input filtering/validation for the vulnerable parameter.

Disable dangerous PHP functions (including eval() and command execution functions).

Restrict access to sensitive directories (e.g., via .htaccess rules).

Enforce SELinux policies to constrain file and process permissions.

Deploy a Web Application Firewall (mod_security) to block known exploit patterns.

Skills Demonstrated

Secure configuration & host hardening

Web app testing and vulnerability exploitation

Reconnaissance and enumeration methodology

Post-exploitation analysis and attack chaining

Secure-by-design thinking (mitigation beyond patching)

Disclaimer

This repository is for educational and defensive security research. Do not use these techniques on systems you do not own or have explicit permission to test.

Short “About” (for GitHub repo description)

Host hardening + pen test of FUEL CMS v1.4.1 (CVE-2018-16763): recon → pre-auth RCE → post-exploitation chain → defense-in-depth mitigations without patching. 

2-line CV Bullet Version

Conducted a host-hardening and penetration testing project on FUEL CMS v1.4.1 (CVE-2018-16763), demonstrating pre-auth RCE, post-exploitation discovery, and attack chaining via insecure deserialization. 

Proposed non-patching mitigations including input validation, disabling dangerous PHP functions, access restrictions, SELinux controls, and WAF rules (mod_security)
