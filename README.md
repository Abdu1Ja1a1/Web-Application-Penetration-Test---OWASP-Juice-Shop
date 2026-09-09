# OWASP Juice Shop — Security Assessment

A simulated penetration test / incident investigation against [OWASP Juice Shop](https://owasp.org/www-project-juice-shop/), a deliberately vulnerable web application used for security training.

📄 **[Full PDF Report](./OWASP_Juice_Shop_Security_Assessment_Writeup.pdf)**

## Environment

| | |
|---|---|
| **App** | OWASP Juice Shop (Docker image: `bkimminich/juice-shop`) |
| **Platform** | Docker Desktop, Windows |
| **Host port** | 3007 |
| **Date started** | 04/08/2026 |
| **Tools used** | Docker Desktop, browser dev tools, Burp Suite, curl |

More detail in [environment-setup.md](./environment-setup.md).

## Methodology

- Deployed Juice Shop locally via Docker Desktop.
- Performed manual reconnaissance of the application (navigation, API endpoints, page source, product reviews).
- Attempted a series of vulnerabilities spanning multiple OWASP Top 10 categories.
- Monitored container logs during each attack to note what would be visible from an operations/monitoring standpoint.
- Used Burp Suite to intercept, inspect, and manipulate HTTP traffic, including a brute-force attack via Intruder.
- Documented each finding using a consistent format, including detection notes and remediation steps.

## Findings Summary

| # | Vulnerability | Severity | Category | Status |
|---|---|---|---|---|
| 1 | [SQL Injection — Login Bypass](./findings/01-sql-injection-login-bypass.md) | High | A05 — Injection | Confirmed |
| 2 | [DOM-Based Cross-Site Scripting (XSS)](./findings/02-dom-xss-search.md) | Medium | A05 — Injection | Confirmed |
| 3 | [Broken Access Control (IDOR) — Basket Endpoint](./findings/03-idor-basket-endpoint.md) | Medium | A01 — Broken Access Control | Confirmed |
| 4 | [Sensitive Data Exposure — Unprotected FTP Directory](./findings/04-ftp-directory-exposure.md) | High | A02 — Security Misconfiguration | Confirmed |
| 5 | [Weak Admin Password (Brute Force)](./findings/05-brute-force-admin-password.md) | High | A07 — Authentication Failures | Confirmed |
| 6 | [Weak Security Question (Password Reset)](./findings/06-weak-security-question.md) | Medium | A07 — Authentication Failures | Confirmed |

## Key Takeaway

This exercise covered four distinct OWASP Top 10 categories — Injection, Broken Access Control, Security Misconfiguration, and Authentication Failures — using a mix of manual testing, browser dev tools, and automated tooling (Burp Suite Intruder).

A recurring theme across findings was the **lack of structured HTTP access logging**. Several attacks (SQLi, DOM XSS, IDOR, brute force) would be difficult to detect after the fact in this environment specifically because request-level logs weren't available — even though the underlying attacks themselves are well-documented and detectable in properly instrumented systems.

This reinforced a key operational lesson: **exploitability and detectability are separate concerns.** A system can be vulnerable in ways that also happen to be invisible to whoever is watching it — which is exactly the kind of gap a systems/SRE engineer should be looking to close through better logging, monitoring, and alerting design.

## Repo Structure

```
owasp-juiceshop-security-assessment/
├── README.md
├── OWASP_Juice_Shop_Security_Assessment_Writeup.pdf
├── environment-setup.md
├── findings/
│   ├── 01-sql-injection-login-bypass.md
│   ├── 02-dom-xss-search.md
│   ├── 03-idor-basket-endpoint.md
│   ├── 04-ftp-directory-exposure.md
│   ├── 05-brute-force-admin-password.md
│   └── 06-weak-security-question.md
└── screenshots/
    ├── finding-01/
    ├── finding-02/
    ├── finding-03/
    ├── finding-04/
    ├── finding-05/
    └── finding-06/
```

## Appendix

- **Deployment method:** Docker Desktop (GUI) — pulled the `bkimminich/juice-shop` image via the Search tab, then ran it with host port 3007 mapped to container port 3000.
- **Tools:** Docker Desktop, browser dev tools, Burp Suite Community Edition, SecLists (`xato-net-10-million-passwords-1000.txt`)
