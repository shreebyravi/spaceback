# SpaceBack: Data guide

All data is made up. The airline, Solvane Air Cargo, and its forwarders are fictional, and any resemblance to real companies is accidental. `SVZ` is a made-up flight code. All times are UTC, from one sample day: 2 November 2026, 02:00.

## Data files

| File | Rows | Contains | Key columns |
|---|---|---|---|
| `data/flights.csv` | 7 | Upcoming departures | `capacity_kg`, `capacity_m3`, `overbooking_limit_pct`, `acceptance_cutoff_utc`, `temp_controlled`, `dg_accepted`, `peak_period` |
| `data/bookings.csv` | 46 | Bookings on those flights | `weight_kg`, `volume_m3`, `awb_issued`, `duplicate_hint`, `rate_per_kg_usd`, `status`, `status_utc`, `rebooked_for` |
| `data/forwarders.csv` | 8 | Forwarder accounts | `tier`, `show_up_rate_90d`, `dg_certified`, `pharma_certified` |
| `data/messages.csv` | 10 | Replies and notes on cases | `booking_id`, `from`, `received_utc`, `text` |
| `data/waitlist.csv` | 13 | Requests waiting for space | `destination`, `cargo_at_terminal_utc`, `latest_departure_utc`, `rate_per_kg_usd` |
| `data/route_history.csv` | 8 | Made-up weekly history for one route, used only as an illustration | `booked_kg`, `late_cancel_kg`, `no_show_kg`, `flown_kg`, `empty_kg` |
| `data/eval_cases.csv` | 6 | Test cases and expected behaviour | `case_id`, `booking_id`, `expected_behavior` |
| `data/recorded/` | 9 answers | Recorded agent answers, shown when no API key is saved | One JSON file per case |
| `data/recorded/stress/` | 6 answers | Answers to the stress tests | One JSON file per test |

## Key definitions

| Term | Meaning |
|---|---|
| Booking limit | Capacity plus the allowed overbooking percentage |
| Free to sell | Booking limit minus what's still booked |
| Empty % | Free weight divided by the booking limit |
| At risk | Two or more of R1-R3, or R4 alone. A reason to ask, never a reason to release |
| R1 | Forwarder's show-up rate over 90 days is below 0.80 |
| R2 | No air waybill by three days before departure |
| R3 | Booked more than 14 days before a busy-period flight |
| R4 | May duplicate a booking on another flight or carrier |
| Available to rebook | Cancelled space not yet replaced, limited by what the flight can really sell |
| Revenue estimate | Weight × the booking's or request's rate. It isn't a forecast |

## Fictional policies

| File | Covers |
|---|---|
| `policies/space_recovery_policy.md` | Risk signals, when space may be released, chasing and messages |
| `policies/fee_policy.md` | Late-change and no-show fees, and waivers |
| `policies/reoffer_rules.md` | Matching freed space to waiting requests, including cut-off |
| `policies/escalation_policy.md` | Who decides what, and when to stop |
| `policies/cargo_acceptance_rules.md` | Simplified rules, including temperature control and dangerous goods |

These aren't real airline rules or IATA regulations.

## The main examples

| Flight | What it shows |
|---|---|
| SVZ 233 | A last-minute cancellation, and a request rejected because it would miss cut-off |
| SVZ 215 | 8,300 kg cancelled, 3,000 kg rebooked, and a sale close to cut-off |
| SVZ 201 | The full space check at 72 hours, with eight different replies |
| SVZ 229 | Space that can't be resold because cut-off has passed |
