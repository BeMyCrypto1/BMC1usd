# BMC1usd_MB_Refund_Structure_And_Lifecycle.md

## BMC1 BeMyCoverage1 LLC — Money Back (MB) Refund Structure and Policy Lifecycle
**Parent Company:** BMC1 BeMyCrypto1 LLC  
**Insurance Entity:** BMC1 BeMyCoverage1 LLC  
**Internal Utility Token:** BMC1usd  
**Public Tokens:** BMC1, BMC1x, BMC1g  
**Network:** Polygon (PoS)  
**CEO:** Ben Macedo  
**Contact:** bmc1.ceo.macedo@gmail.com  

---

# 1. Purpose of This Document

This file defines:

- the 5-year policy lifecycle
- Money Back (MB) refund eligibility
- refund calculation rules
- ticket and accident handling
- policy renewal and rollover
- payout options
- integration with vaults and liquidity pools

It is the **policy logic brain** for the BMC1usd internal token ecosystem.

---

# 2. Policy Lifecycle Overview

Each insurance policy has a **fixed 5-year period**:

1. Policy purchase date
2. Policy active date
3. MB tracking period (5 years)
4. Event monitoring (tickets, accidents, claims)
5. MB eligibility calculation at maturity
6. Policy renewal or closure

---

# 3. MB Eligibility Groups

Two primary groups:

| Group | MB % | Description |
|-------|------|-------------|
| A | 65% | Good driver, low-risk |
| B | 35% | High-risk / SR22 |

---

# 4. Event Tracking

During the 5-year period, the system tracks:

- Minor tickets (up to 5)
- Severe tickets
- At-fault accidents
- Not-at-fault accidents
- Claims settlements
- Total-loss events
- Fraud flags

---

# 5. Minor Ticket Deduction Rule

- Each minor ticket reduces MB by 2.5%
- Maximum minor tickets allowed = 5
- Beyond 5 → policy canceled
- Example: 3 minor tickets for a 65% MB policy:
Adjusted MB = 65% - (3 * 2.5%) = 57.5%


---

# 6. Severe Ticket or At-Fault Accident Rule

- MB becomes 0%
- Policy cancellation may occur
- Funds in MB vault reallocated to:
  - Claims Vault: 80%
  - Stability Vault: 20%

---

# 7. Not-At-Fault Total Loss Accident Rule

- Policyholder’s vehicle is totaled but not at fault
- MB is paid pro-rata up to date of accident
- Policy ends (closed)
- New policy can be purchased
- 5-year MB cycle restarts as if new policy

---

# 8. Pro-Rata MB Calculation for Total Loss

Let:

- MB% = assigned MB (65% or 35%)
- TimeActive = number of months active before total loss
- TotalTime = 60 months (5 years)

Then:



MB_Payout = MB% * (TimeActive / TotalTime) * PremiumPaid


Example:

- 65% MB, 30 months active, $1,000 premium



MB_Payout = 0.65 * (30/60) * 1000 = 325 BMC1usd


---

# 9. MB Vault Update on Total Loss

- Paid MB is transferred to user wallet
- Remaining MB reserved for canceled policy is released to Claims Vault + Stability Vault (80/20)

---

# 10. Policy Renewal Rule

At maturity:

- User can renew policy
- User can adjust coverage amount (premium changes accordingly)
- New 5-year MB cycle begins
- Historical events do not carry over except:
  - Fraud flags
  - Severe violations (may block renewal)

---

# 11. MB Vault Calculation at End of 5-Year Cycle

For active policy:



MB_Adjusted = Base_MB - MinorTicketDeductions - FraudPenalties


Refund payout = MB_Adjusted * PremiumPaid

---

# 12. Payout Options for MB

1. Withdraw as BMC1usd (stable)
2. Swap/reinvest into BMC1, BMC1x, BMC1g
3. Roll over into new policy

Smart contracts allow all 3 options.

---

# 13. MB Vault Integration with Liquidity Pools

- MB vault reserves are **isolated** from Claims Vault
- Only final MB payout triggers vault transfer
- Deduction reallocations feed LP and Stability Vaults
- Ensures solvency and sustainability

---

# 14. Fraud Handling in MB Lifecycle

- Fraud confirmed → MB = 0%
- Policy canceled
- Funds reallocated to Claims + Stability Vault
- Repeat offenders cannot renew

---

# 15. Event Timing and Oracle Trigger

- MB calculation occurs at policy maturity
- Oracle triggers event confirmation for:
  - ticket validity
  - accident verification
  - claims settlement
  - fraud check

- Only validated events affect MB percentage

---

# 16. Renewal Adjustment Formula

If coverage changes:

- New Premium = P_new
- MB% reset according to group (65% / 35%)
- Any historical deductions do not apply
- Exceptions: fraud or severe violations may restrict renewal

---

# 17. Policy Cancellation Trigger Points

1. More than 5 minor tickets
2. Severe ticket
3. At-fault severe accident
4. Confirmed fraud
5. Non-payment of premium

- All funds from MB vault moved to LP as per rules

---

# 18. Key Lifecycle Flow Diagram (Conceptual)



Policy Start → Event Monitoring → Minor Ticket / Accident / Claim → Oracle Validation → MB Deduction → Policy Maturity → Refund Calculation → MB Payout / Roll Over → Policy Renewal or Closure


---

# 19. Integration with User Wallet

- User wallet tracks:
  - Premium paid
  - MB reserve
  - Event deductions
  - Payout options
  - Rollovers

- All BMC1usd movements automated via smart contract
- Users remain non-custodial
- Wallet can hold other tokens: BMC1, BMC1x, BMC1g

---

# 20. Notes on What MB Lifecycle Is Not

- MB is **not a profit guarantee**
- MB does not protect against fraudulent behavior
- MB vault is **isolated**, cannot be borrowed against
- Oracle validation is mandatory for any refund
- Users cannot bypass lifecycle rules

---

# 21. Closing Statement

The MB Lifecycle design ensures:

- Predictable refund eligibility
- Risk-based deductibles
- Transparent auditability
- Fairness for policyholders
- Solvency for investors

It is the **core logic brain** that interacts with oracles, vaults, and smart contracts.

---
