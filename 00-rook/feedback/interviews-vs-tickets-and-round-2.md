# Interviews vs. tickets, and a plan for round 2

For: Sofia Marino (product designer). From: the Dispatch PM. Drafted 13 Oct 2026.

## What this compares

- **Interviews:** 4 calls, 2-5 Sep 2026, console redesign research (Aunt Dot, Mr. Ambrose, Halloran, Kip).
- **Tickets:** 147 handler tickets, 29 Jun-7 Sep 2026, from 12 handlers (83 still open). Grouped by hand; a different call on a few borderline tickets would move a count by one or two.
- **Ping data:** `rook-database`, 29 Jun-6 Sep. Used only where noted.

**The two groups of handlers don't overlap.** The four interviewees filed one ticket between them (Ambrose, 3043). The other 11 handlers filed the rest, and none of them were interviewed. Some differences below may be about who was asked, not about what matters.

## Side by side

| Theme | Interviews (of 4) | Tickets (of 147) | Read |
|---|---|---|---|
| Callout gone before they could answer | 3 | 16 (15 after 12 Aug) | Agree. |
| Phone quiet / far fewer pings | 2 | 30 | Tickets far louder. Interviewees see it as normal; ticket filers ask if the account is broken. |
| Notice that a callout has come in (handler alert, louder, per-responder sound) | 3 | 2 (alert sounds only) | Loud in interviews, rare in tickets. |
| Text too small / status badge | 2 | 4 (2 identical texts) | Loud in interviews, rare in tickets. |
| Dark mode | 1 (very emphatic) | 4 | Rare in tickets; two say other handlers ask on a forum. |
| Filters | 1 (Ambrose) | 16 | Agree on silent reset (4 tickets). Tickets add shared and second-computer problems. |
| Supply (requisitions, failure reports, catalog, maintenance) | 1 (Halloran) | 26 | Agree. Halloran never filed a ticket. |
| Shared or multi-handler use (shared computer, second sign-in, handover notes) | 0 | 8 | Nobody interviewed works with others. |
| Duplicate pings / push on old phones | 0 | 4 | Not covered. |
| Small console bugs and polish (logout, slow Mondays, feed jump, notes limit, export, time zone, map) | 0 | about 25 | Not covered. |
| Account admin (billing, password reset, phone number, photo) | 0 | 11 | Not covered. |

## Where they disagree

1. **How worrying the quiet stretches are.** Tickets from the handlers of Farlight and The Undertow escalate ("Is Farlight still on the list?"). Dot and Kip treat quiet weeks as normal ("I'm not the person to ask about that part"). The ping data shows a real drop for both sets of responders, so the interviews understate it.
2. **Maintenance scheduling.** Halloran says it has "gotten smarter" about busy weeks. Tickets 3054 and 3109 report suits booked on marathon day, and 3057 and 3126 report reminders that arrived after the service date.
3. **Filter persistence.** Ambrose likes it; the tickets show only 2 thank-yous among 16, with the rest about resets and wrong-person or wrong-computer filters.

## What the ping data adds (not from either source)

- Missed pings went from about 4 to about 30 a week after 12 Aug; callouts where nobody took the ping doubled from 5.5% to 11.1%.
- Four responders (Vesper, Meteor Mite, The Undertow, Farlight) were pinged far less after 12 Aug. Two of their handlers (Dot and Kip) were interviewed and filed no tickets.
- Cause not established. Working explanation: the 60s wait caused misses that lowered their score, and the score only changes when they are pinged. This is a hypothesis; it needs response-time data and the routing owner's input.

## Round 2: who

- Handlers of **Farlight and The Undertow** (the largest ticket filers, the biggest drop).
- Handlers of **Corporal Ashgrove and Halfmoon** (smaller drop; useful as a contrast).
- At least one team where **two handlers share a computer or hand over a shift**.
- Someone who handles **three or more responders**, if there is one (the people interviewed handle one or two).

## Round 2: questions

Keep them open. Don't mention the 4.2 release, the timeout, or ranking, and don't suggest a cause. Never ask for anyone's real identity.

**Callouts and pings**
1. Tell me about the last callout your responder wasn't able to take. What happened, minute by minute?
2. Roughly how many seconds went by between the phone going off and the job being gone?
3. How do you find out a callout has come in? Where is your attention when it does?

**Quiet stretches**
4. Tell me about the last week your responder got less work than usual. When did you first notice?
5. When that happened, what did you do, and who did you contact? What were you told?
6. What would you want the console to show you when it's quiet?

**Filters, sharing and handover**
7. Walk me through how you start and end a shift on the console.
8. Who else uses the console you use, and how do you pass things to them?
9. Tell me about a time a saved filter wasn't what you expected.

**Looking at the screen**
10. When do you use the console and in what light? What do you struggle to see?
11. What alerts or sounds do you rely on? Which do you ignore?

**Supply (for handlers who also use it)**
12. Tell me about the last maintenance booking. Was the timing right? How did you find out?

## What not to conclude

- Four interviews and 147 tickets can't say how common a complaint is. Tickets also over-represent handlers who file.
- Interview questions about layout and filters shaped what came up. Round 2 should ask about events, not features.
- A quiet responder is not proof the ranking is broken until the routing owner and the response-time data have been checked.
