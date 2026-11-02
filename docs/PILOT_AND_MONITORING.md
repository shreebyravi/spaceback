# SpaceBack: Pilot and monitoring

A proposed plan for testing SpaceBack on one route. All numbers are starting points to agree with the airline. None has been measured.

## Go or no-go today

**No-go for live operations. Go for a conversation and a shadow pilot.**

| Needed before starting | Status |
|---|---|
| A capacity controller confirms the problem and workflow | Not done |
| Competing and in-house tools have been checked | Partly done |
| Full evals pass on live model calls | Not done: recorded answers only |
| Read-only data access is agreed | Not done |
| Security, privacy and vendor reviews | Not done |
| Named owners and a rollback plan | Proposed below |

## The pilot

| Item | Proposal |
|---|---|
| Scope | One route from one hub |
| People | 2-3 capacity controllers |
| Length | 4-6 weeks |
| Stage 1 | **Shadow, 2 weeks:** the agent proposes, nothing is sent, and controllers compare with their own decisions |
| Stage 2 | **Assisted, 2-4 weeks:** messages and changes go out only after approval |
| In scope | General cargo with free-text forwarder replies |
| Out of scope | Dangerous goods, key accounts and automatic changes |

## Who does what

| Role | Responsibility |
|---|---|
| Cargo Capacity Controller | Reviews every proposal and offer |
| Account manager | Key accounts, difficult and legal replies |
| Cargo acceptance team | Any change to the cargo |
| Senior capacity manager | Releases above 2,000 kg |
| Head of capacity | Owns the pilot and the go or no-go decision |
| Product owner | Runs weekly reviews and sets priorities |

## What success means

| Family | Measure | Starting target, to be agreed |
|---|---|---|
| Value | Share of freed space resold before cut-off | Better than the route's baseline |
| Value | Controller time per case | Under one minute |
| Quality | Proposals approved without edits | Above 80% |
| Adoption | Controllers still choosing to use it after week 2 | All pilot users |
| Risk | Release without written forwarder notice | Zero |
| Risk | Any action without human approval | Zero |
| Risk | Fee amount in a forwarder message | Zero |

## Monitoring

| Signal | Action |
|---|---|
| Any zero-tolerance breach | Pause the pilot and investigate |
| Edit rate rises for two weeks | Sample cases and review the prompt or rules |
| Very fast approvals | Check people are really reviewing |
| AI errors or slow answers | Use the manual process and alert the owner |
| Model, prompt or policy change | Re-run all evals before release |

Evals are also re-run monthly.

## Learning loop

1. **Usage data:** every approval, edit and escalation.
2. **Two weekly questions for controllers:** What slowed you down? What didn't you trust?
3. **Real cases:** new or surprising cases are anonymised and added to the eval set.

## Rollback

Turning SpaceBack off must leave normal work unchanged. During the pilot, the airline's existing process remains available, and SpaceBack is never the only record of a decision.
