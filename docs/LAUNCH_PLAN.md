# SpaceBack: Launch plan

A lead PM's plan for taking SpaceBack from prototype to a controlled launch at one airline.

**Status: nothing here has been run.** Every timeline, target and role is a proposal to agree with the airline. No figure below is a measured result.

## Launch decision

**No-go for live operations today. Go for discovery with an airline, then a shadow pilot if the problem is confirmed.**

The biggest unknown isn't the software. It's whether enough freed space can be resold in time to justify the change.

## What we are trying to prove

| Question | How we answer it | What would stop us |
|---|---|---|
| Is the problem real at this airline? | Interviews and historical booking data | Late losses are small, or are already handled well |
| Can freed space be resold in time? | Historical data on cancellations, waiting demand and cut-off | Too little demand or too little time |
| Is the agent accurate enough? | Evals, then shadow mode | Any hard-limit breach; low agreement with controllers |
| Will controllers use it? | Usage and weekly feedback | They work around it or don't trust it |
| Is the value greater than the cost? | Incremental revenue, then contribution, against AI, integration and review costs | Value doesn't clearly exceed cost |

## Launch stages and gates

Each stage has a gate. Nobody moves on until the head of capacity signs off on it.

| Stage | Proposed length | What happens | Nothing moves on until |
|---|---|---|---|
| **0. Discovery** | 2-4 weeks | Controller interviews; review of current tools and processes; historical baseline | Problem confirmed; baseline measured; sponsor and owners named |
| **1. Readiness** | 4-8 weeks | Complete the requirements below; test on real, anonymised messages | Everything marked "before shadow" is done |
| **2. Shadow pilot** | 2 weeks | One route, live read-only data. The agent proposes, nothing is sent, and controllers compare it with their decisions | Zero hard-limit breaches; agreed agreement rate met |
| **3. Assisted pilot** | 2-4 weeks | Same route. Messages and changes go out only after approval | Value target met; controllers want to keep it |
| **4. Controlled rollout** | Route by route | Add routes one at a time, with a gate for each | Results hold on each new route |
| **5. Limited automation** | Only if justified | Consider automating low-risk steps only | Separate business case and risk approval |

**Out of scope for the pilot:** dangerous goods, key accounts, automatic changes and moving booked cargo between flights.

## What is required

Status today: **Not started** unless stated.

### Before the shadow pilot

| Area | Requirement | Owner |
|---|---|---|
| Sponsor | Named executive sponsor and pilot budget | Head of cargo or capacity |
| Problem | Controller interviews and current process mapped | PM |
| Baseline | 8-12 weeks of history for the pilot route (cancellations, space resold, time per case) | Revenue analyst |
| Data | Read-only booking, flight and waitlist feeds; shared mailbox access | IT and integration lead |
| Rules | Airline's real space, fee, re-offer and escalation rules replace the fictional ones | Capacity and legal |
| AI setup | Approved model, region and server-side gateway | AI engineer and IT security |
| Evals | Large eval set from real, anonymised messages, with repeated runs and release gates. *Started: small synthetic set only* | PM and controllers |
| Security | Security assessment and independent prompt-injection testing | IT security |
| Privacy | Data protection assessment, data-transfer review and retention rules | Privacy and legal |
| Vendor | AI vendor and third-party review | Procurement and security |
| Access | Single sign-on and roles | IT |
| Audit | Permanent record of evidence, proposal, edits, approver and time | Engineering and compliance |
| Monitoring | Dashboard, alerts and a named on-call person | Engineering and PM |

### Before the assisted pilot

| Area | Requirement | Owner |
|---|---|---|
| Actions | Approved write-back to the booking system and mailbox, with an action service | Engineering |
| Pallets and loading | Load control confirms how offers are checked. Pallet and position data, or a manual step | Load control |
| Security and customs | Secure supply chain and customs checks in the offer flow | Cargo security and compliance |
| Forwarders | Message wording approved; forwarder communication agreed | Sales and account managers |
| Training | Controller training, a one-page guide and practice cases | PM and capacity lead |
| Support | Runbook, incident process and a manual fallback | Operations and engineering |
| Regulator | Confirm whether any review or notification is needed | Compliance |

### Before a wider rollout

| Area | Requirement | Owner |
|---|---|---|
| Evidence | Pilot results reviewed against the baseline | PM and revenue analyst |
| Business case | Cost, benefit and ongoing support model | PM and finance |
| Build or buy | Compare with booking-system vendors' options | PM, IT and procurement |
| Scale | Performance, cost and support tested for more routes | Engineering |

## Who owns what

| Role | Accountable for |
|---|---|
| **Head of capacity** | Go or no-go decision at each gate, and can pause at any time |
| **Lead PM** | Problem, scope, metrics, roadmap, learning loop and communication |
| **Capacity controllers** | Using it, judging proposals and giving feedback |
| **Account managers** | Key accounts, difficult replies and forwarder relationships |
| **Cargo acceptance, dangerous goods, load control and security** | Their rules and decisions, which SpaceBack doesn't replace |
| **Senior capacity manager** | Releases above 2,000 kg |
| **AI and software engineers** | Reliability, evals, integrations, security and monitoring |
| **Revenue analyst** | Baselines and value measurement |
| **Privacy, legal and compliance** | Reviews and sign-off |

## Metrics after launch

Measure a baseline first. Compare the pilot route with its own history, and with a similar route not using SpaceBack, so seasonal changes aren't mistaken for results.

### North star

**Space reuse rate: the share of freed space that was rebooked and actually flew, compared with the baseline.**

- **Calculation:** freed kg rebooked and flown ÷ total freed kg.
- **Why this one:** SpaceBack's objective is to reuse space that would otherwise go to waste.
- **Shown beside it:** incremental kg reused and flown per flight, so a high rate on a tiny amount can't look like a big win.
- **What counts as freed:** all confirmed cancellations and reductions, so only easy cases can't be counted.
- **Counts only:** cargo that actually flew. Offers don't count.

### Space funnel

The funnel shows where space is being lost.

| Stage | Metric | What it tells you |
|---|---|---|
| **1. Identified** | Kg and bookings flagged as possibly unused | How much space the check surfaces |
| **2. Confirmed** | Kg confirmed free by a written cancellation or reduction | How many flags were right |
| **3. Released** | Kg released after a person approved | How much space became sellable |
| **4. Offered** | Offers made and kg offered | Whether freed space reaches waiting requests |
| **5. Accepted** | Reallocations accepted and kg | Whether offers suit forwarders |
| **6. Flown** | Reallocated kg that actually flew | The real outcome, which feeds the north star |

Identified space and reallocation counts aren't north stars, because they can rise without creating value.

### Business result

**Is the value greater than the cost?**

Compare incremental revenue, then contribution once finance data is available, with the total cost of running SpaceBack. See the [business case model](BUSINESS_CASE.md).

### Value metrics

| Metric | How it's calculated | Source | Check | Proposed target |
|---|---|---|---|---|
| Empty space on the route | Unused kg ÷ capacity | Flight records | Weekly | Lower than baseline and comparison route |
| Time from cancellation to resale | Cancellation time to accepted offer | SpaceBack log | Weekly | Shorter than baseline |
| Controller time per case | Time from opening to decision | SpaceBack log | Weekly | Under one minute |
| Offer acceptance rate | Accepted offers ÷ offers sent | SpaceBack log | Weekly | Set after shadow |

### AI quality metrics

| Metric | How it's calculated | Check | Proposed target |
|---|---|---|---|
| Approved without edits | Unchanged approvals ÷ all proposals | Weekly | Above 80% |
| Agreement with controller | Same action as the controller's decision | Weekly in shadow | Set before shadow |
| Escalation accuracy | Correct escalations, in a sampled review | Weekly | Set before shadow |
| Citation accuracy | Sources that support the claim, in a sampled review | Weekly | No made-up sources |
| Variation | Same answer across repeated test runs | Each release | Hard-limit cases must be safe every run |
| Eval pass rate | Evals passing | Each change and monthly | No regressions |

### Adoption metrics

| Metric | Check | Proposed target |
|---|---|---|
| Share of eligible cases handled in SpaceBack | Weekly | Most cases by the end of the pilot |
| Controllers choosing to keep using it | Weekly and at each gate | All pilot users |
| Time spent working around it | Weekly feedback | Falling |

### Reliability and cost metrics

| Metric | Check | Proposed target |
|---|---|---|
| AI response time and error rate | Daily | Set before shadow |
| Data feed freshness | Hourly | Set with IT |
| AI cost per case and per recovered kg | Weekly | Clearly below value recovered |

### Guardrails

**Hard limits:** any breach pauses the pilot.

| Must always be zero | Why |
|---|---|
| Release without the forwarder's written notice | Could lose a customer's confirmed space |
| Any message, release or offer without a person's approval | Breaks the core control |
| Fee amount stated in a forwarder message | Fees must be confirmed by a person |
| A dangerous-goods or security decision made by the AI | Must stay with the responsible team |
| Personal or commercial data sent outside approved systems | Privacy and contract risk |

**Warning guardrails:** a breach triggers a review.

| Guardrail | Why it matters | Proposed threshold |
|---|---|---|
| Cargo offloaded or rolled because of a release or offer | Recovered space must not leave a customer's cargo behind | Set before the assisted pilot; any case is reviewed |
| Forwarder complaints and message volume | Too many chasers could damage relationships | No increase from baseline |
| Wrong releases reversed by a person | Shows the agent or process is making mistakes | Set before the assisted pilot |
| Very fast approvals | People may be approving without reading | Sample these cases weekly |
| Offers approved where the cargo didn't fly | Keeps results from being overstated | Reported weekly |

## Monitoring routine

| When | What | Who |
|---|---|---|
| Every day | Hard limits, errors, cost and data feeds | Engineering and PM |
| Every week | Value, quality and adoption; sample of cases; controller feedback | PM, controllers, revenue analyst |
| Every change | Re-run evals before release | AI engineer and PM |
| Every month | Full eval run, drift review and cost review | PM and engineering |
| Each gate | Go, adjust or stop | Head of capacity |

| If this happens | Then |
|---|---|
| Any hard-limit breach | Pause, investigate and report |
| Edit rate rises for two weeks | Sample cases; review prompt and rules |
| Space reuse rate doesn't beat the baseline by the gate | Fix, narrow or stop |
| AI errors or stale data | Fall back to manual work and alert the owner |
| A model, prompt or policy change | Run evals before release |

## Training and communication

| Audience | What they need | When |
|---|---|---|
| Controllers | Training, practice cases and how to disagree with the AI | Before each stage |
| Account managers | Which cases come to them and what they decide | Before assisted pilot |
| Forwarders | Wording of messages, with no surprise automation | Before assisted pilot |
| Leadership | Weekly summary and gate reviews | Throughout |

## Rollback

1. **Pause:** the head of capacity can stop at any time, and must after any hard-limit breach.
2. **Fall back:** controllers keep using the existing process, which stays available.
3. **Diagnose:** report what happened and what was affected within one working day.
4. **Decide:** restart narrower, hold until fixed, or end the pilot.
5. **Correct:** contact any affected forwarder through the account manager, and correct bookings in the booking system.

Turning SpaceBack off must leave normal work unchanged, and it is never the only record of a decision.

## Main launch risks

| Risk | Early sign | Response |
|---|---|---|
| The problem is smaller than expected | Weak baseline | Stop early, which is a valid result |
| Existing tools already do this | Discovery findings | Integrate, narrow or stop |
| Data access takes too long | Missed readiness dates | Start with exports in shadow mode |
| Controllers don't trust it | Low use and many edits | Improve evidence, or narrow scope |
| Too little demand to resell | Low space reuse rate | Focus on routes with waiting demand |
| Forwarders dislike extra messages | More complaints | Limit volume and agree wording with sales |

## Decisions needed from the airline

1. Who is the sponsor, and which route should be first?
2. What baseline and comparison route should we use?
3. What agreement and space reuse targets justify moving on?
4. Which data and AI providers are allowed?
5. Should this be built, bought or added to an existing system?
