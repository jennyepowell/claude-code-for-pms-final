# Addressing issues with quiet responders

For: Helen Achebe · From: Dispatch PM · 16 Oct 2026 · Draft, not committed

## Executive summary

Since 4.2, responders whose pings were missed have dropped down the order and mostly stayed there. The score only changes when someone is pinged, so a responder at the bottom can't recover, and nobody can see that it happened. Lowering the penalty for a missed ping is a one-line change, but on its own it would leave handlers and responders with no way to tell what was wrong or when it was fixed. This brief proposes three changes together. The cause is not yet confirmed, and the open questions below need answers before anyone builds.

## Who it's for

**Responders who have fallen in ranking because of missed pings, not turned-down ones.** A missed ping means nobody answered within the ping wait. A turned-down ping is a "no". The glossary records them separately, but `history.py` scores them the same. Responders who turn work down by choice are not the target, and their ranking stays as it is.

**Example: Meteor Mite and their handler Kip.** Meteor Mite went from ~14 pings a week to ~4 after 12 Aug, and 67% of their pings were missed on 12-14 Aug. Kip also handles The Gale (+43%), so Kip's two cards tell opposite stories. Kip: "I just want it to look less like a coincidence." Today the only answer the product gives them is "hang in there".

## What changes

1. **Kip sees why.** Each coverage card shows a ranking band (e.g. "Lowered by missed pings") and what contributes to it, led by recent pings and how each ended. The exact score is one click down. It reflects recent acceptance, not proximity, and doesn't show routing weights.
2. **Meteor Mite gets a way back.** A responder who is available, quiet, and mostly missed is offered a callout they'd rank for, with a short note on their phone saying why. Taking it restores their place.
3. **A miss costs less than a turn-down.** Today both cost -0.12. A turn-down keeps its cost.

## What it doesn't do

- No change for responders who turn pings down.
- No handler setting or override of ranking.
- No revert of 4.2, and no change to the 60s ping wait or the weights here.
- No writes to the Responder Availability Record (Supply reads it).
- Nothing that assumes a legal identity (Security Policy 4.1).

## What I don't know yet

- **Cause.** I believe misses lowered scores and no-decay kept them down, but the 4.2 weight change should have softened that, and proximity is untested.
- **My data stops at 6 Sep.** Ravi needs to refresh it.
- **Response times.** Did the four answer in 60-90s before 12 Aug? If so, the 60s wait explains the misses.
- **Design intent and where scores live.** Wen and Marcus own both. `history.py` holds scores in memory, so the console may need a new feed.
- **How much a handler should see.** Four interviews, none with the heaviest ticket filers. Sofia designs it; round 2 tests it.

## How we'd know it worked

Proposed: the four back near their pre-12-Aug pings without overall acceptance falling, "phone never goes off" tickets down from ~30, and handlers in round 2 able to say why a card is quiet.

## Next

Availability Confidence (committed for 4.2, not shipped) is the natural home for telling "stopped taking work" from "starved by ranking". I'd like 15 minutes with you this week, and I'd build a clickable prototype of Kip's cards and Meteor Mite's phone with Sofia. Detail and numbers: [brief-detail.md](brief-detail.md).
