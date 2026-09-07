# User Stories and Sprint Notes

## Where a BA fits inside a Scrum team

My own summary: the BA (often blended with Product Owner) keeps the
backlog honest — makes sure every story is clear enough that a
developer doesn't have to guess, and prioritised enough that the team
is always working on what matters most.

## Ceremony cheat-sheet, in my own words

- **Sprint Planning:** deciding what's realistic to commit to
- **Daily Standup:** surfacing blockers fast, not a status theatre
- **Sprint Review:** showing real work to real stakeholders
- **Retrospective:** the team's honesty hour

## A user story I wrote

Feature: Seat-hold countdown timer for the cinema booking site

As a customer selecting seats, I want to see a countdown timer on my
held seats so that I know how much time I have left before I lose them.

**Acceptance criteria:**
1. Given a customer has selected seats, when the seat-hold begins, then
   a visible countdown timer starts at 5:00 minutes.
2. Given 1 minute remains on the timer, when the countdown reaches
   1:00, then the customer sees an on-screen warning message.
3. Given the timer reaches 0:00 without payment being completed, when
   the hold expires, then the seats are released and the customer sees
   a clear "seats released" message rather than a silent failure.

## The vague version I started with (and why it wasn't good enough)

First draft: "As a user, I want the system to handle seat holds
properly." — This wasn't testable: "properly" doesn't tell a developer
what to build or a tester what to check. Rewriting it forced me to
specify the exact timing (5 minutes, 1-minute warning) and the exact
failure behaviour (release + message, not silent expiry).

## A question I'd ask in backlog refinement about this story

Should the 5-minute window be configurable per showtime (e.g. shorter
for near-sold-out screenings), or is a fixed value acceptable for the
first release?
