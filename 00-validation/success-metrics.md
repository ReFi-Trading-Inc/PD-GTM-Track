# Success Metrics - ReFi.Trading

**Team:** ReFi.Trading  
**Product:** ReFi.Trading - Non-Custodial RL Trading Platform  
**Created:** November 28, 2025  
**Last Updated:** November 28, 2025

---

## North Star Metric

> The ONE metric that best captures the core value we deliver to customers

**Metric:** Weekly Active Safe Traders (WAST)

**Definition:** Number of unique users who execute at least one live trade (with real money, not paper trading) protected by a zk-VaR proof in a rolling 7-day period.

**Why This Metric:**  
WAST captures our core value proposition: enabling retail traders to use institutional-grade RL algorithms with cryptographically verified risk protection. Unlike typical "daily active users" (which could include paper traders), WAST measures:
1. **Actual usage** (not just browsing)
2. **Trust** (users commit real capital)
3. **Safety** (all trades have zk-proof verification)

A user who trades once with $100 is infinitely more valuable than 100 users who only paper trade. WAST is our best leading indicator of product-market fit, revenue potential (execution fees), and long-term retention.

**Target:** 
- **Month 1 (Alpha Wave 1):** 10 WAST
- **Month 3 (Post-Experiment Validation):** 40 WAST
- **Month 6 (Public Beta):** 200 WAST
- **Month 12 (Series A):** 1000 WAST

**Current Baseline:** 0 (pre-launch)

**Why these targets:**
- Month 3 target of 40 WAST comes from 00-EXECUTIVE-ACTION-PLAN success criteria (validates product-market fit)
- Month 12 target of 1000 WAST supports $3M ARR milestone ($150/mo × 1000 users at 60% conversion to paid tier)

---

## AARRR Metrics (Pirate Metrics)

### Acquisition

> How do users find you?

**Primary Metric:** Alpha Signups per Month

- **Definition:** Number of unique users who submit email via landing page waitlist or "Get Early Access" CTA
- **Target:** 
  - Month 1: 75 signups (baseline from current traction)
  - Month 2: 150 signups (2x via experiments)
  - Month 3+: 200+ signups (sustained from content marketing)
- **Tracking Method:** PostHog event `signup_submitted` + Airtable form submissions
- **Current:** ~10/week organic (LinkedIn, Reddit, personal network)

**Secondary Metrics:**
- **Traffic sources:** 
  - Target mix: 40% LinkedIn, 30% WhatsApp/Telegram trader groups, 20% Reddit, 10% other
  - Track via UTM parameters
- **Cost per acquisition:** 
  - Target: $0-5 (primarily organic in alpha phase)
  - Track: Total marketing spend / signups
- **Qualified signup rate:**
  - Target: 70%+ signups match ICP (power-retail or small funds, $10K+ account size)
  - Track: Via signup form questions

---

### Activation

> Do users have a great first experience?

**Primary Metric:** Broker Connection Rate (within 7 days of signup)

- **Definition:** % of signups who successfully complete SnapTrade OAuth and have "Connection Successful" status within 7 days
- **Target:** 60%+ (this is Experiment 1 success threshold)
- **Tracking Method:** 
  - PostHog funnel: `signup_submitted` → `broker_oauth_initiated` → `broker_connected`
  - Time delta between events
- **Current:** Unknown (testing in Experiment 1)

**Why this is activation:** Broker connection is our "aha moment." Until a user connects their brokerage account, they cannot experience our core value (RL-driven trades with zk-proof verification). This is the highest-value action a new user can take.

**Activation Flow:**
1. User signs up (email submitted)
2. Welcome email with "Connect Your Broker in 60 Seconds" CTA (within 5 minutes)
3. User selects broker (IBKR or Alpaca via SnapTrade)
4. User completes OAuth authorization
5. **Aha moment achieved:** "Connection Successful" screen shows portfolio + first trade recommendation

**Secondary Activation Metrics:**
- **Time to broker connection:** Median ≤24 hours (target), track distribution
- **Broker preference:** % IBKR vs. Alpaca (informs integration priorities)
- **Drop-off point:** % who abandon at broker selection vs. OAuth screen (diagnose friction)

---

### Retention

> Do users come back?

**Primary Metric:** Weekly Retention (W1)

- **Definition:** % of users who execute at least one trade in Week 1 who also execute at least one trade in the following week (Week 2)
- **Target:** 40%+ (strong signal for product-market fit)
- **Tracking Method:** PostHog cohort analysis
  - Cohort definition: Users who had `first_live_trade` in Week N
  - Retention metric: % who have `trade_executed` in Week N+1
- **Current:** Unknown (will measure starting with Alpha Wave 1)

**Why weekly retention:** Daily is too frequent for trading (users may trade 2-3x/week), monthly is too slow for iterating. Weekly captures habitual usage without false negatives.

**Retention Cohorts:**
- **Week 1 retention:** 40%+ target (users return after first week)
- **Week 4 retention:** 30%+ target (one-month stickiness)
- **Week 12 retention:** 20%+ target (three-month habit formation)

**Secondary Retention Metrics:**
- **Avg trades per week (active users):** Target 3-5 trades/week
- **Paper-to-live conversion:** 60%+ transition from paper trading to live within 14 days
- **Churn reason categorization:** Survey users who stop trading (performance, trust, UX, other)

---

### Revenue (or Value)

> For alpha: What value do users get? (Monetization comes post-PMF)

**Phase 1 (Alpha - Month 1-3): Value Metrics**

Since we're not charging during alpha, we measure value delivery through engagement:

**Primary Value Metric:** Average Notional Traded per Week

- **Definition:** Sum of absolute position sizes across all trades, divided by number of active traders
- **Target:** $2,500/week per active trader
  - Rationale: With progressive caps ($100 → $500 → $5000), expect average position ~$500, 5 trades/week = $2,500
- **Why this matters:** Higher notional → user trust + engagement. Low notional suggests fear or lack of confidence.

**Secondary Value Metrics:**
- **Portfolio performance:** 
  - Median user CAGR: Target ≥10% (vs. S&P 500)
  - Median Sharpe ratio: Target ≥1.0
  - Max drawdown: Target <15%
  - **Note:** These are early indicators but not success criteria (sample size too small, timeframe too short)
- **Risk limit adherence:**
  - % of trades that pass zk-VaR verification: Target 95%+
  - % of users who never hit stop-loss: Target 80%+

**Phase 2 (Beta - Month 4-12): Revenue Metrics**

**Primary Revenue Metric:** Monthly Recurring Revenue (MRR)

- **Target:** 
  - Month 6: $15K MRR (100 paid seats × $150/mo avg)
  - Month 12: $150K MRR (1000 WAST × $150/mo avg, assuming 60% convert to paid tier)
- **Pricing tiers:**
  - Starter: $150/mo (1 asset class, 1 live policy)
  - Pro: $350/mo (multi-asset, 5 live policies)
  - Prime: $995/mo (unlimited policies, low-latency)

**Secondary Revenue Metrics:**
- **Execution fee revenue:** 10 bps × monthly notional volume
  - Target Month 12: $50K/mo (from $50M monthly notional)
- **Fund licensing revenue:** $50-120K/year per fund client
  - Target Month 12: $200K ARR (from 2-3 fund clients)
- **Gross margin:** Target ≥75% (after broker rebates, compute costs)

---

### Referral

> Do users tell others?

**Primary Metric:** Organic Referral Rate

- **Definition:** % of active users who invite at least one other user (via email invite, social share, or referral link) per month
- **Target:** 15%+ (1 in 7 users refers someone)
- **Tracking Method:** 
  - Referral links with unique codes (per user)
  - Social share buttons with UTM tracking
  - "Invite a friend" feature in app
- **Current:** Not yet implemented (will add in Month 2)

**Virality Coefficient Goal:** 0.5 (each user brings 0.5 new users → sustainable organic growth)

**Calculation:** 
- Referral rate × Conversion rate of referrals
- Example: 15% refer × 40% referral conversion = 0.06 coefficient (low, need to improve)

**Secondary Referral Metrics:**
- **Word-of-mouth NPS:** Target 50+ (measure via survey)
- **Social proof events:**
  - % of users who share performance on social: Target 10%+
  - % of users who write reviews/testimonials: Target 5%+
- **Community engagement:**
  - Discord active members: Target 100+ by Month 3
  - LinkedIn/X engagement rate on posts: Target 5%+

---

## Guardrail Metrics

> Metrics that shouldn't get worse while we optimize for growth

| Metric | Threshold | Why It Matters | How We Track |
|--------|-----------|----------------|--------------|
| **Platform uptime** | ≥99.5% | Trading platforms must be reliable; downtime kills trust | StatusPage.io, PagerDuty alerts |
| **Trade execution latency** | p95 <150ms | Slow execution = slippage = user dissatisfaction | PostHog timing events |
| **zk-Proof verification latency** | p95 <3ms | Proofs must be fast or they block trades | Custom logging |
| **Broker API error rate** | <1% | Failed orders = lost revenue + user churn | SnapTrade error logs |
| **Account security incidents** | 0 | Any breach = catastrophic trust loss | Security audit logs, Sentry |
| **Regulatory violations** | 0 | ADGM RegLab compliance is non-negotiable | Manual compliance checklist |
| **User-reported bugs (P0)** | <5/week | Critical bugs must be rare | GitHub Issues, Zendesk |
| **Support response time** | <2 hours | Fast support = higher retention | Zendesk SLA tracking |

**What triggers a guardrail breach:**
- If any guardrail is violated, **pause all growth activities** until fixed
- Example: If uptime drops to 98%, stop new signups, focus engineering on stability
- Guardrails are more important than growth in alpha/beta phases

---

## Data Collection Plan

### Analytics Stack

**Platform:** PostHog (open-source, self-hosted on Google Cloud)

**Why chosen:** 
- Open-source = full control + privacy (critical for financial data)
- Self-hosted = GDPR/ADGM compliant
- Event-based architecture = flexible for custom metrics
- Built-in funnel, retention, and cohort analysis
- Free up to 1M events/month (sufficient for alpha)

**Implementation status:**
- [x] PostHog instance deployed on GCP
- [ ] Events schema defined (see below)
- [ ] Key events implemented (in progress)
- [ ] Dashboard created (Week 1 of MVP sprint)
- [ ] Team has access (via SSO)

---

### Event Schema

**Full schema:** `03-build/analytics/event-schema.md`

**Key events being tracked:**

| Event Name | Trigger | Properties | AARRR Stage |
|------------|---------|------------|-------------|
| `signup_submitted` | User submits email on landing page | email, source, utm_campaign | Acquisition |
| `broker_oauth_initiated` | User clicks "Connect Broker" | broker_type (IBKR/Alpaca) | Activation |
| `broker_connected` | SnapTrade OAuth complete | broker_type, timestamp | Activation |
| `paper_trading_started` | User enters paper trading mode | initial_balance | Activation |
| `trade_recommended` | RL agent generates recommendation | symbol, action, confidence | Engagement |
| `trade_preview_viewed` | User views zk-VaR proof preview | symbol, position_size, proof_valid | Engagement |
| `first_live_trade` | User executes first trade with real $$ | symbol, position_size, caps_tier | Activation → Retention |
| `trade_executed` | Any trade execution (live) | symbol, position_size, profit_loss, proof_hash | Retention |
| `caps_tier_increased` | Progressive caps unlock (Day 1→3→7) | old_cap, new_cap | Retention |
| `risk_limit_hit` | zk-VaR proof FAILS (trade blocked) | symbol, attempted_size, limit_exceeded | Guardrail |
| `referral_sent` | User invites friend | referral_code, channel | Referral |
| `subscription_started` | User converts to paid tier | plan (Starter/Pro/Prime), MRR | Revenue |

**User Properties (tracked at signup + updated):**
- `user_id` (unique)
- `email`
- `signup_source` (LinkedIn, WhatsApp, Reddit, etc.)
- `trader_type` (Power-Retail, Fund Operator, Prosumer)
- `account_size_range` ($10-50K, $50-250K, $250K+)
- `broker` (IBKR, Alpaca)
- `activation_date` (first broker connection)
- `cohort_week` (for retention analysis)
- `ltv` (lifetime value, calculated)
- `referral_count` (how many they've referred)

---

### Dashboard & Reporting

**Dashboard URL:** https://posthog.refi.trading (internal only)

**Refresh frequency:** Real-time (PostHog auto-updates)

**Team access:** 
- Founders: Full access (all dashboards, raw data export)
- Advisors: Read-only (overview dashboard)
- Investors: Monthly summary reports (no raw data)

**Key views:**

1. **Overview Dashboard (North Star + AARRR):**
   - WAST trend (7-day rolling)
   - Acquisition: Signups/month, by source
   - Activation: Broker connection rate, time to first trade
   - Retention: Weekly cohort chart
   - Revenue: MRR (when launched)
   - Referral: Referral rate, virality coefficient

2. **Cohort Analysis (Retention Deep Dive):**
   - Retention table by signup week
   - Segmented by: Broker type, trader type, signup source
   - Churn reasons (from exit surveys)

3. **Funnel Analysis (Conversion Optimization):**
   - Signup → Broker Connect → Paper → Live (visualized)
   - Drop-off points highlighted
   - A/B test comparisons (when running experiments)

4. **Performance Dashboard (User Value):**
   - Median portfolio returns (CAGR, Sharpe, max DD)
   - Notional volume trends
   - Risk limit adherence (% trades with valid proofs)

---

## Success Criteria by Timeline

### Week 1-2 (Experiment Validation Phase)
- [ ] **Experiment 1:** 60%+ simulated broker connection rate
- [ ] **Data collection:** PostHog events firing, no tracking gaps
- [ ] **Decision point:** Does data warrant building real SnapTrade integration?

### Week 3-4 (Experiment 2-3 Validation)
- [ ] **Experiment 2:** 70%+ comprehension + ≥2 point trust lift
- [ ] **Experiment 3:** 60%+ paper-to-live conversion
- [ ] **Decision point:** Can we achieve product-market fit signals?

### Month 2-3 (Alpha Wave 1)
- [ ] **Acquisition:** 150+ signups/month
- [ ] **Activation:** 60%+ broker connection rate (real SnapTrade, not simulation)
- [ ] **North Star:** 10-15 WAST
- [ ] **Retention:** 40%+ weekly retention (W1)
- [ ] **Decision point:** Is this worth scaling to public beta?

### Month 4-6 (Public Beta)
- [ ] **Acquisition:** 200+ signups/month sustained
- [ ] **Activation:** 65%+ broker connection rate
- [ ] **North Star:** 100-200 WAST
- [ ] **Retention:** 40%+ W1, 30%+ W4
- [ ] **Revenue:** $15K MRR (from early paid conversions)
- [ ] **Decision point:** Ready for Series A fundraising?

### Month 7-12 (Scale to Series A)
- [ ] **North Star:** 1000 WAST
- [ ] **Revenue:** $150K MRR ($3M ARR run-rate)
- [ ] **Retention:** 40%+ W1, 30%+ W4, 20%+ W12
- [ ] **Referral:** 15%+ organic referral rate
- [ ] **Decision point:** Raise Series A, expand to APAC/EU markets

---

## Metric Definitions & Calculations

### Weekly Active Safe Traders (WAST)

**Formula:** 
```
WAST = COUNT(DISTINCT user_id) 
WHERE event = 'trade_executed' 
AND trade_type = 'live' 
AND timestamp >= NOW() - 7 days
AND proof_valid = TRUE
```

**Example calculation:**  
- Week of Nov 25-Dec 1: 15 unique users executed live trades with valid zk-proofs
- WAST = 15

**Why we calculate it this way:**  
- `DISTINCT user_id` avoids double-counting heavy traders
- `trade_type = 'live'` excludes paper trading (not our business model)
- `proof_valid = TRUE` ensures safety (our core differentiation)
- 7-day rolling window smooths daily volatility

---

### Broker Connection Rate

**Formula:**
```
Connection Rate = (broker_connected / signup_submitted) × 100
WHERE timestamp >= signup_date AND timestamp <= signup_date + 7 days
```

**Example calculation:**
- 100 signups in November
- 62 completed broker OAuth within 7 days
- Connection rate = 62/100 = 62%

**Why we calculate it this way:**
- 7-day window balances urgency (want fast activation) with realism (some users need time)
- Denominator is signups, not visitors (only counting qualified leads)

---

### Weekly Retention (W1)

**Formula:**
```
W1 Retention = (Active Week N+1 / Active Week N) × 100
WHERE Active = user executed ≥1 live trade in that week
```

**Example calculation:**
- Week 1: 20 users executed live trades (cohort)
- Week 2: 8 of those 20 executed trades again
- W1 retention = 8/20 = 40%

**Why we calculate it this way:**
- Cohort-based (tracks same users over time)
- "Active" defined by action (trade), not just login
- Weekly granularity matches trading behavior (not too fast, not too slow)

---

## Benchmarks & Context

### Industry Benchmarks

| Metric | Our Target | Fintech SaaS Average | Top Quartile |
|--------|-----------|---------------------|--------------|
| **Signup → Activation** | 60% | 25-40% | 60%+ |
| **W1 Retention** | 40% | 20-30% | 40%+ |
| **W4 Retention** | 30% | 10-20% | 30%+ |
| **CAC (Alpha)** | $0-5 | $50-150 | <$50 |
| **Virality Coefficient** | 0.5 | 0.1-0.3 | 0.5+ |

**Sources:** 
- Andreessen Horowitz "16 Startup Metrics" (a16z.com)
- OpenView Partners "SaaS Benchmarks" (openviewpartners.com)
- Baremetrics "SaaS Metrics" (baremetrics.com)
- ReFi.Trading internal analysis of Robinhood/Wealthfront public data

---

### Our Context

**Why our targets differ from benchmarks:**

1. **Higher activation target (60% vs. 25-40%):**
   - We're pre-filtering for highly engaged users (power-retail, not casual investors)
   - Broker connection is intimidating → only serious users complete it
   - This creates higher bar for activation but better quality users

2. **Higher retention target (40% vs. 20-30%):**
   - Trading is habitual (vs. one-time financial tools)
   - Our RL agents create dependency (users see performance, come back)
   - Non-custodial + zk-proofs reduce switching costs to competitors

3. **Lower CAC target ($0-5 vs. $50-150):**
   - Alpha phase is 100% organic (no paid ads)
   - Targeting niche (algo trading) with tight communities (easy to reach)
   - Will increase CAC in beta/growth phase, but validating organic first

4. **Higher virality target (0.5 vs. 0.1-0.3):**
   - Trading performance is inherently shareable (users brag about returns)
   - Non-custodial + zk-proofs are novel (people talk about new tech)
   - Referral incentives built into product ($REFIN rewards post-TGE)

---

## Weekly Review Process

**When:** Every Monday at 10:00 AM UAE time

**Who:** Zeshan Ahmad, Daniel Oosthuyzen

**Format:**
1. **Review dashboard (5 min):**
   - WAST trend (up/down/flat?)
   - Funnel conversion rates (any changes?)
   - Retention cohorts (are users sticking?)
   
2. **Discuss trends (10 min):**
   - What worked last week? (campaigns, features, fixes)
   - What didn't? (experiments that failed, user complaints)
   - Any surprising patterns? (unexpected user behavior, outliers)
   
3. **Identify concerns (5 min):**
   - Are we on track for monthly targets?
   - Any guardrails at risk? (uptime, errors, security)
   - What's blocking growth?
   
4. **Decide actions (10 min):**
   - What should we start doing?
   - What should we stop doing?
   - What should we do differently?
   - Assign owners and deadlines

**Output:** Notion doc with decisions + action items (tracked in weekly sprint)

**Questions to ask every week:**
- Are we hitting our targets?
- What's trending up/down? Why?
- Any surprises in the data?
- What should we do differently this week?
- What experiments should we run next?

---

## Red Flags & Alerts

**Set up alerts for:**

| Condition | Alert Threshold | Action Required | Owner |
|-----------|----------------|-----------------|-------|
| **WAST decline** | 20% WoW drop for 2 consecutive weeks | Investigate user churn, interview lapsed users | Zeshan |
| **Broker connection rate drop** | Below 50% for 7+ days | Check SnapTrade API, test OAuth flow, improve messaging | Daniel |
| **Platform downtime** | >1% over 24 hours | All-hands incident response, user communication | Daniel |
| **Execution latency spike** | p95 >200ms for 1+ hour | Investigate broker API, check Google AI Agent Platform | Daniel |
| **zk-Proof failure rate** | >10% of trades failing verification | Audit proof generation logic, check circuit parameters | Daniel |
| **Zero new signups** | No signups for 3+ days | Check marketing campaigns, review landing page analytics | Zeshan |
| **Negative user feedback spike** | >5 complaints in 24 hours | Triage issues, communicate with users, hotfix if needed | Both |
| **Regulatory inquiry** | Any contact from ADGM/CIRO | Immediate legal consultation, pause risky features | Zeshan |

**PagerDuty Integration:** Critical alerts (downtime, security) trigger SMS to both founders 24/7

---

## Notes & Assumptions

**Key assumptions in our metrics:**

1. **"Safe" in WAST means zk-proof verified:**
   - We're betting that verified trades are more valuable than unverified
   - If users bypass zk-proofs (hack/workaround), this metric becomes meaningless
   - Mitigation: ERC-4337 wallet enforces proof requirement at smart contract level

2. **Weekly granularity is right for trading:**
   - Some users may trade monthly (long-term strategies)
   - We may need to add "Monthly Active Safe Traders" for different user segments
   - Will iterate based on actual user behavior patterns

3. **Broker connection = activation:**
   - Assumes connecting broker is the key "aha moment"
   - If users connect but never trade, we've misidentified activation
   - Will validate in Experiment 1; may need to redefine if wrong

4. **Progressive caps reduce paper-to-live friction:**
   - Assumes $100 starting cap is low enough to reduce fear
   - If users still don't go live, may need to lower to $50 or $25
   - Will validate in Experiment 3

**Limitations:**

- **Small sample size in alpha:** With 10-40 WAST, statistical significance is low. Trends may be noise.
- **Self-selection bias:** Alpha users are early adopters; may not represent broader market.
- **Short timeframes:** Can't measure long-term retention (6-12 months) in 3-month alpha.
- **Performance attribution:** Hard to isolate ReFi.Trading performance from overall market moves.

**How we'll address limitations:**
- Acknowledge uncertainty in investor updates ("directional signals, not proof")
- Supplement quantitative metrics with qualitative user interviews
- Extend alpha timeline if needed to get statistically significant sample
- Compare user returns to benchmark (S&P 500) to isolate alpha

---

## Change Log

| Date | What Changed | Why |
|------|--------------|-----|
| Nov 28, 2025 | Initial metrics defined | Lab 8 exercise |
| [TBD] | Adjusted activation metric after Experiment 1 | Validated broker connection is/isn't aha moment |
| [TBD] | Added Monthly Active Safe Traders (MAST) | Found weekly too frequent for some user segments |
| [TBD] | Changed retention definition | Users engaging with paper trading but not live |
