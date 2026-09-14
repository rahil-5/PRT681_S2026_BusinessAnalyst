# Stakeholder Map and Engagement Plan

## The grid I used

Power/Interest grid, four quadrants:

| | Low Interest | High Interest |
|---|---|---|
| **High Power** | Keep Satisfied | Manage Closely |
| **Low Power** | Monitor | Keep Informed |

## My scenario

Project chosen: Virtual cinema booking website — specifically the
seat-hold/checkout problem identified during discovery.

## The cast of characters

| Who | Power | Interest | Quadrant | How I'd actually reach them |
|-----|-------|----------|----------|-------------------------------|
| Head of Digital/Product Owner | High | High | Manage Closely | Regular short syncs, decision-ready options |
| Payment provider (external) | High | Low | Keep Satisfied | Scheduled check-ins on integration changes |
| Customer support team | Low | High | Keep Informed | Share updates on fixes affecting complaint volume |
| End users/customers | Low | High | Keep Informed / Monitor | Surveys at the point of drop-off |

## The one stakeholder I almost missed

The payment provider's technical team — easy to overlook because they're
external and not in daily standups, but any change to the seat-hold
timing directly affects when a payment authorisation has to complete.

## My engagement plan, in three questions per group

**Group: Customer support**
1. What are the most common complaints about seat booking right now?
2. How often do customers report losing a seat they thought they'd
   secured?
3. What information would help you resolve these complaints faster?

**Group: Payment provider**
1. What's the current timeout window for a payment authorisation?
2. Would a shorter seat-hold window cause any conflicts on your side?
3. What happens if payment succeeds after a seat has already expired?

## What could go wrong with this plan

The payment provider may have limited availability for check-ins,
which could delay validating whether a shorter seat-hold window is
even technically feasible.
