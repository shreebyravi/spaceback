# SpaceBack: Case study

**In short:** I started with an AI booking assistant, found that the core of it already existed, and rebuilt it around a less crowded problem: recovering cargo space that's booked but won't fly. The result is a working prototype on made-up data. It hasn't been tested by an airline, so it shows how I approach an AI product, not proven business results.

## My role

I led the product work: the problem, scope, decisions, test cases, verdicts, pilot plan and what to do next. An AI coding assistant wrote the code, drafted documents and helped with research, working from my direction and reviews.

## The problem

Forwarders book cargo space, then cancel late, send less than they booked, or never show up. An [AGIFORS abstract](https://www.agifors.org/Technical-presentations), on work developed with the Etihad Cargo team, reports 15-30% no-shows and cancellations between three days before departure and departure, as a network average.

Prediction tools flag risk, and fees recover some money, but neither fills the aircraft.

## The turning point

The first version turned a forwarder's request into a booking proposal. While building it, I asked whether this really solved an open problem. Research showed that commercial products already covered much of that work.

So I stopped and compared other airline problems. I chose space recovery because it had a published pain figure and a plausible gap: asking the forwarder, reading the reply, releasing the space and reselling it before cut-off. That gap is still a hypothesis.

## Key decisions

| Decision | Why | What it cost |
|---|---|---|
| A person approves every message, release and offer | A wrong release can lose cargo or a customer | Less time saved |
| Code handles space, fees and rules; AI reads and drafts | Exact results where they matter, and AI only where text needs judgement | More to build |
| Never release on prediction alone | Risk is a reason to ask, not proof | Some space may be recovered later or not at all |
| Open on a dashboard, not one flight | A controller's first question is where to act now | More design work |
| Treat 72 hours as the first alert, not a limit | Cancellations don't wait for a set time | A wider workflow to design |
| Offer space to waiting requests first | Smaller and safer scope | Booked cargo can't be moved yet |
| Show a rough revenue estimate, not a promise | There's no real recovery data | A less dramatic headline |

## How testing changed the product

| What testing or review found | What I did |
|---|---|
| The agent escalated a lithium battery case correctly, but left the acceptance team to redo the checks. I asked why batteries didn't get a policy check | Added an instruction to list each rule as met, not met or missing |
| One message said "pieces" where the forwarder said "pallets", and another chased a third time | Added two instructions and re-ran the cases |
| In one of three runs, the agent proposed a 3,200 kg release instead of escalating | Kept it on record. The app's own rule blocks approval, which shows why hard limits belong in code |

All six evals match in the latest recorded run. These are recorded answers, because no API credit was available, and a full live run hasn't been done.

## What went wrong

- **The first idea wasn't different enough.** I should have checked the market earlier.
- **Model settings caused failures.** Answers were cut off and formats broke, which led to a fixed output structure and larger limits.
- **Early dashboards were hard to read.** Long lines of text became clear cards and clickable numbers.
- **Names clashed with real brands.** Late checks led to renaming the product and fictional airline.
- **A source link didn't show the figure it was cited for.** A review caught it and fixed it before outreach.

## Outcome

- A working prototype, with a dashboard, AI proposals, approvals, rule-checked reallocation, a Space Ledger and a revenue estimate
- Published evals, stress tests, risks, a market scan and a launch plan
- **No business results:** no airline has used it, and nothing shows it recovers revenue

## What I learned

1. A working demo doesn't prove a real problem.
2. In an AI product, the split between AI, code and people is a core product decision.
3. An instruction to an AI isn't a guarantee, because answers can vary between runs.
4. Publishing limits and failures makes the work easier to trust.
5. Reviewing whether a correct answer has good reasoning finds problems that a pass or fail check misses.

## What I'd do next

Speak with capacity teams, measure a baseline, and test the idea in a shadow pilot on one route. See the [launch plan](LAUNCH_PLAN.md).
