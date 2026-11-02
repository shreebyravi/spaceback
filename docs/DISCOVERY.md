# SpaceBack: Discovery

**SpaceBack recovers cargo space that is booked but will not fly, before the flight leaves.**

Prototype with synthetic data. The airline (Solvane Air Cargo), forwarders, flights and bookings are all made up. Nothing here is connected to any real airline or system.

## The problem in one paragraph

Freight forwarders book space on cargo flights and then cancel late, send less than they booked, or never show up. An AGIFORS conference abstract on cargo show-up prediction, developed with the Etihad Cargo team, reports **15-30% no-shows and cancellations in the last three days before departure**, as a network-wide average ([AGIFORS technical presentations](https://www.agifors.org/Technical-presentations), [agenda](https://www.agifors.org/page-18348)). Airlines protect themselves by overbooking and by charging fees (Qantas Freight up to 100% of the charge, American Airlines Cargo a flat fee, ITA Airways Cargo 50%), but fees are charged after the flight has gone. They do not put the cargo back on the plane. Unused space that is not released in time is space that flies empty.

## What already exists, and the gap

| Already solved | Who | What it does |
|---|---|---|
| Predicting no-shows | Wiremind CARGOSTACK (used by Qatar Airways Cargo); show-up models such as the AGIFORS/Etihad work | Scores each booking's chance of showing up and sets overbooking levels |
| Answering incoming requests | CargoAi AirAgent, Awery eMagic, cargo.one AI quoting | Read inbound emails and draft quotes or bookings |
| Booking checks | IBS iCargo, CHAMP Cargospot | Validate capacity, special handling, embargoes |
| Fixed release rules | Some systems (for example SmartKargo allotments) | Release unused allotment space at a set time before departure |

**Gap (hypothesis):** no product found closes the loop between "this booking looks risky" and "the space is resold": ask the forwarder, read the reply, release what is not coming, and offer it to someone waiting, with a person approving. Vendors not fully checked: Accelya, CHAMP (internal docs), Unisys, Freightos/WebCargo, Pelicargo. Not finding the feature is not proof it does not exist.

See [MARKET_SCAN.md](MARKET_SCAN.md) for the sources and what wasn't checked.

## Discovery answers

**User:** Cargo Capacity Controller at an airline cargo division (fictional Solvane Air Cargo, Dubai hub). Watches each upcoming flight's bookings and decides what space to release and resell.

**Workflow:** Pre-departure space recovery for one flight: find bookings that may not fly as booked, reconfirm them with forwarders, release unused space, and re-offer it to waiting requests.

**Trigger:** A flight reaches 72 hours before departure (D-3) and the first alert goes out, or a controller opens any flight at any time, or a cancellation arrives. Late changes happen right up to departure.

**Current process:**

```text
1. Pull the flight's booking list and look at which bookings look risky (forwarder history, no air waybill yet, booked far ahead in a busy period).
2. Email or call each risky forwarder to ask whether the shipment is still coming, and at what weight and volume.
3. Wait for replies, chase the ones that do not answer, and read free-text replies such as "only 2 of 4 pallets".
4. Update bookings and release unused space in the booking system, and work out any late-change or no-show fee.
5. Offer released space to waiting requests or spot sales, often too late to sell it.
```

**Pain points:**
- Chasing is manual and spread over many flights, so it starts late or not at all.
- Replies are free text and partial ("about 1,200 kg, maybe less"), so they take time to read and turn into booking changes.
- Space released close to departure is hard to resell, so it flies empty.
- Fees and exceptions are applied inconsistently, especially for important customers.
- Prediction tools say which bookings are risky but do nothing about them.

**Agent opportunity:** For each risky booking, the agent drafts the reconfirmation message, reads the forwarder's reply, proposes the booking change and the space to release, works out the fee from the fee table, and matches freed space to waiting requests. A person approves every message, every release and every re-offer.

**Synthetic data plan:**
- Flights: capacity in weight and volume, departure time, cut-offs.
- Bookings on the demo flights: forwarder, weight, volume, commodity, special handling, air waybill status, booking date, rate.
- Forwarders: account tier (key account or not), past show-up rate.
- Forwarder replies: free-text messages, including clear, partial, unclear, angry and surprising ones.
- Waiting requests: shipments that want space on the same flight.
- Policies: space recovery rules, fee table, re-offer rules, escalation rules, cargo acceptance rules.
- Eval cases with expected behaviour.

**Human boundary:**
- The agent never sends a message, changes a booking, releases space or re-offers space by itself. It drafts; a person approves.
- It never releases space a forwarder has confirmed, and never releases space on a risk score alone.
- It never waives or invents fees.
- It escalates angry or key-account replies, replies that change the cargo itself (for example new dangerous goods), and large releases.

**Success metric:**
- Prototype: eval cases pass; the agent reads labelled replies correctly; zero releases without a person's approval.
- Pilot (later): kilograms of space recovered and resold per flight, share of risky bookings resolved before 24 hours out, controller time per flight, and no rise in offloads or complaints.

**Initial demo idea:**

```text
The demo will show a departure board -> a flight's list of bookings, including one at 72 hours and one last-minute cancellation -> its bookings, risk signals and rules -> the agent's reading of each forwarder reply and proposed release -> labelled fields with space, fee and re-offer -> the controller approving, editing or escalating, with recovered kilograms on screen.
```

## Why this needs an agent, not just prediction

Prediction already exists and recovers no space by itself. The missing work is several steps across tools (booking list, messages, inbox, fee table, waiting list), reading messy human replies, and ending in actions that are hard to undo (releasing and reselling space). That combination needs an agent with a human gate.

## How it differs from ScreenGate

ScreenGate waits for a flagged payment and helps a person review it. SpaceBack acts first, before a deadline: it starts conversations with outside companies, reads their replies, and moves scarce space from one customer to another.
