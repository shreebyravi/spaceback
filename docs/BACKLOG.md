# SpaceBack: Backlog

User stories for the next scope, with acceptance criteria. **Priorities are provisional.** No real users have confirmed them, and no engineering team has estimated them.

**Priority:** Must = needed for that stage. Should = important, but the stage can run without it. Could = useful later.

## Before a shadow pilot

| ID | Story | Acceptance criteria | Priority |
|---|---|---|---|
| B-1 | As a controller, I see real booking data so that the dashboard reflects my flights | Read-only feed updates the dashboard; stale data shows a warning; nothing is written back | Must |
| B-2 | As a controller, replies arrive automatically so that I don't copy them across | Replies from a shared mailbox reach the right booking; unmatched messages go to a person | Must |
| B-3 | As a capacity manager, the airline's real rules are used so that proposals fit our policy | Fictional policies replaced; rule changes need approval; evals re-run after each change | Must |
| B-4 | As a compliance reviewer, every proposal and decision is saved so that it can be audited | Evidence, proposal, edits, approver and time are stored and can't be silently changed | Must |
| B-5 | As a product owner, each prompt and model version is tracked so that I can explain changes | Each answer records its versions; a change can't be released without an eval run | Must |
| B-6 | As an IT owner, keys and AI calls run on a server so that they're controlled | No key in the browser; calls logged; only approved data is sent | Must |
| B-7 | As a PM, I can compare the agent with controllers so that shadow results can be measured | Agent and controller decisions are shown side by side, with agreement rate and reasons | Must |

## Before an assisted pilot

| ID | Story | Acceptance criteria | Priority |
|---|---|---|---|
| B-8 | As a controller, approved messages and changes are sent so that I don't re-enter them | Only approved actions go out; failures are visible; the booking system stays the record | Must |
| B-9 | As a controller, offer outcomes are tracked so that I know what really came back | Offers show accepted, declined or expired; only cargo that flew counts as recovered | Must |
| B-10 | As a load planner, I confirm offers against pallet limits so that they can actually fly | Pallet sizes and limits shown, or a required manual step before an offer goes out | Must |
| B-11 | As a security lead, secure supply chain status is checked so that offers stay compliant | An offer can't go out when the required status is missing | Must |
| B-12 | As a capacity manager, I see chargeable weight so that value and space are right | Calculations use chargeable weight and show the rule used | Should |
| B-13 | As a controller, I can quickly mark why I disagreed so that the agent can improve | One-click reasons when editing or escalating; reasons appear in weekly reporting | Should |

## Next scope after the pilot

| ID | Story | Acceptance criteria | Priority |
|---|---|---|---|
| B-14 | As a controller, I can move a booked shipment to another flight, with the forwarder's agreement | Rules are checked; the forwarder agrees first; both flights update after approval | Should |
| B-15 | As a capacity manager, allotments are handled correctly | Allotment terms are visible; releases follow the agreement | Should |
| B-16 | As a controller, I see connections and priority cargo | Connections and priority are flagged before release or offer | Should |
| B-17 | As a revenue manager, the airline's show-up predictions set who is asked first | Predictions rank requests; a prediction still can't trigger a release | Could |
| B-18 | As a forwarder, I can confirm, reduce or accept an offer in a portal | Secure access; every action is logged; messages remain an option | Could |

## Known issues in the prototype

| ID | Issue | Priority |
|---|---|---|
| B-19 | Tabs show a small scrollbar on narrow windows | Could |
| B-20 | The log and approvals reset after a page reload | Must before a pilot; covered by B-4 |
| B-21 | A full live AI run of the evals hasn't been done | Must before a pilot |
