# BMC1usd_Policy_MB_Logic_And_Refund_Calculation_Model.md

## BMC1 BeMyCoverage1 LLC — Money Back (MB) Logic, Refund Eligibility, and Refund Calculation Architecture
**Parent Company:** BMC1 BeMyCrypto1 LLC  
**Insurance Entity:** BMC1 BeMyCoverage1 LLC  
**Internal Utility Token:** BMC1usd  
**Public Tokens:** BMC1, BMC1x, BMC1g  
**Network:** Polygon (PoS)  
**CEO:** Ben Macedo  
**Contact:** bmc1.ceo.macedo@gmail.com  

---

# 1. Purpose of This Document

This document defines the **core policy logic** of BMC1 BeMyCoverage1 LLC:

- how the Money Back (MB) refund works
- how eligibility is determined
- how penalties are calculated
- how cancellations are enforced
- how early settlement (total loss, payout) is handled
- how the policy maturity refund is calculated

This document is intended to be:

- developer-ready
- investor-readable
- future smart-contract ready

---

# 2. Key Definition: Money Back (MB) System

The MB system is a reward mechanism where drivers who remain safe can receive a percentage refund of their paid premium after the policy maturity.

The refund system is:

- automatic
- formula-based
- enforced by policy smart contract rules
- supported by oracle event validation

---

# 3. Policy Duration and Maturity

Each policy contract is defined as:

### Fixed Duration: 5 years

At the end of 5 years:

- policy matures
- MB refund eligibility is checked
- refund is paid if eligible
- policy closes permanently
- customer may renew with a new policy contract

---

# 4. Driver Groups and Base MB Percentages

BMC1 BeMyCoverage1 LLC uses two base driver categories:

---

## Group A — Good Drivers
- Base MB refund = **65%**
- LP portion = 35%

---

## Group B — High Risk / SR22 Drivers
- Base MB refund = **35%**
- LP portion = 65%

---

# 5. The MB System Must Be Formula-Based

To avoid manual adjustments, the system must be fully formula-driven.

This ensures:

- fairness
- predictability
- auditability
- scalability

---

# 6. Primary MB Eligibility Requirements

To receive the MB refund, the policyholder must:

1. Complete the 5-year policy term OR valid early settlement event
2. Remain active (not canceled)
3. Not have severe violations
4. Remain under minor ticket threshold
5. Have claims status resolved (no open fraud or unpaid claims)

---

# 7. Severe Violations (Automatic MB Forfeiture)

Severe violations result in:

- immediate MB eligibility loss
- possible policy cancellation

Examples of severe violations include:

- DUI / DWI
- reckless driving
- hit-and-run
- fraud
- license suspension
- felony-related driving offenses
- driving uninsured or invalid registration

### Severe violation effect:
- MB refund becomes 0%
- MB vault funds are transferred to LP vaults
- policy may be canceled

---

# 8. Minor Violations (Ticket Deduction Logic)

Minor tickets do not cancel the policy immediately.

Instead:

- each minor ticket reduces the MB refund percentage by **2.5%**
- maximum 5 minor tickets allowed over 5 years

---

# 9. Minor Ticket Threshold Rule

The policy allows:

### Maximum Minor Tickets Allowed = 5

If minor tickets exceed 5:

- policy is canceled
- MB refund is forfeited

---

# 10. Ticket Deduction Formula

Let:

- `MB_base` = base MB percentage (0.65 or 0.35)
- `Tickets_minor` = total minor tickets during the 5-year period
- `Penalty_per_ticket = 0.025`

Then:

MB_final = MB_base - (Tickets_minor × 0.025)


Constraint:

Tickets_minor <= 5


---

# 11. Example Ticket Deduction Table

| Minor Tickets | Deduction | Final MB (Good Driver 65%) | Final MB (SR22 35%) |
|-------------|-----------|-----------------------------|---------------------|
| 0 | 0% | 65% | 35% |
| 1 | 2.5% | 62.5% | 32.5% |
| 2 | 5% | 60% | 30% |
| 3 | 7.5% | 57.5% | 27.5% |
| 4 | 10% | 55% | 25% |
| 5 | 12.5% | 52.5% | 22.5% |
| 6+ | Cancel | 0% | 0% |

---

# 12. Policy Cancellation Rule

Policy cancellation can occur due to:

- more than 5 minor tickets
- any severe violation
- fraud detection
- non-payment (if premium is financed)
- repeated claims abuse
- invalid identity verification (if required)

Cancellation effect:

- MB eligibility becomes 0%
- MB escrow is forfeited into LP vaults
- policy contract closes

---

# 13. MB Refund Calculation Model

Refund is based on the total paid premium.

Let:

- `P_total = total premium paid over the policy term`
- `MB_final = final MB percentage after deductions`

Then:

Refund = P_total × MB_final


---

# 14. Example Refund Calculation (Good Driver)

Assume:

- P_total = 10,000 BMC1usd
- MB_base = 0.65
- Tickets_minor = 2

Then:

MB_final = 0.65 - (2 × 0.025)  
MB_final = 0.65 - 0.05  
MB_final = 0.60

Refund = 10,000 × 0.60  
Refund = 6,000 BMC1usd

---

# 15. Example Refund Calculation (SR22)

Assume:

- P_total = 10,000 BMC1usd
- MB_base = 0.35
- Tickets_minor = 3

Then:

MB_final = 0.35 - (3 × 0.025)  
MB_final = 0.35 - 0.075  
MB_final = 0.275

Refund = 10,000 × 0.275  
Refund = 2,750 BMC1usd

---

# 16. Early Settlement Logic (Important)

The system must support early settlement cases, such as:

- total loss vehicle payout
- early claim closure that ends policy
- policy buyout / termination event
- customer voluntary cancellation (subject to rules)

In these cases:

- policy ends early
- refund is paid proportionally up to that date
- refund timeline resets if customer buys new policy

---

# 17. Early Settlement Pro-Rata Refund Model

Let:

- `P_total = total premium paid`
- `T_elapsed = elapsed time in days`
- `T_total = total policy duration in days (5 years)`
- `MB_final = MB percentage after deductions`

Then:

Refund = P_total × MB_final × (T_elapsed / T_total)


---

# 18. Example Early Settlement (Not-at-Fault Total Loss)

Assume:

- policy duration = 5 years
- policy ended at 3 years
- P_total = 10,000 BMC1usd
- MB_final = 0.65
- T_elapsed / T_total = 3/5 = 0.60

Refund = 10,000 × 0.65 × 0.60  
Refund = 3,900 BMC1usd

Customer receives:

- claim settlement payout
- plus 3,900 BMC1usd refund up to settlement date

Then:

- policy closes permanently
- customer may start a new 5-year policy fresh

---

# 19. Policy Restart Rule (Your Key Innovation)

If the policy ends early due to total loss settlement:

- the driver is not punished if not at fault
- the driver retains good driver classification
- BUT the policy must restart from zero time

This means:

### previous policy years do not carry into the new contract.

Reason:

- prevents overlapping liabilities
- ensures fairness
- ensures actuarial stability

---

# 20. At-Fault Accident Logic

If the driver is at fault:

- policy may remain active depending on claim severity
- MB eligibility may be reduced or eliminated depending on rule tier

Possible outcomes:

- MB remains unchanged (minor at-fault)
- MB reduced (moderate at-fault)
- MB forfeited (severe at-fault)
- policy canceled (fraud, extreme negligence)

These tiers must be clearly defined later in the final policy rulebook.

---

# 21. Not-at-Fault Accident Logic

If the driver is not at fault:

- MB eligibility remains unchanged
- policy remains active unless vehicle is totaled
- refund continues accumulating normally

This is a major customer trust feature.

---

# 22. Claim-Based MB Adjustment (Optional Enhancement)

Future version may include:

- claims severity affecting MB
- claim frequency affecting MB
- deductible payments affecting MB

Example:

- 1 at-fault claim reduces MB by 10%
- 2 at-fault claims reduces MB by 25%
- 3 at-fault claims cancels policy

This is optional but recommended for actuarial stability.

---

# 23. Refund Payment Timing Rule

Refund is paid only when:

- maturity is reached OR early settlement triggers
- all claims are closed
- all ticket events are validated
- no fraud flags exist

This ensures the system cannot be exploited.

---

# 24. Refund Payout Options

At maturity, policyholder can select:

### Option A — Receive USDC/USDT payout
- BMC1usd burned
- stablecoin sent to user wallet

### Option B — Keep BMC1usd inside ecosystem
- user can use it to buy another policy

### Option C — Convert refund into public ecosystem tokens
- swap BMC1usd → BMC1 / BMC1x / BMC1g
- optional bonus rewards if they lock tokens

---

# 25. Refund Bonus Incentive (Optional)

To encourage ecosystem retention, offer:

- +2% MB bonus if refund stays inside system
- +3% MB bonus if refund is staked in BMC1x pool
- +5% MB bonus if refund is locked for 1 year

This is optional but very powerful.

---

# 26. Policy MB Ledger Model (Internal Accounting)

Each policy contract must track:

- total premium paid
- MB base %
- MB final %
- ticket count
- severe violation flag
- cancellation flag
- claim history
- start date
- maturity date
- settlement date (if early)

This becomes the "policy brain".

---

# 27. Policy MB Status State Machine

Each policy can exist in these states:

| State | Meaning |
|------|---------|
| ACTIVE | policy is running |
| UNDER_REVIEW | oracle flagged event pending |
| CLAIM_ACTIVE | claim open |
| CANCELLED | policy terminated, MB forfeited |
| SETTLED_EARLY | ended due to settlement |
| MATURED | 5 years complete |
| PAID_OUT | refund executed |
| CLOSED | contract fully closed |

This ensures clean lifecycle logic.

---

# 28. Oracle Event Input Requirement

The MB system relies on validated events, including:

- ticket events
- accident events
- fault determination
- claim settlement completion

Oracles will signal these events into the policy contract.

This is discussed further in a dedicated oracle file.

---

# 29. MB Fraud Prevention Mechanism

The contract must block payout if:

- fraud flag is active
- event data is missing
- dispute is unresolved

This ensures integrity.

---

# 30. Investor Confidence Model (Why This Is Attractive)

The MB system is attractive because:

- refund is not arbitrary
- refund is conditional and earned
- penalties strengthen liquidity reserves
- high-risk drivers subsidize sustainability
- contract logic is predictable and auditable

This makes the system more trustworthy than traditional insurers.

---

# 31. Final MB System Summary

### Base MB Rates
- Good Driver = 65%
- SR22/High Risk = 35%

### Penalties
- Minor tickets reduce MB by 2.5% each
- Maximum 5 minor tickets
- Severe violations cancel MB completely

### Refund Timing
- paid at 5-year maturity OR early settlement event
- requires closed claims and validated oracle data

### Early Settlement
- refund is proportional to elapsed time
- policy resets if new policy is purchased

---

# 32. Closing Statement

The Money Back (MB) architecture is the heart of the BMC1 BeMyCoverage1 LLC innovation.

It provides:

- real-world incentive for safe driving
- predictable sustainability for the company
- strong liquidity protection through forfeiture rules
- automated enforcement through smart contract logic

This is the mechanism that differentiates BMC1 BeMyCoverage1 LLC from all traditional insurance competitors.

---
