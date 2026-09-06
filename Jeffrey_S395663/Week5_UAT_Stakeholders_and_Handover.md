# Week 5 — Stakeholders, UAT, Traceability and Handover

**Focus:** Close the loop. Confirm who owns the work, prove the requirements with User Acceptance Testing (UAT), keep a traceability matrix, and hand the release to the business.

---

## 1. Why this week matters

A story in Jira is not a delivered requirement. Week 5 sits between "the team built it" and "the business can sign off".

| Skill | Question it answers |
| --- | --- |
| Stakeholder map / RACI | Who decides, who does the work, who must be informed |
| RAID | What risks, assumptions, issues and dependencies exist |
| Requirements Traceability Matrix (RTM) | Every Must requirement has a story and a test |
| UAT | Real users confirm the process works for them |
| Defect logging | Failed tests become tracked work |
| Change control | New requests are assessed, not silently added |
| Release notes / handover | Support and users know what shipped |

---

## 2. Stakeholder analysis

### 2.1 Power / interest

| Stakeholder | Power | Interest | How the BA engages |
| --- | --- | --- | --- |
| Finance supervisor | High | High | Manage closely — owns sign-off and performance targets |
| Collections officers | Low | High | Involve in workshops, wireframe review and UAT |
| Finance officer | Medium | Medium | Keep informed — invoice status must stay correct |
| Development lead | Medium | High | Collaborate on feasibility, estimates and defects |
| QA / tester | Low | High | Share Gherkin so tests match acceptance criteria |
| Customer (end payer) | Low | High | Do not design from one complaint; sample in process design only |

High power + high interest people should see the wireframe and UAT results. High power + low interest people need a short status, not a long BRD.

### 2.2 RACI

R = Responsible (does the work), A = Accountable (one owner), C = Consulted, I = Informed.

| Activity | BA | Finance supervisor | Dev lead | QA | Collections officer |
| --- | --- | --- | --- | --- | --- |
| Elicit and document requirements | R | A | C | I | C |
| Write user stories and AC | R | A | C | C | I |
| Build the feature | C | I | R / A | I | I |
| Write UAT scripts | R | C | I | C | C |
| Execute UAT | C | A (sign-off) | I | C | R |
| Log and triage defects | R | C | C | C | I |
| Release notes and handover | R | A | C | I | C |

There should be only **one A** on each row. Two Accountable people usually means nobody is accountable.

---

## 3. RAID log (risk management from Week 1)

Week 1 listed risk management as a common BA requirement: identify risks, assumptions, issues and dependencies.

| ID | Type | Description | Impact | Action |
| --- | --- | --- | --- | --- |
| R-01 | Risk | Finance data refresh is delayed, so the overdue list is stale | Officers chase paid invoices | Confirm daily refresh (NFR-03) before UAT |
| A-01 | Assumption | Invoice Status in the finance system is trustworthy | Wrong list | Week 3 data-quality queries must pass |
| I-01 | Issue | Some Paid invoices have a blank PaidDate | Dashboard under-reports collections | Defect to data owner; do not hide it in Power BI |
| D-01 | Dependency | UAT needs a staging copy of invoice data | UAT cannot start | Environment ready is an entry criterion |

---

## 4. Requirements Traceability Matrix (RTM)

The RTM proves that Must requirements were not lost between the BRD, Jira and testing.

| Business goal | FR / NFR | Story | Gherkin / UAT | Result |
| --- | --- | --- | --- | --- |
| Chase overdue debt sooner | FR-01, FR-02 | STORY-01 | UAT-01, UAT-02 | |
| Focus on oldest debt | FR-03 | STORY-02 | UAT-03 | |
| Keep a shared follow-up history | FR-04, NFR-02 | STORY-03 | UAT-04 | |
| Stop calling customers who have paid | FR-05 | STORY-04 | UAT-05 | |
| Restrict access to finance staff | NFR-01 | STORY-01 (auth) | UAT-06 | |
| See monthly collection performance | FR-07 | STORY-05 | UAT-07 | |

A Must requirement that does not appear in both the RTM and a UAT script is not ready for sign-off.

---

## 5. UAT vs other testing

| Type | Who usually runs it | Question it answers |
| --- | --- | --- |
| Unit / integration | Developers | Does this code work with other code? |
| System / QA testing | QA | Does the build match the acceptance criteria? |
| **UAT** | Business users, facilitated by the BA | Does this solve the business problem in real work? |

UAT is not a second QA cycle. If QA has not passed the build, do not start UAT. Users will spend their time finding crashes instead of checking the process.

### Entry criteria (UAT may start)

- Sprint 1 Must stories meet the team's definition of done
- QA has passed the Gherkin scenarios for those stories
- Staging has realistic (or anonymised) invoice data
- UAT scripts and testers are confirmed
- Known open defects are listed so users are not surprised

### Exit criteria (UAT is complete)

- All Must UAT cases passed, or failed cases have an agreed defect and target fix
- No open Critical / High defects
- Finance supervisor has signed the UAT sign-off
- RTM is updated with actual results

---

## 6. UAT scripts (business-user language)

Testers should be collections officers, not only QA.

### UAT-01 Happy path — see overdue invoices

| Step | Action | Expected result |
| --- | --- | --- |
| 1 | Log in as a collections officer | Overdue Invoices screen opens |
| 2 | Look at the list | Only Overdue invoices appear |
| 3 | Check columns | Customer, invoice number, due date, amount, days overdue are present |
| 4 | Check sort | Oldest due date is at the top |

**Pass / Fail:** ______  
**Tester:** ______  
**Date:** ______

### UAT-02 Empty state

| Step | Action | Expected result |
| --- | --- | --- |
| 1 | Use a login / filter with no overdue invoices | Message "No overdue invoices" is shown |

### UAT-03 Ageing filter

| Step | Action | Expected result |
| --- | --- | --- |
| 1 | Choose 90+ days | Only invoices 90+ days overdue remain |
| 2 | Choose All | Full overdue list returns |

### UAT-04 Record follow-up

| Step | Action | Expected result |
| --- | --- | --- |
| 1 | Open invoice 103 | Invoice detail / panel opens |
| 2 | Add follow-up: Phone / promised payment | Note is saved with user name and time |

### UAT-05 Paid invoice leaves the list

| Step | Action | Expected result |
| --- | --- | --- |
| 1 | Confirm invoice 102 is visible while Overdue | Invoice 102 is on the list |
| 2 | After status is Paid (test data), refresh | Invoice 102 is gone |

### UAT-06 Unauthorised access

| Step | Action | Expected result |
| --- | --- | --- |
| 1 | Log in as a user with no finance role | Overdue list is not shown (or access denied) |

### UAT-07 Dashboard (if STORY-05 is in the release)

| Step | Action | Expected result |
| --- | --- | --- |
| 1 | Open the collections dashboard | Cards show overdue total and collected amount |
| 2 | Slice by month / region | Charts change; they match a sample SQL check |

---

## 7. Defects: severity vs priority

| | Meaning | Example |
| --- | --- | --- |
| Severity | How badly the product is broken | Paid invoice still appears on the overdue list (High) |
| Priority | How soon it should be fixed | Fix before UAT sign-off |

A defect log should include: steps to reproduce, expected result, actual result, test data, screenshot, severity, priority.

Do not use hallway conversation as the defect register. Put it in Jira.

---

## 8. Change control

New ideas will appear during UAT ("can we also send reminder SMS?").

| If the request is... | BA action |
| --- | --- |
| A bug against a Must story | Log a defect, fix in this release if High/Critical |
| A small clarification of an in-scope story | Update AC, Confluence and Jira together |
| New functionality (SMS, payment taking, legal letters) | Park as a change request — it was out of scope in Week 4 |

Do not silently enlarge Sprint 1. Record the request, impact, and whether the supervisor still wants it in a later sprint.

---

## 9. Release notes and handover

### Short release note (Sprint 1)

**Collections Tracker — Sprint 1**

- Collections officers can view overdue invoices, filter by ageing, and (if included) record follow-up notes
- Paid invoices are removed from the overdue list
- Access is limited to finance / collections roles
- Known limitation: taking payment is still done in the existing finance system

### Handover checklist

- [ ] Confluence BRD matches what was released
- [ ] Jira stories are Done or have an agreed carry-over
- [ ] RTM updated with UAT results
- [ ] Open defects listed with owners
- [ ] Support / finance know how to use the overdue list
- [ ] Power BI dashboard (if released) has an owner for refresh
- [ ] Sign-off stored with the UAT scripts

---

## 10. Week 5 checklist

- [ ] RACI agreed with the finance supervisor
- [ ] RAID log started
- [ ] Every Must FR appears on the RTM
- [ ] UAT scripts written in business language
- [ ] Defects logged in Jira, not only in chat
- [ ] Out-of-scope UAT ideas parked as change requests
- [ ] Handover pack complete

---

## 11. Key takeaways

- UAT signs off **business value**, not another round of QA.
- Traceability is how a BA proves a requirement was delivered.
- RAID and change control protect scope when testing finds new wishes.
- After Week 5, the same five tools from Week 1 are all in use: Jira (stories and defects), Visio (process), SQL (evidence), Power BI (performance), Confluence (approved documents and handover).
