# Week 2 — Microsoft Visio, As-Is and To-Be Process Maps

**Focus:** Learn process mapping and draw a simple As-Is and To-Be map for overdue invoice collections.

---

## 1. Why process mapping matters

Stakeholders often describe symptoms ("we chase invoices too late") without agreeing on the actual steps. A process map makes the current work visible, then shows the improved future process.

| Term | Meaning |
| --- | --- |
| As-Is | How the process works today, including delays and manual work |
| To-Be | How the process should work after the change |
| Gap | The difference between As-Is and To-Be — this becomes requirements |
| Swimlane | A row or column that shows which role or department owns each step |

**Simple example from Week 1:** a BA can use Visio to show how a customer request moves through different departments. This week applies the same idea to collections.

---

## 2. Microsoft Visio — tool recap

**What it is:** Microsoft Visio is a diagramming and process-mapping tool.  
**Why it is used:** It helps Business Analysts present complex business processes visually.  
**Common use cases:** As-Is and To-Be process maps, flowcharts and data flow diagrams.  
**Simple example:** Map the overdue-invoice chase from Finance → Collections Officer → Customer → Finance.

Draw.io / Lucidchart can be used if Visio is not installed. The analysis is the same; only the drawing tool changes.

---

## 3. Basic flowchart shapes

| Shape | Use it for |
| --- | --- |
| Oval | Start / End |
| Rectangle | A process step |
| Diamond | A yes / no decision |
| Arrow | Direction of flow |
| Document | A report, email or spreadsheet |
| Swimlane | Who does the step |

Keep diagrams readable. If a map needs more than one page, split it by process, not by adding more tiny boxes.

---

## 4. As-Is process — overdue invoice chase

**Business problem:** Finance finds overdue invoices late. Follow-up is recorded in email and Excel, so nobody has one view of what has already been done.

### Roles

- Finance officer
- Collections officer
- Customer
- Finance supervisor

### As-Is steps

1. Invoice due date passes in the finance system.
2. Finance officer exports an Excel list at the end of the month.
3. Supervisor emails the list to collections officers.
4. Officer looks up the customer and phones or emails them.
5. Result is stored in the officer's inbox or a personal spreadsheet.
6. If the customer pays, Finance notices it later when reconciling.
7. If the customer does not pay, the invoice may sit until the next monthly export.

### As-Is pain points

| Pain point | Impact |
| --- | --- |
| Monthly Excel export | Overdue invoices can wait up to 30 days before anyone sees them |
| Follow-up lives in email | Handover fails when a person is away |
| No ageing view | 90-day debts are treated the same as 1-day debts |
| Payment and chase are separate | Officers keep calling customers who have already paid |

### As-Is map (text version for Visio)

```
Finance          Collections           Customer
--------         -----------           --------
Due date
passes
   |
Export Excel
(monthly)
   |
Email list  ---> Receive list
                    |
                 Call / email  ------>  Respond or
                    |                   ignore
                 Save note in
                 personal Excel
                    |
Finance later
sees payment
in bank file
```

---

## 5. To-Be process — collections tracker

**Future process:** overdue invoices appear automatically. Officers work from one list. Follow-up is recorded in the same place. A dashboard shows collection performance.

### To-Be steps

1. System flags an invoice the day after the due date.
2. Collections officer opens a shared overdue list (filtered by ageing).
3. Officer contacts the customer and records the outcome in the tracker.
4. If payment is received, the invoice leaves the overdue list.
5. If there is no payment, the case stays visible and can be escalated at 60 / 90 days.
6. Supervisor reviews the Power BI collections dashboard (Week 3).

### To-Be improvements

| Change | Business value |
| --- | --- |
| Daily overdue flag | Faster follow-up |
| Shared tracker | Anyone can see the last contact |
| Ageing filters | Focus on high-risk accounts |
| Dashboard | Supervisor can manage performance, not just spreadsheets |

### To-Be map (text version for Visio)

```
System              Collections              Customer         Supervisor
------              -----------              --------         ----------
Flag invoice
as overdue
   |
Show in shared
overdue list ---> Open list / filter
                      |
                   Contact customer ------> Pay or
                      |                    promise date
                   Record outcome
                      |
Payment received? --yes--> Invoice leaves list
      |
     no
      |
Stay on list / ------------------------------- Review ageing
escalate at 60/90 days                         dashboard
```

---

## 6. Gap analysis (As-Is → To-Be)

The gap is the source of Week 4 requirements.

| Gap | Requirement idea |
| --- | --- |
| No daily overdue view | System must list invoices past due date |
| Notes in personal Excel | System must store follow-up history |
| No ageing buckets | Users must filter 30 / 60 / 90+ days |
| Supervisor has no live report | Dashboard must show monthly collection performance |
| Officers chase already-paid invoices | Paid invoices must drop off the overdue list |

---

## 7. Visio practice checklist

1. Create two pages: **As-Is Collections** and **To-Be Collections**.
2. Add swimlanes for each role.
3. Use a diamond for "Has the customer paid?"
4. Mark pain points on the As-Is map with a red note.
5. Export both diagrams as PNG/PDF and file them in Confluence later (Week 4).

---

## 8. Week 2 checklist

- [ ] Can explain As-Is, To-Be and gap in one sentence each
- [ ] Drew an As-Is swimlane for collections
- [ ] Drew a To-Be swimlane for collections
- [ ] Listed at least four gaps that can become requirements
- [ ] Saved the diagrams for the BRD in Week 4

---

## 9. Key takeaways

- Map the current process before designing the future one. Otherwise the team may automate a broken process.
- Pain points on the As-Is map become candidate user stories.
- A To-Be map is not a system design. It shows who does what; developers still design how the system works.
- Week 3 checks whether the problem is real by querying overdue invoices and reporting collection performance.
