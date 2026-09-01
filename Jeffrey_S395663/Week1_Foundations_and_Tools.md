# Week 1 — Foundations, Tools and User Stories

**Focus:** Understand what a Business Analyst does, learn the core tools, and practise writing user stories in Jira.

---

## 1. What a Business Analyst does

A Business Analyst sits between the business and the technical team. The job is not to write production code. The job is to understand the problem, capture requirements clearly, and help the team deliver a solution that the business can actually use.

Typical week-to-week work:

- Talk to stakeholders and confirm what problem they are trying to solve
- Document current processes and proposed changes
- Write requirements, user stories and acceptance criteria
- Support developers and testers during delivery
- Help the business test and sign off the solution

---

## 2. Common BA requirements (from job ads)

| Category | Common requirements |
| --- | --- |
| Requirements analysis | Gather, analyse and document business and functional requirements |
| Stakeholder management | Communicate with business, technical and project stakeholders |
| Workshop facilitation | Conduct interviews, workshops and stakeholder meetings |
| Documentation | Produce user stories, functional specifications and business requirements |
| Process analysis | Analyse current processes and identify improvements |
| Communication | Translate technical information into clear business language |
| Risk management | Identify risks, assumptions, issues and dependencies |
| Solution delivery | Work with technical teams to ensure solutions meet business needs |
| Personal skills | Work independently, manage priorities and solve complex problems |

**Interview note:** if a skill is on a resume, be able to explain what it is, why it is used, how you used it, and what value it provided.

---

## 3. Tools and learning resources

| Tool / Technology | Purpose | Learning resource |
| --- | --- | --- |
| Jira | Manage requirements and user stories | Atlassian tutorials |
| Microsoft Visio | Create process maps and diagrams | Microsoft Learn |
| SQL | Query and analyse data | SQL tutorials |
| Power BI | Analyse and visualise business data | Microsoft Learn |
| Confluence | Store and share project documentation | Atlassian tutorials |

---

## 4. Tool notes (4-line structure)

Use this structure for any tool that might appear in class or in an interview.

### 4.1 Jira

**What it is:** Jira is a project management tool used by agile teams.  
**Why it is used:** It helps teams record requirements, manage user stories and track project tasks.  
**Common use cases:** Sprint planning, issue tracking, requirement management and task allocation.  
**Simple example:** A Business Analyst can create a user story in Jira and assign it to the development team.

### 4.2 Microsoft Visio

**What it is:** Microsoft Visio is a diagramming and process-mapping tool.  
**Why it is used:** It helps Business Analysts present complex business processes visually.  
**Common use cases:** As-Is and To-Be process maps, flowcharts and data flow diagrams.  
**Simple example:** A Business Analyst can use Visio to show how a customer request moves through different departments.

### 4.3 SQL

**What it is:** SQL is a language used to access and manage data stored in databases.  
**Why it is used:** It allows Business Analysts to examine data and support evidence-based decisions.  
**Common use cases:** Retrieving data, filtering records, checking data quality and producing reports.  
**Simple example:** A Business Analyst can use an SQL query to identify customers with overdue payments.

### 4.4 Power BI

**What it is:** Power BI is a business intelligence and data visualisation tool.  
**Why it is used:** It converts business data into reports and interactive dashboards.  
**Common use cases:** Performance reporting, trend analysis and presentation of key business metrics.  
**Simple example:** A Business Analyst can create a dashboard showing monthly collection performance.

### 4.5 Confluence

**What it is:** Confluence is an online documentation and collaboration platform.  
**Why it is used:** It allows project teams to store and share requirements and project information.  
**Common use cases:** Meeting notes, business requirements, project documentation and team knowledge sharing.  
**Simple example:** A Business Analyst can publish workshop notes and approved requirements in Confluence.

---

## 5. Jira practice — creating user stories

A user story describes a requirement from the user's point of view:

```
As a <who>
I want <what>
So that <why>
```

Good stories are small enough to discuss in a sprint, valuable to a user, and testable.

### Sample stories for overdue collections

**STORY-01 — View overdue invoices**

```
As a collections officer
I want to see a list of overdue invoices
So that I can follow up with customers before the debt ages further
```

**STORY-02 — Filter by ageing bucket**

```
As a finance supervisor
I want to filter overdue invoices by 30 / 60 / 90+ days
So that I can focus the team on the highest-risk accounts
```

**STORY-03 — Record a follow-up**

```
As a collections officer
I want to record the date and result of each customer follow-up
So that the next person who opens the account knows what already happened
```

### How this would look in Jira

| Field | Example (STORY-01) |
| --- | --- |
| Issue type | Story |
| Summary | View overdue invoices |
| Description | User story + business context |
| Acceptance criteria | List of testable conditions |
| Priority | High |
| Labels | collections, finance |
| Assignee | Developer after sprint planning |

A BA usually **writes and refines** the story. The Product Owner / business owner **prioritises** it. Developers **estimate and build** it.

---

## 6. Acceptance criteria (starter)

Acceptance criteria tell the team when a story is done. Week 4 covers Given-When-Then in more detail. For Week 1, keep them short and testable:

**STORY-01**

- The list shows only invoices past their due date
- Each row shows customer name, invoice number, due date, amount and days overdue
- If there are no overdue invoices, the screen shows "No overdue invoices"
- The list is sorted with the oldest overdue invoice first

---

## 7. Week 1 checklist

- [ ] Can explain the BA role in one minute
- [ ] Can match each job-ad skill to a real task
- [ ] Can describe Jira, Visio, SQL, Power BI and Confluence in four lines
- [ ] Created at least two user stories in Jira (or as practice tickets)
- [ ] Saved this week's notes so they can be reused in Weeks 2–5

---

## 8. Key takeaways

- A BA translates business problems into requirements the team can build and test.
- Tools do not replace analysis. Jira stores stories; Visio shows process; SQL and Power BI provide evidence; Confluence keeps the approved version.
- A user story without a "so that" is usually missing the business value.
- Week 2 uses Visio to show the collections process that these stories are trying to improve.
