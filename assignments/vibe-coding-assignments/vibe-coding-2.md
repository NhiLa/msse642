# Vibe Coding Assignment 2 — Authentication Failures (A07:2025)
 
## 1. Vibe Coding Tool: Claude
 
For this assignment, I used **Claude** (claude.ai) as my vibe coding tool. I chose it because:
 
- It generates complete, interactive front-end applications from a plain-English description with no local setup required on my Mac.
- The artifact output renders live in the browser instantly.
- I can iterate by describing changes conversationally, which made it easy to refine each scenario incrementally until the behavior matched what I wanted.
Compared to Week 3, where I used Replit, Claude felt faster for a self-contained HTML demo since the artifact was live and testable immediately in the chat window.
 
---
 
## 2. Description of the Program

I built a **three-scenario interactive demo**. Each scenario has a tab at the top, and within each tab, the left panel shows a vulnerable server implementation while the right panel shows the secure equivalent.
 
**Scenario 1 - Brute Force Login:** The user selects a password from a dropdown (including one correct password hidden among decoys) and clicks to simulate a login POST request. On the vulnerable side, the server accepts unlimited login attempts with no lockout; an attacker can eventually find the correct password by trying them all. On the secure side, the server tracks failed attempts per IP address and locks the account after 5 failures, returning '429 Too Many Requests.'
 
**Scenario 2 - Weak Password Policy:** The user tries to register with various passwords, including top-10 breached passwords like "123456" and "password." The vulnerable server accepts any password 3+ characters long and stores it as an MD5 hash. The secure server rejects passwords found in breach databases (via HaveIBeenPwned), enforces complexity rules, and stores accepted passwords with bcrypt at cost factor 12.
 
**Scenario 3 - Broken "Remember Me" Token:** The user selects a forged remember-me cookie (e.g. 'remember_99') and sends it to the server. The vulnerable server decodes the user ID directly from the token string, making it trivially guessable and forgeable, including for the admin account. The secure server stores cryptographically random 64-character tokens in a database and looks them up on each request; forged tokens are always rejected with '401 Unauthorized.'
 
**Live demo:** 

