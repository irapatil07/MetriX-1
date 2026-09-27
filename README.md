# MetriX

### Online Verification System for Weighing and Measuring Instruments

MetriX is a digital platform designed to streamline and modernize the verification and re-verification lifecycle of weighing and measuring instruments under Legal Metrology.

The system connects businesses/instrument owners, Legal Metrology Officers (LMOs), Government Approved Test Centres (GATCs), and administrators through a centralized digital workflow.

---

## 📌 Problem Statement

The verification of weighing and measuring instruments can involve multiple manual processes such as application submission, officer assignment, inspection scheduling, field verification, documentation, certificate generation, and record maintenance.

MetriX aims to digitize this lifecycle to improve:

* Transparency
* Traceability
* Verification efficiency
* Record management
* Certificate authenticity
* Public accessibility
* Monitoring of instrument verification status

---

## 💡 Proposed Solution

MetriX provides a centralized online platform where:

1. Businesses register their instruments.
2. Verification or re-verification applications are submitted online.
3. LMOs/GATCs are assigned to verification requests.
4. Inspections are scheduled and conducted.
5. Inspection observations and supporting evidence are recorded.
6. Instruments are marked as **PASS** or **FAIL**.
7. For passed instruments, a digitally generated verification certificate is created.
8. The certificate contains a unique QR code.
9. Anyone can scan the QR code to verify the certificate.
10. Verification history and expiry information can be tracked digitally.
11. Customers can file complaints through the QR-verified instrument page, with automatic LMO assignment and real-time status tracking.

---

## ✨ Key Features

### 🏢 Business / Instrument Owner

* Business registration
* Instrument registration
* Online verification application
* Re-verification application
* Application status tracking
* Certificate access
* Verification history
* Expiry notifications

### 👨‍⚖️ Legal Metrology Officer (LMO)

* View assigned applications
* Record inspection observations
* Upload inspection photographs/documents
* Record test readings
* Review verification history

### 🏭 Government Approved Test Centre (GATC)

* View assigned verification requests
* Mark as PASS / FAIL
* Conduct verification activities
* Submit inspection/test results
* Approve verification results
* Initiate certificate generation

### 🛡️ Administrator

* Manage users and roles
* Manage instrument and application records
* Assign LMOs/GATCs (assigned automatically by system)
* Monitor verification activities
* View dashboards and reports
* Maintain audit records

### 🌐 Public Verification

* Scan certificate QR code
* Verify certificate authenticity
* View certificate status
* Check verification and expiry dates
* Can file complaints (if needed)

---

## 🔄 System Workflow

```text
Business / Owner
       │
       ▼
Register Instrument
       │
       ▼
Submit Verification Application
       │
       ▼
LMO / GATC Assignment
       │
       ▼
Schedule Verification
       │
       ▼
Field Inspection
       │
       ├───────────────┐
       ▼               ▼
     PASS             FAIL
       │               │
       ▼               ▼
Generate          Record Failure
Certificate            │
       │               │
       ▼               ▼
Generate QR       Re-verification / Penalty
       │
       ▼
Public Certificate Verification
```

---

## 🏗️ System Architecture

```text
                    ┌─────────────────────┐
                    │      Frontend       │
                    │   React.js / PWA    │
                    │   / Responsive Web  │
                    └──────────┬──────────┘
                               │
                         REST APIs
                               │
                               ▼
                    ┌─────────────────────┐
                    │       Backend       │
                    │   Python + FastAPI  │
                    └──────────┬──────────┘
                               │
                ┌──────────────┼──────────────┐
                │              │              │
                ▼              ▼              ▼
          PostgreSQL       Object Storage    Authentication
          Database         Async Storage /     JWT / RBAC
                │          SQLite
                ▼               |
                                ▼
        Application Data   Photos/Documents
        & Verification
        Records
                               │
                               ▼
                    Certificate Generation
                    PDF + QR Code
```

---

## 🛠️ Tech Stack

| Component              | Technology                    |
| ---------------------- | ----------------------------- |
| Frontend               | React +  PWA                  |
| Backend                | Python + FastAPI              |
| Database               | PostgreSQL                    |
| ORM                    | SQLAlchemy                    |
| Authentication         | JWT                           |
| API                    | REST API                      |
| File Storage           | Async Storage / SQLite        |
| Certificate Generation | ReportLab                     |
| QR Code                | Python QR Code Library        |
| Version Control        | Git + GitHub                  |

---

## LMO/GATC Allocation — Jurisdiction Mapping

MetriX maintains a government-configured jurisdiction map containing:

State / UT   
District  
Sub-district / local jurisdiction  
LMO office  
Authorized LMO  
Approved GATCs  
Instrument types handled by each GATC  
GATC service area  
Availability/capacity  

When an owner submits a verification request:

```text
Instrument Registration
        ↓
Instrument Location
        ↓
State → District → Local Jurisdiction
        ↓
Identify responsible LMO
        ↓
Check eligible GATCs
        ↓
Assignment / Approval by authorized officer
        ↓
Verification
```

---

## Penalty & Fine Management

MetriX does not automatically impose penalties. It records and facilitates 
government-authorized enforcement actions, notices, orders and applicable payments.
Our system works like this:
```text
Inspection / Complaint
        ↓
Officer records observations
        ↓
Possible violation identified
        ↓
Government officer reviews case
        ↓
Applicable Act / Rules / State provisions considered
        ↓
Government authority decides action
        ↓
If penalty/fine is ordered
        ↓
Officer records official order in MetriX
        ↓
Owner/Manufacturer Dashboard
        ↓
View Notice / Order
        ↓
Pay, if payment is legally applicable
        ↓
Payment/status recorded
```
---

## How the Fine Appears on the Owner/Manufacturer Dashboard

Suppose an officer has completed an inspection and the government authority determines that a penalty/compounding amount is applicable.

The owner's dashboard could show:
```text
_________________________________________________________
| Field             | Example                           |
| ----------------- | --------------------------------- |
| Case ID           | LM-2026-001245                    |
| Instrument ID     | WGH-MH-45821                      |
| Issue             | Unverified instrument             |
| Legal provision   | Section 33 / applicable provision |
| Order status      | Payment Pending                   |
| Amount            | ₹XXXX                             |
| Issuing Authority | Legal Metrology Department        |
| Due Date          | DD/MM/YYYY                        |
| Action            | **View Order / Pay**              |
|___________________|___________________________________|
```

## 🔐 Security

MetriX uses role-based access control to ensure that users can access only the functionality relevant to their role.

Example roles:

```text
ADMIN
BUSINESS / MANUFACTURER
INSTRUMENT OWNER
LMO
GATC
PUBLIC
```

Authentication is handled using token-based authentication.

Important certificate information can also be protected using cryptographic signing and verification mechanisms.

---

## 📄 Certificate Generation

When an instrument successfully completes verification:

```text
Verification Result
        │
        ▼
      PASS
        │
        ▼
Collect Instrument + Owner Data
        │
        ▼
Generate Certificate PDF
        │
        ▼
Generate Unique Certificate ID
        │
        ▼
Generate QR Code
        │
        ▼
Store Certificate
        │
        ▼
Make Certificate Verifiable
```

The QR code directs users to a public verification endpoint where the certificate's validity can be checked.

---

## Complaint Management

A complaint can be submitted through:

### Route 1 — QR Code

A consumer sees a verification certificate and scans its QR code.
```text
Certificate
     ↓
Scan QR
     ↓
Public Certificate Verification
     ↓
View Certificate Details
     ↓
"Report an Issue"
     ↓
Complaint Form
```
This is particularly useful because the complaint can automatically reference:

Certificate ID  
Instrument ID  
Verification date  
Business/instrument details available for the complaint workflow  

The complainant doesn't have to manually enter everything.

### Route 2 — Directly through system

A user can visit the public complaint portal:
```text
MetriX
  ↓
Public Portal
  ↓
Register Complaint
  ↓
Select / Enter:
• Certificate ID
• Instrument ID
• Business
• Location
• Complaint category
• Description
• Photo/document evidence
  ↓
Submit
```
### Complaint Resolution Workflow
```text
             Complaint Submitted
                     ↓
              Complaint ID
                     ↓
           Government Department
                     ↓
           Jurisdiction Mapping
                     ↓
          Assigned LMO / Authority
                     ↓
              Investigation
                     ↓
       ┌─────────────┴─────────────┐
       ↓                           ↓
   No Violation                 Violation
       ↓                           ↓
   Close Case              Enforcement Action
                                   ↓
                         Notice / Order / Fine
                                   ↓
                            Owner Response
                                   ↓
                            Resolution
                                   ↓
                          Complaint Closed
```
## Complaint Status Tracking

The complainant would be able to see something like:
```text
Complaint Status
✓ Submitted
      ↓
✓ Under Review
      ↓
✓ Assigned to Officer
      ↓
✓ Investigation Scheduled
      ↓
● Investigation in Progress
      ↓
○ Resolution / Action
      ↓
○ Closed
```

---

## How all of this connects together

```text

                    METRIX
                       │
       ┌───────────────┼────────────────┐
       │               │                │
       ▼               ▼                ▼
 Jurisdiction      Verification      Complaints
   Mapping           Workflow         Portal
       │               │                │
       ▼               ▼                ▼
 LMO / GATC        Inspection        Complaint ID
 Allocation          Results             │
       │               │                 ▼
       └───────────────┼──────────► Government Review
                       │                 │
                       ▼                 ▼
                  Enforcement       Resolution
                       │
                       ▼
                Official Order
                       │
             ┌─────────┴─────────┐
             ▼                   ▼
         No Payment          Payment Applicable
                                 │
                                 ▼
                          Owner Dashboard
                                 │
                                 ▼
                         Payment / Status
```

---

## 📂 Project Structure


```text
MetriX/
│
├── frontend/
│   ├── src/
│   ├── public/
│   └── package.json
│
├── backend/
│   ├── app/
│   │   ├── api/
│   │   ├── models/
│   │   ├── schemas/
│   │   ├── services/
│   │   ├── auth/
│   │   └── main.py
│   │
│   ├── requirements.txt
│   └── .env.example
│
├── certificates/
│
├── docs/
│
├── README.md
└── .gitignore
```

---

## 🚀 Future Scope

Possible future enhancements include:

* Offline field verification with synchronization
* Mobile-first inspection workflows
* Automated expiry notifications
* Advanced analytics dashboards
* Integration with government systems
* Digital signatures for certificates
* AI-assisted risk scoring for inspection prioritization
* Nationwide GATC and instrument databases
* Public complaint/reporting mechanisms

---

## 👨‍💻 Team

**Team Name:** MetriX 1

**Problem Statement:** SIH26036

**Project:** MetriX

```
MetriX © 2026
```
