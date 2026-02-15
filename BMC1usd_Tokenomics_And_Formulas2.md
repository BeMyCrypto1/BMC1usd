# BMC1usd_Tokenomics_And_Formulas.md

## BMC1 BeMyCoverage1 LLC — Tokenomics & Core Formulas (BMC1usd Internal Utility Token)

  **Parent Company:**           BMC1 BeMyCrypto1 LLC  
  **Insurance Entity:**         BMC1 BeMyCoverage1 LLC  (target launch date Jan 2027)
  **Internal Utility Token:**   BMC1usd  
  **Public Utility Tokens:**    BMC1, BMC1x, BMC1g  
  **Network:**                  Polygon (PoS)  
  **CEO:**                      Ben Macedo  
  **Contact:**                  bmc1.ceo.macedo@bemycrypto1.online

---

# 1. Purpose of This Document

This document defines the **tokenomics logic**, **formulas**, and **economic behavior** 
of the BMC1 BeMyCoverage1 LLC ecosystem, including:

  - How premiums are distributed
  - How Money-Back (MB) refund obligations are calculated
  - How ticket deductions reduce MB eligibility
  - How policy cancellation affects the liquidity pool
  - How yearly conversions of public tokens support reserves
  - How all vaults interact to maintain solvency

This is a **non-code blueprint** intended to guide the final Solidity smart contract implementation.

---

# 2. BMC1usd Token Definition (Internal Utility Stable Token)

### BMC1usd is:

  ✅ Internal settlement token used inside the Car Insurance BeMyCoverage1 ecosystem  
  ✅ 1:1 accounting unit to USD value (target peg to either USDC or USDT)  
  ✅ Used for premium payments, claims settlements, refunds, and vault accounting  
  ✅ Not designed to be publicly traded or used as an investment token  

### BMC1usd is NOT:

❌ A public stablecoin competing with USDC/USDT  
❌ A free-floating token open to speculation  
❌ A replacement for regulated fiat banking systems  
❌ A token meant to be listed on exchanges  

---

# 3. Core Policy Groups (Two-Class Model)

The system defines two primary risk categories:

## Group A: Good Driver Plan (Low Risk)
  - Money-Back Refund Percentage: **65%**
  - Liquidity Pool Portion: **35%**
  - Goal: reward safe drivers and build trust

## Group B: High Risk / SR22 Plan
  - Money-Back Refund Percentage: **35%**
  - Liquidity Pool Portion: **65%**
  - Goal: provide access to insurance while strengthening claims reserves

---

# 4. Base Premium Allocation Formula

Let:

      - `P` = Total premium paid for a policy (in BMC1usd)
      - `MB%` = Money-Back percentage based on plan type
      - `LP%` = Liquidity Pool percentage (remaining amount)
      
### Base Identity:
    Where:
      MB = P × MB%
      LP = P × (1 - MB%)
---

# 5. Group A (Good Driver) Allocation Formula

### Group A Parameters:
    MB% = 0.65
    LP% = 0.35


### Formula:
    MB_A = P × 0.65
    LP_A = P × 0.35

---

# 6. Group B (High Risk / SR22) Allocation Formula

### Group B Parameters:
    MB% = 0.35
    LP% = 0.65

### Formula:
    MB_B = P × 0.35
    LP_B = P × 0.65

---

# 7. Liquidity Pool (LP) Sub-Vault Splitting

The Liquidity Pool portion is divided into sub-vaults.

## Group A LP Sub-Distribution (Recommended)

Let:

    - `LP_A` = Liquidity portion for Group A
    - `C` = Claims Vault
    - `O` = Operations Vault
    - `R` = Reserve Vault

Recommended split:

    | Vault              | % of LP_A |
    |--------------------|-----------|
    | Claims Vault       |     60%   |
    | Operations Vault   |     25%   |
    | Reserve Vault      |     15%   |

### Formulas:
    C_A = LP_A × 0.60
    O_A = LP_A × 0.25
    R_A = LP_A × 0.15


---

## Group B LP Sub-Distribution (Recommended)

Recommended split:

    | Vault             | % of LP_B |
    |-------------------|-----------|
    | Claims Vault      | 70%       |
    | Operations Vault  | 20%       |
    | Reserve Vault     | 10%       |

### Formulas:

    C_B = LP_B × 0.70
    O_B = LP_B × 0.20
    R_B = LP_B × 0.10


---

# 8. Ticket Deduction System (Non-Severe Tickets)

### Goal:
Allow drivers to receive minor tickets but still earn a refund, with penalties.

---

## Ticket Deduction Rules

  - Each non-severe ticket reduces MB% by **2.5%**
  - Maximum allowed tickets = **5**
  - If tickets exceed 5 → policy is canceled
  - Deduction applies at final maturity payout

---

## Ticket Deduction Formula

    Let:
    - `T` = number of non-severe tickets
    - `d` = deduction per ticket = 0.025

### Adjusted MB%:

    MB%_adjusted = MB%_base - (T × d)

---
## Group A Example (Good Driver)

Base MB% = 0.65

### Example: 3 tickets
    MB%_adjusted = 0.65 - (3 × 0.025)
    MB%_adjusted = 0.65 - 0.075
    MB%_adjusted = 0.575


So refund becomes 57.5% instead of 65%.
---
## Group A Example: 5 tickets
    MB%_adjusted = 0.65 - (5 × 0.025)
    MB%_adjusted = 0.65 - 0.125
    MB%_adjusted = 0.525

So refund becomes 52.5%.
---
## Group B Example (SR22)

    Base MB% = 0.35

### Example: 5 tickets
    MB%_adjusted = 0.35 - 0.125
    MB%_adjusted = 0.225
Refund becomes 22.5%.

---

# 9. Ticket Cancellation Trigger

### Cancellation Rule:
    If: 
      T > 5
    Then:
      - Policy is canceled
      - MB vault is forfeited
      - Funds move into LP vault structure

---

# 10. Severe Violation Rules

Severe violations immediately cancel eligibility.

Examples:
  - DUI
  - reckless driving
  - felony hit-and-run
  - driving without insurance
  - driving with suspended license
  - major fraud events

### Severe Violation Result:
  - Policy MB eligibility becomes **0%**
  - Entire MB reserve transfers to LP pool
  - Policy can be terminated immediately

---

# 11. Fault vs Non-Fault Accident Logic

  This is critical to fairness.

## Accident Not Driver Fault (Verified Event)

If accident occurs but driver is NOT at fault:

  - MB eligibility remains unchanged
  - Driver remains in same plan group
  - Vehicle payout is processed
  - Policy may end early if vehicle is totaled

---

# 12. Total Loss / Policy Closure Event

If vehicle is totaled:

  - policy ends early
  - claim is paid
  - MB refund is paid **proportionally or prorated until that date**
  - driver can open a new policy without penalty

---

## Proportional MB Refund Formula

    Let:
        - `D_total` = total policy duration in days (5 years)
        - `D_used` = number of days active before closure
        - `MB_total` = total MB reserve locked
    
    Then:
        MB_refund = MB_total × (D_used / D_total)


---

# 13. Policy Maturity at 5 Years (Standard Outcome)

If driver completes the 5-year period without disqualifying events:

    - the MB refund is paid according to adjusted MB%
    - the LP remains as company sustainability and claims buffer

---

# 14. Policy Renewal Logic

At maturity:

  - policy ends completely
  - renewal is treated as a new policy
  - MB% group is reassigned based on latest driver status

This ensures:

  - clean accounting
  - no infinite policy loops
  - clear NFT lifecycle

---

# 15. BMC1usd Vault Accounting Model

The ecosystem uses multiple vaults:

## Mandatory Vaults
  - Refund Vault (Money-Back locked funds)
  - Claims Vault (accident payouts)
  - Operations Vault (company sustainability)
  - Reserve Vault (long-term solvency)
  - Conversion Vault (yearly swap support)

---

# 16. Public Token Support Model (BMC1 / BMC1x / BMC1g)

The public-facing tokens are:

  - **BMC1** (main utility)
  - **BMC1x** (silver pegged concept)
  - **BMC1g** (gold pegged concept)

They are **not stable**, prone to -pump&dump- behaviors from -whales-, 
so always be on your guard to check daily their prices and move your money wisely.

Their role is:

  - community participation
  - liquidity foundation support
  - credibility reinforcement
  - long-term treasury growth

---

# 17. Yearly Conversion System (Stability Support Engine)

### Purpose:
  Because BMC1, BMC1x, and BMC1g can fluctuate, the ecosystem performs periodic 
  conversion into stable reserves.

---

## Yearly Conversion Rule

Once per year:

  - an approved portion of the token treasury is swapped
  - converted into USDC/USDT
  - optionally minted into BMC1usd accounting units

This protects the ecosystem from volatility.

---

## Conversion Formula

    Let:
      - `X` = amount of BMC1/BMC1x/BMC1g converted
      - `V_market` = market value at time of swap
      - `S` = stablecoin received (USDC/USDT)
    Then:
      S = X × V_market


Stable reserves increase regardless of token price movement.

---

# 18. Trust-Style Locked Reserve Vault

The ecosystem may create a locked reserve structure:

  - funds locked in multi-sig vault
  - time-based release schedule (5 years)
  - visible on-chain proof-of-reserves

This functions similarly to real-world “trust fund mechanics”.

---

# 19. Sustainability Guarantee Logic

This model creates sustainability by design:

### Because:

  - Good drivers contribute less LP (35%)
  - High risk drivers contribute more LP (65%)
  - severe violations and cancellations transfer MB reserve into LP
  - minor ticket penalties increase LP gradually
  - yearly conversion stabilizes long-term reserves

---

# 20. Summary Formula Table (Quick Reference)

    | Policy Type                 | Base MB% | Base LP% |
    |-----------------------------|----------|----------|
    | Group A (Good Driver)       | 65%      | 35%      |
    | Group B (SR22 / High Risk)  | 35%      | 65%      |

---

# 21. Key Economic Guarantees

This system guarantees:

  ✅ Predictable money-back model  
  ✅ Automatic penalties for risky behavior  
  ✅ No human intervention required for enforcement  
  ✅ Strong liquidity reinforcement from high-risk pool  
  ✅ Fair handling of non-fault accidents  
  ✅ Solvency reinforcement via yearly stable conversions  
  ✅ Full auditability via on-chain vault tracking  

---

# 22. Notes for Future Smart Contract Implementation

When converted into Solidity, the contract design should include:

  - Policy NFT per driver policy
  - Vault contract modules
  - AccessControl roles for minting/burning BMC1usd
  - Oracle event triggers (tickets, accidents, claims)
  - Timelock for sensitive actions
  - Multisig governance for treasury conversion

---

# 23. What This Tokenomics Model Avoids (Important)

This model is intentionally designed to avoid:

  - unstable algorithmic peg failures
  - public stablecoin regulatory exposure
  - speculative trading risk of BMC1usd
  - dependency on banks for day-to-day policy settlement
  - human corruption in claim eligibility decisions

---

# 24. Final Statement

  BMC1usd is designed as a **non-public, internal, permissioned utility settlement token**
  supporting the BMC1 BeMyCoverage1 LLC insurance economy, spected to be launched Jan 2027.
  while the public ecosystem tokens  (BMC1, BMC1x, BMC1g) act as long-term treasury reinforcement, 
  liquidity credibility assets,   and open all investors participations tools.

This combination creates a sustainable, blockchain-native car insurance ecosystem.

---
  



