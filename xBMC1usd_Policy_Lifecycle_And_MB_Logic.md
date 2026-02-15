# BMC1usd_Policy_Lifecycle_And_MB_Logic.md

## BMC1 BeMyCoverage1 LLC — Policy Lifecycle, Money-Back Logic, and Eligibility Enforcement

**Parent Company:** BMC1 BeMyCrypto1 LLC  
**Insurance Entity:** BMC1 BeMyCoverage1 LLC  
**Internal Utility Token:** BMC1usd  
**Public Utility Tokens:** BMC1, BMC1x, BMC1g  
**Network:** Polygon (PoS)  
**CEO:** Ben Macedo  
**Contact:** bmc1.ceo.macedo@bemycrypto1.online  

---

# 1. Purpose of This Document

This document defines the **policy lifecycle architecture** for BMC1 BeMyCoverage1 LLC, including:

- How a policy begins, exists, and ends on-chain
- How Money-Back (MB) refunds are calculated and reserved
- How ticket penalties reduce MB eligibility
- How accidents and claims affect policy state
- How policy cancellation triggers forfeiture logic
- How policy maturity (5 years) is finalized
- How renewal creates a new lifecycle

This is a **no-code blueprint** for future Solidity smart contract implementation.

---

# 2. Core Design Philosophy

BMC1 BeMyCoverage1 LLC is built on the idea that:

- Insurance can be automated through **smart contracts**
- Policy agreements can be represented as **NFT-based policy objects**
- Refund promises can be enforced using **vault reserves**
- Driver incentives can be enforced without human intervention

The result is a system that behaves like a **Self-DAO Insurance Machine**:

- Transparent
- Auditable
- Rule-based
- Predictable
- Resistant to manipulation

---

# 3. Key Definitions

## Policy Period (PP)
A single policy lasts:

- **5 years maximum**
- measured in days/seconds on-chain

This 5-year term is called the **Policy Period (PP)**.

---

## Money-Back (MB)
The MB refund is a reward incentive for drivers who remain eligible.

There are two MB plans:

- **65% MB** (Good Drivers)
- **35% MB** (High Risk / SR22 Drivers)

---

## Policy State
A policy exists in one of these states:

- `PENDING`
- `ACTIVE`
- `SUSPENDED`
- `CLAIM_OPEN`
- `CANCELED`
- `TOTAL_LOSS_CLOSED`
- `MATURED`
- `EXPIRED`
- `REFUNDED`
- `RENEWED` (new policy begins)

---

# 4. Policy Creation Flow (Start of Lifecycle)

## Step 1: Customer Applies
Customer enters the BMC1 BeMyCoverage1 ecosystem via:

- website / dApp interface
- mobile app (future)
- agent portal (optional)

Customer selects:

- vehicle
- driver identity
- coverage tier
- deductible
- risk group classification
- policy premium amount

---

## Step 2: Customer Selects Policy Type

Customer selects:

### Policy Type A — Good Driver Plan
- 65% MB after 5 years clean driving

### Policy Type B — SR22 / High Risk Plan
- 35% MB after 5 years clean driving

---

## Step 3: Premium Payment

Customer pays premium using:

- BMC1usd (preferred)
- or USDC/USDT (converted internally into BMC1usd accounting)

Once payment is received:

- Policy NFT is minted
- Policy becomes `ACTIVE`

---

# 5. Policy NFT Architecture (Core Insurance Object)

Each policy is represented by a unique NFT:

### Policy NFT contains:

- policy ID
- wallet owner address
- vehicle VIN/identifier (hashed)
- coverage tier
- deductible
- plan type (A or B)
- start timestamp
- maturity timestamp
- MB base percentage
- ticket counter
- severe violation flag
- at-fault accident counter
- not-at-fault accident counter
- MB eligibility score
- refund vault allocation
- claim vault allocation
- current status

The NFT becomes the **driver’s proof-of-insurance contract**.

---

# 6. Premium Allocation at Policy Start

At the moment premium is paid, the contract allocates premium into vaults.

Let:

- `P` = premium amount paid

---

## Plan A (65% MB) Allocation
MB_reserve = P × 0.65
LP_portion = P × 0.35


- MB_reserve goes into Refund Vault (locked)
- LP_portion goes into LP vault distribution (claims/ops/reserve)

---

## Plan B (35% MB) Allocation



MB_reserve = P × 0.35
LP_portion = P × 0.65


- MB_reserve locked
- LP_portion distributed into liquidity vaults

---

# 7. Ticket Enforcement Logic (Non-Severe Tickets)

## Ticket Rules Summary

- Each non-severe ticket reduces MB by 2.5%
- Maximum 5 tickets allowed during 5-year PP
- Ticket #6 cancels the policy
- Ticket penalties are cumulative

---

## Ticket Recording Logic

Whenever a ticket is detected and verified:

- Ticket counter increments
- Policy state remains `ACTIVE` unless threshold exceeded
- MB eligibility score is reduced

---

## Ticket Deduction Formula

Let:

- `T` = number of tickets
- `d` = 0.025 (2.5% per ticket)
- `MB_base` = 0.65 or 0.35

Then:



MB_adjusted = MB_base - (T × d)


---

## Ticket Threshold Cancellation Rule

If:



T > 5


Then:

- policy becomes `CANCELED`
- MB reserve is forfeited
- MB refund becomes 0

---

# 8. Severe Violation Enforcement Logic

A severe violation is any major driving or legal event that disqualifies the driver.

Examples:

- DUI
- reckless driving
- suspended license driving
- felony hit-and-run
- insurance fraud
- intentional collision

---

## Severe Violation Rule

If a severe violation is verified:

- policy becomes `CANCELED`
- MB reserve becomes forfeited immediately
- all future refund rights become zero

---

# 9. Accident Handling Logic

Accidents must be categorized into:

- **At-Fault Accident**
- **Not-At-Fault Accident**
- **Total Loss Accident**
- **Minor Claim (repairable)**

This is one of the most important fairness mechanics in the entire system.

---

# 10. Not-At-Fault Accident Logic (Driver Protected)

If driver is verified as NOT at fault:

- MB eligibility remains unchanged
- policy continues as normal
- claim is paid from Claims Vault

This is a key incentive: good drivers are not punished for others’ mistakes.

---

# 11. At-Fault Accident Logic (Eligibility Loss)

If driver is verified as at fault:

- policy is flagged as disqualified
- MB eligibility becomes 0
- policy may continue for coverage depending on rules
- driver loses MB reserve at maturity (or sooner if canceled)

This prevents abusive behavior while still allowing coverage obligations to be honored.

---

# 12. Claim Payment Logic

Claims are paid from:

- Claims Vault (primary)
- Reserve Vault (secondary backup)
- emergency liquidity (future optional)

Claims can include:

- repairs
- medical coverage
- third-party liability payouts
- towing and rental coverage
- total loss vehicle replacement payout

---

# 13. Total Loss Closure Logic (Policy Ends Early)

If vehicle is declared totaled:

- policy ends early
- claim payout is processed
- MB refund is paid proportionally (if eligible)

---

## Total Loss Refund Formula (Proportional MB Refund)

Let:

- `D_total` = total days in 5 years
- `D_used` = days elapsed until total loss
- `MB_locked` = MB reserve vault amount

Then:



MB_payout = MB_locked × (D_used / D_total)


The remaining MB_locked is released into the company liquidity pool.

---

# 14. Restart Logic After Total Loss

If driver was not at fault:

- driver is allowed to re-enter immediately
- a new policy is created
- the lifecycle restarts as a new contract

This is important because the old policy was closed fairly.

---

# 15. Policy Suspension Logic (Optional Feature)

The policy may allow temporary suspension due to:

- late payment extension window
- documentation verification pending
- fraud investigation
- temporary driving ban

In `SUSPENDED` state:

- claims cannot be paid
- refund clock may pause
- policy cannot be renewed until cleared

This feature is optional but recommended for real-world complexity.

---

# 16. Policy Cancellation Logic (Main Enforcement Engine)

A policy becomes `CANCELED` if any of the following occurs:

### Ticket Overload
- more than 5 tickets

### Severe Violation
- DUI / reckless / fraud / felony event

### At-Fault Accident (if company chooses strict enforcement)
- MB eligibility removed
- cancellation optional depending on rules

### Customer Cancelation (Voluntary Exit)
- customer chooses to end policy early

---

# 17. Cancellation Financial Result (Forfeiture)

When cancellation occurs:

- MB reserve is forfeited
- funds transfer to LP vaults
- policy ends permanently

This is critical for solvency.

---

## Cancellation Transfer Rule

If policy is canceled:



RefundVaultBalance(policy) → ClaimsVault + OperationsVault + ReserveVault


This strengthens the ecosystem for remaining members.

---

# 18. Policy Maturity Logic (5-Year Completion)

A policy matures when:



current_time >= maturity_timestamp


If policy status is still `ACTIVE`, then:

- driver is eligible for MB payout
- payout is calculated using adjusted MB%
- policy state becomes `MATURED`

---

# 19. Final MB Refund Payout Logic

At maturity, MB payout is calculated.

Let:

- `P` = original premium
- `MB_adjusted` = MB% after ticket deductions
- `RefundAmount` = final payout

Then:



RefundAmount = P × MB_adjusted


---

## Example: Good Driver Plan with 2 Tickets



MB_base = 0.65
T = 2
MB_adjusted = 0.65 - (2 × 0.025)
MB_adjusted = 0.60

Refund = P × 0.60


---

# 20. Remaining MB Reserve Handling (If Deductions Occur)

If MB% is reduced, the difference becomes company liquidity.

Example:

- Base MB reserve was locked at 65%
- Final MB adjusted becomes 60%
- The extra 5% is transferred to LP vaults

---

## Excess Refund Reserve Transfer Formula

Let:

- `MB_locked` = base locked amount
- `MB_payout` = adjusted payout

Then:



MB_excess = MB_locked - MB_payout
MB_excess → LP vault distribution


This means:

- the system is always solvent
- deductions strengthen company reserves automatically

---

# 21. Renewal Logic (New Policy Cycle)

After maturity:

- policy is closed permanently
- NFT is marked as matured
- renewal requires a new policy purchase

Renewal creates a brand-new NFT with:

- new start date
- new maturity date
- updated MB eligibility group
- updated pricing and coverage tier

---

# 22. Coverage Upgrade / Downgrade Rules

Coverage changes should not modify the existing policy NFT.

Instead:

- policy must be terminated early
- new policy is created with new premium and new terms

This avoids complex on-chain modifications that can be exploited.

---

# 23. Fraud Detection (System Protection Layer)

Fraud events trigger:

- suspension or cancellation
- MB eligibility loss
- claim denial logic (case dependent)

Fraud indicators may include:

- repeated false claims
- manipulated accident reporting
- fake ticket data injection attempts
- identity mismatch

Fraud triggers are typically enforced through oracle signals + validator review.

---

# 24. Oracle + Validator Event Feed Integration (Conceptual)

The policy logic requires real-world event data such as:

- DMV tickets
- accident reports
- police records
- claim repair invoices
- fault determination

This is achieved by:

- internal company validators
- regulated data feeds
- oracle-style reporting to the chain

The blockchain does not "guess events"; it only responds to verified signals.

---

# 25. Policy Lifecycle Timeline (Visual Summary)

### Standard Success Path

1. Policy created
2. Premium paid
3. MB reserved + LP allocated
4. Policy remains ACTIVE for 5 years
5. Ticket deductions applied if needed
6. Policy matures
7. MB payout executed
8. Policy ends
9. Customer renews if desired

---

### Cancellation Path

1. Policy created
2. Premium paid
3. Ticket overload or severe violation occurs
4. Policy canceled
5. MB reserve forfeited
6. Funds strengthen company LP
7. Policy ends permanently

---

### Total Loss Path

1. Policy created
2. Premium paid
3. Total loss occurs
4. Claim paid
5. Proportional MB paid
6. Policy closes early
7. Customer may restart new policy

---

# 26. Key Guarantees of This Lifecycle Model

This policy logic guarantees:

✅ Automated reward incentives  
✅ Transparent refund logic  
✅ Clear solvency boundaries  
✅ No manual MB manipulation  
✅ Non-fault drivers protected  
✅ Bad behavior punished economically  
✅ Trust-building mechanism for investors and customers  

---

# 27. What This Policy Model Avoids

This design intentionally avoids:

- human bribery decisions
- refund disputes with unclear rules
- hidden premium allocation
- complex refund calculations requiring subjective judgment
- unfair penalties for non-fault accidents

---

# 28. Final Statement

The BMC1 BeMyCoverage1 LLC policy lifecycle is designed as a fully auditable,
rule-based smart contract system where:

- the customer buys a 5-year insurance contract
- the refund obligation is locked at purchase
- the policy enforces behavior through deductions and cancellation
- the ecosystem remains sustainable through liquidity pool reinforcement

This creates a true blockchain-native insurance structure powered by BMC1usd.

---
