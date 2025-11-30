# ReFi.Trading - Complete GTM & Validation Repository

**Non-Custodial Algorithmic Trading Platform**  
**Status:** Post-Validation → Alpha Build (January 2026)  
**Stage:** Seed Round ($2.45M on $15M post-money)  
**Market:** UAE/GCC Power-Retail Traders (Initial Focus)

---

## 🎯 Validation Results Summary

**60-Day Sprint Completed:** September 1, 2025 - November 30, 2025

| Experiment | Target | Result | Status |
|-----------|--------|--------|--------|
| **1. Broker Connection** | ≥60% | **78%** | ✅ Strong Validation |
| **2. Non-Custodial Trust** | ≥70% + 2pt lift | **82% / +2.8pt** | ✅ Strong Validation |
| **3. Paper-to-Live** | ≥60% | **68%** | ✅ Good Validation |

**Overall: 3/3 Experiments Validated | Confidence: 🟢 HIGH | Decision: GO**

---

## 📁 Repository Structure

```
refi-complete/
│
├── 00-validation/                    # Core validation experiments
│   ├── hypothesis-prioritization.md  # 25 assumptions ranked by risk
│   ├── experiment-plan.md            # 3 detailed experiments
│   ├── success-metrics.md            # North Star (WAST) + AARRR
│   ├── smoke-test-plan.md            # Landing page validation
│   ├── validation-sprint-plan.md     # 60-day execution guide
│   ├── experiment-results-log.md     # Findings documentation
│   └── updated-roadmap.md            # 12-week alpha build plan
│
├── 01-discovery/                     # User research & interviews
│   ├── interview-guide.md            # Interview script
│   ├── interviews/                   # 18 full interview transcripts
│   │   ├── power-retail-01.md
│   │   ├── power-retail-02.md
│   │   ├── power-retail-03.md
│   │   ├── power-retail-04.md
│   │   ├── power-retail-05.md
│   │   ├── power-retail-06.md
│   │   ├── power-retail-07.md
│   │   ├── power-retail-08.md
│   │   ├── power-retail-09.md
│   │   ├── power-retail-10.md
│   │   ├── fund-manager-01.md
│   │   ├── fund-manager-02.md
│   │   ├── fund-manager-03.md
│   │   ├── fund-manager-04.md
│   │   ├── fund-manager-05.md
│   │   ├── regulator-01-ciro-canada.md
│   │   ├── regulator-02-sec-usa.md
│   │   └── regulator-03-adgm-uae.md
│   └── synthesis/
│       ├── key-insights.md           # Top 10 insights across interviews
│       ├── icp-v2.md                 # Data-driven ICP update
│       └── patterns-analysis.md      # Themes & patterns
│
├── 00-foundation/                    # Strategy & positioning
│   ├── initial-problem-statement.md  # Validated problem
│   ├── icp-draft-1.md                # Initial customer profiles
│   ├── regulatory-landscape.md       # Canada, USA, UAE analysis
│   ├── risk-register.md              # Top 15 risks + mitigations
│   └── team-contract.md              # Roles & decision framework
│
├── 03-ideation/                      # Solution design
│   ├── solution-concepts.md          # Architecture options
│   ├── mvp-definition.md             # MVP scope (SnapTrade + zk-VaR)
│   ├── feature-prioritization.md     # MoSCoW framework
│   └── regulatory-alignment-notes.md # Compliance by jurisdiction
│
├── 04-prototyping/                   # Technical specs
│   ├── technical-decisions.md        # Tech stack rationale
│   ├── api-contracts.md              # API specifications
│   ├── data-flow-diagrams.md         # System architecture
│   ├── security-controls.md          # SIWE + RBAC + CSP
│   └── prototype-changelog.md        # Iteration log
│
├── 05-delivery/                      # Go-to-market assets
│   ├── product-roadmap.md            # 12-week alpha plan
│   ├── pricing-and-packaging.md      # Tiered model ($150-$995/mo)
│   ├── demo-script.md                # 5-minute demo flow
│   ├── pitch-deck.md                 # Seed investor deck outline
│   ├── sales-playbook.md             # Alpha recruitment strategy
│   ├── compliance-brief.md           # Regulatory positioning
│   └── reflection.md                 # Lessons learned
│
├── 06-go-to-market/                  # Launch strategy
│   ├── positioning-doc.md            # "Wall Street AI, Radically Accessible"
│   ├── messaging-guide.md            # Value props by segment
│   └── launch-plan.md                # Alpha Wave 1 (50 users)
│
├── 07-experiments/                   # Experiment artifacts
│   ├── experiment-01-broker-connection/
│   │   ├── landing-page-mockup.png
│   │   ├── posthog-dashboard.md
│   │   └── results-summary.md
│   ├── experiment-02-non-custodial-trust/
│   │   ├── video-script.md
│   │   ├── survey-questions.md
│   │   └── results-summary.md
│   └── experiment-03-paper-to-live-transition/
│       ├── dashboard-mockup.png
│       ├── email-sequence.md
│       └── results-summary.md
│
└── resources/
    ├── references.md                 # Key sources & citations
    ├── tools-we-use.md               # Tech stack
    └── meeting-notes/                # Weekly sync notes
        ├── 2025-12-02-validation-kickoff.md
        ├── 2025-12-16-mid-sprint-review.md
        ├── 2026-01-13-experiment-3-results.md
        └── 2026-01-30-go-decision.md
```

---

## 🔑 Key Insights from Validation

### What Worked (Top 5)

1. **Non-Custodial Messaging Resonated Strongly**
   - 82% comprehension rate (target: 70%)
   - +2.8pt trust lift post-video (target: +2.0pt)
   - Quote: *"After FTX, I'll never give my keys to anyone again. This is exactly what I need."* - Power-Retail Trader #2 (UAE, $85K account)

2. **Progressive Caps Reduced Fear**
   - 68% paper → live conversion (target: 60%)
   - Starting at $100 felt "safe" even for $100K+ accounts
   - 22% requested caps increase after Day 3 (strong engagement)

3. **Broker Connection via SnapTrade Was Smooth**
   - 78% connected successfully (target: 60%)
   - IBKR most popular (60%), Alpaca (25%), Kraken (15%)
   - <10s OAuth flow (no friction)

4. **UAE/GCC Market Highly Receptive**
   - 85% of UAE users completed paper trading vs. 60% North America
   - "ADGM regulatory clarity" cited by 8/10 UAE respondents
   - Higher account sizes ($50K+ avg vs. $25K North America)

5. **zk-Proof "Safety Checkmark" Was Sufficient**
   - Users didn't need to understand math, just trust the green ✓
   - "Cryptographic proof" sounded more trustworthy than "AI risk check"
   - 0 users asked about circuit details (simplicity worked)

### What Struggled (Top 3)

1. **Email Frequency Felt Pushy (Experiment 3)**
   - 3 follow-ups in 7 days = "too much"
   - Recommended: 1 email on Day 8 only
   - Open rates dropped 40% → 15% by Email 3

2. **$100 Cap Felt "Too Small" for Large Accounts**
   - 6/10 users with $50K+ accounts wanted $250-500 start
   - Recommendation: Tiered caps by account size
   - <$10K → $100, $10K-$50K → $250, >$50K → $500

3. **7-Day Paper Trading Felt Rushed for Novices**
   - Intermediate traders (3-5 years) wanted 14 days
   - Power-retail (5+ years) were fine with 7 days
   - Recommendation: Default 14 days, opt-in 7-day fast track

### Surprising Findings (Top 3)

1. **Fund Managers Very Interested (Unexpected Segment)**
   - 5/5 sub-$1B fund managers wanted white-label version
   - Willing to pay $5K-10K/month enterprise tier
   - Quote: *"We can't afford Bloomberg + 3 data scientists. This is a 10x cost saver."* - Fund Manager #1 ($450M AUM)

2. **Regulators Were More Open Than Expected**
   - All 3 regulators said "non-custodial + proofs = right direction"
   - Canadian CIRO: "Partner model via SnapTrade is compliant"
   - UAE ADGM: "We encourage this, apply for RegLab sandbox"
   - US SEC: "Monitor, don't over-promise AI capabilities"

3. **Traders Wanted Social Features**
   - "Show me what other traders with my risk profile are doing"
   - "Leaderboard would make me more engaged"
   - "Let me follow top performers" (like eToro)
   - Not in MVP, but strong signal for future

---

## 🎓 Updated ICP (Post-Validation)

**Primary Target: UAE/GCC Power-Retail Traders**

| Attribute | Profile |
|-----------|---------|
| **Experience** | 5-10 years active trading (power-retail) |
| **Account Size** | $50K-$250K (sweet spot: $85K median) |
| **Risk Profile** | Moderate (5% VaR comfortable) |
| **Age** | 32-48 years old |
| **Tech-Savviness** | High (familiar with APIs, wallets) |
| **Current Tools** | TradingView + Alpaca + Excel |
| **Pain Points** | 1) Emotional trading, 2) Time-intensive, 3) No institutional tools |
| **Motivations** | Consistency, time savings, "Wall Street edge" |
| **Geography** | Dubai, Abu Dhabi, Doha, Riyadh |
| **Income** | $150K-$500K annual |

**Secondary Target: Sub-$1B Fund Managers (Emerging)**

| Attribute | Profile |
|-----------|---------|
| **AUM** | $100M-$800M |
| **Team Size** | 3-8 people (lean) |
| **Current Gap** | Can't afford $1M+ quant infrastructure |
| **Willingness to Pay** | $5K-10K/month + performance fee |
| **Use Case** | Institutional-grade RL without hiring PhDs |

---

## 💰 Business Model (Post-Validation)

### Retail Tiers (Primary Revenue)

| Tier | Price/Month | Features | Target User |
|------|-------------|----------|-------------|
| **Starter** | $150 | 1 asset class, 1 RL policy, 5K API calls/day | Experimenting power-retail |
| **Pro** | $350 | Multi-asset, 5 policies, VaR dashboard, 50K calls/day | Serious power-retail |
| **Prime** | $995 | Unlimited, low-latency, Slack support | Professional traders |

### Enterprise (Emerging Opportunity)

| Tier | Price/Year | Features | Target User |
|------|------------|----------|-------------|
| **Fund Lite** | $50K + 10bp | White-label, 1 strategy | Sub-$500M funds |
| **Fund Growth** | $120K + 8bp | Multi-strategy, custom models | $500M-$1B funds |

### Token Economics (Future)

- **$REFIN Token:** Utility + governance
- **Execution Fee:** 10 bps → 70% broker rebate, 20% buy-back, 10% treasury
- **Staking Rewards:** For DePIN node operators (post-Series A)

---

## 📊 Metrics Summary (Post-Validation)

### Validation Sprint Results

| Metric | Target | Actual | Status |
|--------|--------|--------|--------|
| **Broker Connect Rate** | ≥60% | 78% | ✅ +30% |
| **Comprehension Rate (zk-proofs)** | ≥70% | 82% | ✅ +17% |
| **Trust Lift** | ≥+2.0pt | +2.8pt | ✅ +40% |
| **Paper-to-Live Conversion** | ≥60% | 68% | ✅ +13% |
| **NPS (Paper Trading)** | ≥50 | 64 | ✅ +28% |

### Projected Alpha Metrics (12 Weeks)

| Metric | Week 4 | Week 8 | Week 12 |
|--------|--------|--------|---------|
| **Total Signups** | 20 | 50 | 50 |
| **WAST** | 8 | 25 | 42 |
| **Avg Trades/Week** | 2.5 | 4.0 | 5.5 |
| **Platform Uptime** | 99.5% | 99.7% | 99.9% |
| **NPS** | 55 | 60 | 65 |

---

## 🚀 Next Steps (Post-Validation)

**Immediate (Week of Feb 3, 2026):**
- [x] Validation sprint completed (Jan 30, 2026)
- [x] GO decision made (3/3 experiments validated)
- [ ] Hire frontend contractor (starting Feb 5)
- [ ] Hire cryptography specialist for zk-VaR (starting Feb 10)
- [ ] SnapTrade integration kickoff (Feb 5)

**Phase 1: Core Infrastructure (Feb 3 - Mar 2, 2026)**
- [ ] SnapTrade multi-broker integration (IBKR, Alpaca, Kraken)
- [ ] zk-VaR proof engine (Circom circuit, p95 <3ms)
- [ ] ERC-4337 smart wallet integration
- [ ] Security audit (internal)

**Phase 2: Alpha UI Build (Mar 3 - Mar 30, 2026)**
- [ ] Landing page + SIWE auth
- [ ] Paper trading dashboard
- [ ] Live trading dashboard + progressive caps
- [ ] Email automation (Resend)

**Phase 3: Alpha Wave 1 Launch (Mar 31 - Apr 28, 2026)**
- [ ] Recruit 50 alpha users (30 UAE/GCC, 20 other)
- [ ] 7-day paper trading → live transition
- [ ] Weekly support calls with Zeshan (CEO)
- [ ] Hit 40+ WAST by Week 12

**Seed Close (Target: April 2026)**
- [ ] Update investors with alpha traction
- [ ] Close remaining $1.2M seed commitments
- [ ] Use alpha data to validate $15M post-money valuation

---

## 📚 Key Documents

**For Investors:**
- [Pitch Deck Outline](05-delivery/pitch-deck.md)
- [Product Roadmap](05-delivery/product-roadmap.md)
- [Pricing & Packaging](05-delivery/pricing-and-packaging.md)
- [Compliance Brief](05-delivery/compliance-brief.md)

**For Product Team:**
- [Technical Decisions](04-prototyping/technical-decisions.md)
- [API Contracts](04-prototyping/api-contracts.md)
- [Security Controls](04-prototyping/security-controls.md)
- [MVP Definition](03-ideation/mvp-definition.md)

**For GTM Team:**
- [Positioning Document](06-go-to-market/positioning-doc.md)
- [Messaging Guide](06-go-to-market/messaging-guide.md)
- [Sales Playbook](05-delivery/sales-playbook.md)
- [Launch Plan](06-go-to-market/launch-plan.md)

---

## 🧪 Experiments Repository

All experiment artifacts (landing pages, survey questions, dashboard mockups, results) are preserved in:
- `/07-experiments/experiment-01-broker-connection/`
- `/07-experiments/experiment-02-non-custodial-trust/`
- `/07-experiments/experiment-03-paper-to-live-transition/`

---

## 👥 Team

- **Zeshan Ahmad** - CEO, Product & GTM
- **Daniel Oosthuyzen** - CTO, Quant & Systems
- **[Hiring]** - Frontend Lead (starting Feb 2026)
- **[Hiring]** - zk-Cryptography Engineer (starting Feb 2026)

---

## 📞 Contact

- **Website:** https://refi.trading
- **Email:** investors@refi.trading
- **Alpha Application:** [Google Form Link]
- **LinkedIn:** https://linkedin.com/company/refi-trading
- **Twitter:** https://x.com/refitrading
- **Discord:** https://discord.gg/dQtUucQggz

---

**Status:** 🟢 ACTIVE - Building Alpha MVP  
**Last Updated:** November 30, 2025  
**Next Milestone:** SnapTrade Integration Complete (March 2, 2026)

---

*This repository contains the complete validation journey, user research, and go-to-market strategy for ReFi.Trading's non-custodial algorithmic trading platform.*
