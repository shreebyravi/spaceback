# CargoFlow: Product requirements

| | |
|---|---|
| **Product** | CargoFlow AI, a cargo space recovery agent |
| **Owner** | Shree Byravi |
| **Status** | Prototype with made-up data; not validated by an airline |
| **Updated** | 2 November 2026 |

## Summary

CargoFlow helps an airline's capacity team recover cargo space that's booked but won't fly. It shows what changed on every upcoming flight, reads forwarder replies, and helps a person resell freed space before cut-off.

## Problem

Forwarders cancel late, send less than they booked, or never show up. An [AGIFORS abstract](https://www.agifors.org/Technical-presentations) reports 15-30% no-shows and cancellations between three days before departure and departure, as a network average. Prediction and fees don't resell the space. We believe the follow-through is the gap, as set out in the [market scan](MARKET_SCAN.md).

## User

**Primary:** the Cargo Capacity Controller, responsible for how full each flight is.

**Also involved:** account managers for key accounts, the cargo acceptance team for cargo changes, and the senior capacity manager for large releases.

## Goals and measures

| Goal | Measure | Target for a pilot, to be agreed |
|---|---|---|
| Recover more space | Share of freed space resold before cut-off | Better than the route's baseline |
| Save controller time | Time per case | Under one minute |
| Stay safe | Release without written notice, or action without approval | Zero |

None of these has been measured on real operations.

## Non-goals for this scope

- Automatic releases or messages
- Moving booked cargo between flights
- Pallet, position or weight-balance checks
- Accepting dangerous goods or making security decisions
- Replacing booking, revenue or load-control systems

## Requirements

### Dashboard
1. Show totals for flights needing action, free space, cancelled or reduced space, rebooked or offered space, at-risk space and what can be filled.
2. Open details from each number.
3. Rank flights by what can still be saved.
4. Count a sale close to cut-off as needing action.

### Flight view
5. Show the flight's history, rules and bookings, with booking details.
6. Explain each at-risk shipment in plain language.
7. Treat risk as a reason to ask, never a reason to release.

### Automatic check and agent
8. Update space and risk by plain rules.
9. Prepare requests at 72 hours, while allowing any flight to be opened at any time.
10. Read each reply and return status, what the forwarder said, release, message and reasons with sources.
11. Check each proposal in code, and block approval when a check fails.
12. Escalate unclear, angry, key-account, cargo-changing and over-2,000 kg cases.
13. Refuse to release confirmed space, whoever asks.

### Reallocation
14. Check each waiting request for weight, volume, handling, latest departure and cut-off, and show the result of each rule.
15. Show the time left until cut-off.
16. Let a person approve an offer from the flight view or the ledger.
17. Treat an approved offer as an offer until the forwarder accepts.

### Ledger and revenue
18. Show what was cancelled and when, what replaced it, what's available and what can't be used, overall and by flight.
19. Show a rough revenue estimate, clearly labelled, with what's at risk shown separately.

### Trust
20. A person approves every message, release and offer.
21. Fees and rule checks come from code.
22. Label recorded answers and made-up data.
23. Publish test results, including failures.

## How the agent behaves

See [DESIGN.md](DESIGN.md), [AGENT_INSTRUCTIONS.md](AGENT_INSTRUCTIONS.md) and [ARCHITECTURE.md](ARCHITECTURE.md).

## Testing

Six eval cases and six stress tests are in [EVALS.md](EVALS.md). In the latest recorded run, all six evals matched, and five of six stress tests behaved as expected. In the sixth, the agent wrongly proposed a large release, and the app's rule blocks approval. A full live run hasn't been done.

## Dependencies and open questions

- **Dependencies for real use:** read-only booking data, mailbox access, an approved AI setup, and security and privacy reviews.
- **Open questions:** Does a manual reconfirmation process exist as assumed? How much freed space can be resold in time? Do existing tools already do this? Would controllers use it daily?

## Rollout

Discovery with controllers, then a shadow pilot on one route, then an assisted pilot. See [PILOT_AND_MONITORING.md](PILOT_AND_MONITORING.md) and [ROADMAP.md](ROADMAP.md).
