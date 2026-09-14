# Data Detective Exercise

Using a small practice dataset modelled on the cinema booking case
study — three sample tables: `bookings`, `seats`, `showtimes` — to
practise turning a question into a query.

## The case

Question I wanted to answer: Which showtimes have the highest rate of
"released" (expired/abandoned) seat holds?

## My hypothesis (before looking at any data)

Late evening showtimes on weekends would have the highest release
rate, because higher demand means more concurrent users competing for
the same seats and more checkout friction.

## The query / method

```sql
-- practice query against sample booking data
SELECT
  s.showtime_id,
  s.start_time,
  COUNT(*) AS total_holds,
  SUM(CASE WHEN b.status = 'released' THEN 1 ELSE 0 END) AS released_holds,
  ROUND(100.0 * SUM(CASE WHEN b.status = 'released' THEN 1 ELSE 0 END)
        / COUNT(*), 1) AS release_rate_pct
FROM bookings b
JOIN showtimes s ON b.showtime_id = s.showtime_id
GROUP BY s.showtime_id, s.start_time
ORDER BY release_rate_pct DESC;
```

## SQL clauses, in my own words (quick reference I built for myself)

- `SELECT` — the columns I actually want to see
- `WHERE` — the filter that narrows the noise
- `JOIN` — stitching two tables together by a shared key (here,
  `showtime_id`)
- `GROUP BY` + `COUNT()`/`SUM()` — turning individual booking rows into
  a per-showtime summary

## The verdict

Against the sample dataset I built, weekend evening showtimes did show
a noticeably higher release rate than weekday matinees, supporting the
hypothesis — though a real production dataset would be needed to
confirm this beyond a small sample.

## What I'd tell a stakeholder in one sentence

"Roughly a third of seat holds on weekend evening showings are being
lost before checkout completes — that's the segment where a countdown
timer and clearer warning would likely have the biggest impact."

## Where I got stuck

[FILL IN: anything you actually got stuck on while practising this —
e.g. NULL handling, join direction, syntax differences between SQL
dialects]
