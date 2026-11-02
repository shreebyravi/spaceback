# SpaceBack: Business case model

A break-even model an airline can fill in with its own numbers.

**This isn't a forecast.** There are no real volumes, recovery rates, costs or prices here, so it makes no ROI claim. The example numbers are made up to show how the calculation works.

## The question

**How much space would SpaceBack need to recover each month to cover its costs?**

## The calculation

```text
Value per recovered kg = average rate per kg × contribution share

Break-even kg per month = total monthly cost ÷ value per recovered kg

Break-even kg per flight = break-even kg per month ÷ flights per month

Break-even share of empty space = break-even kg per month ÷ empty kg per month
```

Contribution share is the part of revenue left after the extra costs of carrying the cargo.

## Inputs the airline needs

| Input | Source | In this example |
|---|---|---|
| Average rate per kg | Revenue data | USD 2.30, from the made-up route history |
| Contribution share | Finance | 60%, made up |
| Flights per month | Schedule | About 30, from 7 flights per week |
| Empty kg per month | Flight records | About 296,000, from the made-up route history |
| AI cost | Provider pricing × tokens × cases | Part of the monthly cost |
| Hosting, integration and support | IT or vendor | Part of the monthly cost |
| Controller and review time | Pilot measurement | Not included in the example |
| One-time build and setup | Project plan | Not included in the example |

**AI cost per case** = (input tokens × input price) + (output tokens × output price).

## Example only

These use the made-up inputs above. Value per recovered kg = USD 2.30 × 60% = USD 1.38.

| Assumed total monthly cost | Break-even kg per month | Per flight | Share of empty space |
|---|---|---|---|
| USD 10,000 | 7,246 kg | 239 kg | 2.4% |
| USD 25,000 | 18,116 kg | 597 kg | 6.1% |
| USD 50,000 | 36,232 kg | 1,194 kg | 12.2% |

**How to read it:** at an assumed cost of USD 25,000 a month, SpaceBack would need to recover about 18,100 kg a month that would otherwise have flown empty. That's a calculation, not a prediction that it will.

## What the model leaves out

| Possible extra value | Possible extra cost or risk |
|---|---|
| Controller time saved | Controller review time |
| Better fee collection | Forwarder relationship damage |
| Fewer last-minute surprises | Offers that are declined |
| | Space that would have sold anyway |
| | Security, compliance and change costs |

**Only count additional value.** Recovered space should be compared with a baseline, or a similar route, so normal resale isn't counted as a SpaceBack result.

## How to validate it

1. Measure the baseline in [discovery](LAUNCH_PLAN.md).
2. Replace every made-up input with the airline's data.
3. Measure real recovery and offer acceptance during the pilot.
4. Decide at the gate: scale, narrow or stop.

The biggest unknown is the share of freed space that can really be resold before cut-off.
