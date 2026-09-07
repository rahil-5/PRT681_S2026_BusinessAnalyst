# BABOK, In My Own Words

The official BABOK language is dense, so I rewrote each knowledge area
as a plain-English analogy, then tied each one back to my cinema
booking case study to make it concrete.

## The six areas, translated

1. **Planning and Monitoring** → "Deciding how I'll work before I
   start working." For the cinema project: deciding upfront that I'd
   validate the seat-hold problem with data before proposing a fix.
2. **Elicitation and Collaboration** → "Actually asking people what
   they need." For the cinema project: this would mean talking to
   cinema staff and customer support, not just guessing at pain points.
3. **Requirements Life Cycle Management** → "Keeping track of every
   requirement so nothing gets forgotten." E.g. tracking the seat-hold
   timer requirement from idea → ticket → build → test.
4. **Strategy Analysis** → "Figuring out where we are, where we want
   to be." Current state: no visible seat-hold timer. Future state:
   users see a countdown and get warned before losing their seats.
5. **Requirements Analysis and Design Definition** → "Turning messy
   conversations into something precise." E.g. "seats should be held
   for 5 minutes" becomes a specific, testable rule.
6. **Solution Evaluation** → "Checking whether the fix actually
   worked." E.g. did cart abandonment at checkout actually drop after
   adding the countdown timer?

## Requirement types, with my own cinema-project examples

- **Business requirement:** Reduce checkout abandonment on the booking
  site by 15%
- **Stakeholder requirement:** Customer support wants clearer error
  messages when a seat is no longer available
- **Solution requirement (functional):** The system must release a
  held seat automatically after 5 minutes of inactivity
- **Solution requirement (non-functional):** The seat map must load in
  under 2 seconds on mobile
- **Transition requirement:** Existing in-progress bookings need to be
  migrated safely when the new seat-hold logic goes live

## Elicitation technique I'd pick, and why

Scenario: Understanding why users abandon checkout on the cinema site.
Technique I'd use: A mix of analytics review (where do users drop off)
plus a short user survey at the abandonment point, rather than just
interviewing internal staff who don't experience the bug firsthand.
Why not the alternatives: A workshop would be too slow to run for a
narrow, specific drop-off question; observation isn't practical for a
website used privately at home.

## The knowledge area I keep coming back to

Elicitation and Collaboration — because in the cinema case study, the
"seat hold" problem only becomes obvious once you actually watch or ask
someone go through the flow; it's easy to miss from a spec document
alone.
