# ReFi.Trading Risk Register
**Version:** 1.0  
**Last Updated:** November 28, 2025  
**Owner:** Zeshan Ahmad (CEO)

---

## Executive Summary

This risk register identifies, assesses, and provides mitigation strategies for key risks facing ReFi.Trading during our 0→$55M ARR journey. Risks are categorized by type (Technical, Regulatory, Market, Team, Financial) and prioritized using a Risk Score = Likelihood × Impact (both 1-5 scale).

**Top 3 Risks:**
1. **Regulatory Misclassification** (Score: 20/25) - Token deemed security without proper exemption
2. **Broker API Dependency** (Score: 16/25) - SnapTrade or broker integration failure
3. **AI Explainability Requirements** (Score: 15/25) - Unable to meet regulator transparency standards

---

## Risk Assessment Matrix

### CRITICAL RISKS (Score ≥ 15)

#### R001: Regulatory - Token Misclassification
- **Category:** Regulatory / Legal
- **Description:** $REFIN token classified as security in Canada/USA without proper exemption, requiring prospectus or dealer registration
- **Likelihood:** 4/5 (High - CSA Staff Notice 21-327 suggests likely security)
- **Impact:** 5/5 (Critical - Could halt operations, require expensive registration)
- **Risk Score:** 20/25
- **Current Status:** 🔴 High Risk
- **Mitigation Strategy:**
  - ✅ **Immediate:** Defer token launch until post-Series A (2027)
  - ✅ **Q1 2026:** Engage Canadian securities lawyer ($15-20K) for legal opinion
  - ✅ **Q2 2026:** Apply for Reg D 506(c) exemption if proceeding in USA
  - ✅ **Q3 2026:** Structure token as pure utility (governance + staking only, not profit-sharing)
  - ⏳ **2027:** File exemption or register as restricted dealer if needed
- **Owner:** Zeshan Ahmad (CEO) + External Counsel
- **Review Frequency:** Quarterly
- **Last Review:** November 28, 2025
- **Next Review:** February 28, 2026

#### R002: Technical - Broker API Dependency
- **Category:** Technical / Operational
- **Description:** SnapTrade or underlying broker API (IBKR, Alpaca) experiences extended outage or discontinues service
- **Likelihood:** 4/5 (Medium-High - Third-party dependency, historical Alpaca precedent)
- **Impact:** 4/5 (High - Trading halted, user trust loss, revenue impact)
- **Risk Score:** 16/25
- **Current Status:** 🟡 Medium-High Risk
- **Mitigation Strategy:**
  - ✅ **Architecture:** Multi-broker integration via SnapTrade (IBKR, Alpaca, Kraken, Coinbase)
  - ✅ **Monitoring:** Uptime SLA monitoring per broker, alerts on <99.5% uptime
  - ✅ **Fallback:** Direct IBKR API integration as backup (Week 16-20 roadmap)
  - ⏳ **Contractual:** Negotiate SLA with SnapTrade (99.9% uptime, 4-hour response)
  - ⏳ **Communication:** Automated user notifications on broker-specific outages
- **Owner:** Daniel Oosthuyzen (CTO)
- **Review Frequency:** Monthly
- **Last Review:** November 28, 2025
- **Next Review:** December 28, 2025

#### R003: Regulatory - AI Explainability Requirements
- **Category:** Regulatory / Product
- **Description:** Canadian/UAE regulators require detailed AI model explainability that our black-box RL models cannot provide
- **Likelihood:** 3/5 (Medium - CSA Staff Notice 11-349 emphasizes explainability)
- **Impact:** 5/5 (Critical - Could require model redesign or prohibit AI trading)
- **Risk Score:** 15/25
- **Current Status:** 🟡 Medium Risk
- **Mitigation Strategy:**
  - ✅ **Legal:** Interview validation with CIRO Rep confirmed high-level explanations acceptable
  - ✅ **Product:** Build "Why this trade?" feature showing market regime, signal strength, risk metrics
  - ✅ **Architecture:** Log all model decisions with interpretable features (momentum, volatility, regime)
  - ⏳ **Compliance:** Prepare model explainability documentation for regulators
  - ⏳ **Governance:** DAO votes on model deployments create human oversight layer
- **Owner:** Daniel Oosthuyzen (CTO) + Compliance Counsel
- **Review Frequency:** Quarterly
- **Last Review:** November 28, 2025
- **Next Review:** February 28, 2026

---

### HIGH RISKS (Score 10-14)

#### R004: Market - Insufficient Alpha User Acquisition
- **Category:** Market / Growth
- **Description:** Unable to recruit 50 alpha users or achieve 40 WAST by Week 12
- **Likelihood:** 3/5 (Medium - UAE/GCC market receptive but unproven at scale)
- **Impact:** 4/5 (High - Delays seed close, extends burn, reduces investor confidence)
- **Risk Score:** 12/25
- **Current Status:** 🟡 Medium Risk
- **Mitigation Strategy:**
  - ✅ **Validation:** 18 interviews validated ICP and WTP ($350-500/month)
  - ✅ **Pipeline:** Power-Retail Trader #2's 40-person WhatsApp trading group warm intro
  - ✅ **Distribution:** LinkedIn (3x/week), Reddit AMAs (bi-weekly), TikTok (daily)
  - ⏳ **Partnerships:** Negotiate with Dubai trading communities for bulk intros
  - ⏳ **Incentives:** Early adopter pricing ($150/month first 3 months, then $350)
- **Owner:** Zeshan Ahmad (CEO)
- **Review Frequency:** Weekly during alpha (Weeks 9-12)
- **Last Review:** November 28, 2025
- **Next Review:** December 5, 2025

#### R005: Technical - zk-Proof Generation Latency
- **Category:** Technical / Performance
- **Description:** zk-VaR proof generation exceeds 3ms p95 target, degrading user experience
- **Likelihood:** 3/5 (Medium - Circom circuit complexity with 8 state variables)
- **Impact:** 4/5 (High - Slow trading UX, competitive disadvantage vs robo-advisors)
- **Risk Score:** 12/25
- **Current Status:** 🟡 Medium Risk
- **Mitigation Strategy:**
  - ✅ **Design:** Limit circuit to 8 state variables, <65k constraints
  - ✅ **Tech:** Use SnarkJS with WASM backend for optimal performance
  - ⏳ **Optimization:** Batch multiple trade checks into single proof if >5 trades/min
  - ⏳ **Fallback:** Degrade to non-zk risk checks with warning if proof gen >5ms
  - ⏳ **Hardware:** GPU-accelerated proof generation on server-side (DePIN Phase 3)
- **Owner:** Daniel Oosthuyzen (CTO) + zk-Cryptography Engineer
- **Review Frequency:** Weekly during Phase 1 (Weeks 1-4)
- **Last Review:** November 28, 2025
- **Next Review:** December 5, 2025

#### R006: Financial - Burn Rate Exceeds Runway
- **Category:** Financial / Operational
- **Description:** Development costs exceed $70.5K alpha budget or monthly burn exceeds $14.75K
- **Likelihood:** 2/5 (Low - Conservative budget with 10% buffer)
- **Impact:** 5/5 (Critical - Forces emergency fundraising or team cuts)
- **Risk Score:** 10/25
- **Current Status:** 🟢 Low Risk
- **Mitigation Strategy:**
  - ✅ **Budget:** $70.5K alpha (2.9% of $2.45M seed), $14.75K/month = 20-month runway
  - ✅ **Controls:** Weekly budget reviews, approve all >$5K expenses
  - ✅ **Hiring:** Contractors over FTEs for first 6 months (flexibility)
  - ⏳ **Non-Dilutive:** Apply for Alberta Innovates ($125K), SR&ED tax credits (37% cashback)
  - ⏳ **Revenue:** First paying users Week 9+ provide early revenue signal
- **Owner:** Zeshan Ahmad (CEO)
- **Review Frequency:** Weekly
- **Last Review:** November 28, 2025
- **Next Review:** December 5, 2025

#### R007: Regulatory - "Fully Autonomous AI" Prohibition
- **Category:** Regulatory / Product
- **Description:** Regulators prohibit fully autonomous AI trading without human-in-the-loop per CSA 11-349
- **Likelihood:** 5/5 (Very High - CSA explicitly states this in Staff Notice)
- **Impact:** 2/5 (Low - Architecture already designed for human-in-the-loop)
- **Risk Score:** 10/25
- **Current Status:** 🟢 Low Risk (Already Mitigated)
- **Mitigation Strategy:**
  - ✅ **Product Design:** Require user to click "Confirm" per trade (Days 1-30)
  - ✅ **Progressive Trust:** After 30 days + 50 successful trades, enable auto-approval with daily caps
  - ✅ **Kill Switch:** Mandatory "Pause All Trading" button always visible
  - ✅ **Messaging:** Market as "AI Co-Pilot" not "Fully Autonomous Agent"
  - ✅ **Compliance:** DAO governance fulfills "human oversight" for institutional tier
- **Owner:** Daniel Oosthuyzen (CTO) + Product Team
- **Review Frequency:** Quarterly
- **Last Review:** November 28, 2025
- **Next Review:** February 28, 2026

---

### MEDIUM RISKS (Score 5-9)

#### R008: Market - Incorrect ICP Targeting
- **Category:** Market / Product-Market Fit
- **Description:** Power-retail trader persona not actually the best ICP, leading to high churn
- **Likelihood:** 2/5 (Low - 18 interviews validated ICP strongly)
- **Impact:** 4/5 (High - Wasted GTM spend, delayed PMF)
- **Risk Score:** 8/25
- **Current Status:** 🟢 Low-Medium Risk
- **Mitigation Strategy:**
  - ✅ **Validation:** 18 interviews (10 power-retail, 5 funds, 3 regulators) confirmed pain points
  - ✅ **Cohort Analysis:** Track retention by user segment (experience, account size, geography)
  - ⏳ **Pivot Option:** Fund managers showed high interest (5/5) as backup ICP
  - ⏳ **Feedback Loops:** Weekly alpha user interviews to catch ICP misalignment early
- **Owner:** Zeshan Ahmad (CEO)
- **Review Frequency:** Monthly
- **Last Review:** November 28, 2025
- **Next Review:** December 28, 2025

#### R009: Team - Key Person Dependency
- **Category:** Team / Operational
- **Description:** Daniel (CTO) or Zeshan (CEO) unavailable for extended period (illness, accident)
- **Likelihood:** 1/5 (Very Low - Both healthy, no known risks)
- **Impact:** 5/5 (Critical - Technical/strategic decision-making halts)
- **Risk Score:** 5/25
- **Current Status:** 🟢 Low Risk
- **Mitigation Strategy:**
  - ⏳ **Documentation:** Comprehensive technical docs, decision logs, architecture diagrams
  - ⏳ **Cross-Training:** Daniel trains frontend contractor on zk-proof architecture
  - ⏳ **Succession:** Identify backup technical advisor (Amii.ca mentor network)
  - ⏳ **Insurance:** Key person insurance policy ($1M per founder)
- **Owner:** Zeshan Ahmad (CEO)
- **Review Frequency:** Annually
- **Last Review:** November 28, 2025
- **Next Review:** November 28, 2026

#### R010: Technical - Smart Contract Vulnerability
- **Category:** Technical / Security
- **Description:** ERC-4337 smart wallet or zk-VaR verification contract contains exploitable bug
- **Likelihood:** 2/5 (Low - Using audited Biconomy SDK + SnarkJS)
- **Impact:** 5/5 (Critical - User funds at risk, reputational damage)
- **Risk Score:** 10/25
- **Current Status:** 🟢 Low Risk (Mitigated via Audits)
- **Mitigation Strategy:**
  - ✅ **Libraries:** Use battle-tested Biconomy ERC-4337 SDK (>$500M secured)
  - ⏳ **Audit:** Third-party smart contract audit ($15-25K) before mainnet (Week 16)
  - ⏳ **Bug Bounty:** $10K bug bounty program post-audit
  - ⏳ **Insurance:** Smart contract insurance policy ($100K coverage via Nexus Mutual)
  - ⏳ **Limits:** Progressive caps limit blast radius ($100 → $500 → $5K)
- **Owner:** Daniel Oosthuyzen (CTO)
- **Review Frequency:** Per smart contract deployment
- **Last Review:** November 28, 2025
- **Next Review:** Week 16 (Pre-Audit)

---

## Risk Monitoring Dashboard

| Risk ID | Category | Risk Score | Status | Trend | Owner | Next Review |
|---------|----------|------------|--------|-------|-------|-------------|
| R001 | Regulatory | 20/25 | 🔴 High | → Stable | Zeshan | Feb 28, 2026 |
| R002 | Technical | 16/25 | 🟡 Med-High | → Stable | Daniel | Dec 28, 2025 |
| R003 | Regulatory | 15/25 | 🟡 Medium | ↓ Improving | Daniel | Feb 28, 2026 |
| R004 | Market | 12/25 | 🟡 Medium | → Stable | Zeshan | Dec 5, 2025 |
| R005 | Technical | 12/25 | 🟡 Medium | → Stable | Daniel | Dec 5, 2025 |
| R006 | Financial | 10/25 | 🟢 Low | ↓ Improving | Zeshan | Dec 5, 2025 |
| R007 | Regulatory | 10/25 | 🟢 Low | ✅ Mitigated | Daniel | Feb 28, 2026 |
| R008 | Market | 8/25 | 🟢 Low-Med | → Stable | Zeshan | Dec 28, 2025 |
| R009 | Team | 5/25 | 🟢 Low | → Stable | Zeshan | Nov 28, 2026 |
| R010 | Technical | 10/25 | 🟢 Low | ↓ Improving | Daniel | Week 16 |

**Trend Legend:**
- ↑ Worsening: Risk increasing
- → Stable: Risk unchanged
- ↓ Improving: Risk decreasing
- ✅ Mitigated: Risk effectively controlled

---

## Risk Response Protocols

### CRITICAL RISK TRIGGERS (Immediate Action Required)

**If R001 (Token Misclassification) materializes:**
1. Immediately pause all token-related development and marketing
2. Emergency legal consultation within 24 hours
3. Assess registration requirements and timelines
4. Communicate transparently with investors and users
5. Pivot to pure SaaS model if registration infeasible

**If R002 (Broker API Failure) materializes:**
1. Activate status page with real-time updates
2. Switch affected users to backup broker (IBKR direct if SnapTrade down)
3. Freeze new user onboarding until resolution
4. Communicate ETA and workarounds to users
5. Accelerate direct IBKR integration roadmap

**If R003 (AI Explainability) materializes:**
1. Immediately engage regulatory counsel
2. Prepare detailed model documentation and explainability reports
3. Implement enhanced "Why this trade?" UI feature
4. Consider simplified model architecture if needed
5. Apply for regulatory sandbox for experimental testing

---

## Risk Review Cadence

- **Weekly:** R004, R005, R006 (during alpha sprint Weeks 1-12)
- **Monthly:** R002, R008 (operational risks)
- **Quarterly:** R001, R003, R007 (regulatory risks)
- **Annually:** R009 (team risks)
- **Per Event:** R010 (security audits)

---

## Document Control

- **Version History:**
  - v1.0 (Nov 28, 2025): Initial risk register based on 18 validated interviews
- **Next Update:** December 28, 2025 (post-Week 4 sprint review)
- **Owner:** Zeshan Ahmad (CEO)
- **Approvers:** Daniel Oosthuyzen (CTO), Board of Directors
- **Distribution:** Internal (founding team, advisors, investors)
