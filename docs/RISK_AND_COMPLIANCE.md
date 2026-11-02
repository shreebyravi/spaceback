# CargoFlow: Risk and compliance

CargoFlow supports commercial capacity decisions. It does not replace load control, dangerous goods acceptance or security checks.

**This prototype makes no compliance claim.** It uses only made-up data. Real use needs review by the airline's own teams, and by its regulators where they require it.

## Product risks

| Risk | What could happen | In the prototype | Before real use |
|---|---|---|---|
| Wrong release | A customer loses space they need | Only on written notice, with a person's approval. Code checks the amount | Measure edit rates in shadow mode |
| Reading a reply wrongly | Wrong action or wording | Vague replies are chased. Sources shown for checking | Test with real, anonymised replies |
| Message tries to trick the AI | Forwarder or outsider text tries to change the rules | Trick-message tests behaved as expected in the runs so far, and code limits what can happen | Independent security testing |
| Fake identity | Someone claims approval they don't have | Claims in a message aren't accepted as approval | Sender checks and sign-in for all staff |
| Too much trust in the AI | People approve without reading | Reasons and rule checks are visible | Monitor approval speed, and sample cases |
| Unfair treatment | Some forwarders are chased more than others | Reasons are shown and flags lead only to questions | Review by forwarder group and region |
| Relationship damage | Too many chasers annoy customers | Key and angry accounts go to the account manager | Limits on message volume, agreed with sales |
| Revenue overstated | Decisions rely on rough estimates | Labelled as estimates, and offers count only if accepted | Compare with actual results |
| Agent varies between runs | The same case gets a different answer | Stress test S-06 varied; plain-code limits block the unsafe proposal | Run each case many times and keep hard limits in code |
| AI service failure | No proposals for a period | Errors are shown and nothing happens automatically | Manual fallback and alerting |

## Safety, security and regulatory areas

| Area | In the prototype | Needed for real use | Likely owner |
|---|---|---|---|
| Dangerous goods | Never accepts them. Any cargo change goes to acceptance, with fictional rules pre-checked | Align with IATA Dangerous Goods Regulations and approved acceptance processes | Dangerous goods and acceptance |
| Load and balance | Not checked. Totals only | Load control stays the authority. Add pallet, position and weight limits | Load control |
| Cargo security | Not checked | Keep secure supply chain checks in the offer flow, such as regulated agent status and screening | Cargo security |
| Customs and documents | Air waybill status only | Check advance cargo information and customs deadlines by route | Customs compliance |
| Regulator expectations | Not assessed | Confirm whether any system change needs review or notification | Compliance |

## Data and AI governance

| Area | Needed for real use |
|---|---|
| Data protection | Assess forwarder data and staff names under the laws that apply, such as the UAE's data protection law or GDPR |
| Data transfer | Decide which data reaches an AI provider, in which region, and under what terms |
| Retention | Set how long messages, proposals and approvals are kept |
| Access | Single sign-on, roles and no shared accounts |
| Keys | Keep on a server. The prototype's browser-held key approach is not for production |
| Audit | Permanent record of evidence, proposal, edits, approver and time |
| Change control | Re-run evals after any model, prompt or policy change |
| Vendor review | Assess the AI provider, integration partners and sub-processors |

## Required before any live use

These can't be written from outside an airline, so they aren't included here:

- Security assessment and penetration test
- Data protection impact assessment
- AI vendor and third-party review
- Integration and interface specifications
- Support runbook and incident process
- Business case and named sign-offs
