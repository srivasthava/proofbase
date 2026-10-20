# AIDI sample data

**All clients, projects, people and figures below are fictional.** Use them as the reference shape for each record type and as test material for the skill.

Contents:
1. Source documents (raw input)
2. Project frames
3. Weekly entries
4. Quals
5. Past answers
6. Design cards
7. Worked examples, one per job

---

## 1. Source documents

### SOW_Northwind_DHS_Claims_Modernization.docx (extract)
```
STATEMENT OF WORK — Claims Platform Modernization
Client: State of Northwind, Department of Human Services (DHS)
Period of performance: 18 months, starting 2026-07-01
Contract type: Time & Materials with milestone-based deliverables

1. Background
DHS processes ~1.2M benefit claims per year on a 2009 on-premises .NET Framework 4.5 / SQL Server 2012 platform.
Peak-season outages and a 9-day average claim cycle drive this modernization.

2. Scope
- Migrate 14 SQL Server databases (6.8 TB) to Azure SQL Managed Instance
- Upgrade .NET Framework services to .NET 8, containerize, and run on Azure Kubernetes Service behind Azure API Management
- Retire the monolithic claims portal using a strangler-fig approach, one capability at a time
- Global entry via Azure Front Door with WAF; Entra ID for staff SSO
- DevSecOps pipelines (Azure DevOps), IaC (Bicep), observability (Azure Monitor)
- Hypercare and knowledge transfer to DHS operations

3. Governance
- Executive Steering Committee: monthly
- Change Advisory Board: weekly
- Delivery cadence: SAFe, 10-week Program Increments
- Status reporting: weekly written report to DHS program manager

4. Team
34 practitioners.
```

### Weekly_Status_Wk41.pptx (extract)
```
WEEK 41 STATUS (Oct 5–9) — overall: GREEN
Completed
- Wave 1 migration rehearsal: 4 databases (1.9 TB) restored to SQL MI in 5h 40m
- AKS staging cluster hardened against CIS benchmark (92% → 98% pass)
- Eligibility service upgraded from .NET Framework 4.5 to .NET 8 (unit tests 100% passing)
In progress
- Front Door + WAF policy tuning (false positives on legacy SOAP endpoint)
Risks
- R-07: DHS change freeze Nov 20–Dec 1 may compress Wave 2 window (owner: engagement lead)
```

### ADO_Board_Export_Wk42.csv
```
id,title,state,owner,closed
4412,Wave 1 production cutover — 4 DBs to SQL MI (47 min read-only downtime),Done,Data Migration,2026-10-14
4419,Cutover runbook v1.3 published,Done,Data Migration,2026-10-13
4430,WAF custom rule for legacy SOAP endpoint,Done,Platform,2026-10-15
4433,Claims Intake API v2 on AKS (canary 10%),Done,App Modernization,2026-10-16
4436,Strangler route: /eligibility moved from legacy portal to APIM,Done,App Modernization,2026-10-15
4438,Eligibility service .NET 8 container image (412 MB → 118 MB),Done,App Modernization,2026-10-14
4440,Wave 2 dependency mapping,In Progress,Data Migration,
4447,Load test: 3,000 concurrent claim submissions (p95 410 ms),Done,QA,2026-10-16
```

### Mainframe_Assessment_Workforce_Eligibility.pdf (extract)
```
MAINFRAME ASSESSMENT — Unemployment Eligibility System (State Workforce Agency)
Platform: IBM z/OS, CICS, DB2, VSAM; 2.1M lines of COBOL, 640 JCL batch jobs
Annual MIPS cost: $4.6M · 3 remaining COBOL specialists
Recommendation: incremental modernization
- Refactor 11 eligibility functions to Java (Spring Boot), automated conversion + manual review
- Run on Azure Container Apps; DB2 data to Azure SQL Database via CDC
- APIM strangler routing; parallel run with result comparison before each cutover
Status (Week 38): 4 of 11 functions live; parallel-run match 99.98% over 2 weeks
```

---

## 2. Project frames

```json
{
  "record": "project_frame",
  "project_id": "P-101",
  "name": "Claims Platform Modernization",
  "client": "State of Northwind, Department of Human Services",
  "client_descriptor": "a state human-services agency",
  "sector": "State, Local & Higher Ed",
  "scope": [
    "Migrate 14 SQL Server databases (6.8 TB) to Azure SQL Managed Instance",
    "Upgrade .NET Framework services to .NET 8 and run them on AKS behind API Management",
    "Retire the claims portal capability by capability (strangler fig)",
    "Front Door with WAF; Entra ID staff SSO",
    "DevSecOps with Azure DevOps and Bicep; Azure Monitor observability",
    "Hypercare and knowledge transfer"
  ],
  "tech": ["Azure SQL MI", ".NET 8", "AKS", "API Management", "Front Door", "WAF", "Entra ID", "Azure DevOps", "Bicep", "Azure Monitor"],
  "modernization_pattern": "Strangler fig + database migration waves",
  "governance": {
    "steering": "Executive Steering Committee, monthly",
    "change_board": "Change Advisory Board, weekly",
    "cadence": "SAFe, 10-week Program Increments",
    "status_reporting": "Weekly written report to DHS program manager"
  },
  "team_size": 34,
  "start_date": "2026-07-01",
  "evidence": ["SOW_Northwind_DHS_Claims_Modernization.docx §1–4"],
  "open_questions": ["Who is the named DHS program manager for report sign-off?"]
}
```

```json
{
  "record": "project_frame",
  "project_id": "P-104",
  "name": "Eligibility Mainframe Modernization",
  "client": "State Workforce Agency",
  "client_descriptor": "a state workforce agency",
  "sector": "State, Local & Higher Ed",
  "scope": [
    "Refactor 11 COBOL eligibility functions to Java (Spring Boot)",
    "Run services on Azure Container Apps",
    "Replicate DB2 to Azure SQL Database via CDC",
    "Strangler routing through API Management with parallel runs before cutover"
  ],
  "tech": ["COBOL", "CICS", "DB2", "Java", "Spring Boot", "Azure Container Apps", "Azure SQL Database", "API Management"],
  "modernization_pattern": "Incremental refactor with parallel run",
  "governance": {"steering": null, "change_board": null, "cadence": null, "status_reporting": null},
  "team_size": null,
  "start_date": null,
  "evidence": ["Mainframe_Assessment_Workforce_Eligibility.pdf"],
  "open_questions": ["Team size and governance cadence are not in the assessment."]
}
```

---

## 3. Weekly entries (P-101, Week 42)

```json
[
  {"record":"weekly_entry","project_id":"P-101","week":"2026-W42","text":"Moved 4 databases (1.9 TB) to Azure SQL MI in the Wave 1 production cutover with 47 minutes of read-only downtime.","artifact_type":"Deliverable","category":"Cloud migration","tech":["Azure SQL MI"],"metrics":{"databases":4,"data_tb":1.9,"downtime_min":47},"evidence":["ADO #4412"],"confirmed_by":"Data migration lead","sensitivity":"client-confidential"},
  {"record":"weekly_entry","project_id":"P-101","week":"2026-W42","text":"Published cutover runbook v1.3 and walked DHS operations through it.","artifact_type":"Runbook","category":"Operations & support","tech":["Azure SQL MI"],"metrics":{},"evidence":["ADO #4419"],"confirmed_by":"Data migration lead","sensitivity":"client-confidential"},
  {"record":"weekly_entry","project_id":"P-101","week":"2026-W42","text":"Moved /eligibility from the legacy portal to the .NET 8 service on AKS through API Management and retired the old page.","artifact_type":"Deliverable","category":"App modernization","tech":[".NET 8","AKS","API Management"],"metrics":{},"evidence":["ADO #4436"],"confirmed_by":"App modernization lead","sensitivity":"client-confidential"},
  {"record":"weekly_entry","project_id":"P-101","week":"2026-W42","text":"Cut the Eligibility container image from 412 MB to 118 MB.","artifact_type":"Outcome","category":"App modernization","tech":[".NET 8","AKS"],"metrics":{"image_mb_before":412,"image_mb_after":118},"evidence":["ADO #4438"],"confirmed_by":"App modernization lead","sensitivity":"client-confidential"},
  {"record":"weekly_entry","project_id":"P-101","week":"2026-W42","text":"Put Claims Intake API v2 live on AKS at 10% canary traffic.","artifact_type":"Deliverable","category":"App modernization","tech":["AKS"],"metrics":{"canary_pct":10},"evidence":["ADO #4433"],"confirmed_by":"App modernization lead","sensitivity":"client-confidential"},
  {"record":"weekly_entry","project_id":"P-101","week":"2026-W42","text":"Passed a load test of 3,000 concurrent claim submissions at p95 410 ms.","artifact_type":"Outcome","category":"Testing & quality","tech":["AKS"],"metrics":{"concurrent_users":3000,"p95_ms":410},"evidence":["ADO #4447"],"confirmed_by":"QA lead","sensitivity":"client-confidential"},
  {"record":"weekly_entry","project_id":"P-101","week":"2026-W42","text":"Wave 2 dependency mapping is 60% complete.","artifact_type":"In progress","category":"Cloud migration","tech":["Azure SQL MI"],"metrics":{"progress_pct":60},"evidence":["ADO #4440"],"confirmed_by":null,"sensitivity":"client-confidential"}
]
```

---

## 4. Quals

```json
[
  {"record":"qual","qual_id":"Q-001","project_id":"P-101","category":"Cloud migration","statement":"Migrated a state human-services agency's claims databases to Azure SQL Managed Instance, completing a 1.9 TB production cutover with under one hour of read-only downtime.","metric":"47 min downtime · 1.9 TB","tech":["Azure SQL MI"],"evidence":["ADO #4412","Cutover runbook v1.3"],"sensitivity":"reusable","status":"approved","reviewer":"Project lead","review_note":null},
  {"record":"qual","qual_id":"Q-002","project_id":"P-101","category":"App modernization","statement":"Modernized a 2009 .NET Framework claims platform to .NET 8 containers on Azure Kubernetes Service, validated at 3,000 concurrent submissions with 410 ms p95 latency.","metric":"3,000 concurrent · p95 410 ms","tech":[".NET 8","AKS"],"evidence":["ADO #4433","ADO #4438","ADO #4447"],"sensitivity":"reusable","status":"approved","reviewer":"Project lead","review_note":null},
  {"record":"qual","qual_id":"Q-003","project_id":"P-101","category":"App modernization","statement":"Retired a monolithic benefits portal one capability at a time using a strangler-fig pattern behind Azure API Management, with no user-facing outage.","metric":"Zero-outage cutovers","tech":["API Management","AKS"],"evidence":["ADO #4436"],"sensitivity":"reusable","status":"proposed","reviewer":null,"review_note":null},
  {"record":"qual","qual_id":"Q-004","project_id":"P-104","category":"Mainframe modernization","statement":"Refactored 4 of 11 COBOL eligibility functions for a state workforce agency to Java on Azure Container Apps, each verified by a parallel run against production results before cutover.","metric":"4 of 11 functions · 99.98% match","tech":["COBOL","Java","Azure Container Apps"],"evidence":["Mainframe_Assessment_Workforce_Eligibility.pdf (Week 38 status)"],"sensitivity":"reusable","status":"approved","reviewer":"Project lead","review_note":null},
  {"record":"qual","qual_id":"Q-005","project_id":"P-101","category":"Security & compliance","statement":"Hardened Northwind DHS's Kubernetes platform to 98% CIS compliance.","metric":"CIS 92% → 98%","tech":["AKS"],"evidence":["Weekly_Status_Wk41.pptx"],"sensitivity":"reusable","status":"rejected","reviewer":"Project lead","review_note":"Names the client; rewrite with a generalized descriptor."}
]
```

---

## 5. Past answers

```json
[
  {"record":"past_answer","answer_id":"A-001","question":"Describe your approach to migrating large SQL Server estates with minimal downtime.","answer":"We use a wave-based migration factory: discovery with Azure Migrate and DMA, dependency mapping, two full rehearsals per wave, and log-replay cutovers to Azure SQL Managed Instance that keep downtime under an hour.","client_descriptor":"a state revenue department","year":2023,"outcome":"Won","category":"Cloud migration","tags":["sql","migration","cutover","managed instance","downtime"],"source":"RFP_StateRevenue_2023.docx §3.2"},
  {"record":"past_answer","answer_id":"A-002","question":"How will you modernize legacy mainframe applications?","answer":"We modernize mainframes function by function: automated COBOL-to-Java conversion with engineer review, CDC replication from DB2, and a parallel run that compares every result with production before each cutover.","client_descriptor":"a state workforce agency","year":2025,"outcome":"Won","category":"Mainframe modernization","tags":["mainframe","cobol","java","parallel run","db2"],"source":"RFP_WorkforceAgency_2025.pdf §4.1"},
  {"record":"past_answer","answer_id":"A-003","question":"Describe your experience upgrading .NET Framework applications.","answer":"An upgrade factory using the .NET Upgrade Assistant and AI-assisted code changes moved 46 applications to .NET 8, containerized them, and cut hosting cost by 38%.","client_descriptor":"a state licensing board","year":2024,"outcome":"Won","category":"App modernization","tags":[".net","upgrade","containers","legacy"],"source":"RFP_LicensingBoard_2024.docx §2.4"},
  {"record":"past_answer","answer_id":"A-004","question":"How do you retire legacy systems without disrupting users?","answer":"API Management routes each capability to either the legacy system or its modern replacement, so the monolith shrinks one route at a time with rollback in minutes.","client_descriptor":"a county social services department","year":2023,"outcome":"Won","category":"App modernization","tags":["strangler","monolith","api management","incremental"],"source":"RFI_CountySocial_2023.pdf Q7"},
  {"record":"past_answer","answer_id":"A-005","question":"Describe your program governance and status reporting.","answer":"A three-tier governance model (executive steering, program board, delivery teams) with weekly written status, a shared RAID log and PI-based planning.","client_descriptor":"a federal health program office","year":2024,"outcome":"Won","category":"Program governance","tags":["governance","steering","status","raid","safe"],"source":"RFP_FedHealth_2024.docx §6"},
  {"record":"past_answer","answer_id":"A-006","question":"How do you test modernized applications?","answer":"Golden-data regression suites captured from production, contract tests on every API, and a parallel-run period with automated diff reports before each cutover.","client_descriptor":"a federal benefits office","year":2024,"outcome":"Lost","category":"Testing & quality","tags":["testing","regression","parallel run"],"source":"RFP_FedBenefits_2024.pdf §5.3"}
]
```

---

## 6. Design cards

```json
{
  "record": "design_card",
  "design_id": "D-001",
  "name": "Azure SQL Managed Instance migration factory",
  "category": "Cloud migration",
  "cloud": "Azure",
  "context": "Move large estates of SQL Server databases in waves with rehearsed, low-downtime cutovers.",
  "components": [
    {"lane":"Source","name":"On-prem SQL Server 2012","detail":"Compatibility checked with DMA before each wave"},
    {"lane":"Source","name":"Azure Migrate discovery","detail":"Inventory, dependency mapping, SKU sizing"},
    {"lane":"Transfer","name":"Log replay service","detail":"Continuous log shipping; cutover is a log tail plus switch"},
    {"lane":"Target","name":"SQL MI Business Critical","detail":"Zone-redundant, readable secondary for reporting"},
    {"lane":"Operate","name":"Azure Monitor + Defender for SQL","detail":"SQL Insights alerts; vulnerability assessment from day one"}
  ],
  "decisions": [
    {"decision":"SQL MI over Azure SQL Database","why":"Cross-database queries and SQL Agent jobs are needed without rewrite"},
    {"decision":"Log replay over DMS online","why":"Predictable cutover windows for larger databases in rehearsal"}
  ],
  "nfr": ["RPO 0", "RTO under 1 hour", "99.99% SLA"],
  "compliance": ["FedRAMP Moderate", "StateRAMP"],
  "cost": "~$38k / month for 14 databases (from P-101 actuals)",
  "effort": "6–8 weeks per wave of 4–5 databases",
  "build_kit": ["bicep/sqlmi.bicep", "pipelines/cutover.yml", "runbooks/cutover-v1.3.md"],
  "proof": [
    {"engagement_descriptor":"a state human-services agency · Wave 1: 1.9 TB, 47 min downtime","project_id":"P-101","evidence":["ADO #4412"]},
    {"engagement_descriptor":"a state revenue department · 22 databases","project_id":null,"evidence":["RFP_StateRevenue_2023.docx §3.2"]},
    {"engagement_descriptor":"a county health department · 9 databases","project_id":null,"evidence":["Closeout_CountyHealth_2024.pdf"]}
  ],
  "maturity": "gold",
  "source": "harvested",
  "owners": ["Solution architects, P-101"]
}
```

```json
{
  "record": "design_card",
  "design_id": "D-007",
  "name": "Mainframe COBOL to Java on Azure Container Apps",
  "category": "Mainframe modernization",
  "cloud": "Azure",
  "context": "Move mainframe business functions to Java services incrementally, proving each with a parallel run.",
  "components": [
    {"lane":"Mainframe","name":"CICS / COBOL programs","detail":"11 eligibility functions in scope, 4 moved"},
    {"lane":"Mainframe","name":"DB2 + VSAM","detail":"System of record until each function's cutover"},
    {"lane":"Bridge","name":"CDC replication","detail":"Keeps Azure SQL in sync with DB2"},
    {"lane":"Bridge","name":"Parallel-run comparator","detail":"Diffs every transaction; cutover needs a sustained match"},
    {"lane":"Target","name":"Java services on Container Apps","detail":"Spring Boot, converted by tooling and reviewed by engineers"},
    {"lane":"Target","name":"Azure SQL Database","detail":"DB2 retired per table group after cutover"}
  ],
  "decisions": [
    {"decision":"Refactor over rehost emulator","why":"Removes MIPS cost and COBOL skills risk instead of moving it"},
    {"decision":"Container Apps over AKS","why":"Smaller platform team; event-driven scaling fits batch replacements"}
  ],
  "nfr": ["99.95%+ parallel-run match before cutover"],
  "compliance": ["StateRAMP"],
  "cost": null,
  "effort": "8–12 weeks per function group",
  "build_kit": [],
  "proof": [{"engagement_descriptor":"a state workforce agency · 4 of 11 functions live","project_id":"P-104","evidence":["Mainframe_Assessment_Workforce_Eligibility.pdf"]}],
  "maturity": "reviewed",
  "source": "harvested",
  "owners": ["Mainframe modernization team, P-104"]
}
```

```json
{
  "record": "design_card",
  "design_id": "D-008",
  "name": "Event-driven microservices with Service Bus and Dapr",
  "category": "App modernization",
  "cloud": "Azure",
  "context": "Decouple claims processing steps so each scales and fails independently.",
  "components": [
    {"lane":"Publish","name":"Claims Intake","detail":"Publishes ClaimSubmitted events"},
    {"lane":"Publish","name":"Service Bus topic","detail":"Sessions keep one claim's events in order"},
    {"lane":"Process","name":"Eligibility and Payments workers","detail":"Idempotent subscribers; safe to replay"}
  ],
  "decisions": [{"decision":"Dapr pub/sub over direct SDK","why":"Swappable broker and consistent retries"}],
  "nfr": [],
  "compliance": [],
  "cost": null,
  "effort": null,
  "build_kit": [],
  "proof": [],
  "maturity": "draft",
  "source": "hackathon",
  "owners": ["Hackathon team Relay"]
}
```

---

## 7. Worked examples

### Job 1 · Onboard a project
**Input:** the SOW extract in section 1.
**Expected output:** the P-101 project frame in section 2, with one open question asked back to the user.

### Job 2 · Capture the week
**Input:** `ADO_Board_Export_Wk42.csv`.
**Expected output:** the Week 42 entries in section 3, presented as a checklist, all with `confirmed_by: null` until the lead confirms. Item 4440 is tagged `In progress` and left unticked.

### Job 3 · Draft the client report
**Input:** confirmed Week 42 entries plus `Weekly_Status_Wk41.pptx`.
**Expected output:**
```
Summary
Wave 1 is complete: the first four claims databases run on Azure SQL Managed Instance in production, and Eligibility now runs on the modernized .NET 8 platform.

Delivered this week
- Moved 4 databases (1.9 TB) to Azure SQL MI in the Wave 1 production cutover with 47 minutes of read-only downtime
- Published cutover runbook v1.3 and walked DHS operations through it
- Moved /eligibility from the legacy portal to the .NET 8 service on AKS through API Management
- Cut the Eligibility container image from 412 MB to 118 MB
- Put Claims Intake API v2 live on AKS at 10% canary traffic
- Passed a load test of 3,000 concurrent claim submissions at p95 410 ms

Compared with last week
- Wave 1 moved from rehearsal (5h 40m restore) to a production cutover with 47 minutes of read-only downtime
- Eligibility moved from a .NET 8 build with passing unit tests to serving live traffic

Next week
- [to confirm with lead]

Risks and decisions needed
- R-07: DHS change freeze Nov 20–Dec 1 may compress the Wave 2 window (owner: engagement lead)
- Decision needed: should Wave 2 run before or after the change freeze?
```

### Job 4 · Harvest quals
**Input:** confirmed Week 42 entries.
**Expected output:** Q-001, Q-002 and Q-003 shapes from section 4, all with `status: "proposed"`. Item 4419 (runbook) is not harvested as a qual on its own; it becomes evidence for Q-001.
**Counter-example:** Q-005 shows a qual a reviewer rejected because it named the client. The skill must never produce that statement.

### Job 5 · Answer an RFP requirement
**Input:** "Describe your approach to modernizing a legacy .NET and mainframe benefits system without disrupting users, including how you migrate the data."

**Expected matches:**

| Rank | Type | Record | Why it matches | Evidence |
| --- | --- | --- | --- | --- |
| 1 | Qual | Q-004 Mainframe refactor | Mainframe, parallel run, no disruption | P-104 assessment |
| 2 | Past answer | A-004 Strangler-fig retirement | Retire legacy without disruption | RFI_CountySocial_2023 Q7 |
| 3 | Qual | Q-002 .NET to .NET 8 on AKS | .NET modernization with load-tested results | ADO #4433, #4447 |
| 4 | Past answer | A-001 SQL migration factory | Data migration with low downtime | RFP_StateRevenue_2023 §3.2 |

Q-003 is not listed because its status is `proposed`.

**Expected draft:**
```
We modernize legacy benefits systems incrementally, so users never face a big-bang cutover. For mainframe functions, we refactor COBOL to Java one function at a time and verify each with a parallel run against production results before cutover; for a state workforce agency, 4 of 11 functions are live this way [1]. API Management routes each capability to the legacy or modern system, so the old application shrinks one route at a time with rollback in minutes [2]. For .NET services, we upgrade to .NET 8 containers on Azure Kubernetes Service; one platform was validated at 3,000 concurrent submissions with 410 ms p95 latency [3]. Data moves in rehearsed waves with log-replay cutovers that keep downtime under an hour [4].

Sources: [1] Q-004 · [2] A-004 · [3] Q-002 · [4] A-001
```

### Job 6 · Write a design card
**Input:** `Mainframe_Assessment_Workforce_Eligibility.pdf`.
**Expected output:** design card D-007 in section 6 at maturity `reviewed`. It has engagement evidence from P-104 but no published build kit, so it cannot be `proven` yet. Its `cost` stays `null` because the assessment gives the current MIPS cost, not the target run cost.
**Hackathon example:** D-008 enters as `draft` with empty proof, cost and effort, because the source gives none.
