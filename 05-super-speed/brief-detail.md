# Backup detail for the Helen brief (full version before trimming)

For: Helen Achebe · From: Dispatch PM · 16 Oct 2026 · Draft, not committed

## Executive summary

Since 4.2, responders whose pings were missed have dropped down the order and mostly stayed there. The score only changes when someone is pinged, so a responder at the bottom can't recover, and nobody can see that it happened. Lowering the penalty for a missed ping is a one-line change, but on its own it would leave handlers and responders with no way to tell what was wrong or when it was fixed. This brief proposes three changes together: handlers see why a responder is ranked where they are, a responder who was missed gets a way back, and a miss costs less than a turn-down. The cause is not yet confirmed, and the open questions below need answers before anyone builds.

## Who it's for

**Responders who have fallen in ranking because of missed pings, not turned-down ones.** A missed ping means nobody answered within the ping wait. A turned-down ping is a responder saying no. The glossary records them separately, but `history.py` scores them the same. Before 12 Aug nearly every responder turned down 13-29% of pings, and the four quiet ones were in that range. What set them apart was misses after 12 Aug (53-64% of their pings vs ~10-18% for others). Responders who turn work down by choice are not the target, and their ranking stays as it is.

**Example: Meteor Mite and their handler Kip.** Before 12 Aug Meteor Mite got ~14 pings a week; after, ~4. 67% of their pings were missed on 12-14 Aug vs 22% for everyone else, and they had been near-perfect before. Kip also handles The Gale (+43% pings), so Kip's two cards on one screen tell opposite stories. In the 4 Sep interview Kip said: "I just want it to look less like a coincidence." Kip told Meteor Mite to "hang in there", which is the only answer the product gives them today.

Same pattern, other handlers: Vesper (Aunt Dot), Farlight and The Undertow. The last two handlers filed 20 of the 30 "phone never goes off" tickets.

## What changes for them

1. **Kip sees why.** Each coverage card shows a ranking band (for example "Normal" or "Lowered by missed pings") and a list of what contributes to it. The list leads with recent pings and how each ended (taken, turned down, missed), then days since the last ping and the last one taken, availability as Dispatch has it, and capability tags matched. The exact recent-acceptance score is one click down. Two cards that look different now say why, and Kip has something true to tell Meteor Mite. The band is per responder, not per callout, so it reflects recent acceptance, not proximity, which varies by incident. It doesn't show the routing weights, and it ships with the way back (2), so a lowered ranking always comes with a next step.
2. **Meteor Mite gets a way back.** A responder who is marked available, has gone quiet, and whose recent pings were mostly missed is offered a callout they'd rank for, instead of waiting for a ping that never comes. Taking it restores their place. They feel the phone start going off again, with a short note on the phone saying why.
3. **A miss and a turn-down stop being the same thing.** The code treats them identically (-0.12). A missed ping is not a "no", so a miss would cost less. A turn-down keeps its current cost. This is the one number in the proposal, and it is the smallest part.

## What it deliberately doesn't do

- **No change for responders who turn pings down.** Their score, and the way back, apply only where the drop came from misses.
- **No handler setting or override of ranking.** Routing config ships with the release. Handlers see the reason; they don't tune it.
- **No revert of 4.2**, and no change to the 60s ping wait or the 0.60/0.25/0.15 weights here. The data can't separate those two changes yet, so that stays a separate decision.
- **No writes to the Responder Availability Record.** Supply reads it to schedule maintenance, so a "way back" that touched it would change Supply silently. It reads availability only.
- **Nothing that assumes a legal identity** (Security Policy 4.1). It works from cover identity and ping history only.
- **No mutual aid.** Still the Q4 list.

## What I don't know yet

- **Cause is unconfirmed.** I believe misses lowered the four's scores and the no-decay rule kept them down. But the 4.2 weight change should have softened that, and travel-time proximity (a responder who is farther out) is untested. The database holds no scores or locations.
- **My data stops at 6 Sep.** It is six weeks old. Ravi needs to refresh it before we say whether the four recovered on their own.
- **Whether the four answered in 60-90s before 12 Aug.** That decides if the 60s wait alone explains the misses. Needs response times on taken pings from Ravi.
- **Design intent.** Marcus's 14 Aug question (did the ranking change apply to decliners?) is answered in code (yes) but nobody has said whether that was meant. Wen and Marcus own that.
- **Where scores live.** `history.py` holds them in memory and the database has none. Wen or Marcus must confirm the console can read them, and what a new feed would cost.
- **How much a handler should see.** A visible score handlers can't change could invite pressure on responders or comparison between them. Sofia designs the band and the one-click detail. Responders don't see their own score for now.
- **Evidence for the handler card is thin:** four interviews, none with the heaviest ticket filers. Round 2 (Farlight and The Undertow handlers) tests the wording before we build it.

## How we'd know it worked

Proposed, to agree with Ravi and you: the four back to roughly their pre-12-Aug pings per week without overall acceptance falling; "phone never goes off" tickets down from about 30; Kip and the Farlight and Undertow handlers asked in round 2 whether they can tell why a card is quiet.

## One more thing for you

Availability Confidence (committed for 4.2, not shipped) is the natural home for telling "stopped taking work" from "starved by ranking". The slip still needs our conversation. This work makes that conversation easier, so I'd like 15 minutes this week.

## Next

A clickable prototype: Kip's two coverage cards and Meteor Mite's phone, before and after. Sofia owns both surfaces, so I'd build it with her.
