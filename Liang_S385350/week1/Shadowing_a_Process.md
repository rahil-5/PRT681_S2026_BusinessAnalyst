# Shadowing a Process

For this exercise I used a practice case study rather than a real
employer: a **virtual cinema booking website**, where users browse
showtimes, pick seats, and pay online. This is a common type of
practice project for BA training because it has a clear, familiar
process with plenty of stakeholders and edge cases.

## Step 1 — Pick a process worth watching

Process/situation chosen: Booking a movie ticket online, from picking
a film to receiving a confirmed seat.

## Step 2 — Narrate it like a fly on the wall

1. User opens the site and browses films by date/cinema location
2. User selects a showtime and is shown a seat map
3. User picks seats and is taken to checkout
4. User enters payment details and confirms
5. User receives a confirmation email/e-ticket

Clunky parts that would actually happen in real life:
- Seats can get "held" by another user mid-checkout, causing a
  conflict at payment time
- Payment can fail after seats are already reserved, leaving seats
  stuck in limbo if not released properly
- Users on mobile often struggle to zoom into a small seat map

## Step 3 — Name the actual problem

"Users booking tickets on a virtual cinema site struggle to complete a
purchase when seat availability changes mid-session, because the
system doesn't clearly communicate seat holds/expiry, which costs the
business abandoned carts and costs users a frustrating experience."

## Step 4 — Who else has a stake in this?

- Cinema operations team (needs accurate seat/showtime data)
- Payment provider (transaction failures/refunds)
- Customer support (handles complaints about double-booked seats)
- Marketing (cart abandonment affects promo effectiveness)

## Step 5 — What I don't actually know yet

- I'm assuming seat holds currently have no visible countdown timer,
  but haven't confirmed this against a real cinema booking site
- I'm assuming most abandonment happens at the payment step, not
  browsing, but this would need real analytics to confirm

## What surprised me doing this exercise

Even a "simple" booking flow has several timing-dependent edge cases
(seat holds, expiry, concurrent users) that aren't obvious until you
walk through the process step by step.
