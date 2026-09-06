# Week 3 — SQL Queries and Power BI Reporting

**Focus:** Learn basic SQL and create a simple Power BI report for monthly collection performance.

---

## 1. Why a BA needs data skills

Process maps show how work flows. Data shows whether the problem is real and whether the change worked.

From Week 1:

- **SQL** is used to identify customers with overdue payments.
- **Power BI** is used to show monthly collection performance.

A BA does not need to be a database developer. A BA does need to ask the right question, read a result, and spot data quality issues.

---

## 2. SQL — tool recap

**What it is:** SQL is a language used to access and manage data stored in databases.  
**Why it is used:** It allows Business Analysts to examine data and support evidence-based decisions.  
**Common use cases:** Retrieving data, filtering records, checking data quality and producing reports.  
**Simple example:** Identify customers with overdue payments.

### Core clauses

| Clause | Purpose |
| --- | --- |
| `SELECT` | Choose columns |
| `FROM` | Choose the table |
| `WHERE` | Filter rows |
| `JOIN` | Combine related tables |
| `GROUP BY` | Summarise rows |
| `ORDER BY` | Sort the result |
| `COUNT` / `SUM` / `AVG` | Aggregate numbers |

---

## 3. Sample tables (collections)

Imagine two simple tables.

**Customers**

| CustomerId | CustomerName | Region |
| --- | --- | --- |
| 1 | Northside Plumbing | NT |
| 2 | Darwin Office Supplies | NT |
| 3 | Alice Springs Motors | NT |
| 4 | Coastal Builders | QLD |

**Invoices**

| InvoiceId | CustomerId | InvoiceDate | DueDate | Amount | Status | PaidDate |
| --- | --- | --- | --- | --- | --- | --- |
| 101 | 1 | 2026-06-01 | 2026-06-30 | 1200 | Paid | 2026-06-28 |
| 102 | 2 | 2026-06-10 | 2026-07-10 | 800 | Overdue | NULL |
| 103 | 3 | 2026-05-15 | 2026-06-14 | 2500 | Overdue | NULL |
| 104 | 4 | 2026-07-01 | 2026-07-31 | 400 | Open | NULL |
| 105 | 2 | 2026-04-01 | 2026-04-30 | 1500 | Overdue | NULL |

---

## 4. Practice queries

### 4.1 List overdue invoices

```sql
SELECT
    c.CustomerName,
    i.InvoiceId,
    i.DueDate,
    i.Amount,
    DATEDIFF(day, i.DueDate, GETDATE()) AS DaysOverdue
FROM Invoices i
JOIN Customers c ON c.CustomerId = i.CustomerId
WHERE i.Status = 'Overdue'
ORDER BY i.DueDate;
```

This is the Week 1 example in query form: identify customers with overdue payments.

### 4.2 Ageing buckets (30 / 60 / 90+)

```sql
SELECT
    CASE
        WHEN DATEDIFF(day, DueDate, GETDATE()) <= 30 THEN '0-30 days'
        WHEN DATEDIFF(day, DueDate, GETDATE()) <= 60 THEN '31-60 days'
        ELSE '90+ / 61+ days'
    END AS AgeingBucket,
    COUNT(*) AS InvoiceCount,
    SUM(Amount) AS OverdueAmount
FROM Invoices
WHERE Status = 'Overdue'
GROUP BY
    CASE
        WHEN DATEDIFF(day, DueDate, GETDATE()) <= 30 THEN '0-30 days'
        WHEN DATEDIFF(day, DueDate, GETDATE()) <= 60 THEN '31-60 days'
        ELSE '90+ / 61+ days'
    END;
```

### 4.3 Monthly collection performance

```sql
SELECT
    FORMAT(PaidDate, 'yyyy-MM') AS PaidMonth,
    SUM(Amount) AS AmountCollected
FROM Invoices
WHERE Status = 'Paid'
  AND PaidDate IS NOT NULL
GROUP BY FORMAT(PaidDate, 'yyyy-MM')
ORDER BY PaidMonth;
```

### 4.4 Data quality checks a BA should run

```sql
-- Paid invoices should have a paid date
SELECT InvoiceId, Amount, Status, PaidDate
FROM Invoices
WHERE Status = 'Paid' AND PaidDate IS NULL;

-- Overdue invoices should be past the due date
SELECT InvoiceId, DueDate, Status
FROM Invoices
WHERE Status = 'Overdue' AND DueDate >= CAST(GETDATE() AS date);
```

If these queries return rows, the dashboard will be wrong even if the visual looks nice.

---

## 5. Power BI — tool recap

**What it is:** Power BI is a business intelligence and data visualisation tool.  
**Why it is used:** It converts business data into reports and interactive dashboards.  
**Common use cases:** Performance reporting, trend analysis and presentation of key business metrics.  
**Simple example:** A dashboard showing monthly collection performance.

### Suggested report page: Collections Performance

| Visual | What it shows |
| --- | --- |
| Card | Total overdue amount |
| Card | Number of overdue invoices |
| Bar chart | Overdue amount by ageing bucket |
| Line chart | Amount collected by month |
| Table | Invoice-level detail (customer, due date, amount, status) |
| Slicer | Region and status |

### Simple DAX measures

```dax
Total Overdue =
CALCULATE(
    SUM(Invoices[Amount]),
    Invoices[Status] = "Overdue"
)

Amount Collected =
CALCULATE(
    SUM(Invoices[Amount]),
    Invoices[Status] = "Paid"
)

Invoice Count = COUNTROWS(Invoices)
```

`CALCULATE` changes the filter on a measure. `DIVIDE` is safer than `/` because it can handle divide-by-zero.

---

## 6. How Week 3 evidence feeds Weeks 4 and 5

| Finding | What the BA does next |
| --- | --- |
| Most overdue value sits in 61+ days | Raise the priority of ageing filters (STORY-02) |
| Some "Paid" invoices have no PaidDate | Add a data-quality requirement / defect |
| Monthly collected amount is falling | Support the business case for the tracker |
| One region holds most overdue debt | Supervisor may want a region slicer on the dashboard |

SQL answers "is this true?". Power BI helps stakeholders see it in a meeting. Requirements in Week 4 should be based on this evidence, not only on opinions.

---

## 7. Week 3 checklist

- [ ] Can write `SELECT` / `WHERE` / `JOIN` / `GROUP BY`
- [ ] Ran a query that lists overdue invoices
- [ ] Checked at least one data-quality issue
- [ ] Built (or sketched) a Power BI page with cards, a chart and a slicer
- [ ] Noted 2–3 findings that belong in the Week 4 BRD

---

## 8. Key takeaways

- A requirement is stronger when data supports it.
- Filter first (`WHERE`), then summarise (`GROUP BY`).
- Dashboards hide bad data. Always sample the rows behind a KPI.
- Week 4 turns these findings into a BRD, user stories and a wireframe.
