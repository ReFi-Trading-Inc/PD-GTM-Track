# Hypothesis Prioritization - ReFi.Trading

**Team:** ReFi.Trading  
**Date:** November 28, 2025  
**Created By:** Zeshan Ahmad, Daniel Oosthuyzen

---

## Customer Assumptions

> Assumptions about WHO your customers are and HOW they behave

| # | Assumption | Impact | Confidence | Risk Score |
|---|------------|--------|------------|------------|
| C1 | We believe that power-retail traders check their portfolio performance at least 3x daily and are frustrated with manual trade execution | 5 | 3 | 15 |
| C2 | We believe that fund managers with <$50M AUM lack resources to build proprietary RL trading systems | 5 | 4 | 10 |
| C3 | We believe that retail traders in UAE/GCC are more willing to adopt crypto-adjacent fintech than North American traders | 4 | 2 | 16 |
| C4 | We believe that our target users understand and value zero-knowledge proofs for risk verification | 4 | 2 | 16 |
| C5 | We believe that technical prosumers are comfortable with broker API connections and non-custodial wallets | 4 | 3 | 12 |

---

## Problem Assumptions

> Assumptions about the PROBLEM you're solving

| # | Assumption | Impact | Confidence | Risk Score |
|---|------------|--------|------------|------------|
| P1 | We believe that retail traders lose 15-30% annual returns due to emotional trading decisions | 5 | 2 | 20 |
| P2 | We believe that current robo-advisors are too conservative for power-retail traders seeking alpha | 5 | 3 | 15 |
| P3 | We believe that the lack of verifiable, non-custodial automated trading is the #1 barrier to adoption | 5 | 2 | 20 |
| P4 | We believe that traders waste $300-600/month on fragmented tool stacks (data, execution, analytics) | 4 | 3 | 12 |
| P5 | We believe that post-FTX trust crisis makes non-custodial solutions 10x more attractive | 5 | 3 | 15 |

---

## Solution Assumptions

> Assumptions about your PROPOSED SOLUTION

| # | Assumption | Impact | Confidence | Risk Score |
|---|------------|--------|------------|------------|
| S1 | We believe that RL agents can outperform discretionary retail trading by 10%+ CAGR | 5 | 3 | 15 |
| S2 | We believe that zk-VaR proofs provide sufficient trust for users to delegate trading decisions | 5 | 2 | 20 |
| S3 | We believe that ERC-4337 account abstraction wallets are mature enough for production use | 4 | 3 | 12 |
| S4 | We believe that our dual-proof gate (zk-VaR + ACE) differentiates us sufficiently from competitors | 5 | 2 | 20 |
| S5 | We believe that Google AI Agent Platform provides sufficient reliability for mission-critical trading | 4 | 3 | 12 |

---

## Value Assumptions

> Assumptions about willingness to USE or PAY

| # | Assumption | Impact | Confidence | Risk Score |
|---|------------|--------|------------|------------|
| V1 | We believe that retail traders will connect their brokerage accounts (60%+ who sign up) | 5 | 2 | 20 |
| V2 | We believe that users will pay $150-995/month for algorithmic trading automation | 5 | 2 | 20 |
| V3 | We believe that institutional clients will pay $50-120K/year for fund licensing | 5 | 3 | 15 |
| V4 | We believe that users will transition from paper trading to live trading within 14 days | 4 | 2 | 16 |
| V5 | We believe that progressive caps ($100 → $500 → $5000) reduce fear of live trading | 4 | 3 | 12 |

---

## Technical Assumptions

> Assumptions about TECHNICAL FEASIBILITY

| # | Assumption | Impact | Confidence | Risk Score |
|---|------------|--------|------------|------------|
| T1 | We believe that we can achieve p95 order-to-fill latency <150ms via SnapTrade | 4 | 3 | 12 |
| T2 | We believe that zk-SNARK proof generation can be done in <3ms for VaR calculations | 4 | 3 | 12 |
| T3 | We believe that zkSync Era provides sufficient throughput for trade anchoring at scale | 3 | 4 | 6 |
| T4 | We believe that Polygon.io data feeds provide sufficient quality for RL agent training | 4 | 4 | 8 |
| T5 | We believe that our TD3/PPO ensemble can be deployed via Google Agent Development Kit without latency issues | 4 | 3 | 12 |

---

## Market Assumptions

> Assumptions about MARKET CONDITIONS and COMPETITION

| # | Assumption | Impact | Confidence | Risk Score |
|---|------------|--------|------------|------------|
| M1 | We believe that ADGM RegLab sandbox provides faster regulatory approval than other jurisdictions | 4 | 3 | 12 |
| M2 | We believe that there's no competitor offering non-custodial + zk-verified RL trading | 5 | 3 | 15 |
| M3 | We believe that the UAE/GCC market has 100K+ qualified traders for our ICP | 4 | 2 | 16 |
| M4 | We believe that broker partners (IBKR, Alpaca) will maintain API stability and access | 4 | 4 | 8 |
| M5 | We believe that ISO/IEC 42001 AI certification will be a meaningful competitive advantage | 3 | 2 | 12 |

---

## Risk Score Calculation Guide

### Impact if Wrong (1-5)
- **5 = Critical:** Product completely fails if wrong
- **4 = Major:** Requires significant pivot
- **3 = Moderate:** Requires feature changes
- **2 = Minor:** Requires adjustment
- **1 = Minimal:** Negligible impact

### Confidence Level (1-5)
- **5 = Very High:** Validated with strong evidence (10+ data points)
- **4 = High:** Good evidence (5-9 data points)
- **3 = Medium:** Some evidence, not conclusive
- **2 = Low:** Anecdotal evidence only
- **1 = Very Low:** Pure guess, no evidence

### Risk Score = (6 - Confidence) × Impact

---

## Priority Rankings

| Rank | ID | Assumption | Impact | Conf | Risk | Category |
|------|----|------------|--------|------|------|----------|
| 1 | P1 | Traders lose 15-30% returns to emotional decisions | 5 | 2 | 20 | Problem |
| 2 | P3 | Non-custodial + verifiable is #1 barrier to adoption | 5 | 2 | 20 | Problem |
| 3 | S2 | zk-VaR proofs provide sufficient trust | 5 | 2 | 20 | Solution |
| 4 | S4 | Dual-proof gate is sufficient differentiation | 5 | 2 | 20 | Solution |
| 5 | V1 | 60%+ signup-to-broker-connect conversion | 5 | 2 | 20 | Value |
| 6 | V2 | Users will pay $150-995/month | 5 | 2 | 20 | Value |
| 7 | C3 | UAE/GCC traders more willing to adopt | 4 | 2 | 16 | Customer |
| 8 | C4 | Users understand/value zk-proofs | 4 | 2 | 16 | Customer |
| 9 | V4 | Paper-to-live transition within 14 days | 4 | 2 | 16 | Value |
| 10 | M3 | 100K+ qualified UAE/GCC traders exist | 4 | 2 | 16 | Market |

---

## Top 3 Riskiest Assumptions

### 🔴 Priority #1: Broker Connection Conversion (V1)

**Full Statement:**  
We believe that 60% or more of users who sign up for ReFi.Trading will successfully connect their brokerage account via SnapTrade within 7 days of signup.

**Category:** Value

**Why This is Risky:**
- **Impact if wrong (5):** If <40% connect brokers, we can't validate the core product. The entire value proposition depends on users being willing to grant trading access. Without broker connections, we have no way to test actual trading behavior, measure performance, or generate revenue.
- **Confidence level (2):** We have zero real data on this. User interviews suggest interest, but connecting a brokerage account is a significant trust barrier. SnapTrade reduces friction, but we don't know if "interest" translates to action. Alpaca API integration adds complexity. Broker availability may vary by region.
- **Risk score: 20**

**Current Evidence:**
- 10+ user interviews showed interest in "automated trading"
- No data on actual broker connection conversion rates
- SnapTrade case studies show 30-50% connection rates for personal finance apps, but NOT for trading apps
- Industry data shows 60% drop-off at broker OAuth for retail trading apps
- Our Alpaca partner integration (via SnapTrade) is unproven

**If This is Wrong:**
- Cannot validate core product hypothesis (RL agents improve returns)
- Must pivot to different onboarding flow (manual setup, different broker strategy)
- May need to offer "demo trading" with fake money to reduce friction
- Could indicate fundamental trust issue with our value proposition
- Threatens entire go-to-market timeline

---

### 🟡 Priority #2: Non-Custodial Trust Barrier (P3 + S2 combined)

**Full Statement:**  
We believe that the lack of verifiable, non-custodial automated trading is the #1 barrier preventing retail traders from adopting algorithmic trading solutions, AND that our zk-VaR proof system provides sufficient trust to overcome this barrier.

**Category:** Problem + Solution

**Why This is Risky:**
- **Impact if wrong (5):** If users don't care about non-custodial or don't trust zk-proofs, our entire differentiation strategy fails. We've built complex infrastructure (ERC-4337 wallets, zk-SNARKs, dual-proof gates) that may be solving a problem users don't have or don't understand.
- **Confidence level (2):** User interviews confirm "trust concerns" post-FTX, but we haven't validated that OUR specific solution (zk-proofs + non-custodial) resonates. Users may want non-custodial but not understand technical mechanisms. Or they may not care about custody if returns are good.
- **Risk score: 20 (P3) + 20 (S2) = effectively our highest combined risk**

**Current Evidence:**
- Post-FTX sentiment strongly favors "not your keys, not your crypto"
- Zero evidence that retail traders understand zero-knowledge proofs
- No competitor validation of zk-proof-gated trading in market
- Institutional clients may value this, but retail may not care
- Our interviews showed interest in "transparency" but not specifically zk-proofs
- Users expressed preference for established brokers like IBKR and newer platforms like Alpaca

**If This is Wrong:**
- Our core technical differentiation (zk-VaR + non-custodial) may be over-engineered
- Users may prefer simpler "view-only API access" with traditional risk limits
- We may need to pivot to custodial model with better UX (like Robinhood)
- Could indicate we're building for institutional clients, not retail
- May need to dramatically simplify messaging and tech stack

---

### 🟢 Priority #3: Paper-to-Live Transition (V4)

**Full Statement:**  
We believe that users who successfully complete paper trading will transition to live trading (with progressive caps) within 14 days, with 60%+ making their first live trade.

**Category:** Value

**Why This is Risky:**
- **Impact if wrong (4):** If users get "stuck" in paper trading indefinitely, we can't validate actual performance or generate revenue. Paper trading is not our business model. We need live traders to prove the system works and to earn execution fees. A long paper-to-live cycle kills velocity.
- **Confidence level (2):** We have a progressive caps strategy ($100 → $500 → $5000) designed to reduce fear, but no validation it works. Users may love paper trading (zero risk) and never graduate. Or the psychological barrier to "real money" may be insurmountable regardless of caps.
- **Risk score: 16**

**Current Evidence:**
- Industry data: 70%+ of retail traders who paper trade never go live
- Our progressive caps strategy is untested
- User interviews suggested "I'd want to test it first" but didn't specify duration
- No data on what threshold of paper trading performance gives users confidence
- Gamification system (XP, badges) designed to incentivize live trading, but unproven

**If This is Wrong:**
- We may need to eliminate paper trading entirely (force immediate live with tiny caps)
- Could indicate our RL agents don't perform well enough in simulation to build confidence
- May need to add "performance guarantees" or "money-back if underperforms benchmark"
- Might require much longer validation cycles (30-60 days paper before live)
- Could suggest fundamental fear of algorithmic trading we can't overcome with UX alone

---

## Testing Strategy

**Order of Testing:**
1. **Test V1 first (Broker Connection Conversion)** - This is the gate to everything else. If we can't get users to connect brokers, nothing else matters. We need to know this immediately.
2. **Test P3+S2 second (Non-Custodial + zk-Proof Value)** - Once we have broker connections, we need to validate that our core differentiation actually resonates. Do users understand it? Do they care?
3. **Test V4 third (Paper-to-Live Transition)** - Only after we've proven users will connect AND value our approach do we need to validate the transition flow.

**Rationale:**
Sequential dependencies: Can't test paper-to-live without broker connections. Can't validate zk-proof trust without users in the system. Broker connection is the highest-leverage test because it unblocks everything else.

---

## Decision Criteria

**When to pivot:**
- **If V1 is invalidated (<40% broker connect):** Major pivot to different onboarding (demo accounts, simplified flow, or different broker strategy). May need to offer "view-only" mode first.
- **If P3+S2 is invalidated (users don't care about non-custodial/zk-proofs):** Moderate pivot to simpler trust model. Potentially abandon ERC-4337/zk-SNARK complexity in favor of traditional API-key model with better UX.
- **If V4 is invalidated (<40% paper-to-live):** Minor iteration on caps strategy, incentives, or paper trading requirements. Not a fundamental pivot.

**When to persevere:**
- **All top 3 validated (>60% for each):** Full speed ahead on MVP development. Scale alpha program to 200+ users.
- **2 of 3 validated:** Proceed with caution. Double-down on fixing the weak point before scaling.
- **1 of 3 validated:** Serious reconsideration needed. Likely need to pivot customer segment or solution approach.

---

## Notes & Observations

**Team Discussion Highlights:**
- There's tension between our technical sophistication (zk-proofs, ERC-4337) and user understanding. We may be over-engineering for retail.
- Broker connection is clearly the "make or break" metric. If we can't crack this, we have no business.
- UAE/GCC market choice was strategic for regulation, but we have least confidence about user behavior there.
- Progressive caps strategy is our best guess, but completely unvalidated. Could be too conservative OR too aggressive.

**Open Questions:**
- Should we test with "fake money demo" first before requiring broker connection?
- Is SnapTrade the right choice, or should we build direct IBKR integration?
- Do we need a "trust video" explaining zk-proofs, or will that confuse more than clarify?
- What's the minimum paper trading performance that gives users confidence to go live?

---

## Change Log

| Date | Change | Reason |
|------|--------|--------|
| Nov 28, 2025 | Initial prioritization | Lab 8 exercise based on 00-EXECUTIVE-ACTION-PLAN and project docs |
