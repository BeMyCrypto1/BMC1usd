
**Project:** BMC1 BeMyCoverage1 LLC (Car Insurance Ecosystem)  
**Parent Company:** BMC1 BeMyCrypto1 LLC  
**Internal Settlement Token:** BMC1usd (Internal Use Only)  
**Public Tokens:** BMC1, BMC1x, BMC1g  
**CEO:** Ben Macedo  
**Contact:** bmc1.ceo.macedo@bemycrypto1.online
**Network:** Polygon (PoS)

---

## 1. Purpose of This Document

This document defines the **Vault System**, **Liquidity Architecture**, and 
**Reserve Management Model** for the BMC1 BeMyCoverage1 LLC blockchain insurance ecosystem.

The goal is to ensure:

- Fast internal settlement
- Stable internal accounting (BMC1usd = $1 internal value)
- Liquidity always available for accident claims
- Refund payout sustainability (65% / 35% Money Back model)
- Trust-based long-term stability using BMC1, BMC1x, and BMC1g as public support assets

---

## 2. Why Vault Architecture Is Critical

A blockchain insurance company cannot survive without:

- Dedicated liquidity for claims
- Separate reserves for refunds
- Separation between operational funds and policyholder funds
- Transparent accounting of policy liabilities
- Automated on-chain rules that reduce fraud and human intervention

Vault architecture is what prevents:

- insolvency risk
- misuse of funds
- over-minting BMC1usd
- liquidity collapse during large accident events

---

## 3. Core Vault Categories

BMC1 BeMyCoverage1 LLC will operate multiple vaults (wallets/contracts) each with a strict purpose.

### Vault Types Overview

| Vault Name                 | Asset Type          | Purpose |
|-----------                 |------------         |---------|
| Premium Vault              | USDC/USDT           | Collect premiums from policy buyers |
| Settlement Vault           | BMC1usd             | Internal settlement ledger for ecosystem |
| Claims Vault               | USDC/USDT           | Accident settlements and payout liquidity |
| Refund Vault               | USDC/USDT           | Holds future money-back obligations |
| Operations Vault           | USDC/USDT           | Payroll, contractors, marketing, business costs |
| Reserve Vault              | USDC/USDT           | Emergency stability and solvency reserves |
| Public Trust Vault         | BMC1/BMC1x/BMC1g    | Long-term credibility reserve and public support |
| Conversion Vault           | Mixed               | Performs yearly conversions to stable reserves |
| Treasury Governance Vault  | Mixed               | Multi-sig controlled top-level governance wallet |

---

## 4. Recommended Wallet Structure (Polygon)

### Required Wallet Entities

The system should have at minimum:

1. **MultiSig Treasury Wallet** (Main Governance Wallet)
2. **Stablecoin Reserve Wallet**
3. **Claims Liquidity Wallet**
4. **Refund Liability Wallet**
5. **Operations Wallet**
6. **Public Trust Wallet**
7. **Conversion Execution Wallet**

---

## 5. Recommended Implementation Approach

There are 2 options:

---

### Option A (Recommended): Smart Contract Vault System

Vaults are not normal wallets.
Vaults are **smart contracts** that enforce rules like:

- Only specific roles can withdraw
- Daily withdrawal caps
- Time-locks
- Automated distribution logic
- Refund eligibility enforcement

**This is the most secure and auditable approach.**

---

### Option B: MultiSig Wallets Only (Simpler, Less Automated)

Use Gnosis Safe MultiSig for all vaults.

Pros:
- easy to launch
- no custom code risk early

Cons:
- requires human approval for everything
- less automated
- less "self-DAO" behavior

---

## 6. BMC1usd Vault System Design

BMC1usd is internal.
Therefore, the most important vault is:

### **Settlement Vault (BMC1usd Ledger Vault)**

This vault represents the internal dollar balance system.

This is where:

- premiums get credited
- refunds get accounted
- internal transfers happen

BMC1usd never needs public liquidity if it remains internal.

---

## 7. The Stablecoin Base Layer (USDC / USDT)

### Why USDC/USDT Is Required

Even if BMC1usd is internal, claims must pay in assets that are:

- widely accepted
- liquid
- easily swappable
- externally redeemable

Therefore, the system must always maintain USDC/USDT reserves.

---

## 8. Premium Collection Flow (Policy Purchase)

### Flow Example

Customer buys a policy for $1,000.

1. Customer sends **USDC** to Premium Vault
2. Smart contract mints 1,000 BMC1usd internally
3. Policy NFT is issued
4. Policy status becomes ACTIVE
5. Funds are distributed into internal vaults

---

## 9. Premium Distribution Formula

When premium is received, the system splits funds into multiple vaults.

### Suggested Base Split (Example Model)

| Allocation                 | Percent | Destination |
|-----------                 |---------|-------------|
| Claims Liquidity           | 40%     | Claims Vault |
| Refund Liability Reserve   | 35%     | Refund Vault |
| Operations                 | 15%     | Operations Vault |
| Emergency Reserve          | 10%     | Reserve Vault |

> Note: these percentages can be changed later depending on risk model and actuarial math.

---

## 10. Claims Vault (Accident Settlement Pool)

The Claims Vault exists for immediate accident payments.

This vault must always have liquidity.

### Rules

- Funds can only be used for:
  - accident settlements
  - medical/legal claim settlements
  - repair reimbursement
  - total-loss payouts

### Recommended Security Controls

- MultiSig required for payouts above threshold
- Daily cap on withdrawals
- Oracle-driven event confirmation

---

## 11. Refund Vault (Money-Back Reserve Pool)

The Refund Vault holds funds that belong to future refunds.

Refund Vault must never be used for claims.

This prevents insolvency and protects customers.

### Refund Vault Use

Only for:

- maturity refunds after 5 years
- prorated refund upon total-loss settlement (if not at fault)
- cancellation refund logic (if eligible)

---

## 12. Operations Vault (Company Sustainability)

Operations vault is used for:

- salaries
- marketing
- legal compliance
- technology upgrades
- business expansion
- infrastructure costs

This vault is the "business engine".

---

## 13. Reserve Vault (Emergency Solvency Vault)

This is the ecosystem safety net.

This is used only if:

- accident volume exceeds predictions
- major catastrophic events occur
- extreme market conditions

### Recommended Reserve Rule

Reserve Vault cannot be withdrawn unless:

- MultiSig approves
- 48-72 hour time-lock triggers
- a safety oracle confirms emergency event

---

## 14. Public Trust Vault (BMC1/BMC1x/BMC1g Reserve)

This is a special vault holding:

- BMC1
- BMC1x
- BMC1g

This vault is designed like a "trust fund" concept.

It exists to:

- show credibility
- strengthen public confidence
- provide long-term growth reserves
- allow yearly conversion into stable reserves

---

## 15. Public Trust Vault Locking Strategy

The Public Trust Vault should implement a locking cycle.

### Lock Cycle Rule

- tokens deposited are locked for **5 years**
- withdrawals only allowed after lock maturity
- early withdrawals only possible via emergency governance vote

### Why 5 Years?

Because it aligns with the 5-year insurance policy maturity cycle.

---

## 16. Yearly Conversion System (Stability Conversion)

Each year, the system can convert a fixed portion of:

- BMC1
- BMC1x
- BMC1g

into stablecoins:

- USDC
- USDT

and optionally mint equivalent BMC1usd.

---

## 17. Yearly Conversion Vault Logic

### Conversion Flow

1. Once per year (scheduled date)
2. Smart contract triggers conversion event
3. A portion of BMC1/BMC1x/BMC1g is swapped
4. Proceeds go into Refund Vault + Claims Vault

---

## 18. Yearly Conversion Formula

### Define:

- `T_total` = total trust token holdings
- `C_rate` = yearly conversion rate (example: 5%)
- `C_amount` = converted amount

Formula:

C_amount = T_total × C_rate


Example:
- Trust vault holds 10,000,000 BMC1
- Conversion rate = 5%

C_amount = 10,000,000 × 0.05 = 500,000 BMC1


That 500,000 BMC1 is swapped into stablecoins.

---

## 19. Conversion Distribution Formula

After conversion into stablecoins, distribution is:

| Destination        | Percent |
|------------        |---------|
| Claims Vault       | 50% |
| Refund Vault       | 40% |
| Emergency Reserve  | 10% |

---

## 20. Why Convert Regardless of Price?

Your design idea is powerful:

> convert a fixed amount yearly regardless of market price.

This means:

- system builds reserves automatically
- avoids emotional trading decisions
- long-term smoothing effect
- "dollar cost averaging" into stability

Even if BMC1 is low, conversion continues.

Even if BMC1 is high, conversion continues.

---

## 21. Stability Rule: Minimum Liquidity Thresholds

To prevent collapse, the ecosystem must define minimum vault balances.

### Example Thresholds

| Vault | Minimum Balance Rule |
|------|------------------------|
| Claims Vault | must hold >= 20% of active policy liabilities |
| Refund Vault | must hold >= projected refund obligations |
| Reserve Vault | must hold >= 10% of total premiums collected |

---

## 22. Policy Liability Definitions

### Total Active Liability (TAL)

The TAL is the total value of all active policies.

TAL = Σ(policy_premium_value)


This is the system’s exposure base.

---

## 23. Refund Liability Definition

Refund liability depends on the MB percentage.

### Refund Liability (RL)

For each policy:

RL_policy = Premium × MB%


Total refund liability:

RL_total = Σ(RL_policy)


---

## 24. Claims Exposure Definition

Claims exposure is dynamic.

But a conservative formula:

ClaimsExposure = TAL × RiskFactor


Where RiskFactor is determined by actuarial models.

---

## 25. Liquidity Control: Vault Withdrawal Permissions

### Recommended Roles

| Role | Permissions |
|------|------------|
| CEO MultiSig | governance authority |
| Claims Officer | claims payout approvals |
| Oracle Validator | triggers event signals |
| Refund Executor | executes refund payouts |
| System Operator | manages internal mint/burn |

---

## 26. MultiSig Governance Recommendation

### Strongly Recommended Setup

Use Gnosis Safe MultiSig:

- 3 of 5 signatures required
- include cold wallet keys
- include hardware wallets

This prevents:
- internal theft
- single point of failure
- external hacks

---

## 27. User Wallet vs Company Vaults

### Users Must Have Non-Custodial Wallets

Customers should store:

- policy NFT
- internal BMC1usd credits (optional)
- rewards / incentives tokens
- BMC1/BMC1x/BMC1g investments (optional)

Users remain non-custodial.

Company vaults remain separate.

---

## 28. Internal Payout Options for Users

At maturity or refund event, user should be able to choose:

### Refund Options

| Option | User Receives |
|--------|--------------|
| Stable payout | USDC / USDT |
| Internal reinvest | BMC1usd credit |
| Public ecosystem investment | swap into BMC1 / BMC1x / BMC1g |
| Hybrid | split payout across multiple assets |

---

## 29. Vault Interaction With Public Tokens

Public tokens can support the ecosystem in 2 ways:

### 1. Trust Reserve (Locked Support)
Company holds BMC1/BMC1x/BMC1g as credibility reserves.

### 2. Public Investment Engine
Users and investors buy the tokens publicly, increasing:

- liquidity
- perceived credibility
- growth capital

---

## 30. Liquidity Locking Strategy (Public Market Trust)

To strengthen public trust, the company may lock liquidity pools.

### Example Strategy

- create liquidity pools for BMC1/USDC
- lock liquidity for 5 years
- show proof of lock publicly

This signals:

- no rug pull
- long-term ecosystem stability
- real business intent

---

## 31. BMC1usd Internal Liquidity Rule

BMC1usd should not need a public LP.

Instead:

- BMC1usd is always redeemable internally at $1 logic
- backed by vault balances and internal accounting

---

## 32. Redemption Architecture (Internal Redemption)

### Redemption Rule

BMC1usd can be redeemed for USDC/USDT only when:

- policy ends
- refund triggers
- claim payout triggers
- authorized internal settlement event triggers

This prevents:

- public arbitrage attacks
- external liquidity drains
- stablecoin bank-run scenarios

---

## 33. Anti-Bank Run Protection

BMC1usd must be protected against mass withdrawals.

Therefore:

### Withdrawal Rate Limits

- max withdrawal per wallet per day
- max withdrawal per system per day
- emergency pause capability

---

## 34. Vault Security Features

All vault contracts should include:

- `pause()` / `unpause()`
- time-lock withdrawals
- daily withdrawal limits
- blacklisting only for compliance emergencies
- multi-sig required for admin functions
- event logging for all movements

---

## 35. Vault Event Logging (Transparency)

Every vault transaction should emit events like:

- PremiumReceived
- ClaimsPaid
- RefundPaid
- PolicyCanceled
- ConversionExecuted
- ReserveWithdrawal

This allows auditors to verify all flows.

---

## 36. Summary: The Vault System in One Sentence

The BMC1usd vault architecture is a **multi-layer reserve + settlement system** that 
separates premiums, claims liquidity, refund obligations, emergency reserves, 
and public trust token reserves to guarantee long-term solvency and trust.

---

## 37. What This Vault Architecture IS

- A sustainable on-chain treasury system
- A modular structure for claims/refunds
- A transparent trust vault model
- A conversion strategy that stabilizes reserves
- A governance-controlled liquidity design

---

## 38. What This Vault Architecture IS NOT

- It is NOT a public stablecoin bank
- It is NOT an open redemption token for the public
- It is NOT a free-floating stablecoin traded on exchanges
- It is NOT an algorithmic stablecoin model like Terra/LUNA
- It is NOT a custodial banking replacement
- It is NOT a promise of FDIC insurance
- It is NOT a guarantee against all catastrophic events
- It is NOT designed to bypass regulatory frameworks

---

## 39. Next File Recommendation

Next, we should write:

### **BMC1usd_Tokenomics_And_Formulas.md**

This will include:
- full premium allocation formulas
- 65% / 35% MB calculations
- ticket penalty math
- cancellation triggers
- accident settlement proration formulas
- yearly conversion math tables

---
