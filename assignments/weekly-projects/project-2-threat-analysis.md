# Project 2: Secure Design Document & Threat Model Assessment
## Georgia Hiking Club (GHC) Web Application
 
---
 
## Part 1: Secure Design Document
 
### 1.1 Project Description
The Georgia Hiking Club (GHC) is a volunteer-run, nonprofit organization based in Atlanta, Georgia, that organizes guided hiking trips for members with varying fitness levels, both locally and internationally. The club's entire operation (membership management, event registration, trip leader coordination, and payment collection) is conducted through a single web application, making it the organization's most critical asset. The application supports three distinct user roles (Guest, Member, and Administrator/Trip Leader), each with different levels of access to data and functionality. The application also handles a payment portal for membership dues and paid excursions, adding financial data to its sensitive information profile.

### 1.2 Organization Description
The Georgia Hiking Club is a registered non-profit with no physical office and no paid staff. The organization is governed by volunteers, including a Chief Technology Officer (CTO) who is responsible for maintaining the web server and web application. Funding comes from annual member dues and business sponsorships. Because the club operates entirely online and handles both personal health information (medical conditions, fitness notes) and financial transactions (membership fees, trip payments), it faces security obligations comparable to a small business handling sensitive personal data. 
