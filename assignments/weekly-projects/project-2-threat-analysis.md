# Project 2: Secure Design Document & Threat Model Assessment
## Georgia Hiking Club (GHC) Web Application
 
---
 
## Part 1: Secure Design Document
 
### 1.1 Project Description
The Georgia Hiking Club (GHC) is a volunteer, nonprofit organization based in Atlanta, Georgia, that organizes guided hiking trips for members with varying fitness levels, both locally and internationally. The club's entire operation (membership management, event registration, trip leader coordination, and payment collection) is conducted through a single web application. The application supports three distinct user roles (Guest, Member, and Administrator/Trip Leader), each with different levels of access to data and functionality. The application also handles a payment portal for membership dues and paid excursions, adding financial data to its sensitive information profile.

### 1.2 Organization Description
The Georgia Hiking Club is a registered non-profit with no physical office and no paid staff. The organization is governed by volunteers, including a Chief Technology Officer (CTO) who is responsible for maintaining the web server and web application. Funding comes from annual member dues and business sponsorships. Because the club operates entirely online and handles both personal health information (medical conditions, fitness notes) and financial transactions (membership fees, trip payments), it faces security obligations comparable to a small business handling sensitive personal data. 

### 1.3 Deployment Environment
The GHC web application will be deployed on a cloud-hosted infrastructure using a major cloud provider (e.g., AWS or Azure). Since this is a voluntary organization, it lacks a physical office and operates with a limited IT staff. Therefore, this choice eliminates the burden of hardware maintenance while simultaneously providing built-in tools for network segmentation, access control, and system monitoring.

The deployment will consist of at minimum two network tiers:
- A Front End Web Server, accessible from the internet.
- A Backend Database Server, accessible only from the Front End Web Server and never directly from the internet.

A cloud-managed firewall (security group/network access control list) will enforce traffic rules between these two tiers. All traffic from the public internet to the web server will be encrypted via TLS (HTTPS). Backups and audit logs will be stored in isolated cloud storage separate from the production environment.

### 1.4 Secure Concepts Applicable to the Application
**Authentication & Password Policy:** The project description explicitly notes that the site was previously compromised via a brute-force attack due to weak password enforcement. Strong password policies, multi-factor authentication, account lockout mechanisms, and rate-limiting of login attempts are necessary controls.

**Authorization & Role-Based Access Control (RBAC):** The application has three meaningfully different permission levels — Guest, Member, and Administrator (Trip Leader / System Admin). Strict enforcement of these boundaries is critical. For example, a regular member must never be able to view another member's medical records or access the treasury portal.

**Sensitive Personal Data (PII & Medical Information):** Member profiles contain medical conditions and performance notes that are confidential. These fields require encryption at rest, strict access controls limiting visibility to Trip Leaders and System Admins.

**Financial Data & Payment Portal:** The payment portal collects membership dues and excursion fees. This introduces PCI-DSS-adjacent concerns: financial data must be encrypted in transit and at rest, and access to the treasury portal must be tightly restricted to System Admins only.

---
 
## Part 2: Hiking Club Threat Model Assessment
 
---
 
### Deliverable 2A: Architecture Diagram

![GHC Network Architecture Diagram](../images/Architecture Diagram.drawio.png)

**IP Address Summary:**
 
| Component            | Public IP      | Private IP   |
|----------------------|----------------|--------------|
| Front End Web Server | 203.0.113.10   | 10.0.1.10    |
| Backend DB Server    | *(none)*       | 10.0.2.20    |
| Guest Browser        | varies         | N/A          |
| Member Browser       | varies         | N/A          |
| Admin Browser        | varies         | N/A          |

---
 
### Deliverable 2B: STRIDE Threat Model
 
#### 1. Spoofing — Impersonation of Legitimate Users

The GHC application was previously compromised via a brute-force attack on login credentials, confirming that spoofing is a real and demonstrated threat. The application currently lacks enforced password complexity, multi-factor authentication, and account lockout. All of which are standard countermeasures for spoofing. Mitigation requires enforcing strong passwords, implementing MFA (especially for admin roles), adding login rate limiting and account lockout after repeated failures, and logging all authentication events for review.

#### 2. Tampering — Unauthorized Modification of Data

The application description explicitly anticipates database tampering as a risk. Tampered data in this application could take many forms: a malicious actor might modify a member's event completion record to erase a pattern of no-shows, alter a medical record to hide a condition from trip leaders, manipulate payment records to avoid dues, or tamper with waiting list positions to gain access to a popular trip. Mitigations include prepared statements / parameterized queries to prevent SQL injection, strict input validation on all user-supplied fields, integrity hashing of critical records, immutable audit logs stored outside the production database, and file integrity monitoring on the web server.

