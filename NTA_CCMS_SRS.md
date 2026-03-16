# Software Requirements Specification (SRS)
## NTA Call Centre Management System (CCMS)

---

| Field              | Details                              |
|--------------------|--------------------------------------|
| Document Title     | Software Requirements Specification  |
| Prepared For       | National Testing Agency (NTA)        |
| Document Type      | SRS                                  |
| Version            | 1.0                                  |
| Date               | March 2026                           |
| Status             | Draft                                |

---

## Table of Contents

1. [Introduction](#1-introduction)
   - 1.1 Purpose
   - 1.2 Scope
   - 1.3 Definitions, Acronyms, and Abbreviations
   - 1.4 References
   - 1.5 Document Overview
2. [Overall System Description](#2-overall-system-description)
   - 2.1 System Overview
   - 2.2 System Context and Constraints
   - 2.3 User Roles and Responsibilities
   - 2.4 Operating Environment
   - 2.5 Assumptions and Dependencies
3. [Call Handling and Processing](#3-call-handling-and-processing)
   - 3.1 Call Handling Flow
   - 3.2 Conversation Processing
   - 3.3 Query Ticket Creation
4. [Query Resolution Workflow](#4-query-resolution-workflow)
   - 4.1 Agent Resolution Window
   - 4.2 Agent Resolution Outcome
   - 4.3 Unresolved Query Handling
   - 4.4 Similar Issue Combination
   - 4.5 Final Citizen Response
5. [Citizen Notification System](#5-citizen-notification-system)
   - 5.1 Notification Channels
   - 5.2 Notification Content
   - 5.3 Bulk Response Support
6. [Reopening Query Workflow](#6-reopening-query-workflow)
7. [Functional Requirements](#7-functional-requirements)
   - 7.1 Login and Access Management
   - 7.2 Call Management
   - 7.3 AI Voice Bot
   - 7.4 Transcription
   - 7.5 Query Categorization
   - 7.6 Ticket Management
   - 7.7 Similar Issue Grouping
   - 7.8 Escalation Management
8. [Non-Functional Requirements](#8-non-functional-requirements)
   - 8.1 Performance Requirements
   - 8.2 Security Requirements
   - 8.3 Availability and Reliability
   - 8.4 Scalability
   - 8.5 Usability
   - 8.6 Maintainability
   - 8.7 Compliance
9. [Reports and Dashboards](#9-reports-and-dashboards)
   - 9.1 Dashboard Metrics
   - 9.2 Report Types
10. [System and Integration Requirements](#10-system-and-integration-requirements)
    - 10.1 Telephony Services
    - 10.2 AI Services
    - 10.3 Infrastructure Requirements
    - 10.4 Data and Master Information
11. [Agent Operations](#11-agent-operations)
    - 11.1 Agent Dashboard
    - 11.2 Agent Workflow
12. [Data Requirements](#12-data-requirements)
    - 12.1 Data Storage
    - 12.2 Data Retention
    - 12.3 Data Privacy
13. [Interface Requirements](#13-interface-requirements)
    - 13.1 User Interfaces
    - 13.2 Hardware Interfaces
    - 13.3 Software Interfaces
    - 13.4 Communication Interfaces
14. [System Constraints and Limitations](#14-system-constraints-and-limitations)
15. [Appendix](#15-appendix)
    - 15.1 Ticket Status Lifecycle
    - 15.2 Role-Permission Matrix
    - 15.3 Phase-wise Feature Rollout

---

## 1. Introduction

### 1.1 Purpose

This Software Requirements Specification (SRS) document defines and documents the complete functional and non-functional requirements of the **NTA Call Centre Management System (CCMS)** for the National Testing Agency (NTA).

This document is intended to:

- Establish a clear and shared understanding among all stakeholders of what the software product will do for the NTA Call Centre.
- Provide a comprehensive description of system functions to help stakeholders evaluate whether the system meets operational needs.
- Reduce development risk and effort by ensuring all requirements are reviewed, validated, and agreed upon before design and implementation begin.
- Identify omissions, inconsistencies, or ambiguities early in the development lifecycle to prevent costly late-stage corrections.
- Serve as a formal baseline for validation and verification, enabling effective test planning, acceptance criteria definition, and compliance measurement.
- Facilitate system handover, onboarding, and user understanding of process flows during deployment.
- Act as a foundation for future enhancements, system evolution, and Phase 2 feature additions.

The system will enable NTA to efficiently manage citizen calls, grievances, query resolution, escalation, grouping of similar issues, and automated communication through AI-enabled call processing.

---

### 1.2 Scope

**System Name:** NTA Call Centre Management System (CCMS)

**Operational Purpose:** The CCMS is a centralized, AI-augmented call centre platform designed to handle inbound citizen queries directed at the National Testing Agency helpline. It automates call intake, routes calls to agents, generates grievance tickets, and manages the full resolution lifecycle through to citizen notification.

**Key Capabilities:**

| Capability | Description |
|---|---|
| AI-based Call Intake | Automated voice bot collects citizen details before agent transfer |
| Citizen Identification | Real-time validation of citizen application numbers and identity |
| Call Transcription | Real-time transcription of all conversations |
| Agent-Assisted Handling | Agents interact with citizens and manage ticket resolution |
| Query Categorization | AI-driven classification into predefined query types |
| Grievance Ticket Generation | Unique ticket creation for every query |
| Resolution Tracking | End-to-end status management from creation to closure |
| Officer Review | Exam Head Officers review all unresolved escalated tickets |
| Issue Grouping | AI groups similar unresolved tickets for batch resolution |
| Automated Communication | Citizen updates via WhatsApp, SMS, and AI outbound calls |

**Out of Scope (Phase 1):**
- QA Login functionality (deferred to Phase 2)
- AI-suggested resolutions during agent interaction (deferred to Phase 2)
- Integration with LMS or external examination authority portals

---

### 1.3 Definitions, Acronyms, and Abbreviations

| Term / Acronym | Definition |
|---|---|
| NTA | National Testing Agency |
| CCMS | Call Centre Management System |
| SRS | Software Requirements Specification |
| AI | Artificial Intelligence |
| IVR | Interactive Voice Response |
| CRM | Customer Relationship Management |
| Citizen | A candidate or user calling the NTA helpline |
| Agent | Call centre executive handling citizen queries |
| Exam Head Officer | Officer responsible for reviewing and resolving unresolved grievances |
| Grievance ID | Unique system-generated identifier assigned to each citizen query ticket |
| T+1 | Resolution deadline: within one working day from ticket assignment |
| DG Login | Director General login — highest administrative access |
| QA | Quality Assurance |
| API | Application Programming Interface |
| SMS | Short Message Service |
| STT | Speech-to-Text |
| NLP | Natural Language Processing |
| SLA | Service Level Agreement |
| RBAC | Role-Based Access Control |
| MFA | Multi-Factor Authentication |
| TLS | Transport Layer Security |
| PII | Personally Identifiable Information |

---

### 1.4 References

| Reference | Description |
|---|---|
| NTA Helpline Operational Manual | Internal operational guidelines for NTA helpline management |
| TRAI Guidelines | Telecom Regulatory Authority of India guidelines for IVR/call centre |
| DPDP Act, 2023 | Digital Personal Data Protection Act (India) |
| ISO/IEC 25010 | Software Quality Model for non-functional requirements |
| IEEE 830-1998 | IEEE Recommended Practice for Software Requirements Specifications |
| Aadhaar API Documentation | For citizen identity validation integration |

---

### 1.5 Document Overview

This document is organized as follows:

- **Section 2** provides an overall description of the system, user roles, and operating environment.
- **Sections 3–6** describe the core operational workflows: call handling, resolution, notifications, and ticket reopening.
- **Section 7** details all functional requirements.
- **Section 8** defines non-functional requirements including performance, security, and availability.
- **Sections 9–11** cover reporting, integration, and agent operations.
- **Sections 12–14** address data, interface, and system constraints.
- **Section 15** provides supporting appendices including status lifecycle diagrams and role-permission matrix.

---

## 2. Overall System Description

### 2.1 System Overview

The NTA Call Centre Management System (CCMS) is a multi-tiered, AI-integrated software platform that manages the complete lifecycle of citizen queries directed to the NTA helpline.

The system operates through a structured workflow:

```
Citizen Call
    │
    ▼
AI Voice Bot (Language, Name, Exam, Application No.)
    │
    ▼
Identity Validation
    │
    ▼
Route to Available Agent
    │
    ▼
Real-time AI Transcription + Categorization
    │
    ▼
Grievance Ticket Created
    │
    ├──[Resolved by Agent]──► Ticket: "Resolved by Agent" ──► Citizen Notified
    │
    └──[Unresolved]──────────► Escalated to Exam Head Officer Dashboard
                                    │
                                    ├──[Officer Resolves]──► Citizen Notified
                                    │
                                    ├──[AI Groups Similar]──► Common Response ──► Bulk Notify
                                    │
                                    └──[Citizen Dissatisfied]──► Ticket Reopened
```

**Key Architectural Principles:**

- Queries resolved by agents are marked **Resolved by Agent** and do not proceed to officer review.
- Only unresolved tickets are escalated and visible in the Exam Head Officer dashboard.
- AI performs passive assistance during Phase 1 (transcription, categorization, grouping); active suggestion in Phase 2.

---

### 2.2 System Context and Constraints

- The system shall operate as a web-based platform accessible over secure HTTPS connections.
- The system shall integrate with external telephony providers, AI/NLP services, and citizen communication channels.
- All citizen data handled by the system is subject to applicable Indian data protection regulations.
- The system shall be designed to handle approximately **20,000 inbound calls per day**.

---

### 2.3 User Roles and Responsibilities

#### 2.3.1 System Administrator (DG Login)

**Purpose:** Full administrative control over the CCMS platform.

**Responsibilities:**
- Manage system configuration and platform settings
- Create and manage user accounts and role assignments
- Define and update query categories and sub-categories
- Configure communication templates (SMS, WhatsApp, AI call scripts)
- Set grouping rules and similarity thresholds for AI issue grouping
- Configure escalation rules and T+1 SLA settings
- Manage role-permission mappings across all login types
- Monitor system health and audit logs

---

#### 2.3.2 Agent Login

Agents are call centre operations staff who handle citizen interactions and manage ticket resolution.

**Sub-roles:**

| Sub-role | Description |
|---|---|
| **Team Lead Login** | Head of agent team; oversees agent performance, reassigns tickets, monitors SLA breaches |
| **Exam Lead Login** | Exam-specific query resolver; handles escalated queries for a specific exam |
| **Call Agent Login** | Front-line agent handling inbound calls directly |

**Common Agent Responsibilities:**
- Receive and handle transferred calls from the AI voice bot
- Review AI-generated transcripts and categorizations
- Resolve citizen queries where possible within T+1
- Create and update grievance tickets
- Mark tickets as unresolved when resolution is beyond agent scope
- Request additional information from citizens
- Update ticket status and add notes

---

#### 2.3.3 Citizen / Candidate Login

**Purpose:** Self-service portal for citizens to track and engage with their grievances.

**Responsibilities:**
- Log in using mobile number, application number, or OTP
- Track the status of existing grievance tickets
- Receive automated updates from the system
- Submit additional information or documents when requested
- Reopen tickets if the provided resolution is unsatisfactory

---

#### 2.3.4 Officer Login

Officers review unresolved grievances and provide final resolutions.

**Sub-roles:**

| Sub-role | Description |
|---|---|
| **Exam Department Login** | Department-level officer who reviews and acts on unresolved tickets |
| **Exam Head Login** | Senior officer who approves common responses for grouped issues and oversees resolution quality |

**Common Officer Responsibilities:**
- View dashboard of unresolved escalated tickets
- Provide final resolutions or request additional information
- Review AI-generated grouped issues and approve common responses
- Monitor resolution timelines and SLA compliance

---

#### 2.3.5 QA Login *(Phase 2)*

**Purpose:** Quality assurance and compliance auditing.

**Responsibilities:**
- Conduct call quality audits
- Review transcripts for accuracy and compliance
- Validate agent responses against quality benchmarks
- Generate QA compliance reports
- Flag tickets for re-training or process improvement

---

### 2.4 Operating Environment

| Component | Specification |
|---|---|
| Platform | Web-based application (browser-accessible) |
| Deployment | Cloud-hosted (AWS, Azure, or GCP) |
| Network | Secure HTTPS; IP whitelisting for API endpoints |
| Browsers | Chrome (latest), Firefox (latest), Edge (latest) |
| Mobile Support | Responsive design for citizen-facing portal |
| Telephony | Twilio / Airtel IQ / Exotel or equivalent |
| AI Platform | AWS (Transcribe, Comprehend) / OpenAI / equivalent |
| Languages | Hindi, English, and other regional languages (Bengali, Tamil, etc.) |

---

### 2.5 Assumptions and Dependencies

**Assumptions:**
- The telephony provider will supply a dedicated toll-free number for the NTA helpline.
- Citizens calling in will have access to their application number, registered mobile number, or Aadhaar number for identity verification.
- Exam master data (exam names, schedules, application data) will be provided by NTA and loaded into the system prior to go-live.
- Agent workstations will have stable internet connectivity of sufficient bandwidth for real-time call handling.
- NTA will provide approved query categories, sub-categories, and resolution templates during the configuration phase.
- Aadhaar/application number validation APIs will be made available to the system.

**Dependencies:**
- Telephony provider availability and SLA for inbound call handling
- AI/NLP service uptime for transcription and categorization
- WhatsApp Business API approval and configuration by Meta
- SMS gateway integration and DLT registration compliance (as per TRAI)
- Timely availability of citizen validation datasets from NTA

---

## 3. Call Handling and Processing

### 3.1 Call Handling Flow

The inbound call handling workflow is as follows:

| Step | Actor | Action |
|---|---|---|
| 1 | Citizen | Dials the NTA helpline toll-free number |
| 2 | AI Voice Bot | Answers the call and greets the citizen |
| 3 | AI Voice Bot | Asks for preferred language selection |
| 4 | AI Voice Bot | Collects citizen's name, exam name, and application number |
| 5 | AI System | Transcribes and validates citizen-provided information |
| 6 | Telephony System | Routes the call to an available agent based on queue and exam type |
| 7 | Agent | Receives the call with pre-populated citizen details |
| 8 | Agent + AI | Interaction begins; AI performs real-time transcription and analysis |
| 9 | Agent | Resolves or escalates the query |
| 10 | System | Grievance ticket is created or updated on call completion |

**Call Routing Rules:**
- Calls shall be routed based on agent availability and, where configured, exam type specialization.
- If no agent is available, the citizen shall receive an estimated wait time and be offered a callback option (if supported by telephony provider).
- Calls shall not be dropped without an acknowledgment message to the citizen.

---

### 3.2 Conversation Processing

During an active call, the AI system performs the following real-time operations:

| Processing Task | Description | Phase |
|---|---|---|
| Speech-to-Text Transcription | Converts spoken dialogue to text in real time | Phase 1 |
| Query Category Detection | Classifies the query into predefined categories | Phase 1 |
| Query Sub-category Detection | Further narrows classification to sub-categories | Phase 1 |
| Query Summary Generation | Auto-generates a concise summary of the citizen's issue | Phase 1 |
| Keyword Extraction | Identifies key terms for search and grouping | Phase 1 |
| Suggested Resolution | AI proposes a resolution for agent review | Phase 2 |

**Transcription Requirements:**
- Transcripts shall be generated in the language spoken by the citizen.
- For regional language calls, automatic translation to English shall be supported.
- Transcripts shall be time-stamped and speaker-labeled (Agent / Citizen).
- Transcripts shall be saved and linked to the grievance ticket upon call completion.

---

### 3.3 Query Ticket Creation

Upon completion of a call, the system shall automatically generate a grievance ticket containing all of the following information:

| Field | Description |
|---|---|
| Grievance ID | Unique system-generated identifier (format: NTA-YYYYMMDD-XXXXX) |
| Citizen Name | As provided by the citizen or fetched from validation API |
| Citizen Mobile Number | Registered or calling number |
| Application Number | As validated by the system |
| Exam Name | Exam linked to the query |
| Exam Type | Category of examination |
| Call Date and Time | Timestamp of the call |
| Query Category | AI-detected primary category |
| Query Sub-category | AI-detected secondary category |
| Query Summary | AI-generated summary of the citizen's issue |
| Call Transcript | Full time-stamped transcript |
| Keywords | Extracted keywords for search and grouping |
| Assigned Agent ID | Agent who handled the call |
| Ticket Status | Initial status: "Open" or "Pending Agent Action" |
| Call Recording Link | Secure link to the recorded call audio |

**Ticket Creation Rules:**
- Every call that completes the AI intake process shall result in a grievance ticket.
- Duplicate call detection: if the same citizen calls within 24 hours about the same exam, the system shall flag potential duplicate and prompt the agent to merge or create a new ticket.
- Tickets shall be immutable in their original creation data; only status and notes fields shall be updatable post-creation.

---

## 4. Query Resolution Workflow

### 4.1 Agent Resolution Window

Agents and their hierarchy are allocated a **T+1 (one working day)** window to act on all assigned tickets.

**Escalation on T+1 Breach:**
- If no action is taken on a ticket within T+1, the system shall:
  - Auto-escalate the ticket to the Team Lead
  - Send an SLA breach notification to the Team Lead
  - Log the breach for reporting purposes

**Possible Agent Actions Within T+1:**

| Action | Resulting Ticket Status |
|---|---|
| Resolve the query | Resolved by Agent |
| Request additional information | Pending Citizen Response |
| Mark as unresolved | Escalated to Officer |

---

### 4.2 Agent Resolution Outcome

When an agent resolves a query:

1. Ticket status shall change to **"Resolved by Agent"**.
2. The system shall generate a resolution summary combining:
   - Agent-provided resolution notes
   - Relevant links or documents (if applicable)
3. The citizen shall receive the resolution summary automatically through all configured communication channels (SMS, WhatsApp, AI outbound call).
4. Such resolved tickets shall **not** appear in the Officer dashboard.
5. The ticket shall remain visible to agents for reference and audit.
6. If the citizen indicates dissatisfaction with the agent resolution, the ticket status shall change to **"Reopened"** and re-enter the resolution queue.

---

### 4.3 Unresolved Query Handling

When a ticket is marked unresolved by an agent:

1. Ticket status shall change to **"Escalated to Officer"**.
2. The ticket shall appear exclusively in the **Exam Head Officer dashboard**.
3. Agents shall lose edit access to the ticket; the ticket becomes read-only for agents.
4. Officers shall have the following options:

| Officer Action | Resulting Ticket Status |
|---|---|
| Provide final resolution | Resolved by Officer |
| Request additional information | Pending Citizen Response |
| Mark for AI grouping | Grouped / Pending Batch Response |
| Reassign to another officer | Re-assigned |

---

### 4.4 Similar Issue Combination

The system shall use AI to identify, group, and batch-resolve similar unresolved tickets.

**Grouping Criteria:**

The AI shall analyze and group tickets based on a combination of the following signals:

| Signal | Weight |
|---|---|
| Query Category | High |
| Query Sub-category | High |
| Exam Name | High |
| Keywords | Medium |
| Transcript Semantic Similarity | Medium |
| Resolution Context (if prior) | Low |

**Grouping Process:**

1. System AI continuously scans unresolved escalated tickets for similarity above a configurable threshold.
2. When a group is formed, all associated tickets are linked and a **"Group ID"** is assigned.
3. AI generates a **common suggested response** for the group.
4. The Exam Head Officer reviews the group, the constituent tickets, and the suggested response.
5. Officer may:
   - Approve the common response as-is
   - Edit and approve the response
   - Reject the grouping (tickets revert to individual unresolved status)
6. Upon approval, the common response is sent to all citizens associated with the grouped tickets.
7. All grouped tickets shall change status to **"Resolved – Batch Response"**.

**Grouping Administration:**
- Admins shall be able to configure similarity thresholds, minimum group size, and grouping scope (e.g., restrict grouping to same exam only).

---

### 4.5 Final Citizen Response

Final responses from officer resolution or batch responses shall be delivered to citizens through all configured channels:

| Channel | Trigger Condition |
|---|---|
| SMS | Always sent for every resolution |
| WhatsApp | If citizen's number is WhatsApp-enabled |
| AI Outbound Call | For high-priority tickets or as configured by admin |

**Response Content:**
- Grievance ID
- Query summary
- Resolution text or common response
- Instructions for reopening the ticket
- Helpline contact for further assistance

**Citizen Feedback Mechanism:**
- The AI outbound call shall include an option for the citizen to indicate satisfaction or dissatisfaction.
- SMS and WhatsApp messages shall include a reply option or link to reopen.
- If the citizen indicates dissatisfaction, the ticket status shall change to **"Reopened"** automatically.

---

## 5. Citizen Notification System

### 5.1 Notification Channels

The system shall support the following citizen communication channels:

| Channel | Protocol / API | Use Case |
|---|---|---|
| SMS | SMS Gateway (Twilio / Airtel IQ / MSG91) | Status updates, grievance ID delivery, resolution summary |
| WhatsApp | WhatsApp Business API (Meta) | Richer notification with formatting, documents, and reply options |
| AI Outbound Call | Text-to-Speech IVR (AI Voice Bot) | High-touch resolution delivery, satisfaction check |

**Channel Priority:**
- All three channels shall be triggered simultaneously unless the admin configures a priority hierarchy.
- If a WhatsApp message fails, the system shall fallback to SMS.
- AI outbound call scheduling shall respect citizen's time zone and permissible call hours (9 AM – 6 PM).

---

### 5.2 Notification Content

Notifications shall be configurable by the Admin and shall include the following standard fields:

| Field | Required | Notes |
|---|---|---|
| Greeting | Yes | Citizen's name |
| Grievance ID | Yes | For reference and tracking |
| Current Ticket Status | Yes | Resolved, Pending, Escalated, etc. |
| Resolution Summary | Conditional | Included when ticket is resolved |
| Common Response Text | Conditional | Included for batch responses |
| Reopen Instructions | Yes (on resolution) | How to reopen if dissatisfied |
| Helpline Number | Yes | For further assistance |

**Template Management:**
- All notification templates shall be configurable by the Admin.
- Templates shall support variable substitution (e.g., {{citizen_name}}, {{grievance_id}}).
- Templates shall be available in all supported languages (Hindi, English, and regional languages).
- Changes to templates shall require admin-level authorization and shall be versioned for audit.

---

### 5.3 Bulk Response Support

The system shall support bulk communication for grouped issues:

- Upon officer approval of a grouped common response, the system shall automatically dispatch notifications to all citizens in the group via all enabled channels.
- Bulk dispatch shall be logged with timestamps, delivery status, and channel used.
- Failed deliveries shall be retried up to 3 times with configurable retry intervals.
- Bulk dispatch shall support rate limiting to comply with SMS/WhatsApp API quotas.
- Admins shall be able to schedule bulk notifications for off-peak hours if required.

---

## 6. Reopening Query Workflow

### 6.1 Reopen Workflow

The reopen mechanism allows citizens to flag an unsatisfactory resolution and re-enter the active resolution process.

**Reopen Triggers:**

| Trigger | Channel |
|---|---|
| Citizen indicates dissatisfaction during AI outbound call | AI Voice Bot |
| Citizen replies "Reopen" or equivalent to SMS/WhatsApp | SMS / WhatsApp |
| Citizen logs into the citizen portal and requests reopen | Web Portal |

**Reopen Process:**

1. Ticket status changes to **"Reopened"**.
2. Ticket re-enters the active work queue.
3. Reopened ticket is assigned to:
   - The original agent (if within agent resolution scope), or
   - The appropriate officer (if previously escalated)
4. A notification is sent to the assigned agent/officer informing them of the reopen.
5. The citizen receives a confirmation notification acknowledging the reopen request.
6. All reopen events are logged with timestamps and reason (if captured).

**Reopen Restrictions:**
- Citizens shall be permitted to reopen a ticket a maximum of **3 times** (configurable by admin).
- After the maximum reopen limit, the ticket shall be escalated to the Exam Head for manual review.
- Tickets can only be reopened within **30 days** of the last resolution (configurable by admin).

---

## 7. Functional Requirements

Requirements are identified using the convention: **FR-[Module]-[Number]**

---

### 7.1 Login and Access Management

| ID | Requirement |
|---|---|
| FR-LAM-01 | The system shall support multi-role login with distinct access permissions per role. |
| FR-LAM-02 | The system shall support Admin (DG) Login with full system access. |
| FR-LAM-03 | The system shall support Agent Logins: Team Lead, Exam Lead, and Call Agent. |
| FR-LAM-04 | The system shall support Citizen Login via mobile OTP or application number. |
| FR-LAM-05 | The system shall support Officer Logins: Exam Department and Exam Head. |
| FR-LAM-06 | The system shall support QA Login in Phase 2 with read-only access to transcripts and tickets. |
| FR-LAM-07 | The system shall enforce Role-Based Access Control (RBAC) across all modules. |
| FR-LAM-08 | The system shall support Multi-Factor Authentication (MFA) for Admin and Officer logins. |
| FR-LAM-09 | The system shall lock accounts after 5 consecutive failed login attempts. |
| FR-LAM-10 | The system shall maintain a full audit log of all login and logout events. |
| FR-LAM-11 | Admin shall be able to create, modify, suspend, and delete user accounts. |
| FR-LAM-12 | The system shall support session timeout after a configurable period of inactivity. |
| FR-LAM-13 | Admin shall be able to assign multiple exams or categories to Agent/Officer accounts. |

---

### 7.2 Call Management

| ID | Requirement |
|---|---|
| FR-CM-01 | The system shall receive and process inbound calls from the NTA helpline toll-free number. |
| FR-CM-02 | The system shall connect incoming calls to the AI voice assistant immediately upon answer. |
| FR-CM-03 | The system shall route calls to available agents after AI intake is complete. |
| FR-CM-04 | The system shall display a queue position or estimated wait time to the citizen if no agent is available. |
| FR-CM-05 | The system shall support call recording for all inbound calls. |
| FR-CM-06 | The system shall support call transfer between agents. |
| FR-CM-07 | The system shall display pre-populated citizen details (from AI intake) on the agent screen before the agent answers. |
| FR-CM-08 | The system shall log call start time, end time, duration, and outcome for each call. |
| FR-CM-09 | The system shall support configurable call routing rules (by exam type, agent availability, skill). |
| FR-CM-10 | The system shall provide agents with a soft-phone interface or CTI (Computer-Telephony Integration) integration. |

---

### 7.3 AI Voice Bot

| ID | Requirement |
|---|---|
| FR-AIB-01 | The AI voice bot shall greet the citizen in the default language (Hindi/English) and offer language selection. |
| FR-AIB-02 | The AI voice bot shall collect the citizen's name. |
| FR-AIB-03 | The AI voice bot shall collect the citizen's exam name. |
| FR-AIB-04 | The AI voice bot shall collect the citizen's application number. |
| FR-AIB-05 | The AI voice bot shall validate the application number against the citizen database. |
| FR-AIB-06 | The AI voice bot shall handle failed validation gracefully and allow the citizen to retry up to 3 times. |
| FR-AIB-07 | The AI voice bot shall transfer the call to an agent along with all collected data. |
| FR-AIB-08 | The AI voice bot shall support at minimum Hindi and English; regional languages (Bengali, Tamil, etc.) shall be supported. |
| FR-AIB-09 | The AI voice bot shall be capable of conducting AI outbound calls for citizen notification (Phase 1). |
| FR-AIB-10 | The AI outbound call shall include a citizen satisfaction prompt and capture the response for ticket update. |

---

### 7.4 Transcription

| ID | Requirement |
|---|---|
| FR-TR-01 | The system shall record and transcribe all call conversations in real time. |
| FR-TR-02 | Transcripts shall be speaker-labeled (Agent / Citizen). |
| FR-TR-03 | Transcripts shall be time-stamped at configurable intervals. |
| FR-TR-04 | Transcripts generated in regional languages shall be automatically translated to English and stored alongside the original. |
| FR-TR-05 | Transcripts shall be stored and linked to the corresponding grievance ticket. |
| FR-TR-06 | Transcripts shall be searchable by keyword, grievance ID, citizen name, or application number. |
| FR-TR-07 | Transcripts shall be read-only for agents; only admins shall be able to redact sensitive information. |
| FR-TR-08 | Transcription accuracy shall be monitored; accuracy metrics shall be available in admin reports. |
| FR-TR-09 | Transcripts shall be available for QA review in Phase 2. |

---

### 7.5 Query Categorization

| ID | Requirement |
|---|---|
| FR-QC-01 | The AI system shall automatically categorize every query into a predefined primary category. |
| FR-QC-02 | The AI system shall automatically assign a sub-category within the primary category. |
| FR-QC-03 | Predefined query categories shall include at minimum: Admit Card Issue, Application Correction, Exam Centre Issue, Result Query, Payment Issue, Other. |
| FR-QC-04 | Agents shall be able to override the AI-assigned category and sub-category. |
| FR-QC-05 | All category overrides shall be logged for AI training and quality monitoring purposes. |
| FR-QC-06 | Admin shall be able to add, modify, or deactivate query categories and sub-categories. |
| FR-QC-07 | The AI shall extract and store keywords from each call transcript for search and grouping. |
| FR-QC-08 | The AI shall generate a concise query summary (maximum 200 words) for each ticket. |

---

### 7.6 Ticket Management

| ID | Requirement |
|---|---|
| FR-TM-01 | The system shall generate a unique Grievance ID for every completed call. |
| FR-TM-02 | Grievance IDs shall follow a standardized format (e.g., NTA-YYYYMMDD-XXXXX). |
| FR-TM-03 | The system shall assign tickets to the handling agent automatically upon ticket creation. |
| FR-TM-04 | The system shall track all status changes with timestamps and user identity. |
| FR-TM-05 | Tickets shall support the following statuses: Open, Pending Agent Action, Resolved by Agent, Pending Citizen Response, Escalated to Officer, Resolved by Officer, Resolved – Batch Response, Reopened, Closed. |
| FR-TM-06 | The system shall support ticket reassignment by Team Lead or Admin. |
| FR-TM-07 | The system shall support ticket merging when duplicates are identified. |
| FR-TM-08 | The system shall support ticket reopening by citizens within the configurable reopen window. |
| FR-TM-09 | The system shall enforce a maximum reopen limit per ticket (default: 3, configurable). |
| FR-TM-10 | The system shall send SLA breach alerts when tickets exceed the T+1 resolution window. |
| FR-TM-11 | Ticket search shall support filtering by Grievance ID, citizen name, application number, exam name, category, status, and date range. |
| FR-TM-12 | All ticket changes shall be logged in an immutable audit trail. |

---

### 7.7 Similar Issue Grouping

| ID | Requirement |
|---|---|
| FR-SIG-01 | The system shall use AI to automatically identify and group similar unresolved escalated tickets. |
| FR-SIG-02 | Grouping shall be based on query category, sub-category, exam name, keywords, and semantic transcript similarity. |
| FR-SIG-03 | Each group shall be assigned a unique Group ID. |
| FR-SIG-04 | The AI shall generate a common suggested response for each group. |
| FR-SIG-05 | The Exam Head Officer shall review and approve, edit, or reject common responses before dispatch. |
| FR-SIG-06 | Upon approval, the system shall dispatch the common response to all citizens in the group. |
| FR-SIG-07 | Rejected groupings shall revert all constituent tickets to individual unresolved status. |
| FR-SIG-08 | Admin shall configure similarity thresholds and minimum group sizes. |
| FR-SIG-09 | Grouping activity shall be logged and visible in officer and admin dashboards. |
| FR-SIG-10 | A citizen's ticket shall not appear in more than one group simultaneously. |

---

### 7.8 Escalation Management

| ID | Requirement |
|---|---|
| FR-EM-01 | Only unresolved tickets shall be escalated to the Officer dashboard. |
| FR-EM-02 | Tickets resolved by agents shall never be visible in the officer escalation queue. |
| FR-EM-03 | The system shall auto-escalate tickets that breach the T+1 SLA to the Team Lead. |
| FR-EM-04 | Escalation rules (time thresholds, escalation targets) shall be configurable by Admin. |
| FR-EM-05 | Escalated tickets shall carry a full history: transcript, agent notes, categorization. |
| FR-EM-06 | Officers shall receive in-app and email notifications when new escalated tickets are assigned. |
| FR-EM-07 | Officers shall be able to re-escalate a ticket to a higher officer tier if needed. |

---

## 8. Non-Functional Requirements

### 8.1 Performance Requirements

| ID | Requirement |
|---|---|
| NFR-PERF-01 | The system shall support approximately 20,000 inbound calls per day. |
| NFR-PERF-02 | Concurrent call handling capacity shall be determined and finalized with the telephony provider during procurement. |
| NFR-PERF-03 | The agent dashboard shall load within 3 seconds under normal load conditions. |
| NFR-PERF-04 | Ticket search results shall be returned within 2 seconds for queries on standard fields. |
| NFR-PERF-05 | AI transcription latency shall not exceed 2 seconds behind real-time speech. |
| NFR-PERF-06 | AI categorization shall complete within 5 seconds of call completion. |
| NFR-PERF-07 | Bulk notification dispatch for up to 10,000 citizens shall complete within 30 minutes. |
| NFR-PERF-08 | The system shall handle peak loads (e.g., post-exam result release) without degradation in availability. |

---

### 8.2 Security Requirements

| ID | Requirement |
|---|---|
| NFR-SEC-01 | All data in transit shall be encrypted using TLS 1.2 or higher. |
| NFR-SEC-02 | All data at rest (tickets, transcripts, recordings, PII) shall be encrypted using AES-256. |
| NFR-SEC-03 | All public-facing APIs shall be secured with API keys and IP whitelisting. |
| NFR-SEC-04 | Admin and Officer logins shall require Multi-Factor Authentication (MFA). |
| NFR-SEC-05 | The system shall enforce the principle of least privilege; each role shall access only the data and functions relevant to its responsibilities. |
| NFR-SEC-06 | Citizen PII (name, mobile, Aadhaar, application number) shall be masked in logs and non-essential views. |
| NFR-SEC-07 | The system shall maintain a tamper-proof audit log for all data access and modifications. |
| NFR-SEC-08 | The system shall undergo regular security vulnerability assessments (quarterly recommended). |
| NFR-SEC-09 | All call recordings and transcripts shall be accessible only to authorized roles. |
| NFR-SEC-10 | The system shall comply with the Digital Personal Data Protection (DPDP) Act, 2023. |

---

### 8.3 Availability and Reliability

| ID | Requirement |
|---|---|
| NFR-AVL-01 | The system shall maintain a minimum uptime of 99.5% during NTA's operational hours. |
| NFR-AVL-02 | Planned maintenance windows shall be scheduled outside of business hours (10 PM – 6 AM IST). |
| NFR-AVL-03 | The system shall support automated failover for critical components (telephony routing, database). |
| NFR-AVL-04 | Recovery Time Objective (RTO): The system shall recover from an unplanned outage within 4 hours. |
| NFR-AVL-05 | Recovery Point Objective (RPO): No more than 1 hour of data loss shall occur in the event of failure. |
| NFR-AVL-06 | The system shall send automated alerts to the admin team within 5 minutes of a critical component failure. |

---

### 8.4 Scalability

| ID | Requirement |
|---|---|
| NFR-SCL-01 | The system architecture shall support horizontal scaling to handle increased call volumes during peak periods. |
| NFR-SCL-02 | The database shall be designed to scale to at least 5 years of historical ticket data without performance degradation. |
| NFR-SCL-03 | Additional exam categories, agent accounts, and communication templates shall be addable without system downtime. |

---

### 8.5 Usability

| ID | Requirement |
|---|---|
| NFR-USE-01 | The agent dashboard shall present all call-related information in a single-screen view without horizontal scrolling. |
| NFR-USE-02 | The citizen-facing portal shall be accessible on mobile devices with responsive design. |
| NFR-USE-03 | The system shall provide Hindi and English interface options for agents and citizens. |
| NFR-USE-04 | Training for new agents shall be completable within one working day using system documentation. |
| NFR-USE-05 | The system shall provide inline help and tooltips for key actions on all user-facing screens. |

---

### 8.6 Maintainability

| ID | Requirement |
|---|---|
| NFR-MNT-01 | The system shall be built on a modular architecture to allow independent module updates without full system redeployment. |
| NFR-MNT-02 | All integration endpoints (telephony, AI, messaging) shall be configurable via admin settings without code changes. |
| NFR-MNT-03 | System logs shall be retained for a minimum of 12 months and shall be exportable. |
| NFR-MNT-04 | The system shall provide a configuration export/import feature for backup and migration of admin settings. |

---

### 8.7 Compliance

| ID | Requirement |
|---|---|
| NFR-CMP-01 | The system shall comply with TRAI guidelines for call centre operations in India. |
| NFR-CMP-02 | The system shall comply with the DPDP Act, 2023 for handling citizen personal data. |
| NFR-CMP-03 | SMS communications shall comply with DLT (Distributed Ledger Technology) registration requirements as mandated by TRAI. |
| NFR-CMP-04 | WhatsApp communications shall comply with Meta's WhatsApp Business Policy. |
| NFR-CMP-05 | All call recordings shall be stored in compliance with applicable data retention and privacy laws. |

---

## 9. Reports and Dashboards

### 9.1 Dashboard Metrics

Each role shall have access to a dedicated dashboard displaying relevant real-time metrics:

#### Agent Dashboard

| Metric | Description |
|---|---|
| My Open Tickets | Count and list of tickets assigned to the agent |
| Tickets Resolved Today | Count of tickets resolved by the agent today |
| SLA Breach Alerts | Tickets approaching or past the T+1 deadline |
| Average Handle Time | Agent's average call and resolution time |
| Pending Citizen Responses | Tickets awaiting citizen input |

#### Team Lead Dashboard

| Metric | Description |
|---|---|
| Team Open Tickets | All open tickets across the agent team |
| SLA Breaches | Tickets that have exceeded the T+1 window |
| Agent Performance | Resolution rate and handle times per agent |
| Escalations Today | Count of tickets escalated to officer today |

#### Officer Dashboard

| Metric | Description |
|---|---|
| Unresolved Escalated Tickets | All tickets escalated from agents |
| Grouped Issues | Active AI-grouped issue sets awaiting approval |
| Pending Approvals | Common responses awaiting officer sign-off |
| Resolved Today | Tickets resolved by officers today |
| Average Officer Resolution Time | Officer-level resolution efficiency |

#### Admin Dashboard

| Metric | Description |
|---|---|
| Total Calls Received | Today, week, month |
| Queries Resolved by Agents | Count and percentage |
| Unresolved Pending Officer Action | Current count |
| Reopened Grievances | Count and trend |
| Grouped Issues | Active and resolved groupings |
| Average Resolution Time | System-wide SLA performance |
| Channel-wise Notification Delivery Rates | SMS, WhatsApp, AI Call success rates |
| System Health Indicators | API status, call routing status, AI service status |

---

### 9.2 Report Types

The system shall support the following exportable reports:

| Report | Filters Available | Format |
|---|---|---|
| Daily Call Volume Report | Date, exam name | PDF, Excel |
| Ticket Resolution Report | Date range, agent, status, category | PDF, Excel |
| SLA Compliance Report | Date range, agent, team | PDF, Excel |
| Escalation Analysis Report | Date range, exam, officer | PDF, Excel |
| Grouping and Batch Response Report | Date range, group, exam | PDF, Excel |
| Citizen Notification Delivery Report | Date range, channel | PDF, Excel |
| Agent Performance Report | Date range, agent, team | PDF, Excel |
| Query Category Analysis | Date range, category, sub-category | PDF, Excel |
| Reopened Ticket Report | Date range, reason | PDF, Excel |

---

## 10. System and Integration Requirements

### 10.1 Telephony Services

The system shall integrate with a supported telephony provider (Twilio, Airtel IQ, Exotel, or equivalent).

**Required Telephony Capabilities:**

| Capability | Description |
|---|---|
| Toll-Free Numbers | Dedicated NTA helpline toll-free number provisioning |
| Voice API and Webhook Integration | Programmable call control and event-driven routing |
| Call Recording | Server-side recording with secure storage and retrieval |
| Call Routing and Transfer | Queue management, agent transfer, and callback support |
| IVR/Voice Bot | AI voice bot integration via VXML or REST API |
| SMS Gateway | Outbound SMS for citizen notifications |
| WhatsApp Business API | Rich messaging for citizen notifications |
| DLT Compliance | SMS routes compliant with TRAI DLT requirements |

**Telephony SLA Requirements:**
- Call answer rate (AI bot): 99% within 5 seconds
- Call routing time (to agent): less than 30 seconds from AI intake completion
- SMS delivery confirmation: within 60 seconds of dispatch

---

### 10.2 AI Services

AI capabilities shall be provisioned via AWS, OpenAI, or similar qualified platforms.

| Capability | Description | Phase |
|---|---|---|
| Speech-to-Text (STT) | Real-time transcription of call audio | Phase 1 |
| Multi-Language Translation | Hindi, English, Bengali, Tamil, and other regional languages | Phase 1 |
| Automatic Grievance Classification | NLP-based query categorization and sub-categorization | Phase 1 |
| Keyword Extraction | Identifies key terms for search and grouping | Phase 1 |
| Query Summary Generation | Concise AI-generated summary of citizen issue | Phase 1 |
| Similar Grievance Detection | Semantic similarity scoring for ticket grouping | Phase 1 |
| Common Response Generation | AI-drafted batch response for officer review | Phase 1 |
| Resolution Suggestion | AI-proposed resolutions for agent assistance | Phase 2 |

**AI Service Requirements:**
- STT accuracy shall meet a minimum of 90% word accuracy for Hindi and English.
- Classification accuracy shall be monitored; corrections by agents shall feed back into model improvement.
- AI services shall operate within the data residency and compliance requirements applicable to NTA.

---

### 10.3 Infrastructure Requirements

| Requirement | Specification |
|---|---|
| Daily Call Capacity | Approximately 20,000 calls/day |
| Concurrent Calls | To be finalized with telephony provider; initial estimate based on peak hour analysis |
| API Security | All public APIs secured via HTTPS with API key authentication and IP whitelisting |
| Data Residency | All citizen data stored within India (as per DPDP Act requirements) |
| Backup | Automated daily backups with 30-day retention minimum |
| Disaster Recovery | Multi-zone deployment with automated failover |
| Monitoring | Real-time infrastructure monitoring with alerting (CPU, memory, API response time, error rates) |

---

### 10.4 Data and Master Information

The following master data sets are required for system operation:

| Data Set | Description | Owner |
|---|---|---|
| Query Category Master | Hierarchical list of categories and sub-categories | NTA Admin |
| Resolution Mapping | Pre-approved resolution templates per category | NTA Admin |
| Citizen Validation Dataset | Mobile number, Aadhaar, and application number validation API/dataset | NTA / UIDAI |
| Exam Master Data | Exam name, type, schedule, and registration period | NTA |
| Officer and Agent Role Mappings | Assignment of staff to exams, teams, and roles | NTA Admin |
| Communication Templates | SMS, WhatsApp, and AI call script templates | NTA Admin |
| Call Recording Storage Policy | Retention period, access controls, archival rules | NTA / Legal |
| Grouping Configuration | Similarity thresholds, group size rules | NTA Admin |

---

## 11. Agent Operations

### 11.1 Agent Dashboard

Each agent login type (Team Lead, Exam Lead, Call Agent) shall have a dedicated dashboard view.

**Call Agent Dashboard shall include:**

| Element | Description |
|---|---|
| Incoming Call Panel | Incoming call notification with citizen pre-details from AI intake |
| Active Ticket View | Current ticket being worked on |
| My Ticket Queue | All open tickets assigned to the agent |
| Transcript Panel | Real-time and post-call transcript view |
| Category and Summary Panel | AI-assigned category, sub-category, and summary (editable) |
| Resolution Notes | Free-text field for agent resolution notes |
| Action Buttons | Resolve / Escalate / Request Info / Transfer |
| Call Controls | Hold, Mute, Transfer, End Call |

**Team Lead Dashboard additional views:**
- Team-wide ticket queue with SLA indicators
- Agent availability and workload distribution
- Manual ticket reassignment capability
- SLA breach alerts and escalation triggers

---

### 11.2 Agent Workflow

**Standard Call Agent Workflow:**

1. Receive incoming call notification; citizen details pre-populated on screen.
2. Greet citizen and verify identity (confirm name, application number).
3. Review AI-generated transcript and categorization in real time.
4. Interact with citizen to understand the full query.
5. Attempt resolution using available knowledge base and system tools.
6. On call completion:
   - If resolved: add resolution notes, click "Resolve", confirm status → "Resolved by Agent".
   - If more info needed: click "Request Info", specify what is needed → status → "Pending Citizen Response".
   - If unresolvable: click "Escalate", optionally add notes → status → "Escalated to Officer".
7. System auto-generates ticket and triggers appropriate citizen notification.

---

## 12. Data Requirements

### 12.1 Data Storage

| Data Type | Storage Location | Encryption |
|---|---|---|
| Grievance Tickets | Relational database (PostgreSQL / MySQL) | AES-256 |
| Call Transcripts | Document store (S3 / Azure Blob) | AES-256 |
| Call Recordings | Object storage with CDN delivery | AES-256 |
| Citizen PII | Encrypted fields in relational DB | AES-256 |
| Notification Logs | Relational or time-series database | AES-256 |
| Audit Logs | Append-only log store | AES-256 |
| AI Models | ML model registry (managed by AI provider) | Provider-managed |

---

### 12.2 Data Retention

| Data Type | Retention Period | Post-Retention Action |
|---|---|---|
| Grievance Tickets | 5 years | Archive to cold storage |
| Call Transcripts | 3 years | Archive, then delete |
| Call Recordings | 1 year (configurable) | Delete or archive per policy |
| Citizen PII | For ticket lifetime + 2 years | Anonymize or delete |
| Notification Logs | 1 year | Archive |
| Audit Logs | 5 years | Archive (immutable) |

---

### 12.3 Data Privacy

- Citizen PII shall only be accessible to roles with explicit authorization.
- Citizen data shall never be used for purposes beyond grievance resolution without explicit consent.
- The system shall support a citizen's right to access and request deletion of their data in accordance with the DPDP Act, 2023.
- Data anonymization tools shall be available to admins for compliance requests.

---

## 13. Interface Requirements

### 13.1 User Interfaces

| Interface | Users | Key Characteristics |
|---|---|---|
| Agent Web Application | Call Agent, Exam Lead, Team Lead | Single-page app, real-time updates, CTI integration |
| Officer Web Portal | Exam Department, Exam Head | Ticket review, grouping management, approval workflows |
| Admin Console | DG / Admin | Full configuration, user management, reporting |
| Citizen Self-Service Portal | Citizens | Mobile-responsive, OTP login, ticket tracking |
| QA Portal *(Phase 2)* | QA staff | Transcript review, scoring, compliance reporting |

---

### 13.2 Hardware Interfaces

- Agent workstations shall have headsets or handsets compatible with the CTI integration.
- Minimum recommended specification for agent workstations: 8 GB RAM, modern browser, stable broadband (minimum 10 Mbps).
- No proprietary hardware is required for citizen interactions.

---

### 13.3 Software Interfaces

| Interface | Purpose | Protocol |
|---|---|---|
| Telephony Provider API | Call routing, recording, SMS | REST / Webhook |
| WhatsApp Business API | Outbound messaging | REST |
| STT/NLP AI Service | Transcription, classification | REST / WebSocket |
| Citizen Validation API | Application number / Aadhaar validation | REST |
| Exam Data API / Database | Exam master data lookup | REST / Direct DB |
| Email/Notification Service | Admin and agent alerts | SMTP / REST |

---

### 13.4 Communication Interfaces

- All API communications shall use HTTPS (TLS 1.2+).
- Webhooks shall be validated with signature verification.
- WebSocket connections for real-time transcription shall be secured and authenticated.

---

## 14. System Constraints and Limitations

| Constraint | Description |
|---|---|
| Telephony Concurrency | Maximum concurrent calls is bounded by the telephony provider's provisioned capacity. |
| AI Accuracy | Transcription and categorization accuracy is dependent on audio quality and AI model maturity; regional language accuracy may be lower than Hindi/English initially. |
| WhatsApp API Limitations | Subject to Meta's messaging policies, template approval processes, and rate limits. |
| DLT Registration | SMS delivery requires pre-approved DLT templates; new templates may take 24–72 hours to activate. |
| Aadhaar API | Citizen validation via Aadhaar is subject to UIDAI's API availability and terms of service. |
| Phase 2 Features | QA Login and AI-suggested resolutions are explicitly deferred to Phase 2 and are not in scope for Phase 1 delivery. |
| Data Residency | All data must be stored within India; offshore AI processing must comply with applicable data protection requirements. |
| Browser Compatibility | The system is optimized for modern browsers; Internet Explorer is not supported. |

---

## 15. Appendix

### 15.1 Ticket Status Lifecycle

```
[Call Completed]
      │
      ▼
   [Open]
      │
      ▼
[Pending Agent Action]
      │
      ├──[Agent Resolves]────────────────────► [Resolved by Agent]
      │                                                │
      ├──[Agent Requests Info]──► [Pending             │
      │                           Citizen Response]    │
      │                               │                │
      │                    [Citizen Responds]          │
      │                               │                │
      ├──[Agent Escalates]──────► [Escalated to Officer]
      │                                │
      │                ┌───────────────┤
      │                │               │
      │     [Officer Resolves]  [AI Groups Tickets]
      │                │               │
      │    [Resolved by Officer]  [Officer Approves]
      │                │               │
      │                └───────┬───────┘
      │                        │
      │              [Resolved – Batch Response]
      │                        │
      │         ┌──────────────┴───────────────┐
      │         │                              │
      │  [Citizen Satisfied]        [Citizen Dissatisfied]
      │         │                              │
      │       [Closed]                    [Reopened]
      │                                        │
      └────────────────────────────────────────┘
                    (re-enters queue)
```

---

### 15.2 Role-Permission Matrix

| Feature / Module | Admin (DG) | Team Lead | Exam Lead | Call Agent | Officer (Dept) | Officer (Head) | Citizen | QA (P2) |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| User Management | R/W | - | - | - | - | - | - | - |
| System Configuration | R/W | - | - | - | - | - | - | - |
| Category Management | R/W | - | - | - | - | - | - | - |
| Call Handling | R | R/W | R/W | R/W | - | - | - | R |
| Ticket View (All) | R/W | R/W | R/W | Own | Escalated | Escalated | Own | R |
| Ticket Resolution | - | R/W | R/W | R/W | R/W | R/W | - | - |
| Ticket Escalation | - | R/W | R/W | R/W | - | - | - | - |
| Ticket Grouping | R/W | - | - | - | R | R/W | - | R |
| Officer Response Approval | - | - | - | - | - | R/W | - | - |
| Citizen Notification | R/W | - | - | - | R/W | R/W | - | - |
| Reports (All) | R/W | Team | Exam | Own | Exam | Exam | - | R |
| Audit Logs | R | - | - | - | - | - | - | R |
| Transcript Access | R | R | R | Own Call | Escalated | Escalated | - | R |
| Ticket Reopen | - | - | - | - | - | - | R/W | - |

*R = Read, W = Write/Edit, P2 = Phase 2 only*

---

### 15.3 Phase-wise Feature Rollout

| Feature | Phase 1 | Phase 2 |
|---|:---:|:---:|
| AI Voice Bot (Intake) | ✓ | |
| Call Transcription | ✓ | |
| Query Categorization | ✓ | |
| Grievance Ticket Management | ✓ | |
| Agent Dashboard | ✓ | |
| Officer Dashboard | ✓ | |
| Similar Issue Grouping | ✓ | |
| Batch Response | ✓ | |
| Citizen Self-Service Portal | ✓ | |
| SMS Notifications | ✓ | |
| WhatsApp Notifications | ✓ | |
| AI Outbound Calls | ✓ | |
| Admin Console | ✓ | |
| Core Reports and Dashboards | ✓ | |
| QA Login and Auditing | | ✓ |
| AI-Suggested Resolutions | | ✓ |
| Advanced Analytics | | ✓ |
| Predictive Escalation | | ✓ |

---

*End of Document*

---

*Document prepared based on NTA Call Centre Management System operational requirements. Version 1.0 – March 2026.*
