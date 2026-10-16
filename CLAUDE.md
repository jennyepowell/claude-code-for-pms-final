# Rook Industries — course working file

## Session scope — Product School lab

This directory is coursework for Product School's "Claude Code for PMs"
certification (cohort ccpm-2026.1). Everything in it is a fictional
teaching scenario.

- Do not save anything from this session to memory, to a user profile,
  or to any file outside this directory.
- Do not carry context from this directory into unrelated sessions.
- Rook Industries is not a real company. Nothing here is a fact about
  the world.
- Read and write only within this directory.
  Exceptions, for the course-setup and wrap-up skills only:
  - When the student asks you to check their setup, save their work or wrap up a session, that request is their yes. You may run the GitHub command-line program installed at ~/.ccpm/gh for those checks and saves, and look in that folder to find it.
  - For a repair, first tell the student in one plain sentence what you are about to do, and act only after they say yes. Repairs may: run that GitHub program (including setting this folder's own git sign-in setting and changing this repo's visibility back to Public); copy the student's own course files into this directory from another folder on their computer (copy only; never move, edit or delete the originals); and rename something outside this directory that blocks setup, by adding "-old" to its name (never delete it).
  Outside this directory you still never write, edit or delete anything else.

<!-- Keep the block above at the top of this file. Everything you add
     during the course goes below this line. -->

---

## Working context

I am the new PM for **Rook Dispatch** (replacing Priya, who left 21 Aug 2026).
Sources: rook-wiki (Company pages, Team directory, Releases, Q3 roadmap,
Product briefs, 4.2 comments) and `00-rook/company/notes/handoff-from-priya.docx`.
Also in this folder: `00-rook/code/dispatch-routing/` (routing code) and
`00-rook/feedback/` (empty). A `rook-database` connector exists; not yet read.

### Company and products
- Rook sells coordination/provisioning software to masked responders
  (independent, not employees) and their handlers and quartermasters.
  Subscription, priced per active responder. Monthly release train, 4.x numbers.
- **Dispatch** (mine): handler web console + responder phone app. Incident ->
  rank available responders -> ping top one -> taken, or turned down/missed
  and it moves on. Routing config ships with the release; handlers can't change it.
- **Supply**: requisitions, quartermaster approval, maintenance, field failure
  reports. Reads (never writes) the Responder Availability Record that Dispatch
  writes, and schedules maintenance into low-callout periods, so Dispatch
  changes to availability flow into Supply silently.
- **Confidentiality:** cover identities are never stored; no mapping to legal
  identity exists. Never design anything that assumes one (Security Policy 4.1)
  and never try to work out who anyone is.

### People (4.2 comments use roles only)
| Role in comments | Person | Notes |
| --- | --- | --- |
| Engineering manager | Marcus Oyelaran (Site Aleph) | Runs Dispatch eng; blunt; first stop. Asked the key 4.2 question |
| Staff engineer | Wen Li (Berlin) | Built the ping-ranking logic; the only "documentation" of it |
| Product designer | Sofia Marino (Site Aleph) | Console + phone app; ran the September interviews |
| Support lead | Nadia Hoffmann (Berlin) | Owns tickets; has the breakdown; worth a standing 15 min |
| (not in comments) | Helen Achebe | Director of Product, my boss; owns roadmap and commitments |
| (not in comments) | Ravi Menon (Singapore) | Data analyst; weekly acceptance-rate reporting |
| Priya | Priya Raghunathan | Former PM; unreachable except via Marcus |

Handlers named in wiki: Halloran (Sgt. Bulwark; Supply), Aunt Dot (Vesper),
Mr. Ambrose (Captain Vantage), Kip (Meteor Mite, The Gale).

### Vocabulary
- **Callout** unit of work; **ping** a callout offered to one responder.
  **Taken / turned down / missed** (nobody answered within the **ping wait**;
  recorded separately from turned down, both move it on).
- **Acceptance rate** = taken / pings; headline metric, reported weekly in
  aggregate. **Time-to-accept** = median seconds ping to taken.
  **Coverage gap** = no available responder had the tags (not the same as low acceptance).
- **Routing priority**: score from proximity (travel-time estimate), availability,
  capability match, recent acceptance history. Turning down or missing a ping
  lowers recent acceptance and so future rank.
- **Capability tags**: flight, structural-entry, hazmat-tolerant, cold-weather,
  aquatic, crowd-management, de-escalation. **Mutual aid**: not supported; Q4 list.
- Supply: requisition, field failure report, service interval.

### Where things stand (as of the wiki; verify before relying)
- **Releases:** 4.0 (7 Apr: nav, profile redesign, override audit log); 4.1
  (16 Jun: travel-time proximity, bulk callout, push reliability); 4.2 (12 Aug:
  proximity weighted up vs. acceptance history, ping wait 90s -> 60s, filter
  persistence, 3 fixes).
- **4.2 problem:** callout tickets ~3x normal since ~12 Aug and flat since;
  about two-thirds "phone never goes off", one-third "gone before I could answer".
  The one-third has a known cause (60s wait). The two-thirds is **unexplained**.
- **Competing explanations, none yet tested:** Priya says seasonal (August is
  soft) and not to revert; Marcus repeated that. But two changes shipped together,
  so the seasonal claim can't be separated from them without data. Marcus's
  unanswered question (14 Aug): does the proximity change apply to responders who
  turn pings down? Config doesn't distinguish them. Wen Li was away then and
  hasn't answered. No real numbers have been pulled; Ravi's weekly report is the source.
- **Don't assume** 4.2 is the cause, or that it's seasonal. Check data first.
- **Roadmap is stale** (last reviewed 30 Jun, all owned by Priya). Committed for
  4.2: who-gets-pinged (shipped), ping timeout tuning (shipped as 60s), and
  **Availability Confidence (not in the 4.2 notes; apparently slipped)**.
  4.3: requisition approval chains (Supply). Q4 exploring: handler phone app,
  shared cover between responders. Priya flagged the slipped items need a
  conversation with Helen; it hasn't happened.
- **Briefs:** Routing Override Audit Log and Bulk Callout appear shipped (4.0,
  4.1) though the pages read as proposals. Handler Phone App (8 Sep) is for
  handlers; responders already have a phone app. Requisition Approval Chains
  asks for one thing (second approval over $2,000) then piles on four more;
  scope is undecided.
- **Gaps:** no written description of how pings are decided (Priya asked me to
  write it); no baseline for time-to-full-coverage; September interview
  database ("Customer interviews") not yet read.

### Working notes
- Priya's handover is opinion, not data; label it as such.
- Treat roadmap "Committed" as unverified until Helen confirms.


### Added at wrap-up, Module 1
- "Seasonal" is only supported if acceptance rate and ticket volume were also hit in prior Augusts; the 3x ticket jump started the day of the 12 Aug release, which fits seasonality poorly.
- The two-thirds / one-third ticket split is Nadia's rough count from 26 Aug, callout tickets only. "Phone never goes off" may be several causes (ranked too low, push delivery, seasonal); not yet separated.
- Next reads: Nadia's ticket breakdown (any pattern in who is affected), weekly acceptance rate incl. prior Augusts (Ravi / `rook-database`), the Customer interviews, and the routing code in `00-rook/code/dispatch-routing/`.
- Still open: Marcus's question whether the proximity change was meant to apply to responders who turn pings down; Wen Li hasn't answered. Availability Confidence slip not yet raised with Helen.
- Ping data (`rook-database`, to 6 Sep): after 12 Aug missed pings went ~4 to ~30 a week, acceptance rate 76.6% to 64.0% (back to ~73% by the week of 31 Aug), callouts a week down ~15%, callouts where nobody took the ping 5.5% to 11.1%. Tickets ran ~6.5 a week before and ~26 a week after, starting the week of 10 Aug. The 60s wait clearly bit; the data can't separate it from the weight change.
- Four responders (Vesper, Meteor Mite, The Undertow, Farlight) went from ~14 to ~4 pings a week after 12 Aug; 67% of their pings were missed on 12-14 Aug vs 22% for everyone else, and they were near-perfect before. Corporal Ashgrove and Halfmoon slipped about a quarter and held. Cause not confirmed.
- Routing code (`history.py`): a miss and a turn-down cost the same (-0.12, a take gives +0.08), and the score never moves unless the responder is pinged (2019 TODO, no decay), so a miss streak can leave someone stuck low. Weights now 0.60 proximity / 0.25 history / 0.15 capability; the lower history weight should make this less likely, not more. Hypothesis, not verified.
- Tickets (147, my own grouping): 30 quiet-phone, 16 gone-too-fast (the 65/35 split holds), 16 filters, 26 Supply. The four interviewed handlers filed one ticket between them; the 11 ticket filers were never interviewed. Round-2 plan is in `00-rook/feedback/interviews-vs-tickets-and-round-2.md`.
- Still open: response times on taken pings (Ravi) to test whether the four answered in 60-90s before; Wen Li / Marcus on rank collapse and whether the 60s and weight changes can be tested apart; no availability data in the database; the non-callout ticket rise (~6.5 to ~15 a week, Supply included) is unexplained. Don't change `config.py` without telling Marcus.
- Ping log looks sound: after a missed ping the next ping follows 91-93s later before 12 Aug and 61-63s after, and no turned-down ping has a gap over 40s, so misses aren't being logged as turn-downs (says nothing about whether a push arrived). `pings` has only callout, responder, time, outcome; handler per responder is in `responders`, and `callouts` has area/time only.
- Reporters vs affected: Farlight (Linda Pruitt, 19 tickets) and The Undertow (Desmond Okafor, 21) lost ~70% of pings with ~64% missed and filed 20 of the 30 quiet-phone tickets. Vesper (Aunt Dot) and Meteor Mite (Kip) lost the same and filed none. Kip also has The Gale (+43%), so Kip's combined -7% hides it. Halloran filed none, Ambrose one. Handlers' own ping counts in tickets match the database.
- Timing: "gone too fast" tickets began on release day (first 12 Aug 15:41, 7 in week one) and fade as misses fall; quiet-phone tickets began 17 Aug and peaked 26 Aug-1 Sep, after the data change. Vesper was first choice in 23 of 25 pings before and leftovers after (last taken 17 Aug); Farlight stayed first choice in 8 of 11 but missed 7 (last taken 14 Aug, then 4 days with no ping).
- Other changes in the window: 4.2 also shipped console filter persistence and three defect fixes that aren't described anywhere (ask Marcus); 4.1 (16 Jun) changed proximity to travel time and fixed push. Overnight callouts fell ~40% vs ~5-10% by day, but misses rose in every time band and equally on weekdays and weekends. The data starts 29 Jun, so there is no prior August to test "seasonal".

### Added at wrap-up, Module 4
- Marcus's 14 Aug question (did the 4.2 ranking change apply to responders who'd been turning pings down?): in the code, yes, it applies to everyone. `rank_for_callout` removes nobody and nothing separates decliners. Likely he is asking about design intent (which only Priya and Wen Li know) and whether the early complaints are a side effect or intended.
- The question's premise doesn't hold in the data: before 12 Aug nearly every responder turned down ~13-29% of pings, and the four who went quiet (Vesper, Farlight, The Undertow, Meteor Mite) sat in that range. What set them apart was misses after 12 Aug (53-64% of their pings vs ~10-18% for others), not turn-downs.
- Recovery for a quiet responder: the score only changes when they are pinged (no decay), a take is +0.08 and a miss or turn-down -0.12, so they need to be pinged and take it, roughly 3 takes per 2 misses to break even, and nothing on their side can trigger it.
- Caveat: the 4.2 weight change (history 0.40 to 0.25, proximity 0.45 to 0.60) should soften the history effect, so a miss streak alone doesn't obviously explain the collapse to ~1 ping a week. Proximity (a farther-away responder losing out) is untested; the database has no scores or locations.
- Suggested reply to Marcus: applies to everyone; the four weren't habitual decliners; ask whether a miss should count the same as a turn-down, and ask Wen Li or him to check the actual scores and the proximity effect. Not yet sent.
- Helen's 16 Oct request (one-pager on what we'd build for quiet responders, clickable if possible) is answered by `05-super-speed/brief.md` (about 540 words) and `prototype.html` (handler console with Kip's two cards plus Meteor Mite's phone, a Release applied and a Simulate callout button). `brief-detail.md` keeps the longer first draft, including the open questions the brief dropped.
- Decisions the brief now makes: it targets responders ranked down by missed pings, not turned-down ones; a missed ping counts for zero, with a one-time recalculation at release ignoring past misses; ranking status shows as Low, Fair or Good from recent acceptance only, with no score shown and a list of the last five pings. The way back stays for anyone still quiet after the recalculation. Fair and Good cut-offs and credit sizes in the prototype are placeholders.
- In the code, availability is a filter (`available_for`), not a score input, though the glossary lists it as one; proximity is per callout, so the status can't reflect it. A farther-away responder could read Good yet stay quiet, and proximity is still untested.
- Left out of the brief and still open: cause unconfirmed, data stops 6 Sep, response times (did the four answer in 60-90s before 12 Aug), whether the recalculation is feasible (scores sit in memory in `history.py`) and what it does to others and to Supply, and Wen and Marcus not yet asked. A per-responder 60 or 90s wait was floated but is not in the brief. Availability Confidence still needs the talk with Helen.
- I checked the prototype's script for syntax only; it has not been clicked through in a browser.

### Added at wrap-up, Module 6
- The `review-checklist` skill (`.claude/skills/review-checklist`) checks a brief on six points: current experience, problem, owner, success measure, scope start vs end, problem before fix. It reviews only and does not rewrite.
- Run on `05-super-speed/brief.md`: five points passed; scope start vs end was Partly. The brief frames the target as four quiet responders, but change 3 recalculates every responder's score at release, and no success measure covers those others beyond overall acceptance staying at or above ~73%.
- Fix before it goes to Helen: add a measure for the non-target responders (how many change rank, no drop in their pings or acceptance), or reword the title and "Who it's for" to say it reaches everyone; also say whether the recalculation is feasible. Not yet done.
- Smaller points: the owner is a role ("Dispatch PM"), not a name; "taking it restores their place" in change 2 is untested (a take is +0.08 against -0.12 per miss).
- The review was run on the local file. The GitHub link in the prompt pointed at another account's repo (MichaelaBourgeois), not the student's own.
