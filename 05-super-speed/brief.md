# Addressing issues with quiet responders

For: Helen Achebe · From: Dispatch PM · 16 Oct 2026 · Draft, not committed

**Owner:** Dispatch PM, accountable for the brief and for the result. Marcus Oyelaran (engineering manager) would own the build, once he agrees it is feasible. Helen decides whether it goes ahead.

## Executive summary

Since 4.2, four responders have gone quiet: their pings fell about 70% and have not come back. Most of the pings they did get were missed, and a missed ping lowers ranking. The score only changes when someone is pinged, so a responder at the bottom can't recover, and nobody can see that it happened. The cause is not yet confirmed. This brief proposes three changes together. They cover what the handler sees, a way back for the responder, and how a missed ping is counted, which includes a one-time recalculation of every responder's score at release, not just the four. It is not a one-line fix, because stopping misses from counting alone would leave handlers and responders with no way to tell what was wrong or when it was fixed.

## The problem today

**What handlers and responders see now.** Neither the handler console nor the phone app shows a responder's ranking or why their pings have dried up. A responder just stops getting pings. The handler sees a quiet card and has to guess. Responders and handlers have no way to see a change in ranking, or the reason for it.

**What happened.** After 12 Aug (4.2: 60s ping wait, more weight on proximity), a responder whose pings were missed fell down the order. A missed ping and a turned-down ping both cost -0.12 in `history.py`, a take gives +0.08, and nothing moves the score unless the responder is pinged. So a responder who drops low gets few pings, and a low score is stuck.

**Who it affects.** Four responders: Vesper (Aunt Dot), Meteor Mite (Kip), The Undertow (Desmond Okafor) and Farlight (Linda Pruitt). They went from ~14 to ~4 pings a week, and 53-64% of their pings were missed against ~10-18% for others. Two more (Corporal Ashgrove, Halfmoon) slipped about a quarter and held. Two of the four handlers filed 20 of the 30 "phone never goes off" tickets.

**Example: Meteor Mite and their handler Kip.** 67% of Meteor Mite's pings were missed on 12-14 Aug. Kip also handles The Gale (+43%), so Kip's two cards tell opposite stories. Kip: "I just want it to look less like a coincidence." Today the only answer the product gives them is "hang in there".

**What we don't know.** The cause is unconfirmed. Proximity may also be pushing these responders down, and the database has no scores or locations to test it. Data stops 6 Sep.

## Who it's for

**Responders who have fallen in ranking because of missed pings, not turned-down ones.** A missed ping means nobody answered within the ping wait. A turned-down ping is a "no". The glossary records them separately, but `history.py` charges them the same today. Responders who turn work down by choice are not the target, and their ranking stays as it is, apart from the one-time recalculation in change 3, which touches every responder.

## What changes

1. **Kip sees why.** Each coverage card shows a ranking status ("Low", "Fair" or "Good") and a Ranking Status Explanation: the last five pings with their dates and how each ended, plus a line on how the status changes: taking a ping raises it, turning one down lowers it, and missed pings don't change it. No score or routing weights are shown. The status reflects recent acceptance, not proximity.
2. **Meteor Mite gets a way back.** A responder who is available and has gone quiet, whose recent pings were mostly missed, is offered a callout they'd rank for, with a short note on their phone saying why. Taking it restores their place. After the recalculation in 3, this is for anyone who is still quiet.
3. **A missed ping counts for zero, past ones included.** Today a miss and a turn-down both cost -0.12. A miss would cost nothing, and at release every responder's score is recalculated once, ignoring past misses. This is the one change that reaches responders outside the target group: their scores are recalculated too, and their rank may shift. Only turned-down pings lower the ranking status, and a turn-down keeps its cost. The status moves in steps (Low, Fair, Good) as pings are taken or turned down, so one turn-down doesn't drop a responder straight to Low.

## What it doesn't do

- No change to how turned-down pings are counted. Responders who turn pings down keep their current rules, except for the recalculation noted in change 3.
- No handler setting or override of ranking.
- No revert of 4.2, and no change to the 60s ping wait or the weights here.
- No writes to the Responder Availability Record (Supply reads it).
- Nothing that assumes a legal identity (Security Policy 4.1).

## How we'd know it worked

Proposed targets, for Helen to confirm, checked four weeks after release:

- **Pings:** each of the four back to at least ~12 pings a week (they had ~14 before 12 Aug), with overall acceptance rate not below its current ~73%.
- **Tickets:** "phone never goes off" tickets at or below ~5 in the four weeks, from ~30 so far.
- **Handlers:** in round 2 interviews, handlers can say why a card is quiet. Target: all of those interviewed.
