# CargoFlow: Recover cargo space before it flies empty

**The ask:** 30 minutes with a capacity or revenue management lead, to test whether this workflow matches your reality and whether a small pilot on one route is worth exploring.

## The problem

Forwarders cancel late, send less than they booked, or never show up. Published industry work developed with the Etihad Cargo team reports **15-30% no-shows and cancellations** in the last three days before departure, as a network average.

By the time the airline knows, the space may be too late to sell. Fees recover some money, but they don't fill the aircraft.

## The gap we believe exists

Tools can predict which bookings may not show. Inbox tools can handle incoming requests. We haven't found a public description of a product joining the steps in between:

**Flag → ask the forwarder → read the reply → release the space → resell it before cut-off**

This is still a hypothesis, and your team is best placed to test it.

## What CargoFlow does

- **One view of what matters now:** every flight ranked by what can still be saved, with plain reasons for each at-risk shipment.
- **AI that reads messy replies:** "only 2 of 4 pallets, about 1,200 kg" becomes a proposal with its sources.
- **Reselling with the rules in view:** each waiting request is checked for weight, volume, handling and cut-off.
- **One ledger:** what was cancelled, what replaced it, and what's still available, with a revenue estimate.

## Why your team stays in control

- A person approves every message, release and offer.
- Code, not AI, handles space, fees and rule checks.
- It never releases on prediction alone, whoever asks.
- Dangerous goods, load control and security stay with their current owners.

In testing, the agent refused a trick message and a fake approval. In one test it wrongly proposed a large release, and the app's own rule blocked approval. That's the reason for keeping limits in code.

## What exists today

A working prototype with made-up data. It includes a dashboard, the agent workflow, a Space Ledger, a revenue view, quality checks and full documentation.

**It isn't proven:** no airline has tested it, it isn't connected to real systems, and it doesn't check pallets or aircraft balance yet.

## A small, safe next step

| Stage | Length | What happens |
|---|---|---|
| **Discovery** | 30 minutes | Compare the workflow with how your team works today |
| **Shadow pilot** | About 2 weeks | One route. The agent proposes, nothing is sent, and controllers compare it with their own decisions |
| **Assisted pilot** | 2-4 weeks | Messages and changes go out only after approval, once reviews are complete |

**The question a pilot answers:** how much more space can be resold before cut-off, and how much time does it save?

## See it

- **Try the prototype:** https://shreebyravi.github.io/cargoflow/
- **Read the documents:** https://github.com/shreebyravi/cargoflow
- **Contact Shree Byravi:** https://www.linkedin.com/in/shree-byravi/
