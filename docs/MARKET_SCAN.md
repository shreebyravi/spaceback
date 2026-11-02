# CargoFlow: Market scan

Public desk research, last updated 2 November 2026. It uses vendor pages and trade press, which are often marketing. It doesn't include private demos, contracts or airlines' in-house tools.

**Finding from public material:** tools predict show-ups and handle incoming requests. We found no public description of a product that reconfirms an at-risk booking, reads the reply, releases the space and re-offers it, all with human approval.

**This is a hypothesis, not proof.** Not finding a feature in public material doesn't mean it doesn't exist. A vendor could add it, and an airline may already do it in-house.

## What we found

| Who | Publicly described | Reconfirm, read, release and re-offer? | Sources |
|---|---|---|---|
| Wiremind CARGOSTACK | Booking-level show-up forecasts, overbooking and alerts for flights needing attention. Qatar Airways Cargo licensed its overbooking module in 2023 | Not described | [Wiremind](https://wiremind.io/cargostack-optimiser/capacity-management), [Aviation Business News](https://www.aviationbusinessnews.com/cargo/qatar-airways-cargo-selects-wiremind-solutions) |
| Sabre with Etihad Cargo | Regression model flags bookings likely to no-show or under-deliver | Prediction described; follow-through not described | [AGIFORS abstract](https://www.agifors.org/Technical-presentations) |
| Accelya FLX ONE Cargo and FLX AIViator | AI for capacity forecasts, overbooking and utilisation. Vendor reports forecast accuracy above 92% | Not described | [Accelya](https://w3.accelya.com/resources/press-releases/accelya-launches-flx-one-cargo-platform/), [STAT Times](https://www.stattimes.com/air-cargo/accelya-launches-ai-driven-flx-one-cargo-1355025) |
| IBS Software iCargo | Agentic AI suite for revenue management, customer service, mail and sales | Not described in the public launch coverage | [IBS](https://www.ibsplc.com/news/ibs-software-unveils-ai-powered-virtual-agents-to-transform-air-cargo-at-25th-cargo-forum), [Air Cargo Week](https://aircargoweek.com/ibs-software-unveils-ai-powered-virtual-agent/) |
| CHAMP Cargospot neo | Cargo management with AI for decisions, capacity and commercial planning | Not described | [STAT Times](https://www.stattimes.com/air-cargo/thai-airways-boosts-cargo-operations-with-cargospot-neo-1360574) |
| CargoAi AirAgent and CargoCoPilot | Reads mailboxes and drafts replies; handles rates, tracking and bookings | Handles incoming work; this loop not described | [Air Cargo Week](https://aircargoweek.com/70-percent-of-email-enquiries-for-airlines-and-forwarders-of-cargoais-customer-base-handled-by-ai-agent/) |
| Awery eMagic | Turns emails, text and images into quotes | Not described | [Air Cargo Week](https://aircargoweek.com/emagic-tool-speeds-up-air-cargo-booking/) |
| cargo.one | AI quoting from emails and rate management | Not described | [The Loadstar](https://theloadstar.com/ls_press_release/cargo-one-launches-ai-powered-quoting-workflows-and-expands-rate-management-to-help-forwarders-win-more-business/) |
| Freightos WebCargo | Booking marketplace connecting airlines and forwarders | Not described | [WebCargo](https://www.webcargo.co/about) |

## Not checked enough

- **Pelicargo:** our search found nothing relevant, so we can't say what it offers here.
- **Unisys, Kale Logistics and Nallian:** product pages weren't reviewed.
- **Vendor capacity modules:** detailed documentation isn't public, including iCargo's and Cargospot's. Allotment release or waitlist features may exist there.
- **In-house tools:** airlines may run processes no vendor page shows.

## How CargoFlow would fit

CargoFlow could work with these tools rather than replace them. A prediction system could say which bookings to ask about first, and a booking system would remain the record. CargoFlow would add the follow-through in between.

## The main risk

A larger vendor with booking-system access could add this capability. CargoFlow's prototype value is showing the workflow, and that value doesn't depend on being the only one able to build it.

## What to ask an airline

1. When a booking looks risky today, what happens next, and who does it?
2. How do forwarder replies reach the controller, and how long do they take to handle?
3. How much freed space gets resold before cut-off?
4. Does your booking system or a vendor already handle this?
