# Project: ALUMNI CONNECT – STUDENT & ALUMNI ENGAGEMENT PLATFORM

- **Industry:** Education / EdTech  
- **Project Type:** B2C Salesforce CRM implementation for student-alumni networking  
- **Target Users:** Students, Alumni, College Career Services, Administrators  

---

## 1.1 Problem Statement

Colleges and universities often struggle to maintain strong engagement between alumni and current students. Networking, mentorship, and placement opportunities are fragmented, and there is no centralized platform for alumni-student interactions. This leads to missed opportunities for career guidance, internships, and funding support.

To address this, the institution wants to implement a Salesforce CRM–based Alumni Connect Platform to:

- Automate alumni and student registration and profile management  
- Enable alumni-student networking and mentorship programs  
- Manage events, job postings, and career support activities  
- Provide dashboards to track engagement and outcomes  

---

## 1.2 Use Cases

### Alumni Management
- Maintain alumni profiles with education, career, and expertise details.  
- Segment alumni based on industry, graduation year, and location.  

### Student Engagement
- Students can search for alumni mentors based on career interest.  
- Enable direct communication (chat/email scheduling) with alumni.  

### Event Management
- Schedule alumni meets, webinars, and mentorship sessions.  
- Send automated SMS/email invites and reminders.  

### Job & Internship Opportunities
- Alumni can post job openings and internships.  
- Students can apply directly through the portal.  

### Donations & Fundraising
- Track alumni contributions and donations.  
- Generate receipts and acknowledgments automatically.  

### Reporting
- Dashboard for alumni-student interactions.  
- Track number of mentorship sessions, job referrals, and events.  
- Monitor fundraising contributions and engagement trends.  

---

## 1.3 Phase 1 — Problem Understanding & Industry Analysis

**Goal:** Understand networking challenges, define scope & success criteria.  

**Steps:**
1. **Requirement Gathering:**
   - Students want to connect with alumni for mentorship, guidance, job referrals.  
   - Alumni want to engage with their alma mater (events, donations, networking).  
   - Admin wants a single platform to manage alumni & student data.  
2. **Stakeholder Analysis:** Students, Alumni, College Admins, Placement Officers.  
3. **Business Process Mapping:** Current system is manual (spreadsheets, emails).  
4. **Use Case Examples:**  
   - Alumni directory search  
   - Student–alumni chat/connection requests  
   - Event invitations (Webinars, Reunions)  
   - Donation management  
5. **AppExchange Exploration:** Check for existing community templates / Nonprofit Cloud apps.  

**Deliverables:** Problem statement doc, user stories (e.g., “As a student, I want to search alumni by industry so I can find mentors”).  

---

## 1.4 Phase 2 — Org Setup & Configuration

**Goal:** Prepare Salesforce org with users, profiles, permissions for alumni & students.  

**Steps:**
1. **Edition:** Education Cloud (preferred) or Sales Cloud + Community.  
2. **Company Profile:** Set timezone, currency (for donations), locale.  
3. **Users & Licenses:**
   - Admin  
   - Alumni Coordinator (staff)  
   - Students (Community users)  
   - Alumni (Community users)  
4. **Profiles & Permission Sets:**  
   - Alumni Profile (read/write personal info, view events, donations)  
   - Student Profile (search alumni, request connection, join events)  
   - Admin Profile (full access)  
5. **Roles & Hierarchy:**  
   - Admin > Alumni Coordinator > Alumni/Students  
6. **OWD & Sharing Rules:**  
   - Alumni & Students private by default  
   - Sharing rules to allow “Connections”  
7. **Sandbox Setup:** Developer sandbox for build, UAT for testing  

**Deliverables:** Org ready with profiles, roles, and login policies.  

---

## 1.5 Phase 3 — Data Modeling & Relationships

**Goal:** Design objects for alumni, students, connections, and events.  

**Objects & Fields:**
- **Alumni** (Custom Object or Contact Record Type)  
  - Fields: Name, Graduation Year, Course, Current Employer, Designation, Industry, Location.  
- **Student** (Custom Object or Contact Record Type)  
  - Fields: Name, Batch, Course, Area of Interest, Career Goals.  
- **Connection Request** (Custom Object)  
  - Fields: Student, Alumni, Status (Pending/Accepted/Rejected), Request Date.  
- **Event** (Standard Campaign or Custom Object)  
  - Fields: Title, Date, Mode (Online/Offline), Participants.  
- **Donation** (Opportunity Object)  
  - Fields: Alumni, Amount, Date, Purpose.  

**Relationships:**
- Student ↔ Alumni (via Connection Request object).  
- Alumni ↔ Event (many-to-many via Campaign Members).  

**Deliverables:** ER diagram, field list, sample records.  

---

## 1.6 Phase 4 — Process Automation (Admin)

**Goal:** Automate connection approvals, event registrations, and notifications.  

**Steps:**
1. **Flows:**  
   - Student sends connection request → notify Alumni.  
   - Alumni accepts → update status + notify Student.  
2. **Approval Process:** Admin approval for some connections (optional).  
3. **Email Alerts:**  
   - Notify Alumni when new event is scheduled.  
   - Notify Students when Alumni accepts their request.  
4. **Event Automation:** Auto-create “Event Participants” when users register.  

**Deliverables:** Flows, notifications, approval processes tested.  

---

## 1.7 Phase 5 — Apex Programming (Developer)

**Goal:** Extend automation with custom logic.  

**Possible Apex Use Cases:**
- Trigger: Auto-create donation acknowledgment record when Opportunity = Closed Won.  
- Trigger: Auto-update “Active Connections Count” on Student & Alumni objects.  
- Batch Apex: Send monthly engagement summary to alumni.  
- Future/Queueable Apex: Handle bulk connection requests asynchronously.  

**Deliverables:** Apex triggers & classes with test coverage.  

---

## 1.8 Phase 6 — User Interface Development

**Goal:** Build engaging alumni & student portal.  

**Steps:**
1. **Community / Experience Cloud Site:**  
   - Branded “Alumni Connect Portal”.  
   - Navigation: Alumni Directory, Events, Donations, Connections.  
2. **Lightning Record Pages:**  
   - Alumni Profile page showing employment, interests, donations.  
   - Student Profile page with interests & achievements.  
3. **Custom LWCs:**  
   - “Find Alumni” search filter (by batch, industry, location).  
   - “Request Connection” button.  
   - “Event Registration” component.  

**Deliverables:** Portal mockups, record pages, LWC components.  

---

## 1.9 Phase 7 — Integration & External Access

**Goal:** Allow external apps to connect with Salesforce.  

**Examples:**
- Integrate LinkedIn API → auto-fetch alumni work history.  
- Payment Gateway integration → handle alumni donations.  
- Zoom/MS Teams integration → auto-generate links for online events.  

**Deliverables:** Integration plan, API contracts, configured Named Credentials.  

---

## 1.10 Phase 8 — Data Management & Deployment

**Goal:** Manage alumni/student data and release changes smoothly.  

**Steps:**
1. Import alumni & student lists via Data Loader.  
2. Deduplicate alumni records (using matching rules).  
3. Setup backups (weekly export).  
4. Deployment: Git + SFDX, change sets for metadata migration.  

**Deliverables:** Clean data, deployment plan.  

---

## 1.11 Phase 9 — Reporting, Dashboards & Security Review

**Goal:** Measure engagement & donations, ensure security.  

**Reports/Dashboards:**
- Active Alumni by Year/Industry.  
- Connection Requests (Pending vs Accepted).  
- Event Participation Trends.  
- Donations by Year & Purpose.  

**Security:**
- Restrict donation info (only Admin can view).  
- Field-level security for sensitive fields (email, phone).  
- Audit Trail & IP login restrictions.  

**Deliverables:** Reports, dashboards, security checklist.  

---

## 1.12 Phase 10 — Final Presentation & Demo Day

**Goal:** Showcase Alumni Connect platform end-to-end.  

**Steps:**
1. Demo scenario: Student searches → sends request → Alumni accepts → event participation → donation record.  
2. Pitch slide deck: Problem → Solution → Demo → Impact.  
3. Handoff documentation for Admins & Users.  
4. Collect feedback from mentor & refine.  

**Deliverables:** Demo deck, walkthrough recording, handoff docs.  
