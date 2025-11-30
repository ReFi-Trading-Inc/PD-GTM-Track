# Interview Transcript: Fund Manager #01

**Participant:** Fund Manager #1
**Title:** Founder & Portfolio Manager
**Date:** September 18, 2025  
**Duration:** 52 minutes  
**Location:** Singapore (Video call)  
**Interviewer:** Zeshan Ahmad (CEO)  
**Stage:** Discovery / Market Expansion

---

## Participant Profile

| Attribute | Details |
|-----------|---------|
| **AUM** | $450 million |
| **Strategy** | Long/short equity (quantitative momentum + fundamental overlay) |
| **Team Size** | 6 people (PM, 2 analysts, trader, ops, IR) |
| **Strategy** | Quantitative momentum + fundamental overlay |
| **Location** | Singapore (MAS-licensed fund) |
| **Experience** | 15 years (Goldman Sachs prop trading → started fund 2018) |
| **Age** | 42 |
| **Education** | BS Computer Science, MBA |

---

## Interview Summary

**Key Quote:**  
> *"We're too small to afford a $1M+ quant infrastructure, but too sophisticated for off-the-shelf retail tools. You're filling a massive gap. If you can offer this as a white-label enterprise product, I'd pay $5-10K/month easily. It's a 10x cost savings versus building it ourselves."*

**Validation Insights:**
- ✅ **UNEXPECTED:** Strong interest from sub-$1B fund managers (not our target)
- ✅ Enterprise/white-label model is highly attractive ($5-10K/month willingness)
- ✅ "Institutional infrastructure for mid-market funds" is a real pain point
- ⚠️ Needs: Multi-user RBAC, audit trails, regulatory reporting
- ⚠️ Sales cycle will be longer (6-12 months), needs compliance review

**ICP Fit:** 🟡 Secondary Market (not MVP target, but strong future opportunity)

---

## Full Transcript

**[00:00] Introduction & Fund Overview**

**Zeshan:** Thanks for making time. I know you're incredibly busy managing the fund. Before we talk about ReFi.Trading, can you give me an overview of your fund? What's your investment strategy?

**Fund Manager #1:** Sure. We're a long/short equity fund. We're quantitatively driven—about 70% systematic, 30% discretionary overlay. Our edge is momentum + quality factors. We're looking for stocks with strong price momentum backed by improving fundamentals—earnings growth, margins, free cash flow.

**Zeshan:** What's your AUM?

**Fund Manager #1:** Right now, $450 million. We launched in 2018 with $50 million. We've grown steadily—mostly institutional LPs now. Pension funds, family offices, a few high-net-worth individuals.

**Zeshan:** And team size?

**Fund Manager #1:** Six of us. Me as PM, two analysts who do fundamental research, one trader who executes, one ops person who handles admin and compliance, and one IR person who manages LP relationships. Very lean.

**[05:34] Current Tech Stack & Pain Points**

**Zeshan:** Walk me through your current trading infrastructure. What tools are you using?

**Fund Manager #1:** [Laughs] It's a Frankenstein setup. We use Bloomberg terminals—that's $2,500 per month per seat, so $15K/month just for data. We have a proprietary Python backtesting framework I built back in 2019—it works, but it's brittle. Every time we want to add a new data source or test a new factor, I have to rewrite code.

For execution, we use Interactive Brokers Trader Workstation. Our trader manually enters orders based on signals from the Python system. It's not fully automated because... honestly, we never had the resources to build an execution algo.

**Zeshan:** So there's no automation between signal generation and execution?

**Fund Manager #1:** Correct. The Python system generates a CSV every morning: "Buy 500 AAPL at market, Sell 300 TSLA at limit $180," etc. Our trader reviews it, maybe adjusts a few orders based on pre-market action, then manually places them in TWS. It's slow. And it introduces human error—typos, missed orders.

**Zeshan:** Have you thought about automating that?

**Fund Manager #1:** Constantly. But here's the problem: to build a production-grade execution system, I'd need to hire a quant developer—probably $150K-$200K salary. Then we'd need to maintain it, debug it, handle edge cases. For a fund our size, that's a huge investment. We're at this awkward middle ground: too big for retail tools, too small for institutional infrastructure.

**[12:28] The "Awkward Middle" Problem**

**Zeshan:** Tell me more about that "awkward middle." What do you mean?

**Fund Manager #1:** There's a massive gap in the market. If you're a $10 billion fund, you hire a team of 10 PhDs, build custom infrastructure, and it's fine. If you're a retail trader with $50K, you use TradingView and manually trade. But what if you're a $200-800 million fund? You can't afford the $10M+ it takes to build institutional-grade systems, but you're too sophisticated for retail tools.

**Zeshan:** What would "institutional-grade" look like for you?

**Fund Manager #1:** A few things:

One: **Automated signal generation**—backtesting, factor research, walk-forward validation. Ideally using machine learning, not just linear factors.

Two: **Automated execution**—the system generates signals, checks risk limits, and routes orders to the broker without human intervention.

Three: **Compliance and audit trails**—every decision logged, every risk check documented. When the MAS (Monetary Authority of Singapore) audits us, I can hand them a report.

Four: **Multi-user access**—my analysts can research and backtest, but only I can approve trades. Role-based access control.

**Zeshan:** What are you paying now for your current setup?

**Fund Manager #1:** Let me add it up. Bloomberg: $180K/year. Data feeds (FactSet, Quandl): $40K/year. Cloud compute for backtesting (AWS): $10K/year. IBKR commissions: $15K/year. That's $245K/year just for infrastructure. Plus my time maintaining the Python system—probably 10 hours a week, which is $100K/year of opportunity cost. So all-in, we're spending $350K/year.

**Zeshan:** And if you could replace that with a single platform at $5K/month?

**Fund Manager #1:** [Pauses] That's $60K/year. A $290K savings. That would be massive. We could use that to hire another analyst or return it to LPs as lower fees.

**[22:15] Introducing ReFi.Trading's Enterprise Model**

**Zeshan:** Let me describe what we're building—initially for retail, but I'm realizing there might be a fund version. We use reinforcement learning to generate trade signals. Before every trade, we generate a cryptographic proof that it's within your risk limits—VaR caps, position limits, leverage. The system then auto-executes via broker APIs. Everything is logged on-chain for audit purposes.

**Fund Manager #1:** [Leans forward] Keep going.

**Zeshan:** For funds, we'd offer a white-label version. You'd get your own branded instance—"Fund Manager #1's firm Quant Engine powered by ReFi." Multi-user RBAC: your analysts can backtest, your trader can preview orders, but only you can approve live trading. All decisions are logged with timestamps, user IDs, and cryptographic proofs. When MAS audits you, you export a CSV with full lineage.

**Fund Manager #1:** This is exactly what we need. What's the pricing?

**Zeshan:** We're still figuring it out, but for funds, we're thinking base fee of $5K/month, plus a small percentage of AUM—maybe 5 basis points. For you at $450M AUM, that's $5K/month + $18.75K/year in performance fees = ~$78K/year all-in.

**Fund Manager #1:** [Nods] That's 78% cheaper than our current setup. And we'd get better technology—machine learning instead of linear factors. This is a no-brainer.

**[28:40] Regulatory and Compliance Needs**

**Zeshan:** One concern: regulatory. You're MAS-licensed in Singapore. Would using our platform create any issues?

**Fund Manager #1:** Good question. MAS cares about a few things: custody, conflicts of interest, and operational risk.

**Custody:** If you're non-custodial—we keep our assets at our prime broker, you just send trade instructions—that's fine. You're a technology vendor, not a custodian.

**Conflicts of interest:** If you're trading against us or front-running our orders, that's a problem. But if you're not a broker-dealer, you don't have access to our order flow. So no conflict.

**Operational risk:** MAS will ask, "What happens if ReFi.Trading goes down?" We'd need a backup plan—maybe a kill switch to disable algo trading and revert to manual. But that's manageable.

**Zeshan:** We'd absolutely provide a kill switch. And since it's non-custodial, worst case, you just stop using our platform and go back to manual trading. Your capital is always at your prime broker.

**Fund Manager #1:** Right. That's the beauty of non-custodial. It's a nice-to-have, not a must-have. If you shut down tomorrow, we don't lose capital—we just lose the technology. That's acceptable risk.

**[34:50] Feature Requests for Enterprise Version**

**Zeshan:** If we built this for funds, what would be your top 3 feature requests?

**Fund Manager #1:** One: **Custom model training**. I don't want to use your generic RL model—I want to train it on our proprietary data and factors. Give me an SDK or API where I can upload our data, configure the reward function, and train a custom model.

**Zeshan:** That's doable. We'd probably charge extra for custom models—maybe $10K one-time setup fee.

**Fund Manager #1:** Fine. Worth it.

**Fund Manager #1:** Two: **Multi-asset support**. We trade US equities, but we're expanding into Europe and Asia. I need to route orders to different brokers—Interactive Brokers for US, maybe Saxo Bank for Europe. Can your platform handle multi-broker routing?

**Zeshan:** Yes. We're integrating with SnapTrade, which supports multiple brokers. You could connect IBKR for US, Saxo for Europe, all from one platform.

**Fund Manager #1:** Perfect.

**Fund Manager #1:** Three: **Regulatory reporting**. Give me a one-click button that exports all trades, risk checks, and audit logs in a format that MAS or the SEC accepts. Bonus points if it's pre-formatted for Form PF or 13F filings.

**Zeshan:** That's a great idea. We could build report templates for common filings. Would you pay extra for that?

**Fund Manager #1:** Absolutely. Regulatory compliance is a huge pain. If you save me 10 hours a quarter on Form PF, that's worth $1K/year.

**[42:30] Competitive Landscape & Alternatives**

**Zeshan:** Are there other platforms you've looked at? QuantConnect, Alpaca, etc.?

**Fund Manager #1:** I've looked at everyone.

**QuantConnect:** Great for backtesting, but not a production system. It's a research environment. I'd still need to build my own execution layer.

**Alpaca:** Retail-focused. No RBAC, no audit trails, no white-label. Not serious for a fund.

**Bloomberg AIM (Automated Investment Manager):** This is the closest to what you're describing. But it's $100K+/year, and it's Bloomberg—clunky, legacy tech. Also, it's rule-based, not machine learning.

**Building in-house:** We'd need to hire 2-3 engineers, spend 12-18 months, and budget $500K+. That's the nuclear option.

**Zeshan:** So if we can offer Bloomberg AIM functionality at $5K/month with better tech...

**Fund Manager #1:** You'd have every sub-$1B fund manager beating down your door. There are thousands of funds in our size range globally. We're all stuck in the same awkward middle.

**[48:15] Go-to-Market for Funds**

**Zeshan:** If we decided to pursue this market, how would we reach funds like yours?

**Fund Manager #1:** A few channels:

**One:** Prime brokers. IBKR, Goldman, Morgan Stanley—they have relationships with thousands of funds. If you partner with them, they can introduce you. Maybe the broker even subsidizes your platform because it generates more trading volume for them.

**Two:** Fund administrator networks. Funds outsource back-office to admins like SS&C, Citco, Apex. If you integrate with their systems—reporting, reconciliation—they'll refer you.

**Three:** Industry conferences. CFA Institute events, AIMA (Alternative Investment Management Association), stuff like that. Set up a booth, give a demo, collect business cards.

**Four:** Direct outreach. You could scrape the SEC's Form ADV filings—every RIA has to disclose their AUM. Filter for funds with $100M-$1B AUM, cold email them. I'd respond to a well-crafted email about this.

**Zeshan:** That's super helpful. One last question: what's your buying process? If we launched tomorrow, how long before you'd sign a contract?

**Fund Manager #1:** [Laughs] Good question. For a fund, it's not like a retail SaaS where I swipe my credit card. We'd need to:

**One:** Internal evaluation. I'd test it for 30-60 days in paper trading. Make sure it works, that the RL model is sound.

**Two:** Compliance review. Our compliance officer (who's also our ops person) would review your terms, privacy policy, security. Maybe ask for a SOC 2 audit report.

**Three:** Legal review. Our lawyer would review the contract. Any indemnification clauses, liability limits, IP ownership.

**Four:** Operational due diligence. We'd want to visit your office (or Zoom), meet the team, understand your business continuity plan.

All-in, that's probably 3-6 months from first demo to signed contract. Faster if you already have other fund clients as references.

**Zeshan:** So the sales cycle is longer, but the contract value is higher.

**Fund Manager #1:** Exactly. $5-10K/month, 12-month contracts, low churn once we're live. It's a very different model than $150/month retail with high churn.

**[52:00] Closing**

**Zeshan:** This was incredibly valuable. You've given us a lot to think about. If we build an enterprise version, would you want to be a design partner?

**Fund Manager #1:** 100%. I'd co-develop it with you. Give you feedback, help with prioritization, even introduce you to other fund managers in my network. If you build this, I'm in.

**Zeshan:** Amazing. I'll keep you updated on our progress. Thanks again.

**Fund Manager #1:** My pleasure. Good luck.

---

## Key Takeaways

### ✅ Emerging Opportunity: Sub-$1B Funds

1. **Massive Underserved Market**
   - "Awkward middle" between retail tools and institutional infrastructure
   - $100M-$800M AUM range (thousands of funds globally)
   - Current spend: $250-500K/year on fragmented tools
   - Willing to pay: $5-10K/month for unified platform

2. **White-Label Model is Attractive**
   - Branded as their own ("Fund Manager #1's firm Quant Engine")
   - Builds trust with LPs
   - Differentiates them from competitors

3. **10x Cost Savings**
   - Current: $350K/year (Bloomberg, data, cloud, commissions)
   - ReFi.Trading: $60-80K/year (base fee + AUM fee)
   - Savings can fund additional analyst or reduce LP fees

4. **Regulatory Structure Works for Funds**
   - Non-custodial = low regulatory risk
   - Technology vendor classification (not broker-dealer)
   - Need backup/kill switch for operational risk

### ⚠️ Enterprise Requirements (Not in MVP)

1. **Multi-User RBAC**
   - Analysts: Backtest & research
   - Traders: Preview orders
   - PM: Approve & execute
   - Compliance: Audit trails only

2. **Custom Model Training**
   - Upload proprietary data
   - Configure reward function
   - Train bespoke RL models
   - Willing to pay $10K+ setup fee

3. **Multi-Broker/Multi-Asset**
   - IBKR for US equities
   - Saxo Bank for Europe
   - Prime broker for futures
   - Single platform, multiple venues

4. **Regulatory Reporting**
   - One-click exports (Form PF, 13F, etc.)
   - Pre-formatted for SEC/MAS
   - Audit trail with timestamps + user IDs
   - SOC 2 audit report (builds trust)

### 📊 Business Model for Funds

| Component | Pricing | Annual Revenue (per fund) |
|-----------|---------|---------------------------|
| **Base Fee** | $5K/month | $60K |
| **AUM Fee** | 5 bps on $450M | $22.5K |
| **Custom Model** | $10K one-time | $10K (Year 1 only) |
| **Regulatory Module** | $1K/year | $1K |
| **Total (Year 1)** | - | **$93.5K** |
| **Total (Year 2+)** | - | **$83.5K** |

**10 Funds = $835K ARR** (vs. 50 retail users at $350/mo = $210K ARR)

**LTV:CAC Ratio:**
- Retail: 6-month payback, high churn (20%/year) → LTV ~$1,800
- Enterprise: 6-month sales cycle, low churn (5%/year) → LTV ~$800K

### 🎯 ICP for Enterprise (Future)

| Attribute | Profile |
|-----------|---------|
| **AUM** | $100M-$800M (sweet spot: $300-500M) |
| **Strategy** | Quantitative or quant-overlay |
| **Team Size** | 3-8 people (lean) |
| **Current Pain** | Fragmented tools, can't afford $1M+ infrastructure |
| **Willingness to Pay** | $5-10K/month base + 5 bps AUM |
| **Decision Maker** | Founder/PM (sometimes CTO if larger) |
| **Sales Cycle** | 3-6 months (due diligence, compliance, legal) |
| **Geography** | Global (Singapore, US, Europe, UAE) |

### 🚀 GTM Strategy for Funds (Phase 2)

**Channel 1: Prime Broker Partnerships**
- IBKR, Goldman, Morgan Stanley
- Mutual benefit: more trading volume
- Potential: Broker subsidizes platform (lowers cost to funds)

**Channel 2: Fund Administrator Integrations**
- SS&C, Citco, Apex
- Integrate reporting & reconciliation
- Admins refer funds to us

**Channel 3: Direct Outreach**
- Scrape SEC Form ADV (public data)
- Filter: $100M-$1B AUM, quant strategies
- Cold email with case study (Fund Manager #1's firm as reference)

**Channel 4: Industry Events**
- CFA Institute, AIMA conferences
- Booth + demo
- Collect leads, follow up

### ⏱️ Timeline

**Not for MVP (Q1 2026):** Focus on retail first, validate core tech

**Phase 2 (Q3-Q4 2026):** After retail alpha succeeds
- Build enterprise features (RBAC, custom models, reporting)
- Sign 3-5 pilot funds (Fund Manager #1's firm as design partner)
- Validate willingness to pay at $5-10K/month

**Phase 3 (2027):** Scale enterprise
- Hire enterprise sales rep
- Partner with prime brokers
- Target: 20 funds = $1.5-2M ARR

---

## Recommended Actions

| Priority | Action | Owner | Timeline |
|----------|--------|-------|----------|
| **P2** | Document fund requirements (RBAC, custom models, reporting) | Zeshan | Q2 2026 |
| **P2** | Keep Fund Manager #1 warm (quarterly check-ins) | Zeshan | Ongoing |
| **P2** | Scrape SEC Form ADV for sub-$1B funds | Ops | Q2 2026 |
| **P2** | Reach out to 5 similar funds for validation | Zeshan | Q2 2026 |
| **P3** | Build enterprise roadmap (post-retail MVP) | Product | Q3 2026 |

**Note:** Do NOT pursue funds until retail MVP is validated (Q1-Q2 2026). This is a future opportunity, not a distraction from core focus.

---

## Interviewer Notes

**Surprising Finding:**
- We did NOT expect fund managers to be interested
- Fund Manager #1 found us (mutual connection), not targeted outreach
- This validates a massive adjacent market ($100M-$1B AUM funds)

**Strategic Implications:**
- Retail-first remains correct path (faster sales cycle, validate tech)
- But fund opportunity is 10x larger revenue per customer
- Could become primary revenue driver by Series A (2027)
- Need to design MVP with "enterprise upgrade path" in mind

**Risk:**
- Don't get distracted by enterprise shiny object
- 3-6 month sales cycles will kill us at seed stage
- Validate retail first, then pivot up-market

**Opportunity:**
- If retail MVP works, we have a clear path to $10M+ ARR via funds
- Fund Manager #1 could become a strategic advisor + reference customer
- Fund market has lower CAC (referral-driven) and lower churn

**Status:** 🟡 Future Opportunity (Q3 2026) | ✅ Keep Warm
