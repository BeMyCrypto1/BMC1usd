
## BMC1usd Internal Utility Token Design (Polygon Ecosystem)

**Company:** BMC1 BeMyCoverage1 LLC  
**Parent Company:** BMC1 BeMyCrypto1 LLC  
**CEO:** Ben Macedo  
**Contact:** bmc1.ceo.macedo@bemycrypto1.online  


**Since we had defined the overall BMC1usd why and what is not in the readme.md file and all.
Here we now concentrate in the actual logical code development design architecture and how
it works, along with all interactive actions of the Car Insurance Wallet creation for policy holding
to token holdings, and processes for the settlements as well as the initial car insurance buying and
token transfer to-and-from USDC, or USDT with BMC1usd token.*



## 1. Purpose of This Document

This document defines the **BMC1usd token design**, including:

- what BMC1usd is intended to do
- minting and burning rules
- supply limitations and decimal precision
- internal balance accounting model
- access control and security protections
- how BMC1usd interacts with vaults and policy lifecycle logic

This file is written as a **technical blueprint** before Solidity implementation.

---

## 2. What is BMC1usd?

BMC1usd is the **internal settlement and accounting token** of the BeMyCoverage1 insurance ecosystem.

It is designed to behave as a **stable $1 equivalent token** for all internal insurance operations, including:

- policy premium payments
- claim settlements
- money-back (MB) refunds
- treasury reserve accounting
- internal reinvestment flows

BMC1usd is designed for **Polygon** usage due to low gas fees and fast transaction confirmation.

---

## 3. Token Standard Choice (Internal Non-ERC20)

### Primary Design Option (Recommended)
BMC1usd is designed as a **non-ERC20 internal ledger token**, meaning:

- it is not publicly tradable
- it is not transferable to arbitrary addresses
- it is not listed on DEXs
- it is not designed for open circulation

Instead, it exists as a balance stored inside BeMyCoverage1 smart contracts.

This is ideal for an insurance system because it keeps BMC1usd focused as a **utility accounting instrument**, not a speculative token.

---

## 4. Token Decimal Precision

BMC1usd uses:

### **18 decimals**
This matches Ethereum/Polygon ERC20 standard precision and ensures:

- precise premium calculations
- accurate MB refund math
- accurate ticket deduction math
- fair claim settlement rounding

Example:

- 1.000000000000000000 BMC1usd = $1.00

---

## 5. BMC1usd Supply Model

### 5.1 Supply Philosophy
BMC1usd should not be created randomly.  
It must only exist when backed by valid system activity such as:

- premiums paid into the system
- stablecoin reserves deposited (USDC/USDT)
- yearly conversions from public ecosystem tokens

BMC1usd supply is treated as **internal accounting liquidity**.

---

### 5.2 Supply Type Options

#### Option A (Dynamic Supply - Recommended)
No fixed max cap. Supply expands/contracts based on:

- premium inflows
- claim payouts
- refund payouts
- yearly conversion reinforcements

This mimics how real insurance cashflow behaves.

#### Option B (Hard Capped Supply)
A maximum supply is set, for example:

- 1,000,000,000 BMC1usd cap

This can improve investor confidence but may reduce system flexibility.

**Recommendation:** Start with Option A, add Option B later if needed.

---

## 6. Minting Rules (Creation of BMC1usd)

### 6.1 Who Can Mint?
Only the BeMyCoverage1 core contract system can mint BMC1usd.

No public wallet can mint.

Minting can only be triggered by:

- Premium Payments
- Yearly Treasury Reinforcement
- Admin Emergency Actions (multi-sig only)

---

### 6.2 Minting Event #1: Policy Premium Payment

When a customer buys a policy, the system creates BMC1usd equal to the premium value.

#### Example Formula:
BMC1usd_Minted = Premium_USD


#### Ledger Action:
- Customer balance increases
- Premium Vault increases

#### Example:
Customer pays $2,000 premium:

Mint 2,000 BMC1usd
PremiumVault += 2,000
PolicyLedger[User] += 2,000


---

### 6.3 Minting Event #2: Yearly Treasury Reinforcement

Each year, the ecosystem may convert value from:

- BMC1
- BMC1x
- BMC1g

into stable reserves (USDC/USDT), and then reinforce BMC1usd backing.

#### Example Formula:
BMC1usd_Minted = ValueConvertedToStable_USD


This ensures long-term stability even if public token prices fluctuate.

---

### 6.4 Minting Event #3: Emergency Liquidity Injection

In rare scenarios, multi-sig governance may authorize emergency minting.

This must be heavily restricted and logged, and must require:

- multi-sig approval
- timelock delay
- on-chain event logs
- strict maximum cap per emergency mint

---

## 7. Burning Rules (Destruction of BMC1usd)

Burning reduces the internal supply when BMC1usd exits the system.

### 7.1 Burn Trigger #1: Money-Back Refund (MB Payout)

When a policy matures after 5 years and the driver qualifies:

- the MB payout is released
- BMC1usd is deducted from internal vault balances

#### Example Formula:
MB_Payout = PremiumPaid * MB_AdjustedPercent


Example:
Premium = $2,000  
MB % = 65%  
MB_Payout = 2,000 * 0.65 = 1,300 BMC1usd


The payout may be withdrawn or reinvested.

---

### 7.2 Burn Trigger #2: Claim Settlement

When an accident claim is validated and approved:

Claim_Payout = Approved_Claim_Value_USD


BMC1usd is burned or transferred from Claims Vault allocation.

---

### 7.3 Burn Trigger #3: Policy Cancellation

If the policy is canceled due to:

- too many minor tickets
- severe ticket event
- fraud detection
- non-payment

then the system reallocates MB amounts into the company Claims/LP Vault.

BMC1usd is removed from the customer refund eligibility pool.

---

## 8. Transfer Restrictions (Internal Only Design)

### 8.1 Standard Transfer Function Disabled
BMC1usd will not allow:

- `transfer()`
- `approve()`
- `transferFrom()`

because these create open circulation and external trading.

### 8.2 Allowed Movements
BMC1usd can only move inside system-controlled flows:

- Premium Payment
- MB Refund Release
- Claims Settlement
- Treasury Allocation
- Reinvestment into public tokens (BMC1/BMC1x/BMC1g)

---

## 9. Vault Interaction Model

BMC1usd operates through internal vault accounting.

### Core Vaults

| Vault Name | Purpose |
|-----------|---------|
| Premium Vault | Stores incoming premiums |
| Refund Vault | Holds MB allocations until maturity |
| Claims / Liquidity Vault | Pays claims and supports ecosystem liquidity |
| Treasury Reserve Vault | Stores yearly reinforcement reserves |
| Trust Vault (optional) | Locks public tokens for credibility and long-term backing |

---

## 10. User Balance Model

Even though BMC1usd is internal, users still need visible balances.

Each user has an internal ledger record:

mapping(address => uint256) internalBalance;


Users can view:

- policy premium history
- MB eligibility
- MB percentage remaining
- ticket deductions
- claim impacts
- available withdrawable amount

---

## 11. Money-Back (MB) Eligibility Logic

### Base Groups

| Driver Category | Default MB % |
|----------------|--------------|
| Good Driver Group (A) | 65% |
| Higher Risk Group (B) | 35% |

Both require **5-year clean driving maturity**.

---

## 12. Minor Ticket Deduction Logic

Minor ticket events deduct MB eligibility:

### Deduction Rate
- **2.5% deduction per minor ticket**
- maximum of **5 minor tickets**
- exceeding 5 tickets cancels policy

#### Formula:
MB_AdjustedPercent = MB_BasePercent - (TicketCount * 2.5%)


Example (Group A):
- Base MB = 65%
- Ticket count = 3

MB_Adjusted = 65% - (3 * 2.5%) = 57.5%


Maximum penalty:
- 5 tickets

MB_Adjusted = 65% - 12.5% = 52.5%


If ticket count > 5:
- policy canceled
- MB forfeited to Claims/LP vault

---

## 13. Severe Ticket / At-Fault Accident Logic

Severe events include:
- DUI
- reckless driving
- major speeding violations
- fraud attempt
- at-fault serious accident

These events trigger:

- MB forfeiture
- policy cancellation (depending on severity)
- internal reallocation to Claims Vault

---

## 14. Not-At-Fault Accident Logic (Special Case)

If a driver has an accident that is not their fault:

- MB eligibility remains intact
- policy continues normally

If vehicle is totaled and policy is settled early:

- the policy is closed
- eligible MB is paid out proportional to time active
- driver may restart a new 5-year policy cycle with same group rating

This is required to keep fairness for safe drivers.

---

## 15. Access Control & Permissions

### Role-Based Access System

The contract must define strict roles such as:

| Role | Authority |
|------|----------|
| DEFAULT_ADMIN_ROLE | governance and role management |
| MULTISIG_GOVERNANCE_ROLE | emergency pause, treasury approvals |
| POLICY_MANAGER_ROLE | create/issue policies |
| VALIDATOR_ROLE | submit ticket/accident events |
| ORACLE_ROLE | external event confirmation |
| TREASURY_ROLE | yearly conversions |
| PAUSER_ROLE | emergency pause |

No single role should have unlimited power.

---

## 16. Security Protections (Required)

BMC1usd must include:

### 16.1 Multi-Sig Governance
Critical actions require multi-signature approval.

### 16.2 Emergency Pause
Ability to pause:
- minting
- burning
- withdrawals
- claim payouts

### 16.3 Timelock
Treasury actions and recovery actions must be time delayed.

### 16.4 Daily Mint Limits (Optional but Recommended)
To prevent unexpected supply inflation.

Example:
MaxMintPerDay = $5,000,000 equivalent


### 16.5 Auditable Logs
All major actions must emit on-chain events:

- policy created
- premium paid
- MB adjusted
- claim paid
- ticket recorded
- policy canceled
- MB payout executed

---

## 17. Quantum-Resilience Strategy (Future Proofing)

Polygon currently uses ECDSA signatures, which may be vulnerable in future quantum computing environments.

BMC1usd design should support:

- ERC-4337 smart wallets
- wallet migration functionality
- multi-sig controls
- guardian recovery system
- time delay withdrawals

The system is designed as:

### **Quantum-Resilience Ready**
(not fully quantum-proof, but migration-ready)

---

## 18. Summary

BMC1usd is designed as:

- an internal stable $1 accounting token
- non-ERC20 and non-publicly tradable
- backed by vault reserves and stablecoins
- integrated directly into the insurance lifecycle logic
- protected by multi-sig governance, timelocks, and oracle validation
- Polygon-native for speed and low gas
- future-proofed for recovery and quantum-resilience strategies

BMC1usd will serve as the core internal settlement unit for:

- policy buying and renewal
- claims payouts
- MB incentives and refunds
- long-term treasury reinforcement

---
