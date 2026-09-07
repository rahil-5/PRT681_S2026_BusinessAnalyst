# From As-Is to To-Be: A Process Story

## The process

Chosen process: Seat selection and checkout on the virtual cinema
booking website.

## Chapter 1 — How it works today (the as-is)

1. User selects a showtime and is shown a seat map
2. User clicks seats — the system marks them as "held" but shows no
   visible timer or expiry warning
3. User proceeds to payment
4. If payment takes too long, the held seats can silently expire and
   become available to someone else
5. User submits payment for seats that may no longer be theirs,
   triggering a failed transaction or a support ticket

## Chapter 2 — Where it hurts

- Users lose seats without warning, causing complaints and lost sales
- Customer support handles a steady stream of "why was I charged/not
  charged for seats I thought I had" tickets
- No clear technical rule exists for how long a hold should last,
  making the bug hard to reproduce and fix consistently

## Chapter 3 — The redesign (the to-be)

1. User selects seats — system starts a visible 5-minute countdown
   timer on screen
2. At 1 minute remaining, the user gets an on-screen warning
3. If the timer expires, seats are released automatically and the user
   is shown a clear message (not a silent failure)
4. Payment authorisation is only accepted while the hold is still
   valid, preventing charge-without-seat scenarios

## Chapter 4 — What has to be true for this to work

- The payment provider must confirm their authorisation window is
  compatible with a 5-minute hold
- The seat-hold logic needs to be enforced server-side, not just
  visually in the browser, or users could bypass the timer
- Customer support needs updated scripts for the new error message

## The diagram

A simple swimlane with two lanes (User, System) covering: select seats
→ hold starts → warning at 1 min → timer expires or payment completes
→ confirmation or release.

## What this exercise taught me about process mapping

The as-is process looked "fine" until I forced myself to write out
what happens when something goes wrong (expired hold) — that's where
the real requirement showed up, not in the happy path.
