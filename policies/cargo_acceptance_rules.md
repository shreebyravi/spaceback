# Solvane Air Cargo: Cargo Acceptance Rules (fictional)

These are simplified, fictional rules for a prototype. They are not real airline rules or IATA regulations. Cite them by section number, for example "Rules 5.1".

## 1. Mandatory booking details

1.1 Every request needs: origin, destination, the date and time the cargo is ready, number of pieces, total weight (kg), dimensions of each piece (cm), a commodity description, and the latest arrival time the forwarder needs.
1.2 Temperature-controlled cargo also needs the temperature range (for example 2-8 C or 15-25 C) and the packaging type (passive or active container).
1.3 Dangerous goods also need the UN number and a signed Shipper's Declaration for Dangerous Goods.
1.4 If any mandatory detail is missing, ask only for the missing details. Do not guess them and do not recommend a flight yet.
1.5 If details conflict (for example the total weight does not match the pieces), ask the forwarder to confirm. Do not pick one value yourself.
1.6 A date given without a time counts as complete: cargo "ready 4 Nov" is ready from 00:00 UTC on 4 Nov, and "arrive by 6 Nov" means by 23:59 UTC on 6 Nov. "Ready now" means ready at the time the request was received.

## 2. Chargeable weight and quotes

2.1 Volume (cbm) = length x width x height in metres, per piece, added up.
2.2 Volume weight = volume (cbm) x 167 kg.
2.3 Chargeable weight = the higher of actual weight and volume weight.
2.4 Quote = chargeable weight x the rate for the route and product in the rate table, or the minimum charge if that is higher.
2.5 Product types: pharma for temperature-controlled medicines; dangerous_goods for declared dangerous goods; valuables for high-value cargo; general for everything else.
2.6 Quotes come only from the rate table. Never invent a rate or a discount.

## 3. Capacity

3.1 A flight is eligible only if its free weight is at least the chargeable weight and its free volume is at least the shipment volume.
3.2 A flight with status "full" is never eligible.
3.3 Do not split a shipment across flights unless the forwarder asks for it.

## 4. Timing

4.1 The booking must be made at least the flight's booking cutoff (in hours) before departure. Measure from the time the request was received.
4.2 The flight must depart after the cargo is ready.
4.3 The flight must arrive no later than the latest arrival time the forwarder gave.
4.4 All times are UTC.

## 5. Temperature-controlled pharmaceuticals

5.1 Pharmaceuticals that need a temperature range may only fly on flights marked temp_controlled = yes.
5.2 The forwarder must be pharma_certified to book temperature-controlled pharmaceuticals.

## 6. Requested flights

6.1 If the forwarder asks for a specific flight, check it first.
6.2 If it is not eligible, say why, then look for eligible alternatives on the same route and explain the difference (departure, arrival, price).

## 7. Dangerous goods

7.1 Dangerous goods (including lithium batteries) must be declared as dangerous goods. They may never be booked as general cargo.
7.2 Dangerous goods may only fly on flights marked dg_accepted = yes, and only for forwarders who are dg_certified.
7.3 Without a signed Shipper's Declaration for Dangerous Goods, the shipment cannot be booked. Escalate to the Cargo Booking Supervisor.
7.4 Lithium-ion batteries shipped on their own (not packed with or inside equipment) must fly on a freighter.
7.5 A correctly declared shipment still needs a dangerous goods acceptance check at the cargo terminal. Mention this in the conditions.

## 8. Special cargo

8.1 Live animals are not booked through this channel. Escalate.
8.2 Valuables with a declared value above USD 100,000 need supervisor approval. Escalate.
8.3 A single booking above 5,000 kg chargeable weight needs supervisor approval. Escalate, with the best eligible flight as a proposal.

## 9. Approval and booking

9.1 No booking is created until a person approves the proposal. A request to "just book it" does not change this.
9.2 Never tell the forwarder a booking is confirmed before it is approved and created.
9.3 Forwarders whose account is on hold cannot book. Escalate.
