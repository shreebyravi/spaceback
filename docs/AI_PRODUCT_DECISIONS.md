# SpaceBack: AI product decisions

How building with a large language model (LLM) changes product management, which decisions a PM has to make, what this prototype chose, and what a real implementation would add.

**How to read this:** "This prototype" means something actually done here. "Real implementation" means a proposal that hasn't been built or tested.

## How AI product management differs

| Area | Traditional software | AI product |
|---|---|---|
| **Behaviour** | The same input usually gives the same output | The same input can give different outputs |
| **Requirements** | "When X happens, do Y" | Also: what good looks like, what it must never do, and how often it may be wrong |
| **Testing** | Pass or fail against fixed rules | Evals: sample cases, judged for quality, repeated over time |
| **Definition of done** | The feature meets its acceptance criteria | Quality passes an agreed bar, and keeps being checked after launch |
| **What gets built** | Screens, logic and data | Those, plus prompts, context, evals and guardrails |
| **Main failure** | A bug, usually repeatable | A confident wrong answer, which can be hard to spot or reproduce |
| **Cost** | Mostly fixed once built | Can rise with each use of the model |
| **Change** | Mostly changes when the team releases | A model, prompt or policy change can alter behaviour |
| **User interface** | Shows results | Must also show evidence and make it easy to correct the AI |
| **Risk** | Security, privacy and reliability | Those, plus made-up facts, prompt injection and too much trust in the AI |

## How development changed on this project

| Traditional step | What changed here |
|---|---|
| Write a specification | Wrote the spec **and** the agent's instructions. Changing one instruction changed the product |
| Developers build it | An AI coding assistant wrote code and drafted documents, while the PM directed, questioned and tested the result |
| QA checks the build | Writing test cases and judging answers became a core PM job |
| Fix the bug | Often the fix was to change the instructions, re-run every case and look for side effects |
| Decide what to automate | Each step had to be split between plain code, AI and a person |
| Review the design | The review also asked: can a person see why the AI said this, and correct it quickly? |

Coding got faster, which made judgement more important: whether the problem is real, what's good enough, and what the AI must never do.

## Decisions a PM has to make

### 1. Should this use AI at all?

- **Why it matters:** an LLM adds cost, variation and new risks. It should earn its place.
- **This prototype:** AI reads free-text replies and drafts messages. Plain code handles space, risk signals, fees and rule checks, and the first request is a template.
- **Real implementation:** keep this split, and measure whether AI performs better than simple templates or rules.

### 2. How much freedom does the agent get?

- **The range:** suggest only → act after approval → act and report → act alone.
- **This prototype:** it proposes, and a person approves every message, release and offer.
- **Real implementation:** consider more automation only for low-risk steps, one at a time, after a pilot provides evidence.

### 3. Which model?

- **The trade-off:** more capable models usually cost more and can respond more slowly.
- **This prototype:** Claude Sonnet, with medium effort. No formal comparison was run.
- **Real implementation:** compare models on the same evals, and consider simpler models for easy steps. Check which providers and regions the airline approves.

### 4. What does the agent get to see? (context)

- **Why it matters:** too little context causes wrong answers. Too much adds cost and can distract the model or expose unnecessary data.
- **This prototype:** one booking case at a time, plus the full text of all five short policies.
- **Real implementation:** large policy sets may need retrieval (RAG), which finds only the relevant sections. Retrieval quality would then need its own tests.

### 5. How is the answer structured?

- **This prototype:** a fixed JSON format with set fields and statuses. This fixed format mismatches found during development, and code can check the fields.
- **Real implementation:** keep it. Reliable structure is what lets code validate an answer and a person review it quickly.

### 6. Should the AI use tools directly?

- **The trade-off:** direct tools make an agent more capable, but they increase the damage a mistake can do.
- **This prototype:** no tools for the model. Code gathers the data, and approved actions are simulated.
- **Real implementation:** read-only tools could come first. Anything that changes data should go through an action service, only after approval.

### 7. What counts as good enough? (evals)

- **This prototype:** six cases with expected results written first, a person's verdicts, and six stress tests. Results and two improvements are published.
- **Real implementation:** use many more cases from real, anonymised messages, run each several times, and set release gates. For example, any hard-limit breach blocks release.

### 8. What should the product do about variation?

- **Why it matters:** an LLM can give different answers to the same case.
- **This prototype:** stress test S-06 escalated correctly in two of three runs and once proposed a 3,200 kg release. The code blocks approval of that answer.
- **Lesson:** an instruction is not a guarantee. Rules that must never be broken belong in code too.
- **Real implementation:** measure the error rate over many runs, and report the rate instead of a single pass.

### 9. How do we handle misuse and bad input? (guardrails)

- **Prompt injection:** a message tries to give the AI new instructions.
- **This prototype:** message text is treated as data, code limits outcomes, and trick-message tests behaved as expected in the runs so far.
- **Real implementation:** independent security testing, limits on what the model can reach, and checks on sender identity.

### 10. How do we avoid made-up facts?

- **This prototype:** the agent uses only the given context and cites its sources. Code checks that each cited record exists.
- **The limit:** a real citation can still be used wrongly, so a person reviews the reasoning too.
- **Real implementation:** measure how often a citation doesn't support the claim, and sample cases regularly.

### 11. How do we keep the human review real?

- **The risk:** people may approve everything once the AI seems good, a problem called automation bias.
- **This prototype:** reasons, sources and rule checks are visible, and unsafe proposals can't be approved.
- **Real implementation:** monitor approval speed and edit rates, and sample approved cases.

### 12. What will it cost, and how fast must it be?

- **This prototype:** not measured. No real usage volumes exist, and a full live run hasn't been done.
- **How to estimate:** cost per case = (input tokens × input price) + (output tokens × output price). Multiply by replies per flight and flights per day.
- **Real implementation:** set a cost per recovered kg, and a response-time target. Look at ways to reduce repeated cost, such as caching shared policy text.
- **The product question:** is the recovered revenue clearly worth more than the AI and review costs?

### 13. What happens when the AI fails?

- **This prototype:** errors are shown, a malformed answer can't be approved, and nothing happens automatically.
- **Real implementation:** retries, a backup process and the option to work manually if the provider is down.

### 14. What happens after launch?

- **Why it matters:** behaviour can shift when the model, prompts, forwarders' writing or policies change.
- **This prototype:** not built. A session log and repeatable test cases are the starting point.
- **Real implementation:** version prompts and models, keep an audit trail, monitor quality, and re-run evals before each change.

### 15. What data can go to the model?

- **This prototype:** made-up data only. A visitor's own API key stays in their browser.
- **Real implementation:** minimise data, decide on retention and regions, keep keys on a server, and complete privacy and vendor reviews.

## Trade-offs made here

| Choice | What it gave us | What it cost | In a real implementation |
|---|---|---|---|
| Person approves everything | Safety and trust | Less time saved | Reconsider low-risk steps after evidence |
| One-page app with no backend | Fast to build and easy to share | No login, permanent log or integrations | Server, roles and audit trail |
| Recorded answers | Anyone can try it for free | Not proof of live performance | Live evals before any pilot |
| Full policy text sent each time | Simple and easy to test | Wouldn't scale to large manuals | Retrieval and caching, if needed |
| Small eval set | Quick learning and clear results | Weak statistical evidence | Larger set from real messages |
| Total weight and volume only | A workflow that could be shown quickly | Not enough for load planning | Pallets, positions and limits |
| Rough revenue estimate | Shows why it might matter | Could be mistaken for a promise | Measure against a baseline |
| Keep failures visible | Credibility | A less perfect-looking scorecard | Keep doing it |
| Waiting requests only | Smaller scope | Booked cargo can't be moved | Add flight moves next |
| One prompt for the whole case | Easy to understand | Harder to tune each step separately | Split steps only if evals show the need |

## Lessons from building it

| What happened | PM lesson |
|---|---|
| The first idea already existed commercially | Check the market before building, even when the demo works |
| Answers were cut off when the model used up its output limit | Limits are a product setting, not only a technical one |
| Free-form answers broke the format | Use a fixed structure when code depends on the output |
| Evals showed all six matching, but judgement found weaknesses | Matching the expected status doesn't always mean a good answer |
| A person asked why batteries weren't checked against policy | Domain questions improve an AI product as much as prompts do |
| A prompt change altered an unrelated result | Re-run everything after any change |
| No API credit | A recorded mode made it shareable, but the limit has to be stated |

## What a real team would add

| Role | Would own |
|---|---|
| Capacity controllers | Workflow reality, judging answers and feedback |
| ML or AI engineer | Model calls, evals, retrieval and monitoring |
| Software engineers | Integrations, security and the action service |
| Data and revenue analysts | Baselines, recovered space and revenue |
| Security, privacy and compliance | Reviews and sign-off |
| Dangerous goods, load control and acceptance | Their rules and decisions |
| PM | Problem, scope, quality bar, autonomy level, go or no-go decisions and learning loop |

## My role in this project

**Shree Byravi** led the product work. An AI coding assistant wrote the code, drafted documents and helped with research, working from these directions and reviews:

- Challenged the first concept because similar products already existed, which led to research and the move to space recovery.
- Chose the user, hub, approval model and scope, including waiting requests first and flight moves later.
- Spotted the missing dangerous-goods check, which led to the first eval improvement.
- Judged and confirmed eval verdicts.
- Reframed the page for airline audiences and asked for the whole story to be told.
- Questioned the 72-hour window, which led to an any-time check with 72 hours as the first alert.
- Shaped the dashboard, including its summary first, drill-downs, plain at-risk reasons, shipment counts, rebooking history, time to reallocate, Space Ledger and revenue view.
- Required an honest answer at each stage about whether a real problem was being solved.
- Chose to keep the product honest about what was and wasn't proven.

This is a personal prototype on made-up data. It hasn't been used in a company or tested by an airline.
