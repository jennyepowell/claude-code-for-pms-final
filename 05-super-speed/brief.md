# Addressing issues with quiet responders

For: Helen Achebe · From: Dispatch PM · 16 Oct 2026 · Draft, not committed

## Executive summary

Since 4.2, responders whose pings were missed have dropped down the order and mostly stayed there. The score only changes when someone is pinged, so a responder at the bottom can't recover, and nobody can see that it happened. Making a missed ping stop counting against ranking is a one-line change, but on its own it would leave handlers and responders with no way to tell what was wrong or when it was fixed. This brief proposes three changes together. The cause is not yet confirmed.

## Who it's for

**Responders who have fallen in ranking because of missed pings, not turned-down ones.** A missed ping means nobody answered within the ping wait. A turned-down ping is a "no". The glossary records them separately, but `history.py` charges them the same today. Responders who turn work down by choice are not the target, and their ranking stays as it is.

**Example: Meteor Mite and their handler Kip.** Meteor Mite went from ~14 pings a week to ~4 after 12 Aug, and 67% of their pings were missed on 12-14 Aug. Kip also handles The Gale (+43%), so Kip's two cards tell opposite stories. Kip: "I just want it to look less like a coincidence." Today the only answer the product gives them is "hang in there".

## What changes

1. **Kip sees why.** Each coverage card shows a ranking status ("Low", "Fair" or "Good") and a Ranking Status Explanation: the last five pings with their dates and how each ended, plus a line on how the status changes: taking a ping raises it, turning one down lowers it, and missed pings don't change it. No score or routing weights are shown. The status reflects recent acceptance, not proximity.
2. **Meteor Mite gets a way back.** A responder who is available and has gone quiet, whose recent pings were mostly missed, is offered a callout they'd rank for, with a short note on their phone saying why. Taking it restores their place. After the recalculation in 3, this is for anyone who is still quiet.
3. **A missed ping counts for zero, past ones included.** Today a miss and a turn-down both cost -0.12. A miss would cost nothing, and at release every responder's score is recalculated once, ignoring past misses. Only turned-down pings lower the ranking status, and a turn-down keeps its cost. The status moves in steps (Low, Fair, Good) as pings are taken or turned down, so one turn-down doesn't drop a responder straight to Low.

## What it doesn't do

- No change for responders who turn pings down.
- No handler setting or override of ranking.
- No revert of 4.2, and no change to the 60s ping wait or the weights here.
- No writes to the Responder Availability Record (Supply reads it).
- Nothing that assumes a legal identity (Security Policy 4.1).

## How we'd know it worked

Proposed: the four back near their pre-12-Aug pings without overall acceptance falling, "phone never goes off" tickets down from ~30, and handlers in round 2 able to say why a card is quiet.
