# ReFi.Trading Solution Concepts
**Version:** 1.0  
**Date:** November 28, 2025  
**Status:** Validated via 18 user interviews

---

## Core Solution: Non-Custodial AI Trading Platform

**One-Line Pitch:** Wall Street AI, radically accessible—non-custodial algorithmic trading with cryptographic safety proofs.

### The Three Pillars

#### 1. Non-Custodial Architecture
**Problem It Solves:** Post-FTX, 89% of interviewed traders (16/18) refuse to give custody of assets to third parties.

**How It Works:**
- User's assets remain at their broker (IBKR, Alpaca, Kraken, Coinbase)
- ReFi.Trading integrates via SnapTrade API (approved partner with trading permissions)
- AI generates trade signals → routes to user's broker via OAuth → executes in user's account
- Platform NEVER has access to withdraw or transfer user funds

**Validation:** 16/18 users rated non-custodial as 10/10 importance

#### 2. Cryptographic Risk Proofs (zk-VaR)
**Problem It Solves:** 94% of traders (17/18) cited emotional decision-making as #1 pain point; need algorithmic discipline.

**How It Works:**
- Before every trade, zk-SNARK proof generated showing trade complies with risk limits
- Proof verifies: VaR ≤ user-defined max, position size ≤ caps, portfolio doesn't exceed exposure limits
- Proof stored on-chain (zkSync Era L2) for auditability
- ERC-4337 smart wallet only signs trades if proof is valid
- AI strategy remains private (zero-knowledge)

**Validation:** 82% comprehension rate, +2.8pt trust lift on 10pt scale

#### 3. Progressive Caps (Graduated Risk Exposure)
**Problem It Solves:** 60% fear (11/18) of giving AI "too much power" on day 1; need safety ramp.

**How It Works:**
- Days 1-2: $100 max per trade, $500 daily limit (paper trading)
- Days 3-6: $500 max per trade, $2.5K daily limit (first live trades)
- Days 7-14: $5K max per trade, $25K daily limit
- Day 15+: User sets custom limits based on comfort

**Validation:** 12/14 users who tested concept felt "$100 start was safe"

---

## Feature Set by Tier

### Starter Tier ($150/month)
- 1 asset class (equities only)
- 1 live RL policy (PPO or TD3, pre-trained)
- 5K API calls/day (sufficient for 20-30 trades/day)
- Email support (24-hour response)
- Basic portfolio dashboard
- Progressive caps system
- zk-VaR proof verification

**Target User:** Trading experimenters, proof-of-concept seekers

### Pro Tier ($350/month) ⭐ 70% CHOOSE THIS
- Multi-asset (equities, crypto, ETFs, options Q2 2026)
- 5 live policies (can A/B test strategies)
- 50K API calls/day (sufficient for 200+ trades/day)
- VaR dashboard (drawdown, Sharpe, win rate)
- Priority email + Slack community support (2-hour response)
- Custom risk parameter editor
- Weekly performance reports

**Target User:** Serious power-retail traders, our primary ICP

### Prime Tier ($995/month)
- Unlimited policies
- Unlimited API calls
- Low-latency endpoints (AWS ORD1, co-located near exchanges)
- Slack-priority support (<30 min response during market hours)
- 1:1 monthly strategy review call
- Custom model training ($10K one-time setup fee, optional)
- API access for algo traders

**Target User:** Sophisticated quants, small fund managers

---

## Enterprise / Fund Tier (Phase 2 - Q3 2026)

### Fund Lite ($50K/year + 10bp AUM)
- White-label agent (your branding)
- 1 custom strategy (we train on your data)
- Multi-user RBAC (3 seats: PM, trader, analyst)
- Regulatory reporting (Form PF, 13F)
- SLA: 99.9% uptime
- Dedicated account manager

**Target User:** Sub-$500M funds, family offices

### Fund Growth ($120K/year + 8bp AUM)
- Multi-strategy portfolio
- Custom model training (unlimited iterations)
- 10 user seats
- API for algo integration
- Co-location option
- Audit support (SOC 2, compliance exams)

**Target User:** $500M-$1B funds

**Revenue Potential:** 10 funds @ avg $83.5K = $835K ARR (4x retail in Phase 2)

---

## Differentiation Matrix

| Feature | ReFi.Trading | QuantConnect | Composer | Wealthfront | Bloomberg AIM |
|---------|--------------|--------------|----------|-------------|---------------|
| **Non-Custodial** | ✅ Yes | ⚠️ Paper only | ❌ Custodial | ❌ Custodial | ✅ Yes |
| **Live RL Agents** | ✅ Yes | ❌ Backtest only | ❌ Rule-based | ❌ Passive robo | ✅ Yes |
| **zk-Proof Risk** | ✅ Cryptographic | ❌ Software checks | ❌ None | ❌ Black box | ⚠️ Proprietary |
| **Progressive Caps** | ✅ Built-in | ❌ Manual | ❌ None | ❌ None | ⚠️ Custom |
| **Retail Accessible** | ✅ $150-995/mo | ⚠️ DIY steep curve | ✅ $9-49/mo | ✅ Free-0.25% | ❌ $100K+/year |
| **Multi-Broker** | ✅ IBKR, Alpaca, Kraken, Coinbase | ⚠️ IBKR only | ⚠️ Alpaca only | ❌ Proprietary | ✅ Yes |
| **Transparent AI** | ✅ On-chain proofs | ⚠️ Code visible | ❌ Black box | ❌ Black box | ❌ Proprietary |

**Key Competitive Advantages:**
1. Only platform combining live RL + non-custodial + cryptographic risk
2. Trust post-FTX: users keep custody, we prove safety
3. Regulatory-friendly: human-in-the-loop + audit trail + broker supervision
4. Accessible pricing: institutional power at retail cost

---

## Technical Innovation: zk-VaR Circuit Deep Dive

### The Challenge
Prove that a proposed trade respects risk limits WITHOUT revealing:
- User's full portfolio positions
- AI model weights or strategy logic
- Historical PnL or account size

### The Solution: Zero-Knowledge Value-at-Risk (zk-VaR)

**Circuit Inputs (Public):**
1. Merkle root of user's portfolio state (hashed positions)
2. Trade proposal (asset, quantity, direction, limit price)
3. User-defined VaR limit (e.g., "max 5% portfolio risk")
4. Proof verification timestamp

**Circuit Inputs (Private / Witness):**
1. Full portfolio positions and cost basis
2. AI model's confidence score and regime detection
3. Historical return distribution (for VaR calculation)
4. Current market volatility

**Circuit Logic (Circom):**
```
1. Reconstruct portfolio from witness, verify Merkle root matches public input
2. Simulate proposed trade execution
3. Calculate portfolio VaR using historical simulation (95% confidence)
4. Assert: calculatedVaR <= userDefinedVaRLimit
5. Output: 1-bit pass/fail signal
```

**Circuit Constraints:** <65,000 (SnarkJS WASM benchmark: <3ms proof gen)

**Proof Output:**
- zk-SNARK proof (π) ~200 bytes
- Public signals: trade ID, VaR limit, pass/fail, timestamp
- Stored on zkSync Era L2 (gas cost: ~$0.05/proof at current rates)

**User Experience:**
1. User proposes trade (or AI suggests trade)
2. 2-3 second delay (proof generation + verification)
3. UI shows: ✅ "Risk proof verified" with green checkmark
4. Trade executes to broker
5. On-chain link: "View proof on zkSync block explorer"

---

## Regulatory Alignment Features

### Human-in-the-Loop (CSA 11-349 Compliance)
**Requirement:** Canadian regulators require meaningful human control over AI trading decisions

**Implementation:**
- **Days 1-30:** User must click "Confirm" for EVERY trade
- **Days 31+:** After 50 successful trades + user opt-in, enable "auto-approve" mode
- **Always:** "Pause All Trading" kill switch visible on every screen
- **Always:** Daily recap email at 6 PM user local time with all trades for review

**Proof Point:** Regulator #1 (CIRO regulator interview) confirmed this satisfies "human-in-the-loop" principle

### Explainability Without Revealing Strategy
**Requirement:** Regulators want to understand "why" AI made decisions

**Implementation:**
- **High-Level Transparency:** "Trade triggered by bullish momentum signal + low volatility regime"
- **Feature Attribution:** Show which market conditions contributed (e.g., "AAPL 50-day MA crossover, VIX <15")
- **Regime Detection:** Display current market state (trending/mean-reverting/high-vol/low-vol)
- **Confidence Score:** Show AI's certainty (e.g., "85% confidence")
- **NOT Revealed:** Exact model weights, neural network architecture, proprietary signals

**Proof Point:** Regulator interviews (3/3) confirmed high-level explanations sufficient, not full parameter transparency needed

### Audit Trail Architecture
**Requirement:** Regulators need ability to reconstruct decisions for investigations

**Implementation:**
- **Event Sourcing:** Every action logged (user login, risk parameter change, trade proposal, trade execution, proof generation)
- **Immutable Storage:** Logs on IPFS (pinned), proof hashes on zkSync Era L2
- **Retention:** 7 years (Canadian securities law requirement)
- **Regulator Access:** API endpoint for CIRO/SEC/ADGM to query specific user/timeframe with warrant
- **User Access:** Full transparency—users see same audit trail as regulators

---

## Roadmap: Solution Evolution

### Phase 1: MVP (Weeks 1-12, Current)
**Focus:** Prove core concept with 50 alpha users, 40 WAST

**Features:**
- SnapTrade multi-broker integration (IBKR, Alpaca, Kraken, Coinbase)
- 2 pre-trained RL policies (PPO, TD3)
- zk-VaR proof engine (8 state variables, <3ms gen)
- ERC-4337 smart wallet
- Progressive caps system
- Paper trading → live with human-in-the-loop

### Phase 2: Scale Retail (Months 4-12)
**Focus:** $3M ARR, 2,000 paid users

**New Features:**
- Custom risk parameter editor
- 5 RL policy library (add RVI-Q, A3C, SAC)
- Options trading support (via IBKR)
- Social features (leaderboards, copy top performers—WITH risk proofs)
- Mobile app (iOS, Android)
- Referral program (3 invite codes per user)

### Phase 3: Enterprise Launch (Months 13-24)
**Focus:** $14M ARR, add fund managers

**New Features:**
- Fund Lite / Fund Growth tiers
- Multi-user RBAC (seats for PM, traders, analysts, compliance)
- Custom model training API
- Regulatory reporting (Form PF, 13F, TRACE)
- Co-location options (AWS ORD1, Equinix NY4)
- White-label branding

### Phase 4: DePIN & Token Launch (Months 25-36)
**Focus:** $30M ARR, decentralize infrastructure

**New Features:**
- $REFIN token TGE (post-Series A)
- DePIN node operator rewards (stake $REFIN, run GPU/data nodes)
- Fee-based buy-back & burn (10bp execution fee → 70% broker rebate, 20% buy-back, 10% treasury)
- Governance DAO (token holders vote on new RL models, risk parameter ranges)
- Proof worker decentralization (zk-proof generation via staked nodes)

### Phase 5: Global & Marketplace (Months 37-48)
**Focus:** $55M ARR, full platform

**New Features:**
- Strategy Marketplace (3rd-party quants publish RL policies, 70/30 revenue split)
- Multi-geo compliance (Canada, USA, UAE, UK, Singapore, Hong Kong)
- Futures & commodities support
- Smart ETF MARL module (multi-asset RL for portfolio construction)
- Institutional custody integration (Fireblocks, BitGo for crypto)

---

## Key Design Principles

1. **Trust Through Mathematics, Not Marketing**
   - Cryptographic proofs > vague "AI safety" claims
   - On-chain audit trail > opaque black box
   - Open-source zk circuits > proprietary "secret sauce"

2. **Sovereignty First**
   - User custody > platform convenience
   - Transparent risk limits > hidden liquidation rules
   - Kill switch > "trust us"

3. **Regulatory by Design, Not Retrofit**
   - Human-in-the-loop from day 1 (not added later under regulatory pressure)
   - Explainability built into AI architecture (not post-hoc rationalization)
   - Audit trail immutable (not editable logs)

4. **Progressive Complexity**
   - Start simple (Starter tier, 1 asset class) → scale to sophisticated (Prime, multi-asset)
   - Paper trading → small caps → full power
   - Pre-trained models → custom model training

5. **Economic Alignment**
   - Flat monthly fee (user success ≠ platform revenue, avoids perverse incentives)
   - Token buy-back ties protocol health to user activity (Phase 4)
   - Stakers earn from infrastructure provision, not speculation (DePIN rewards)

---

## Success Metrics

### Product-Market Fit Signals
- ✅ **40+ WAST** by Week 12 (Weekly Active Safe Traders)
- ✅ **NPS ≥ 50** (currently 64 in alpha)
- ✅ **40%+ retention** W1→W2 (currently 45%)
- ✅ **<3% monthly churn** (typical for financial SaaS: 5-7%)

### Performance Metrics
- **Aggregate User PnL:** ≥60% positive (target)
- **Sharpe Ratio:** ≥2.0 (our 3.1-year backtest: 2.07)
- **Max Drawdown:** <-10% (our backtest: -7.48%)
- **Win Rate:** ≥55%

### Technical Health
- **Proof Generation:** <3ms p95 (critical path)
- **Order-to-Fill Latency:** <150ms p95
- **Uptime:** 99.5%+ (5 nines = $100K+ insurance cost, defer to Phase 2)
- **Broker API Errors:** <1% of calls

---

## Document Control

**Version:** 1.0  
**Last Updated:** November 28, 2025  
**Next Review:** February 28, 2026 (post-alpha)  
**Owner:** Zeshan Ahmad (CEO) + Daniel Oosthuyzen (CTO)  
**Distribution:** Internal (founding team, advisors, investors)

---

**"Trust through transparency. Power through proof."**

*— ReFi.Trading Solution Concepts v1.0*
