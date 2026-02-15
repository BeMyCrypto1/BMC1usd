# BMC1usd_Vault_And_Liquidity_Foundation_Formula_Model.md

## BMC1 BeMyCoverage1 LLC — Vault Architecture, Liquidity Foundation, MB Pools, and Sustainability Formulas
**Parent Company:** BMC1 BeMyCrypto1 LLC  
**Insurance Entity:** BMC1 BeMyCoverage1 LLC  
**Internal Utility Token:** BMC1usd  
**Public Tokens:** BMC1, BMC1x, BMC1g  
**Network:** Polygon (PoS)  
**CEO:** Ben Macedo  
**Contact:** bmc1.ceo.macedo@gmail.com  

---

# 1. Purpose of This Document

This document defines the **vault and liquidity pool structure** of BMC1 BeMyCoverage1 LLC.

It explains exactly:

- where policy premium money goes
- how refunds (Money Back / MB) are reserved
- how accident settlements are funded
- how sustainability funding works
- how the LP remains solvent over time
- formulas for tracking all flows transparently

This is the financial backbone of the BMC1 blockchain insurance ecosystem.

---

# 2. Core Problem Being Solved

Traditional insurance keeps premiums and pays claims later.

BMC1 insurance must instead:

- hold funds transparently in vaults
- allocate refund eligibility up front
- remain solvent for accident payouts
- protect liquidity for 5 years
- allow predictable MB calculations

---

# 3. High-Level Vault System Overview

BMC1 BeMyCoverage1 LLC uses 4 major vault categories:

---

## Vault 1 — Policy Reserve Vault (MB Vault)
Stores funds reserved for future Money Back refunds.

This vault represents customer "earned refund value".

---

## Vault 2 — Claims Liquidity Vault (LP Claims Vault)
Stores funds for:

- accident settlements
- repair payouts
- towing
- rental coverage
- medical coverage (if applicable)

This is the core accident liquidity pool.

---

## Vault 3 — Operations Vault (Sustainability Vault)
Stores funds for:

- employee salaries
- infrastructure costs
- oracle expenses
- legal compliance
- marketing
- investor relations
- customer support
- long-term ecosystem growth

---

## Vault 4 — Stability Vault (Emergency + Buffer Vault)
Stores emergency reserves for:

- black swan accident years
- extreme claim spikes
- catastrophic events
- regulatory reserve requirements

This vault increases investor confidence.

---

# 4. Why Multiple Vaults Are Mandatory

If all premiums go into one pool, then:

- refunds become unstable
- claims can drain refund money
- company cannot budget operations
- system becomes fragile

Vault separation creates:

- transparency
- accountability
- risk containment
- audit readiness

---

# 5. Premium Flow Entry Logic

Every policy premium payment enters the system as:

- USDC or USDT deposit
- converted into BMC1usd internal settlement units
- then distributed into vaults based on policy type

---

# 6. Policy Group Categories

There are two primary policy groups:

---

## Group A — Good Driver Plan
- Money Back (MB): **65%**
- Liquidity allocation: **35%**

---

## Group B — High Risk / SR22 Plan
- Money Back (MB): **35%**
- Liquidity allocation: **65%**

---

# 7. The Key Question: Where Does the Remaining Percentage Go?

This is the most important vault question.

Example:

- Group A pays 1000 BMC1usd
- MB reserve = 650 BMC1usd
- Remaining 350 BMC1usd must cover:
  - claims
  - operations
  - stability reserves

Same for Group B:

- MB reserve = 350 BMC1usd
- Remaining 650 BMC1usd funds everything else

Therefore, the remaining percentage must be subdivided.

---

# 8. Vault Allocation Formula (Recommended)

To avoid confusion, BMC1 must define a **standard split** inside the non-MB portion.

---

## Group A Split (Good Driver)

Let:

- Premium = P
- MB% = 65%
- NonMB% = 35%

Then:

- MB Vault = 65% of P
- Remaining 35% of P is distributed into:

| Allocation | % of Premium (P) | Purpose |
|----------|------------------|---------|
| Claims Vault | 20% | accident settlements |
| Operations Vault | 10% | salaries + costs |
| Stability Vault | 5% | emergency reserve |

Total = 65% + 20% + 10% + 5% = 100%

---


### Group A Formula

MB_Vault_A = P * 0.65
Claims_Vault_A = P * 0.20
Ops_Vault_A = P * 0.10
Stability_Vault_A = P * 0.05

---

## Group B Split (SR22 / High Risk)

Let:

- Premium = P
- MB% = 35%
- NonMB% = 65%

Then:

| Allocation | % of Premium (P) | Purpose |
|----------|------------------|---------|
| MB Vault | 35% | refund reserve |
| Claims Vault | 45% | accident settlements |
| Operations Vault | 15% | high admin cost |
| Stability Vault | 5% | emergency reserve |

Total = 35% + 45% + 15% + 5% = 100%

---

### Group B Formula
MB_Vault_B = P * 0.35
Claims_Vault_B = P * 0.45
Ops_Vault_B = P * 0.15
Stability_Vault_B = P * 0.05

---

# 9. Why Claims Vault Must Be Higher for SR22 Group

SR22 drivers are statistically higher risk.

Therefore:

- claim probability is higher
- claim severity is higher
- operational cost is higher

This justifies why SR22 contributes more liquidity.

---

# 10. Ticket Deduction Effects on MB Vault

Minor ticket penalties do NOT remove money instantly.

Instead:

- MB refund eligibility decreases
- MB reserved funds are reallocated at maturity

This is a key advantage of the system.

---

# 11. Minor Ticket Deduction Rule (2.5%)

Each confirmed minor ticket reduces MB percentage by 2.5%.

Max minor tickets allowed = 5

---

# 12. MB Percentage After Tickets Formula

Let:

- MB% = base MB percentage (65% or 35%)
- TicketCount = number of minor tickets confirmed
- TicketPenalty = 2.5% each

Then:


---

# 9. Why Claims Vault Must Be Higher for SR22 Group

SR22 drivers are statistically higher risk.

Therefore:

- claim probability is higher
- claim severity is higher
- operational cost is higher

This justifies why SR22 contributes more liquidity.

---

# 10. Ticket Deduction Effects on MB Vault

Minor ticket penalties do NOT remove money instantly.

Instead:

- MB refund eligibility decreases
- MB reserved funds are reallocated at maturity

This is a key advantage of the system.

---

# 11. Minor Ticket Deduction Rule (2.5%)

Each confirmed minor ticket reduces MB percentage by 2.5%.

Max minor tickets allowed = 5

---

# 12. MB Percentage After Tickets Formula

Let:

- MB% = base MB percentage (65% or 35%)
- TicketCount = number of minor tickets confirmed
- TicketPenalty = 2.5% each

Then:

MB_Adjusted = MB% - (TicketCount * 2.5%)


Constraints:

- TicketCount must be ≤ 5
- If TicketCount > 5 → policy cancellation

---

# 13. Example: Group A with 5 Minor Tickets

Base MB = 65%

TicketCount = 5

Penalty = 12.5%

So:


Constraints:

- TicketCount must be ≤ 5
- If TicketCount > 5 → policy cancellation

---

# 13. Example: Group A with 5 Minor Tickets

Base MB = 65%

TicketCount = 5

Penalty = 12.5%

So:
MB_Adjusted = 65% - 12.5% = 52.5%

Meaning:

- refund is 52.5% instead of 65%
- the remaining 12.5% becomes additional LP liquidity for the company

---

# 14. Where Does the Lost MB Refund Go?

When MB is reduced, that amount should be reallocated.

Recommended rule:

### Lost MB % goes into Claims Vault + Stability Vault.

Example:

- 70% of lost MB → Claims Vault
- 30% of lost MB → Stability Vault

This strengthens the pool and protects solvency.

---

# 15. Lost MB Allocation Formula

Let:

- MB_Lost = (Base_MB - Adjusted_MB) * P

Then:

Claims_Bonus = MB_Lost * 0.70
Stability_Bonus = MB_Lost * 0.30


This makes the system more sustainable and risk-resistant.

---

# 16. Severe Ticket or At-Fault Accident Rule

If severe event occurs:

- MB becomes 0%
- policy may be canceled depending on severity

Then:

### The entire MB vault portion is transferred into Claims Vault and Stability Vault.

Suggested split:

- 80% to Claims Vault
- 20% to Stability Vault

---

# 17. Severe Event MB Forfeiture Formula

Let:

- MB_Forfeited = P * MB%

Then:



Claims_Bonus = MB_Forfeited * 0.80
Stability_Bonus = MB_Forfeited * 0.20


---

# 18. Policy Cancellation Liquidity Flow

If policy is canceled due to violations:

- MB refund becomes 0%
- unused premium funds become company liquidity

Recommended split:

| Vault | Allocation |
|------|------------|
| Claims Vault | 70% |
| Operations Vault | 20% |
| Stability Vault | 10% |

This supports business sustainability and claim solvency.

---

# 19. Policy Maturity Settlement Model (5 Years)

At the end of 5 years, the contract checks:

- accident record
- fault record
- ticket count
- fraud status

If eligible:

- MB refund is released to user wallet

If not eligible:

- MB vault funds are reallocated to LP reserves.

---

# 20. Refund Payment Mechanics

Refund is paid using:

- BMC1usd internal balance transfer
- backed by USDC/USDT reserves held in custody vaults

Refund can be:

- withdrawn as USDC/USDT
- reinvested into BMC1/BMC1x/BMC1g
- rolled into new 5-year policy

---

# 21. The "Liquidity Foundation" Concept

Liquidity Foundation = total of:

- Claims Vault
- Stability Vault
- Conversion Reserves
- Locked Trust Vaults

This foundation is what gives investors confidence.

---

# 22. Liquidity Foundation Total Formula

Let:

- CV = Claims Vault
- SV = Stability Vault
- TR = Trust Reserve Vault
- CR = Conversion Reserve (annual swaps)
- RV = Refund Vault (MB vault)

Then:



LiquidityFoundation = CV + SV + TR + CR


Refund Vault is excluded because it is considered "customer reserved".

However, in total balance sheet:



TotalSystemAssets = CV + SV + TR + CR + RV + OpsVault


---

# 23. Why Refund Vault Should Not Be Used for Claims

Refund vault is legally and ethically a customer reserve.

If it is used to pay claims:

- refunds become unreliable
- the system becomes fraudulent
- investors will distrust the company

Therefore:

### Refund vault must be isolated.

---

# 24. Annual Conversion Strategy (Public Tokens → Stable Reserves)

The ecosystem includes:

- BMC1
- BMC1x
- BMC1g

Their price fluctuates.

BMC1 uses them as "growth assets", not settlement assets.

Therefore, every year:

- a fixed amount is swapped into USDC/USDT
- deposited into Stability Vault + Trust Vault

This reduces volatility risk.

---

# 25. Annual Conversion Formula

Let:

- YearlySwapAmount = fixed amount of token units OR % of treasury
- TokenPrice = oracle price feed
- StableReceived = output stablecoins

Then:



StableReceived = YearlySwapAmount * TokenPrice


The system then allocates:

- 60% into Stability Vault
- 40% into Trust Reserve Vault

---

# 26. Conversion Vault Distribution Rule

Suggested distribution:

| Destination | % |
|------------|---|
| Stability Vault | 60% |
| Trust Reserve Vault | 40% |

This ensures the company can survive market crashes.

---

# 27. Trust Reserve Vault Concept

The Trust Reserve Vault is designed like a "corporate irrevocable trust model":

- locked liquidity
- multi-sig controlled
- timelock enforced
- cannot be drained instantly

This vault is meant to signal:

- legitimacy
- long-term solvency
- investor trust
- long-term operational survival

---

# 28. Trust Reserve Vault Lock Rule

Recommended lock:

- 5 years rolling lock cycles
- new deposits extend future maturity schedule

This creates a perpetual reserve structure.

---

# 29. Trust Reserve Vault Release Rules

Trust vault funds can only be released when:

- claims exceed a defined threshold
- catastrophic event declared
- investor governance vote approved
- regulatory solvency requirement

This prevents reckless spending.

---

# 30. Emergency Trigger Formula

Let:

- ClaimsYear = total claims paid in 12 months
- PremiumYear = total premiums received in 12 months

If:



ClaimsYear / PremiumYear > 0.85


Then emergency mode triggers:

- partial trust vault release allowed

This is the "black swan protection".

---

# 31. Operating Expense Sustainability Formula

Operations Vault must be stable.

Recommended rule:

- Ops vault should maintain at least 18 months of runway

Let:

- MonthlyCost = estimated company expenses
- OpsVaultBalance = current balance

Then:



RunwayMonths = OpsVaultBalance / MonthlyCost


If RunwayMonths < 18:

- conversion system increases stable allocation into Ops Vault

---

# 32. Vault Transparency Reporting (Investor Ready)

Every quarter, BMC1 should publish:

- total premium collected
- total MB reserved
- total claims paid
- vault balances
- trust reserve locked amounts
- liquidity ratio

This is critical for credibility.

---

# 33. Liquidity Health Ratios

### Claims Coverage Ratio


ClaimsCoverageRatio = ClaimsVault / ExpectedClaims


### Refund Coverage Ratio


RefundCoverageRatio = RefundVault / OutstandingRefundLiability


### Stability Ratio


StabilityRatio = StabilityVault / TotalPremiumsCollected


---

# 34. Recommended Minimum Ratios

| Ratio | Minimum Recommended |
|------|----------------------|
| Refund Coverage Ratio | 1.00 |
| Claims Coverage Ratio | 1.20 |
| Stability Ratio | 0.10 |

This means:

- refunds always backed
- claims over-collateralized
- stability reserves exist

---

# 35. Key Vault Summary Table

| Vault Name | Function | Risk Protection |
|-----------|----------|----------------|
| Refund Vault (MB) | refunds to customers | protects customer trust |
| Claims Vault | accident settlements | prevents insolvency |
| Ops Vault | payroll + growth | ensures sustainability |
| Stability Vault | emergency reserves | black swan protection |
| Trust Reserve Vault | locked reserves | investor confidence |

---

# 36. Why This Model Works for Investors

This model provides:

- predictable refund obligations
- visible solvency structure
- locked reserve credibility
- risk-adjusted allocation
- automatic enforcement via smart contracts

It makes BMC1 BeMyCoverage1 LLC appear:

- legitimate
- scalable
- sustainable
- auditable

---

# 37. Closing Notes

The MB percentage (65% or 35%) does not mean the company has no revenue.

The company revenue comes from:

- claims margin efficiency
- unused liquidity vault growth
- ticket forfeiture reallocation
- canceled policies liquidity capture
- annual token conversion reserves
- operational optimization

This makes BMC1 a hybrid of:

- insurance company
- DeFi treasury management
- blockchain risk pool protocol

---

