# BMC1usd_Minting_Burning_And_Supply_Cap_Model.md

## BMC1 BeMyCoverage1 LLC — Minting, Burning, Supply Cap, and Peg Stability Model
**Parent Company:** BMC1 BeMyCrypto1 LLC  
**Insurance Entity:** BMC1 BeMyCoverage1 LLC  
**Internal Utility Token:** BMC1usd  
**Public Tokens:** BMC1, BMC1x, BMC1g  
**Network:** Polygon (PoS)  
**CEO:** Ben Macedo  
**Contact:** bmc1.ceo.macedo@gmail.com  

---

# 1. Purpose of This Document

This document defines the official design rules for:

- how **BMC1usd is created (minted)**
- how **BMC1usd is destroyed (burned)**
- how the **1:1 USD peg is maintained**
- how the **total supply is controlled**
- how the **insurance refund promises remain safe**
- how **policy vault reserves remain solvent**

This document is written to be clear for:

- developers
- auditors
- investors
- regulators (if needed later)
- institutional partners

---

# 2. What BMC1usd Is

## Definition
**BMC1usd is an internal utility settlement token** used exclusively inside the BMC1 BeMyCoverage1 LLC insurance ecosystem.

It functions as:

- internal accounting currency
- policy premium unit
- claims settlement unit
- refund unit (Money Back Program)

It behaves like a digital prepaid balance, similar to:

- Starbucks prepaid card
- Amazon gift credit
- airline miles accounting
- closed-loop corporate credits

---

# 3. What BMC1usd Is NOT

BMC1usd is NOT:

- a public stablecoin open to all markets
- a decentralized stablecoin like DAI
- an algorithmic stablecoin like UST
- a public traded ERC-20 token intended for speculation
- a yield-bearing investment token
- a token intended for open exchange listings

BMC1usd is strictly:

> **internal settlement money for insurance operations.**

---

# 4. Why BMC1usd Must Have Controlled Minting

In an insurance ecosystem, unlimited minting is dangerous because it could create:

- fake liabilities
- artificial balances
- insolvency risk
- investor distrust
- inability to pay claims

Therefore:

## BMC1usd minting MUST be tied to real collateral deposits.

---

# 5. Peg Stability Definition (1:1 Rule)

The peg rule is:

### 1 BMC1usd = 1 USD of stable reserve value

The stable reserve value is defined as:

- USDC
- USDT
- (optionally) DAI
- (optionally) tokenized T-Bills in the future

The peg is not enforced by market arbitrage.

It is enforced by:

> **company-controlled mint/burn + reserve vault accounting.**

---

# 6. Collateral Model (Backing Design)

The BMC1usd system must operate under a strict collateralization model.

## 6.1 Primary Collateral Assets
The collateral that backs BMC1usd should be:

- USDC (Polygon)
- USDT (Polygon)

These are liquid, recognized, and stable.

---

## 6.2 Optional Secondary Collateral (Future)
The system may later include:

- DAI
- Tokenized treasuries (RWA)
- Tokenized money market funds

But only after maturity.

---

# 7. Minting Rule (The Only Way BMC1usd Is Created)

## Rule
BMC1usd can only be minted if stable collateral is deposited.

### Example
If a customer deposits:

- 1,000 USDC

Then the system can mint:

- 1,000 BMC1usd

---

# 8. Minting Formula

Let:

- `Deposit_USDC`
- `Deposit_USDT`

Then:

    Mint_BMC1usd = Deposit_USDC + Deposit_USDT

If:

Deposit_USDC = 700  
Deposit_USDT = 300  

Then:

Mint_BMC1usd = 1000

---

# 9. Minting Process (Operational Flow)

## Step-by-step minting
1. Customer buys a policy and pays using:
   - USDC
   - USDT
   - (optional future: credit card -> company converts into stablecoin)

2. Stablecoins are transferred into the:
   **Insurance Reserve Vault**

3. Smart contract confirms receipt

4. Contract mints equivalent BMC1usd into:
   - customer policy wallet OR
   - policy NFT vault balance

---

# 10. Who Can Mint BMC1usd?

Minting authority should be restricted to:

### Option A: MultiSig Treasury Controller (Recommended)
Only a MultiSig wallet can trigger minting.

### Option B: Smart Contract Minting Gateway (Best Future Version)
A smart contract automatically mints when it receives USDC/USDT.

---

# 11. Burning Rule (The Only Way BMC1usd Is Destroyed)

BMC1usd is burned when:

- refunds are paid
- claims are paid
- a policy ends and balances are settled
- policy is canceled and balances are moved into company pool

Burning ensures that supply stays balanced.

---

# 12. Burning Formula

Let:

- `Redeem_BMC1usd`

Then:

Burn_BMC1usd = Redeem_BMC1usd


If a policy ends and customer receives payout:

- 650 BMC1usd refund

Then:

- 650 BMC1usd must be burned from the contract ledger.

---

# 13. Redemption Rule (Conversion Back Into Real Stablecoins)

When the customer wants to cash out, the system does:

1. Burn customer BMC1usd balance
2. Send USDC or USDT from the stable reserve vault

---

# 14. Redemption Formula

Let:

- `BMC1usd_Amount`

Then:

USDC_Payout + USDT_Payout = BMC1usd_Amount


Example:

BMC1usd_Amount = 1000  
USDC_Payout = 700  
USDT_Payout = 300  

Total = 1000

---

# 15. Redemption Constraints (Important)

To protect the insurance company:

## 15.1 Redemption may be delayed if claims are active
Example:

- customer has open claim
- customer cannot withdraw refund balance until claim closes

## 15.2 Redemption may require policy maturity
Example:

- refund only happens at 5-year maturity unless early settlement applies

---

# 16. Supply Cap Model (Should There Be a Max Supply?)

This is extremely important.

BMC1usd can be designed in two ways:

---

## Model A: No Fixed Max Supply (Recommended)
BMC1usd supply expands and contracts based on:

- new policy deposits
- claim settlements
- refund settlements

This is the same way USDC operates.

### Why it is safe
Because minting is only allowed if collateral exists.

So supply is always backed.

---

## Model B: Hard Cap Supply
Example:

- max supply = 10 billion BMC1usd

### Why this is risky
If the company grows beyond that cap, you must redeploy a new contract.

This creates ecosystem friction.

---

# 17. Recommended Supply Strategy

### Official Recommendation:
**BMC1usd should NOT have a hard max cap.**

Instead:

- enforce minting only through stable reserve deposits
- enforce solvency checks
- enforce vault reserve accounting

This makes BMC1usd scalable.

---

# 18. Supply Safety Mechanism (The Real "Cap")

The real supply limit is:

> **The amount of USDC/USDT stored in the Reserve Vault.**

So the cap is dynamic.

Formula:

Max_BMC1usd_Supply = TotalStableReserves


Where:

TotalStableReserves = Vault_USDC + Vault_USDT


---

# 19. Insurance Solvency Rule (Most Important Rule)

This is the key investor safety statement.

### The contract must enforce:

Total_BMC1usd_Circulating <= Total_Stable_Reserves


This ensures full backing.

---

# 20. Why the 65% MB / 35% MB Model Still Works

You asked an important question:

> If 65% goes back to driver, and 35% goes to LP, how do we pay claims?

Answer:

Because the LP portion is not “extra money”.

It becomes the insurance risk pool.

---

# 21. Premium Allocation Model

Let:

- `P = Premium Amount`
- `MB = Money Back Percentage`
- `LP = Liquidity Pool Portion`

Then:

MB_Reserve = P × MB
LP_Reserve = P × (1 - MB)


---

## 21.1 Good Driver Group (65% MB)
MB = 0.65

MB_Reserve = P × 0.65
LP_Reserve = P × 0.35


---

## 21.2 High Risk / SR22 Group (35% MB)
MB = 0.35

MB_Reserve = P × 0.35
LP_Reserve = P × 0.65


---

# 22. Where the LP Portion Goes (Your Concern Answered)

The LP portion is not just one bucket.

It can be split into multiple internal sub-vaults.

This is where your business becomes sustainable.

---

# 23. Recommended Internal Vault Sub-Buckets

### The LP portion should be split into:

| Vault Bucket | Purpose |
|-------------|---------|
| Claims Vault | accident claim payouts |
| Catastrophic Reserve Vault | major losses, multi-vehicle claims |
| Operating Vault | employees, legal, infrastructure |
| Growth Vault | marketing, expansion, partnerships |
| Reinsurance Vault | future third-party insurance coverage |
| Profit Vault | long-term company sustainability |

---

# 24. Recommended LP Distribution (Example Model)

This is one recommended split of the LP portion:

| Sub-Vault | % of LP Portion |
|----------|------------------|
| Claims Vault | 50% |
| Catastrophic Reserve Vault | 15% |
| Operating Vault | 15% |
| Growth Vault | 10% |
| Reinsurance Vault | 5% |
| Profit Vault | 5% |

This is adjustable.

---

# 25. Example Calculation (Good Driver Policy)

Let premium P = 1,000 BMC1usd.

Good Driver:

- MB = 65%
- LP = 35%

So:

MB Reserve = 650  
LP Reserve = 350  

Now distribute the 350 LP:

- Claims Vault (50%) = 175
- Catastrophic Vault (15%) = 52.5
- Operating (15%) = 52.5
- Growth (10%) = 35
- Reinsurance (5%) = 17.5
- Profit (5%) = 17.5

---

# 26. Example Calculation (SR22 / High Risk Policy)

Let premium P = 1,000 BMC1usd.

High Risk:

- MB = 35%
- LP = 65%

So:

MB Reserve = 350  
LP Reserve = 650  

Now distribute 650 LP:

- Claims Vault (50%) = 325
- Catastrophic Vault (15%) = 97.5
- Operating (15%) = 97.5
- Growth (10%) = 65
- Reinsurance (5%) = 32.5
- Profit (5%) = 32.5

---

# 27. Why This Multi-Vault LP System Is Important

Because it ensures:

- claims are always funded first
- catastrophic events do not bankrupt the company
- company has operational sustainability
- growth is possible without destroying reserves

This is how real insurance companies work.

---

# 28. The Money Back Reserve Is Not Spendable (Locked Logic)

The MB reserve should be treated as:

> locked escrow for the customer

It should not be used for company expenses.

It is only released if:

- driver qualifies at maturity
- driver policy ends with no violations
- policy ends early due to total loss settlement

---

# 29. Ticket Deduction System Impact on Mint/Burn

If a driver gets minor tickets:

- their MB % is reduced
- the deducted portion is moved into LP reserves

Example:

Original MB = 65%  
Ticket deduction = 12.5%  
New MB = 52.5%

The deducted 12.5% becomes extra liquidity.

---

# 30. Ticket Deduction Formula

Let:

- `MB_initial`
- `Tickets_minor`
- `Penalty = 2.5% per ticket`
- `PenaltyCap = 5 tickets`

Then:

MB_final = MB_initial - (Tickets_minor × 0.025)


But:

Tickets_minor <= 5


---

# 31. Total Cancellation Rule (Beyond 5 Tickets)

If minor tickets exceed 5:

- policy is canceled
- MB reserve is forfeited
- MB reserve transfers into LP pool

This is extremely powerful sustainability logic.

---

# 32. Minting/Burning Safety in Early Policy Termination

If a policy ends early due to:

- not-at-fault total loss accident
- settlement payout event

Then:

- refund is paid only up to that date
- BMC1usd is burned accordingly
- stable reserves are released accordingly
- new policy starts from zero again

This is how you preserve fairness.

---

# 33. Policy Restart Rule (After Not-at-Fault Total Loss)

Your rule is correct:

- driver stays in good driver category
- but must restart 5-year cycle
- refund clock resets

This prevents infinite overlapping liabilities.

---

# 34. How the System Prevents "Unlimited Liability"

Without restart logic, a driver could:

- claim payout at year 4.5
- keep refund eligibility running
- buy new policy and still count old years

That would create:

- massive financial imbalance

Therefore:

### restart rule is mandatory.

---

# 35. How BMC1usd Supply Remains Balanced Over Time

The BMC1usd supply naturally stabilizes because:

- new policies mint new supply
- claims burn supply
- refunds burn supply
- canceled policies burn or redirect balances internally

Thus BMC1usd supply becomes a reflection of:

> active policy obligations.

---

# 36. Peg Stability Protection Mechanisms

To ensure the peg always holds, the ecosystem must enforce:

## 36.1 Full Reserve Backing
No mint without collateral.

## 36.2 Emergency Pause Switch
If oracle/attack happens, stop transfers.

## 36.3 MultiSig Governance
No single person can drain vault.

## 36.4 Timelock Withdrawals
Large withdrawals require delay window.

---

# 37. Treasury "Run Protection" Mechanism

If too many users try to cash out at once:

- stable reserves must still cover liabilities

The best protection is:

### Maintain reserve ratio above 100%.

Example:

Reserves = 110%
Liabilities = 100%


This extra 10% is safety buffer.

---

# 38. Recommended Reserve Ratio Policy

| Reserve Policy | Meaning |
|---------------|---------|
| 100% backing | minimum required |
| 110% backing | recommended |
| 125% backing | ideal for credibility |

This can be achieved by treasury conversions of BMC1/BMC1x/BMC1g.

---

# 39. Final Recommended Rules Summary

## Minting Rules
- Mint only when stablecoin collateral is deposited
- Mint equals deposited stablecoins
- Minting controlled by MultiSig or automated gateway

## Burning Rules
- Burn whenever payout/refund/claim settlement happens
- Burning required to keep liabilities accurate

## Supply Model
- No fixed cap
- Dynamic cap tied to stable reserve vault balance

## Peg Model
- enforced internally, not market arbitrage
- 1:1 backed by USDC/USDT reserves

## LP Distribution
- LP portion must be subdivided into multiple vault buckets
- claims funded first, sustainability funded second

---

# 40. Closing Statement

BMC1usd is designed to be:

- stable
- internally controlled
- fully collateral-backed
- scalable
- safe for long-term insurance liabilities

The mint/burn model ensures that:

- the token cannot inflate irresponsibly
- the company cannot overpromise refunds
- the ecosystem remains solvent even during high claim periods

This structure provides the foundation required for:

- investor trust
- long-term sustainability
- real-world insurance adoption

---
