# Lab 13 — Portfolio Mandate Defense

## Statement types: Meridian Foundation Reserve

| Statement | Type | Reason |
| --- | --- | --- |
| S1 — Seven-year horizon; annual rebalancing | Hard constraint | It sets the investment time frame and the permitted rebalancing cadence. |
| S2 — CPI + 4% net of costs over rolling five-year periods | Objective | This is the return outcome the reserve is intended to pursue. |
| S3 — $0.75m quarterly payout; 12 months held in cash or daily-liquid government securities | Hard constraint | It specifies a required reserve for known distributions. |
| S4 — 60% global equities / 40% U.S. investment-grade bonds benchmark | Preference | It provides a performance comparison, but does not require tracking it or impose an allocation limit. |
| S5 — Long-only; no borrowing, shorts, or derivatives | Hard constraint | These are direct limits on permitted investment activity. |
| S6 — No single issuer above 8% | Hard constraint | It is a quantitative issuer-concentration limit. |
| S7 — Turnover no more than 25% without committee approval | Hard constraint | Turnover above the limit is not permitted unless the committee approves it. |
| S8 — At least 90% redeemable within five business days | Hard constraint | It is a measurable liquidity minimum. |
| S9 — No calendar-year loss greater than 10%, with no measure or breach rule | Unverifiable promise | It sounds like a limit, but it cannot be tested until the loss measure and consequences of a breach are defined. |
| S10 — No sector, ESG, tax, or home-bias preference; no pilot objective stated | Missing | The mandate does not say what the pilot should optimize. |

## Part V — known-answer verification

`python mandate.py` matched the known-answer table: A passes every checkable rule; B fails the reserve, liquidity, and issuer rules; and C fails the reserve rule. I then changed A's Cash weight to `-2` and global equity index fund weight to `64`; the checker reported a lowest weight of `-2.0 FAIL`, a reserve weight of `10.0 pass`, and no other failure. I restored the original A weights afterward.

## Part E — candidate D

Candidate D is 3% Cash and 97% Global equity index fund, with all other holdings at 0%. It passes every checkable rule in `mandate.py`: weights total 100%, the 3% reserve minimum is met, 100% is redeemable within five business days, and there is no single-company exposure.

The objection holds: a 97% global-equity reserve could reasonably be rejected because it may experience a calendar-year loss greater than 10%, even though it passes every checkable rule. Statement S9 decides the objection, but the CIO must define the loss measure and breach rule before it can be tested.

For a partner's candidate D that carries excessive downside risk while passing the checker, I would cite S9; if it instead exposes the absence of a stated optimization target, I would cite S10.

## Question for the CIO

**Question:** What exactly does “cannot have a calendar-year loss greater than 10%” mean: which return measure applies, and what action or exception follows if the limit is breached?

**Answer that would change my portfolio:** If it is a strict total-return limit with no exceptions, I would reduce global equities and add cash, Treasury bills, and investment-grade bonds to limit downside risk. If it is only a monitoring guideline or permits temporary breaches, I could hold more global equities to pursue CPI + 4%.

## Investment policy statement mapping

An investment policy statement records a client's objectives, constraints, governance, and preferences so that portfolio decisions can be checked against them. Here, S2 is the return objective; S1, S3, and S5–S8 are time-horizon, spending, legal/implementation, concentration, turnover, and liquidity constraints; S4 is the benchmark; S9 is an incomplete risk constraint; and S10 identifies missing preferences and a missing optimization instruction.

## Reflection

A portfolio can pass every coded rule and still be wrong because the checker only tests rules that are precise enough to measure; it cannot judge an undefined downside-risk rule or choose among otherwise permissible portfolios without a stated objective. I was least sure about S4 because a benchmark is useful for evaluation, but it is not itself a portfolio constraint unless the CIO also sets a requirement such as a tracking-error limit or a mandate to track it.
