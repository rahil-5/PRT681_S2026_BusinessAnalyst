# Week 4 — Requirements, User Stories and a Simple Wireframe

**Focus:** Turn the collections process and data findings into a small Business Requirements Document (BRD), Jira-ready stories, acceptance criteria and a low-fidelity screen sketch.

---

## 1. From analysis to requirements

Weeks 1–3 produced:

- A business problem (overdue invoices are chased late and tracked in Excel)
- As-Is / To-Be process maps
- SQL evidence and a Power BI view of collection performance

Week 4 writes this down so developers, testers and the business share one meaning.

| Requirement type | Question it answers | Example |
| --- | --- | --- |
| Business requirement | Why are we doing this? | Reduce overdue debt that is older than 60 days |
| User requirement | Who needs what? | Collections officers need a shared overdue list |
| Functional requirement (FR) | What must the system do? | Display invoices with status Overdue |
| Non-functional requirement (NFR) | How well must it do it? | List loads in under 3 seconds for 10,000 invoices |
| Constraint | What must we not break? | Do not change the finance posting rules |

---

## 2. Mini BRD — Customer Collections Tracker

Store this page in **Confluence** after review. Confluence is the source of approved requirements; Jira is the source of delivery work.

### 2.1 Problem statement

Finance only exports overdue invoices once a month. Follow-up notes sit in email and personal spreadsheets. Officers sometimes chase customers who have already paid. Supervisors cannot see live collection performance.

### 2.2 Vision / outcome

Collections officers work from one overdue list, record each follow-up, and supervisors can see monthly collection performance without waiting for a manual Excel pack.

### 2.3 Scope

| In scope (Sprint 1) | Out of scope |
| --- | --- |
| View overdue invoices | Taking customer payments inside the tracker |
| Filter by ageing bucket (30 / 60 / 90+) | Changing invoice generation or GST logic |
| Record follow-up notes | Automated legal letters |
| Remove paid invoices from the overdue list | Full CRM replacement |
| Read-only Power BI collections dashboard | Mobile app |

Out of scope is as important as in scope. It stops hidden extra work from entering the sprint.

### 2.4 Stakeholders (summary)

| Stakeholder | Interest |
| --- | --- |
| Finance supervisor | Live performance, fewer 90-day debts |
| Collections officers | One list and a place to record calls |
| Finance officer | Invoice status stays accurate |
| Development team | Clear, testable stories |
| Customers | Fair contact — not repeated calls after they have paid |

Week 5 expands this into a RACI and power/interest map.

### 2.5 Functional requirements

| ID | Requirement | Priority |
| --- | --- | --- |
| FR-01 | The system shall list invoices with status Overdue | Must |
| FR-02 | Each row shall show customer, invoice number, due date, amount and days overdue | Must |
| FR-03 | Users shall filter the list by 30 / 60 / 90+ ageing buckets | Must |
| FR-04 | Users shall record follow-up date, method and result against an invoice | Must |
| FR-05 | Invoices that become Paid shall leave the overdue list | Must |
| FR-06 | If no overdue invoices exist, the screen shall show a clear empty message | Should |
| FR-07 | Supervisors shall view monthly collected amount and overdue totals | Should |

### 2.6 Non-functional requirements

| ID | Requirement |
| --- | --- |
| NFR-01 | Only finance / collections roles can open the overdue list |
| NFR-02 | Follow-up notes are kept for audit (who entered them and when) |
| NFR-03 | The overdue list refreshes from finance data at least once per day |
| NFR-04 | Personal customer data is visible only to authorised staff |

---

## 3. User stories and INVEST

Format:

```
As a <who>
I want <what>
So that <why>
```

**INVEST:** Independent, Negotiable, Valuable, Estimable, Small, Testable.

| ID | Story | Linked FR |
| --- | --- | --- |
| STORY-01 | As a collections officer, I want to see overdue invoices so that I can follow up before the debt ages further | FR-01, FR-02, FR-06 |
| STORY-02 | As a finance supervisor, I want to filter by ageing bucket so that the team works the highest-risk accounts first | FR-03 |
| STORY-03 | As a collections officer, I want to record each follow-up so that the next person knows what already happened | FR-04, NFR-02 |
| STORY-04 | As a collections officer, I want paid invoices to disappear from the overdue list so that I do not call customers who have already paid | FR-05 |
| STORY-05 | As a finance supervisor, I want a monthly collections dashboard so that I can track performance without a manual Excel pack | FR-07 |

---

## 4. Acceptance criteria (Given–When–Then)

Gherkin makes stories testable. QA and UAT can reuse the same scenarios.

### STORY-01 — View overdue invoices

```gherkin
Scenario: Overdue invoices are listed oldest first
  Given I am a logged-in collections officer
  And there are overdue invoices in the finance data
  When I open the Overdue Invoices screen
  Then I see only invoices with status Overdue
  And each row shows customer, invoice number, due date, amount and days overdue
  And the list is sorted with the oldest due date first

Scenario: Empty state
  Given I am a logged-in collections officer
  And there are no overdue invoices
  When I open the Overdue Invoices screen
  Then I see the message "No overdue invoices"
```

### STORY-02 — Filter by ageing

```gherkin
Scenario: Filter 90+ days
  Given I am on the Overdue Invoices screen
  When I choose the 90+ days filter
  Then I see only overdue invoices that are 90 days or more past due
```

### STORY-03 — Record a follow-up

```gherkin
Scenario: Save a call result
  Given I have opened overdue invoice 103
  When I record follow-up date today, method "Phone" and result "Promised payment Friday"
  Then the note is saved against invoice 103
  And the note shows my name and the time it was entered
```

### STORY-04 — Paid invoices leave the list

```gherkin
Scenario: Paid invoice is removed
  Given invoice 102 is overdue and visible on the list
  When its status changes to Paid
  Then invoice 102 is no longer shown on the Overdue Invoices screen
```

---

## 5. Low-fidelity wireframe

A wireframe is a simple layout. It is not a visual design. Its job is to let stakeholders point at something and say "that field is missing".

```
--------------------------------------------------------------
|  LOGO     Collections Tracker              [User] [Logout] |
--------------------------------------------------------------
|  OVERDUE INVOICES                                          |
|  Filter: (All) (0-30) (31-60) (90+)     Search customer... |
|------------------------------------------------------------|
| Invoice | Customer              | Due date | Amount | Days |
| 105     | Darwin Office Supplies| 30 Apr   | 1,500  | 124  |
| 103     | Alice Springs Motors  | 14 Jun   | 2,500  |  79  |
| 102     | Darwin Office Supplies| 10 Jul   |   800  |  53  |
|------------------------------------------------------------|
|  Selected: Invoice 103                                     |
|  Last follow-up: none                                      |
|  [Add follow-up]     [View customer]                       |
--------------------------------------------------------------
```

Empty state:

```
|  No overdue invoices                                       |
|  New overdue items will appear here after the daily refresh|
```

---

## 6. Jira backlog practice

| Jira field | What the BA enters |
| --- | --- |
| Issue type | Story (bugs later in UAT) |
| Summary | Short verb phrase, e.g. "View overdue invoices" |
| Description | User story + link to Confluence BRD |
| Acceptance criteria | Given-When-Then from section 4 |
| Priority | Must stories first (STORY-01 to STORY-04) |
| Labels | `collections` `sprint-1` |
| Linked issues | FR IDs or Confluence page |

Sprint 1 suggestion: STORY-01, STORY-02, STORY-04 (list + filter + paid-invoice removal). STORY-03 and STORY-05 can follow if capacity remains.

---

## 7. Confluence — where the approved version lives

**What it is:** an online documentation and collaboration platform.  
**Why it is used:** teams store and share requirements and project information.  
**Common use cases:** meeting notes, business requirements, project documentation and knowledge sharing.  
**Simple example:** publish the workshop notes, As-Is/To-Be images, this mini BRD and the approved stories.

Suggested Confluence page tree:

```
Collections Tracker
 ├── Week 2 As-Is and To-Be diagrams
 ├── Mini BRD (this document)
 ├── User stories and acceptance criteria
 └── Decisions / out of scope
```

Rule: if Jira and Confluence disagree, update both. Do not leave two "current" versions.

---

## 8. Week 4 checklist

- [ ] Problem, vision, in-scope and out-of-scope written down
- [ ] FRs and NFRs numbered
- [ ] Stories follow As a / I want / So that
- [ ] Each Must story has Given-When-Then criteria
- [ ] Wireframe reviewed with at least one business stakeholder
- [ ] Stories ready to paste into Jira

---

## 9. Key takeaways

- Scope control is a BA skill. "No" belongs in the BRD as out of scope.
- Acceptance criteria turn a story from a wish into a test.
- A rough wireframe finds missing fields faster than another paragraph of text.
- Week 5 proves these requirements with UAT, a traceability matrix and handover.
