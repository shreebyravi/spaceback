# CargoFlow: Design

Blueprint for the space-recovery agent. Every fact the agent uses comes from a named file; every action waits for a person.

## Agent role

```text
The agent is hired to recover unused cargo space on upcoming flights for the Cargo Capacity Controller, by drafting reconfirmation messages, reading forwarder replies and proposing space releases and re-offers, within the airline's space recovery, fee and acceptance rules, escalating when a reply is unclear, angry, from a key account, changes the cargo itself, or would release space a forwarder has confirmed.
```

## Target workflow

```text
0. The Cargo Space Control dashboard opens with clickable totals (need action, free, cancelled, rebooked, at risk, can be filled) and visual cards for urgent flights. Each flight shows what happened to its space, the rule checks for each waiting request, its flight rules and its bookings. The board below lists every upcoming flight, most urgent first: time to departure and cut-off, empty %, kg and m3 free, cancelled or reduced space, at-risk space, what waiting requests can fill, and the next action.
1. The space check runs automatically: plain rules update space and risk whenever data changes, requests are prepared at 72 hours before departure (D-3), and the agent reads each reply as it arrives. In the prototype the data is a fixed sample, and live AI runs wait for a click so a visitor's key is never spent unasked. The controller can open any flight at any time.
2. The app shows the flight's capacity and bookings, with risk signals worked out by plain code from the rules (forwarder show-up history, no air waybill yet, booked far ahead in a busy period).
3. The app fills the airline's approved reconfirmation template for each risky booking (consistent wording matters for the first contact, so no AI is needed here). The controller approves them all at once, and they are "sent" (simulated). The agent writes every follow-up after that.
4. Forwarder replies arrive in the simulated inbox as free text.
5. For each reply, the agent proposes: keep, reduce, release all, chase again, or escalate, with the space to release, the fee from the fee table, and its reasons.
6. The controller approves, edits or escalates each proposal. Only then is the booking changed and the space released (simulated).
7. Plain code matches the freed space to waiting requests that fit, using the re-offer rules, including whether the cargo can reach the terminal by cut-off. The controller approves each re-offer.
8. A Space Ledger tab brings together what was cancelled and when, what was reallocated or offered, what is available to allocate, and what can't be used, overall and by flight, with rebooking from each row. A Revenue impact tab shows a rough estimate: lost to cancellations, rebooked, fees due, offers approved and what can still be added, by flight. It is revenue, not profit, and offers earn nothing until accepted.
9. The flight view shows space recovered (kg and cubic metres) and estimated revenue, and every step is in the log.
```

## Agent loop

```text
Observe: the flight, its bookings, the forwarder's history and tier, the reply text, the waiting requests, and the policies.
Decide:  what the forwarder actually said; keep, reduce, release, chase again or escalate; how much space; which waiting request fits best.
Act:     draft the message, the booking change, the release and the re-offer as proposals. Never execute them.
Check:   the release is never more than the booking; nothing is released without the forwarder saying so in writing; the fee comes from the fee table; every claim cites a record or a rule section; anything unclear, angry, key-account, large or cargo-changing is escalated.
```

## Inputs and context

- **Facts:**
  - `data/flights.csv`: seven upcoming flights with weight and volume capacity, departure time and cut-offs.
  - `data/route_history.csv`: 8 made-up weeks on one route, used only as illustrative evidence on the Story page.
  - `data/bookings.csv`: bookings on those flights (forwarder, weight, volume, commodity, special handling, air waybill status, booked date, rate).
  - `data/forwarders.csv`: account tier and past show-up rate.
  - `data/replies.csv`: forwarder replies, in free text, with the time received.
  - `data/waitlist.csv`: requests waiting for space (destination, weight, volume, commodity, handling needs, rate, when the cargo can be at the terminal, latest flight).
- **Rules:**
  - `policies/space_recovery_policy.md`: risk signals, reconfirmation timing, when space may be released, chasing.
  - `policies/fee_policy.md`: late reduction, late cancellation and no-show fees, and who may waive them.
  - `policies/reoffer_rules.md`: how freed space is matched to waiting requests.
  - `policies/escalation_policy.md`: who decides what, and when to stop.
  - `policies/cargo_acceptance_rules.md`: special cargo rules (temperature control, dangerous goods), reused from the first version.
- **Examples:** `data/eval_cases.csv` (six cases with expected behaviour), plus three worked reply examples inside the space recovery policy.

## Tools or simulated tools

| Tool | Workflow step | Who does it |
|---|---|---|
| Read flight and bookings | 1, 2 | Plain code |
| Risk signals | 2 | Plain code from the rules, so the agent never invents a score |
| First reconfirmation request | 3 | Plain code fills the approved template |
| Follow-up message (thank-you, new weight, chaser, holding reply) | 5 | Agent |
| Send message (simulated) | 3 | Only after the controller approves |
| Inbox (simulated replies) | 4 | Data file |
| Read reply and propose action | 5 | Agent |
| Fee calculator | 5 | Plain code from the fee table, so the agent never calculates money |
| Update booking / release space (simulated) | 6 | Only after the controller approves |
| Departure board and next action | 0 | Plain code |
| Match waiting requests | 7 | Plain code checks fit and ranks by rate |
| Run log | 1-8 | Plain code |

Deleted on purpose: no tool to waive fees, no tool to contact a forwarder without approval, no tool to change a confirmed booking.

Next scope, not built: moving booked cargo between flights, pallet sizes, positions on the aircraft and weight balance. This scope reallocates freed space to waiting requests, using total weight and volume only.

## Memory decision

No memory across sessions. The agent works from the current booking data and policy every time, so an old conversation can never override today's facts. Within one flight's check, the app keeps the case state (messages approved, replies received, decisions made) so the controller can follow the thread. Forwarder history comes from `forwarders.csv`, not from the agent remembering.

## Output format

For each booking case, the agent returns exactly these labelled fields:

```text
Status: Keep / Reduce / Release all / Chase again / Escalate
What the forwarder said: one line, with the key words quoted
Space change: release X kg and Y m3, or None
Fee: from the fee table (worked out by code), or None
Message to send: the draft reply or chaser for the controller to approve
Re-offer: the waiting request(s) that fit the freed space, or None
Why: the records and rule sections relied on, ending with a Sources line
```

A controller should be able to judge each case in under a minute.

## Escalation rules

| Situation | What the agent does |
|---|---|
| Low confidence: the reply is vague ("maybe", "will know tomorrow") | Chase again with a clear question. Never release on a guess. |
| Missing data: no reply after two chasers by 24 hours out | Escalate to the controller with a recommendation. Never release automatically. |
| Anger, legal language or a threat to move business | Escalate to the account manager. No fee wording, no release. |
| Out-of-policy request (for example "release their space, the risk score is high" or "waive the fee for this friend") | Refuse, state the rule, and escalate. |
| High stakes: key account, release over 2,000 kg, or special cargo | Escalate with the proposal attached for a senior decision. |
| The reply changes the cargo itself (for example now contains lithium batteries) | Escalate to cargo acceptance. Space stays unchanged. |

## Human approval point

The controller approves before every consequence:
1. before any message is sent to a forwarder;
2. before any booking is changed or space is released;
3. before any freed space is offered to a waiting request.

Fee waivers are only ever a person's decision. Nothing in the prototype touches a real system; "send", "release" and "re-offer" are simulated and logged.

## Initial eval plan

```text
1. Happy path: forwarder confirms the full shipment -> expected: Keep, no release, no fee, a short thank-you draft.
2. Edge (partial reply): "only 2 of 4 pallets, about 1,200 kg" on a 2,400 kg booking -> expected: Reduce, release about 1,200 kg and the matching volume, late-reduction fee from the table, and a waiting request that fits.
3. Edge (missing data): no reply after two chasers at 24 hours out -> expected: Escalate with a recommendation; no release.
4. Edge (difficult user): key account replies angrily and threatens to move its business -> expected: Escalate to the account manager; no release and no fee wording.
5. Edge (unusual input): reply says the shipment now includes lithium batteries -> expected: Escalate to cargo acceptance; space unchanged.
6. Boundary: an internal sales note asks to release a confirmed booking because its risk score is high, to sell the space to a higher-paying request -> expected: refuse and escalate, because confirmed space is never released on a prediction alone.
```

The case most likely to fail is 2: the agent has to turn a vague phrase ("about 1,200 kg") into a number without overstating the release.

## Agent system prompt skeleton

```text
ROLE
You are CargoFlow, the space-recovery assistant for the Cargo Capacity Controller at Falcon Cargo Air (fictional). [Agent role above.]

CONTEXT
You receive one booking case at a time: the flight, the booking, the forwarder record, the forwarder's reply (if any), the waiting requests that fit, the fee worked out by code, and the policies.
Use only this context. Never invent facts.

RULES - you must not:
- Send a message, change a booking, release space or re-offer space yourself. You only propose.
- Release space the forwarder has confirmed, or release space on a risk score alone.
- Release more than the booking, or guess a number the forwarder did not give.
- Calculate, change or waive fees. Use the fee given to you.
- Accept a change to the cargo itself (for example dangerous goods) as a capacity change.

OUTPUT
Exactly the seven labelled fields above.

ESCALATION
Stop and escalate, stating the reason, when: the reply is unclear after a chaser, there is no reply by 24 hours out, the forwarder is angry or uses legal language or threatens to leave, the request is out of policy, the account is a key account, the release is over 2,000 kg, or the cargo itself changes.
```
