# SpaceBack: Decision log

Key product decisions and why they were made. A later decision replaces an earlier one; nothing is rewritten.

| # | Date | Decision | Why | Alternative rejected |
|---|---|---|---|---|
| 1 | 31 Oct 2026 | Rebuild as space recovery, not a booking assistant | Research showed booking intake and quoting already exist in commercial products | Keep the booking assistant |
| 2 | 31 Oct 2026 | Start with cargo space; leave passenger disruption for later | Space recovery has a published pain figure and a plausible product gap. Passenger disruption is crowded and integration-heavy | Build both at once |
| 3 | 31 Oct 2026 | Plain code for space, risk, fees and rule checks | These must be exact and auditable | Let the AI calculate them |
| 4 | 31 Oct 2026 | A person approves every message, release and offer | A wrong release can lose cargo or a customer | Automatic low-risk approvals |
| 5 | 31 Oct 2026 | First request comes from an approved template | First contact needs consistent wording, and AI adds nothing there | AI writes every message |
| 6 | 31 Oct 2026 | Never release on prediction alone | Risk is a reason to ask, not proof that cargo won't come | Release high-risk bookings automatically |
| 7 | 31 Oct 2026 | No memory across sessions | An old conversation must never override today's data | Long-term agent memory |
| 8 | 31 Oct 2026 | Use recorded answers when there's no API key | Anyone should be able to try it at no cost, and answers are clearly labelled | Require every visitor to bring a key |
| 9 | 31 Oct 2026 | E-05: pre-check acceptance rules before escalating | The acceptance team shouldn't have to redo checks. The agent still doesn't decide | Escalate with no checks |
| 10 | 2 Nov 2026 | Space check is available at any time; 72 hours is only the first alert | Cancellations don't wait for a 72-hour mark | A check that opens only at 72 hours |
| 11 | 2 Nov 2026 | Open on a dashboard ranked by what can still be saved | A controller's first question is where to act now | Open on one flight |
| 12 | 2 Nov 2026 | Split space into free now, at risk and can be filled | At-risk space can't be sold yet, so one "% empty" figure misleads | A single empty percentage |
| 13 | 2 Nov 2026 | Check runs automatically; a person still approves | A check someone must remember to start can be missed | A manual Start button |
| 14 | 2 Nov 2026 | Live AI runs wait for a click in the prototype | A visitor's API key should never be spent without asking | Run every case automatically |
| 15 | 2 Nov 2026 | Cargo cut-off is the deadline for reselling | New cargo can't be accepted after it, even if the flight hasn't left | Use departure time |
| 16 | 2 Nov 2026 | This scope offers space only to waiting requests | The rules mostly exist. Moving booked cargo needs new rules and the forwarder's agreement | Move booked cargo between flights now |
| 17 | 2 Nov 2026 | Count a sellable flight near cut-off as needing action | Otherwise a sale can expire unnoticed | Count only replies and due checks |
| 18 | 2 Nov 2026 | Show a revenue estimate, not a promised figure | There's no real data on how much space can be resold | Claim a recovery rate |
| 19 | 2 Nov 2026 | Publish limits and "Needs work" results | An airline will find weaknesses anyway, and honesty builds trust | Show only passing results |
| 20 | 2 Nov 2026 | Use a fictional airline and an original aviation look | The page must not imply affiliation with any airline | Copy an airline's branding |
| 21 | 2 Nov 2026 | Forwarder's own words in messages; no third chaser | Fixes for E-02 and E-03 from the quality checks | Accept the wording and the extra chaser |
| 22 | 2 Nov 2026 | Rename the product SpaceBack and the fictional airline Solvane Air Cargo, flight code SVZ | Earlier names were close to real aviation and logistics brands in the same region | Keep the earlier names |
| 23 | 2 Nov 2026 | Replace the pilot document with a fuller launch plan | A team needs stage gates, requirements, owners and post-launch metrics in one place | Keep a shorter pilot note |
| 24 | 2 Nov 2026 | Publish a break-even model, not an ROI claim | There are no real inputs, so any ROI would be invented | Show a headline ROI |
| 25 | 2 Nov 2026 | Make space reuse rate the north star; revenue becomes the business result | The objective is to reuse wasted space. Revenue shows whether that is worth the cost | Keep revenue as the north star |
