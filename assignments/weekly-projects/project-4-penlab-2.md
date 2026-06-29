# Project 4 - Penetration Testing, Part 2

## Part 1: Website Penetration Testing Procedure

### Summary Table

| PHASE | DESCRIPTION | TOOLS |
| --- | --- | --- |
| Website Penetration Testing: Information Gathering (Ch 14) | In this phase, the penetration tester collects as much information as possible about the Hiking Club web application before attempting any attacks. This includes identifying the web server technology, frameworks, directories, hidden pages, and user input fields. For the Hiking Club, this is especially important given that it stores sensitive member data including medical conditions, payment information, and fitness notes. The goal is to map out the attack surface before any active testing begins. | DirBuster |
| Website Penetration Testing: Gaining Access (Ch 15) | In this phase, the penetration tester attempts to exploit vulnerabilities discovered during the information gathering phase. For the Hiking Club, this includes testing for SQL injection on the login and payment portal, cross-site scripting (XSS) on member profile fields, and brute force attacks on the authentication page (which the club has already been compromised by once). The goal is to simulate what a real attacker would do to gain unauthorized access to sensitive member data. | OWASP ZAP |

---

### Tool Description and Analysis

#### DirBuster
**Vendor Website:** https://www.kali.org/tools/dirbuster/

DirBuster is a multi-threaded Java application designed to brute force directories and file names on web servers. It works by sending HTTP requests to a target web server using a wordlist of common directory and file names, revealing hidden or unlinked pages that may not be publicly accessible. This makes it particularly useful for uncovering administrative panels, backup files, or configuration files left exposed on the server.

DirBuster is included in the default installation of Kali Linux 2019 and can be launched directly from the application menu.

For the Hiking Club application, DirBuster would be used to map out all directories and files on the web server, including any hidden admin panels used by administrators to manage members, trips, and payments. Since the Hiking Club stores sensitive data such as medical conditions and payment history, discovering unprotected or misconfigured directories could reveal serious vulnerabilities. For example, an exposed `/admin` or `/payments` directory could allow an attacker to access or modify member data without authentication.

---

#### OWASP ZAP
**Vendor Website:** https://www.zaproxy.org/

OWASP ZAP (Zed Attack Proxy) is a free, open-source web application security scanner maintained by the Open Web Application Security Project (OWASP). It acts as a proxy between the browser and the web application, intercepting and analyzing all traffic to identify security vulnerabilities such as SQL injection, cross-site scripting (XSS), and broken authentication. ZAP includes both automated scanning and manual testing tools, making it suitable for both beginners and experienced penetration testers.

OWASP ZAP is included in the default installation of Kali Linux 2019.

For the Hiking Club application, OWASP ZAP would be used to perform both automated and manual penetration testing on the authentication page, member profile forms, and payment portal. Given that the club was previously compromised via a brute force attack on the login page, ZAP's authentication testing features would be particularly valuable. Additionally, ZAP's active scanner would test all input fields, such as member registration forms and trip leader notes, for SQL injection and XSS vulnerabilities that could expose confidential medical information or payment data stored in the system.
