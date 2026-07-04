<!-- markdownlint-disable MD033 MD041 -->

# FreeTV iOS — Full-Cycle QA Project

### STR · STD · STP · SRS · API Testing · Security Disclosure

![Status](https://img.shields.io/badge/Status-Completed-9EE817?style=flat-square)
![Test Cases](https://img.shields.io/badge/Test%20Cases-123-blue?style=flat-square)
![Pass Rate](https://img.shields.io/badge/Pass%20Rate-80%25-9EE817?style=flat-square)
![Defects](https://img.shields.io/badge/Defects-9-red?style=flat-square)
![Platform](https://img.shields.io/badge/Platform-iOS-lightgrey?style=flat-square)

End-to-end manual QA project for the **FreeTV iOS streaming application**, covering the full QA lifecycle — requirements, test planning, design, execution, defect reporting, and final reporting — following the **IEEE 830** and **IEEE 829** standards.

[![FreeTV QA Project Cover](https://github.com/quality-krl/FreeTV_iOS_E2E_QA_Project_STR_STD_STP_SRS/raw/main/assets/screenshots/freetv_cover.png)](https://github.com/quality-krl/FreeTV_iOS_E2E_QA_Project_STR_STD_STP_SRS/blob/main/assets/screenshots/freetv_cover.png)

---

## 📥 Full Documentation

📄 **[Open the full documentation (PDF) →](https://quality-krl.github.io/FreeTV_iOS_E2E_QA_Project_STR_STD_STP_SRS/docs/FreeTV_QA_Documentation.pdf)**
SRS, STP, STD and STR in a single **108-page** file that opens directly in your browser.

The file is organized **results-first** — the outcome comes first, and each document below it drills down into the layer that supports it:

| Document | Standard | Description |
| -------- | -------- | ----------- |
| **STR** — Software Test Report | IEEE 829 | Full test results, execution summary, defect register, RTM, and release recommendation |
| **STD** — Software Test Design | IEEE 829 | 123 test cases with steps, test data, and evidence across four suites |
| **STP** — Software Test Plan | IEEE 829 | Scope, objectives, approach, environment, schedule, and entry/exit criteria |
| **SRS** — Software Requirements Specification | IEEE 830 | 36 Functional + 19 Non-Functional requirements |

---

## 📋 Project Overview

| Field                 | Details                                          |
| --------------------- | ------------------------------------------------ |
| **System Under Test** | FreeTV iOS App — v1.25.32 (build 142)            |
| **Test Type**         | Manual Functional, Non-Functional, API, Database |
| **Environment**       | Production                                       |
| **Device**            | iPhone 14 Pro · iOS 26.3.1 · 128 GB · 4G         |
| **Standards**         | IEEE 830 (SRS) · IEEE 829 (STP / STD / STR)      |
| **Prepared by**       | Kirill Kovalevski                                |
| **Mentor**            | Gal Matalon                                      |

---

## 📊 Execution Summary

| Status      | Count   |
| ----------- | ------- |
| ✅ Passed    | 99      |
| ❌ Failed    | 9       |
| ⏸️ Blocked  | 15      |
| ⏭️ Skipped  | 0       |
| 📋 **Total** | **123** |

**Pass Rate: 80%** — or **91%** (99 / 109) once the database suite, blocked by production constraints, is excluded.

---

## 🧪 Results by Suite

| Suite          | Total   | Passed | Failed | Blocked | Pass Rate |
| -------------- | ------- | ------ | ------ | ------- | --------- |
| Functional     | 71      | 67     | 4      | 0       | 94%       |
| Non-Functional | 20      | 16     | 3      | 1       | 80%       |
| API            | 18      | 16     | 2      | 0       | 89%       |
| Database       | 14      | 0      | 0      | 14      | N/A       |
| **Total**      | **123** | **99** | **9**  | **15**  | **80%**   |

> Database cases were designed to demonstrate data-integrity validation but blocked from execution due to production-environment constraints (no direct DB access — see constraint CON-003).

---

## 🐛 Defect Summary

| Severity       | Count |
| -------------- | ----- |
| 🔴 S2 · High    | 2     |
| 🟠 S3 · Medium  | 2     |
| 🟢 S4 · Low     | 5     |
| **Total**      | **9** |

All 9 defects were logged as **Open** (Fixed: 0 · Closed: 0) at the close of the test cycle.

### 🔴 High Severity

| ID    | Title                                                              | Requirement     |
| ----- | ------------------------------------------------------------------ | --------------- |
| FTV-5 | OTP remains valid for 60 minutes — exceeds the defined security threshold | FR-007, NFR-011 |
| FTV-8 | Multiple content endpoints accessible without authentication       | FR-013, NFR-010 |

### 🟠 Medium Severity

| ID    | Title                                                       | Requirement |
| ----- | ----------------------------------------------------------- | ----------- |
| FTV-7 | Internal system architecture exposed in API error responses | NFR-010     |
| FTV-9 | Playback position not restored after app force-close        | NFR-020     |

### 🟢 Low Severity

| ID    | Title                                                        |
| ----- | ------------------------------------------------------------ |
| FTV-1 | Profile name truncation inconsistency                        |
| FTV-2 | Silent blocking — no error feedback for invalid phone number |
| FTV-3 | Special characters accepted without error feedback           |
| FTV-4 | Search history cleared without confirmation prompt           |
| FTV-6 | CATCH UP category label displayed in English                 |

> ⚠️ **Responsible Disclosure:** The security findings (FTV-7, FTV-8) were reported to the FreeTV development team. Sensitive endpoint URLs and internal architecture details are withheld from this public documentation.

---

## 🔍 Testing Areas

- Onboarding & Authentication
- Live TV Streaming
- VOD & Catch-Up Content
- Search & Search History
- Watchlist Management
- Profile Management (multi-profile)
- Navigation
- API Endpoints (auth, content, search, watchlist)
- Database-related Validation
- Performance, Security, Compatibility, Localization, Recovery

---

## 🛠️ QA Methodologies

- Positive / Negative Testing
- Boundary Value Analysis (BVA)
- Equivalence Partitioning
- Exploratory Testing
- Edge Case Testing
- Risk-based Testing

---

## 🧰 Tools Used

| Tool                | Purpose                                          |
| ------------------- | ------------------------------------------------ |
| TestRail            | Test case management — 123 cases across 4 suites |
| JIRA                | Bug tracking — 9 defects filed                   |
| Fiddler             | API traffic capture and analysis                 |
| Postman             | API request replay and validation                |
| ScreenPal           | Screenshot annotation                            |
| iOS Screen Recording| Video evidence for reproduction steps            |

### Key API Discoveries

- OTP validation endpoint uses **PUT**, not POST as originally assumed
- **4 simultaneous search requests** fire on each keystroke (search-as-you-type)
- Content endpoints return **200 OK without authentication** — security vulnerability (FTV-8)
- Watchlist endpoint correctly enforces **device-level authentication**

---

## 🚦 Release Recommendation

> **NOT RECOMMENDED FOR RELEASE** in the current state. Two High-severity defects must be resolved and retested first: **FTV-5** (OTP validity period) and **FTV-8** (unauthenticated content access).

[![Risk Assessment](https://github.com/quality-krl/FreeTV_iOS_E2E_QA_Project_STR_STD_STP_SRS/raw/main/assets/screenshots/freetv_risk_assessment.png)](https://github.com/quality-krl/FreeTV_iOS_E2E_QA_Project_STR_STD_STP_SRS/blob/main/assets/screenshots/freetv_risk_assessment.png)

---

## 🗂️ Sample Defect Documentation

Each defect was logged in JIRA with severity, priority, related requirement, environment, reproduction steps, expected vs. actual results, and annotated screenshot / video evidence.

**FTV-5 · High Severity** — OTP remains valid far beyond the industry standard (release blocker):

[![FTV-5 JIRA Bug Report](https://github.com/quality-krl/FreeTV_iOS_E2E_QA_Project_STR_STD_STP_SRS/raw/main/assets/screenshots/freetv_jira_ftv5.png)](https://github.com/quality-krl/FreeTV_iOS_E2E_QA_Project_STR_STD_STP_SRS/blob/main/assets/screenshots/freetv_jira_ftv5.png)

**FTV-4 · Low Severity** — with annotated on-device screenshot evidence:

[![FTV-4 JIRA Bug Report](https://github.com/quality-krl/FreeTV_iOS_E2E_QA_Project_STR_STD_STP_SRS/raw/main/assets/screenshots/freetv_jira_ftv4.png)](https://github.com/quality-krl/FreeTV_iOS_E2E_QA_Project_STR_STD_STP_SRS/blob/main/assets/screenshots/freetv_jira_ftv4.png)

---

## 📊 Test Execution Results

[![Overall Test Results](https://github.com/quality-krl/FreeTV_iOS_E2E_QA_Project_STR_STD_STP_SRS/raw/main/assets/screenshots/freetv_results_summary.png)](https://github.com/quality-krl/FreeTV_iOS_E2E_QA_Project_STR_STD_STP_SRS/blob/main/assets/screenshots/freetv_results_summary.png)

[![Results by Suite](https://github.com/quality-krl/FreeTV_iOS_E2E_QA_Project_STR_STD_STP_SRS/raw/main/assets/screenshots/freetv_results_by_suite.png)](https://github.com/quality-krl/FreeTV_iOS_E2E_QA_Project_STR_STD_STP_SRS/blob/main/assets/screenshots/freetv_results_by_suite.png)

[![Defect Summary by Severity](https://github.com/quality-krl/FreeTV_iOS_E2E_QA_Project_STR_STD_STP_SRS/raw/main/assets/screenshots/freetv_defects.png)](https://github.com/quality-krl/FreeTV_iOS_E2E_QA_Project_STR_STD_STP_SRS/blob/main/assets/screenshots/freetv_defects.png)

[![Requirements Coverage](https://github.com/quality-krl/FreeTV_iOS_E2E_QA_Project_STR_STD_STP_SRS/raw/main/assets/screenshots/freetv_coverage.png)](https://github.com/quality-krl/FreeTV_iOS_E2E_QA_Project_STR_STD_STP_SRS/blob/main/assets/screenshots/freetv_coverage.png)

---

## 👤 Author

**Kirill Kovalevski** — QA Engineer

**Mentor:** Gal Matalon · **Institution:** המכללה לאוטומציה · **Duration:** April — June 2026
