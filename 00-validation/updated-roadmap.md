

---

## 🎯 SCENARIO A: GO - BUILD FULL MVP

**Conditions Met:**
- ✅ Experiment 1: [X%] broker connection (≥60% target)
- ✅ Experiment 2: [X%] comprehension + [X.X]pt trust lift (≥70% + 2pt target)
- ✅ Experiment 3: [X%] initiated live (≥60% target)

**Confidence:** [🟢 High / 🟡 Medium] - Proceed with full MVP build

**Strategic Priorities (Next 12 Weeks):**
1. **Week 1-4:** SnapTrade Integration + zk-VaR Proof Engine (Phase 1)
2. **Week 5-8:** Alpha UI Build + Progressive Caps System (Phase 2)
3. **Week 9-12:** Alpha Wave 1 Launch (50 users) + Iteration (Phase 3)

---

### Phase 1: Core Infrastructure (Weeks 1-4)
**Duration:** January 31 - February 27, 2026 (4 weeks)  
**Owner:** Daniel (CTO) + External Contractors  
**Budget:** $45,000 (seed funds)

#### Week 1-2: SnapTrade Integration
**Goal:** Connect to IBKR, Alpaca, Kraken, Coinbase via SnapTrade API

**Technical Deliverables:**
- [ ] SnapTrade API client setup (TypeScript SDK)
  - Authentication: `clientId` + `consumerKey`
  - User management: `userId` + `userSecret` per end-user
  - OAuth flow integration for broker connections
  
- [ ] Broker connection flow (based on Experiment 1 learnings)
  - **Route:** `/app/connect-broker`
  - **Components:** Broker selection → SnapTrade OAuth → Success screen
  - **Improvements from validation:**
    - [List specific UI changes based on Experiment 1 drop-offs]
    - Example: "Add tooltips explaining IBKR vs Alpaca differences"
    - Example: "Increase OAuth loading time from 3s to 5s for mobile"
  
- [ ] Account data sync (holdings, balances, transactions)
  - Polling frequency: Max 4x/day for holdings, 1x/day for transactions
  - Webhook setup for real-time trade confirmations
  
- [ ] Error handling & reconnection flow
  - Handle expired tokens, revoked connections
  - Clear UX for re-authorization (based on Experiment 1 feedback)

**Backend Architecture:**
```
┌──────────────┐
│  Next.js App │
└──────┬───────┘
       │
       ↓
┌──────────────────┐
│  SnapTrade API   │ (External)
└────────┬─────────┘
         │
    ┌────┴────┐
    │         │
┌───▼───┐ ┌──▼───────┐
│  IBKR │ │Alpaca    │
└───────┘ └──────────┘
```

**Success Criteria:**
- [ ] OAuth flow completes in <10 seconds (p95)
- [ ] Account sync latency <2 seconds (p95)
- [ ] Broker API error rate <1%
- [ ] Support for 3+ brokers (IBKR, Alpaca + 1 crypto exchange)

**Key Risks & Mitigations:**
- **Risk:** SnapTrade partner approval takes 3-6 weeks
  - **Mitigation:** Already completed during Experiment 1 (mock OAuth validated demand)
  - **Backup:** Direct IBKR API integration if SnapTrade delays
  
- **Risk:** Alpaca API rate limits during testing
  - **Mitigation:** Use IBKR for dev/staging, Alpaca only for production

---

#### Week 3-4: zk-VaR Proof Engine (MVP)
**Goal:** Generate zk-SNARK proofs for every trade, verify on-chain

**Technical Deliverables:**
- [ ] Circom circuit for 95% historical-simulation VaR
  - **Inputs (8 state variables):**
    1. Current portfolio value
    2. Proposed trade notional
    3. Historical returns (30-day window)
    4. User's VaR limit (%)
    5. Current position sizes
    6. Correlation matrix (simplified 3x3)
    7. Asset volatilities
    8. Timestamp
  
  - **Output:** Proof π that VaR_calculated ≤ VaR_limit
  
  - **Constraint count target:** <65k (proof gen <3ms on laptop)
  
- [ ] SnarkJS proof generation service
  - **Endpoint:** `POST /api/proof/generate`
  - **Input:** Trade details + portfolio state
  - **Output:** zk-SNARK proof + public inputs
  - **Latency target:** p95 <3ms (local), p99 <5ms
  
- [ ] On-chain verification (Base testnet)
  - Deploy verifier contract (auto-generated from Circom)
  - Batch poster service (bundles 10+ trades per tx)
  - Store proof hashes on-chain, full proofs on IPFS
  
- [ ] ERC-4337 smart wallet integration
  - User's trading wallet requires valid proof to execute
  - Dual-gate: (1) User signature + (2) zk-proof verification
  - Wallet creation flow during onboarding

**Architecture:**
```
Trade Request
     ↓
┌─────────────────┐
│ zk-VaR Engine   │ (Circom + SnarkJS)
└────────┬────────┘
         │
    ┌────▼────┐
    │  Proof  │ (π, public inputs)
    └────┬────┘
         │
    ┌────▼──────────┐
    │ ERC-4337      │ (Smart Wallet)
    │ Verifier      │
    └────┬──────────┘
         │
    ┌────▼─────┐
    │ Execute  │ (If proof valid)
    │ Trade    │
    └──────────┘
```

**Success Criteria:**
- [ ] Proof generation <3ms (p95) on laptop
- [ ] On-chain verification <120k gas
- [ ] 0 invalid proofs accepted (security invariant)
- [ ] Proof verification UX shows "Verified ✓" within 1 second

**Adjustments from Experiment 2:**
> [Document specific changes based on validation feedback]
> Example: "Users found zk-SNARK explanation too technical. Simplified to 'Cryptographic Safety Check' in UI. Show green checkmark, not technical proof details."

**Key Risks & Mitigations:**
- **Risk:** Circom circuit exceeds constraint budget
  - **Mitigation:** Use reward-centering to keep numeric ranges SNARK-friendly
  - **Backup:** Reduce correlation matrix to 2x2, use simpler VaR estimator
  
- **Risk:** On-chain gas costs too high for frequent trades
  - **Mitigation:** Batch 10+ proofs per transaction (reduce per-trade cost to ~$0.05)
  - **Backup:** Store only proof hashes on-chain, full proofs on IPFS

---

#### Week 4: Integration Testing & Security Audit (Internal)
**Goal:** End-to-end flow works: Broker connect → Trade request → Proof gen → Execution

**Testing Scenarios:**
1. **Happy Path:** User connects IBKR → Sets conservative risk → Places $500 AAPL trade → Proof generated → Trade executed → Confirmed on broker
2. **VaR Rejection:** User tries to place $10k trade exceeding 5% VaR limit → Proof fails → Trade rejected with clear error message
3. **Broker Error:** IBKR API returns 429 rate limit → Trade queued → Retry with exponential backoff → Success on retry
4. **Smart Wallet:** User deploys ERC-4337 wallet → Sets VaR limit 3% → Proof gate enforced → Cannot bypass via direct broker API

**Security Checklist:**
- [ ] SnapTrade API keys stored in env variables (never client-side)
- [ ] User's broker credentials never stored by ReFi.Trading
- [ ] zk-proof circuit code reviewed (no hidden backdoors)
- [ ] Smart wallet ownership transfer tested (user can revoke ReFi access)
- [ ] Rate limiting on proof generation endpoint (prevent DoS)

**Deliverables:**
- [ ] Test suite: 50+ unit tests, 20+ integration tests
- [ ] Security report: Internal audit with threat model
- [ ] Demo video: 3-min walkthrough of full flow (for investors)

---

### Phase 2: Alpha UI Build (Weeks 5-8)
**Duration:** February 28 - March 27, 2026 (4 weeks)  
**Owner:** Zeshan (CEO) + Frontend Contractor  
**Budget:** $25,000 (contractor + design)

#### Architecture: Integrated UI (Based on Dev-PhasesV2.pdf)

**Tech Stack:**
- **Framework:** Next.js 14+ (App Router)
- **Styling:** Tailwind CSS + shadcn/ui components
- **State:** Zustand for global state
- **Auth:** SIWE (Sign-In With Ethereum) + RBAC
- **Wallet:** Wagmi + RainbowKit (ERC-4337 support)
- **Analytics:** PostHog (self-hosted)

**Folder Structure:**
```
apps/
  web/
    app/
      landing/              # Marketing site
      auth/                 # SIWE login flow
        api/
          siwe/nonce/       # Nonce generation
          siwe/verify/      # Signature verification
          auth/refresh/     # Refresh tokens
          auth/logout/      # Session termination
      explorer/             # Portfolio dashboard
        [hash]/             # Proof verification page
        search/             # Search trades/proofs
        timeline/           # Trade history timeline
      trading/              # NEW: Trading interface
        paper/              # Paper trading dashboard
        live/               # Live trading dashboard
      admin/                # Admin panel (RBAC-gated)
        routes/
          [symbol]/         # Asset routing config
    src/
      lib/                  # Utilities
      styles/               # Global CSS
    middleware.ts           # Auth middleware
    next.config.mjs
packages/
  ui/                       # Shared components
    tokens.ts               # Design tokens
    components/
  api-clients/              # Generated clients
    explorer/
    trading/                # NEW: Trading API client
    admin/
    auth/
```

#### Week 5: Landing Page + Auth Flow

**Landing Page (`/landing`):**
- Hero: "Stop Losing 15-30% Returns to Emotional Trading"
  - (Use winning headline from Experiment 1 A/B test)
- Trust bar: Backtest results (28% CAGR, 2.07 Sharpe)
- Benefits: Institutional AI + Non-custodial + zk-proofs
- Social proof: "50+ power-retail traders in alpha"
- CTA: "Join Alpha Waitlist" → leads to `/auth/signup`

**Auth Flow (SIWE):**
- **Route:** `/auth/login`
- **Components:**
  1. Connect wallet (RainbowKit)
  2. Generate nonce (server-side, 5-min TTL)
  3. Sign message (EIP-4361)
  4. Verify signature (server-side)
  5. Create session (httpOnly cookies)
  
- **Security (from Dev-PhasesV2.pdf Section J):**
  - [ ] Single-use nonces (prevent replay)
  - [ ] Nonce bound to address, domain, chainId
  - [ ] Session ID regeneration on login
  - [ ] CSRF protection on all state-changing endpoints
  - [ ] Refresh token rotation (detect reuse, revoke family)

**Deliverables:**
- [ ] Landing page (mobile-first, <2s load time)
- [ ] SIWE auth flow (end-to-end tested)
- [ ] Session management (refresh, logout)
- [ ] RBAC middleware (admin vs. user roles)

---

#### Week 6-7: Paper Trading Dashboard

**Route:** `/trading/paper`

**Components:**

1. **Portfolio Summary Card**
   - Total value: $XX,XXX
   - PnL: +$X,XXX (+X.X%) [color-coded: green if +, red if -]
   - Sharpe ratio: X.XX
   - Current VaR: X.X% / [User limit]% (progress bar)

2. **Trade History Table**
   - Columns: Date | Ticker | Action | Qty | Price | PnL | Proof Hash
   - Click proof hash → opens `/explorer/[hash]` (proof verification page)
   - Filter: Last 7 days / 30 days / All time
   - Export: Download CSV

3. **Risk Profile Selector**
   - Conservative (3% VaR limit)
   - Moderate (5% VaR limit)
   - Aggressive (8% VaR limit)
   - Custom (user sets own limit)
   
   - Shows current trades/day estimate for each profile
   - Change triggers email: "Risk profile updated to [X]"

4. **Daily Recap Email (Automated)**
   - Sent at 6 PM EST every trading day
   - Subject: "Your AI traded [X] times today | PnL: +$X (+X%)"
   - Body:
     - Today's trades (ticker, qty, price, rationale)
     - Updated portfolio stats
     - Link to dashboard
   
   - Uses Resend.com API (transactional emails)

5. **Progressive Caps Timeline**
   - Shows: "You're on Day [X] of paper trading"
   - Timeline: Day 1 → Day 7 → "Go Live"
   - After Day 7: Big CTA button "Ready to Go Live? Start with $100"
   
   - **Adjustments from Experiment 3:**
     - [List specific changes based on feedback]
     - Example: "Offer $50 starting cap option for risk-averse users"
     - Example: "Show 'Extend Paper Trading' option for users who want 14 days"

**Backend:**
- Paper trades generated daily using real-time market data (Polygon.io API)
- TD3/PPO RL agent runs on server (TorchScript model)
- Trade rationale generated using template + AI model outputs
- Trades stored in MongoDB: `paper_trades` collection

**Deliverables:**
- [ ] Paper trading dashboard (all 5 components above)
- [ ] Daily email automation (tested with 10 alpha users)
- [ ] Mobile-responsive (70% of traffic expected on mobile)
- [ ] PostHog event tracking: `paper_trade_viewed`, `risk_profile_changed`, `go_live_clicked`

---

#### Week 8: Live Trading Dashboard + Progressive Caps System

**Route:** `/trading/live`

**Components:**

1. **Progressive Caps Enforcer (Backend)**
   - User table: `user_id`, `live_trading_start_date`, `current_cap`
   - Logic:
     ```
     if days_live <= 2:
         max_notional = $100
     elif days_live <= 6:
         max_notional = $500
     elif days_live <= 14:
         max_notional = $5,000
     else:
         max_notional = user.custom_limit (default: $10,000)
     ```
   
   - Trade requests exceeding cap are rejected with error:
     - "Trade exceeds your Day [X] cap of $[Y]. Cap increases to $[Z] in [N] days."

2. **Live Dashboard (Similar to Paper, with Differences)**
   - **Real broker integration:** Trades route to SnapTrade → IBKR/Alpaca
   - **Real-time PnL:** Updates every 60 seconds (WebSocket via SnapTrade)
   - **Proof verification:** Every trade shows green checkmark "Verified ✓"
   - **Trade confirmation:** Email + push notification for every fill
   
   - **Safety Banner (Top of Page):**
     - "You're on Day [X] of live trading. Max trade size: $[Y]"
     - Progress bar: Day 1 → Day 3 → Day 7 → Day 14 → Unrestricted

3. **"Go Live" Onboarding Flow (Triggered from Paper Dashboard)**
   - **Step 1:** Confirm broker connection (or reconnect if expired)
   - **Step 2:** Review progressive caps timeline (consent required)
   - **Step 3:** Set initial capital amount (must be ≥$500 in broker)
   - **Step 4:** Deploy ERC-4337 smart wallet (one-time, ~$5 gas)
   - **Step 5:** Activate live trading (flips `user.live_enabled = true`)
   
   - **Email confirmation:** "Welcome to Live Trading! Your first cap is $100."

4. **First Live Trade Celebration (UX Delight)**
   - Confetti animation on dashboard when first live trade executes
   - Email: "🎉 Congrats on your first live trade! Here's what happened..."
   - Badge unlocked: "Live Trader" (shown on profile)

**Backend Changes:**
- New MongoDB collection: `live_trades` (separate from paper trades)
- Trade execution queue (Redis-backed) for retry logic
- Slack alert to team when user goes live (for monitoring early alpha)

**Deliverables:**
- [ ] Live trading dashboard (real broker integration)
- [ ] Progressive caps system (backend + frontend)
- [ ] "Go Live" onboarding flow (5 steps above)
- [ ] First trade celebration UX
- [ ] PostHog events: `went_live`, `first_live_trade`, `cap_increased`

---

### Phase 3: Alpha Wave 1 Launch (Weeks 9-12)
**Duration:** March 28 - April 25, 2026 (4 weeks)  
**Owner:** Zeshan (CEO) - Product & User Success  
**Goal:** 50 Alpha users → 40 Weekly Active Safe Traders (WAST)

#### Week 9: Alpha Onboarding (First 20 Users)

**Recruitment:**
- [ ] Email Experiment 1-3 completers (top 30 high-intent users)
  - Subject: "You're in! ReFi.Trading Alpha starts Monday"
  - Body: Personal invite, Calendly link for onboarding call
  - Incentive: "First 20 users get lifetime 20% discount"

- [ ] LinkedIn post: "Alpha Wave 1 is live. 50 spots, invite-only."
  - Target: Power-retail traders from previous experiments
  - CTA: "Apply here" → Google Form → Manual approval

**Onboarding Process:**
1. **Kickoff Call (30 mins, Zeshan):**
   - Walk through platform
   - Answer questions about non-custodial + zk-proofs
   - Set expectations: "You're alpha testers, not customers yet"
   
2. **Welcome Email:**
   - Login link: `https://alpha.refi.trading`
   - Onboarding checklist:
     - [ ] Connect wallet (create ERC-4337 if needed)
     - [ ] Connect broker (IBKR or Alpaca)
     - [ ] Choose risk profile
     - [ ] Start paper trading (7 days)
   
3. **Daily Check-Ins (First Week):**
   - Zeshan sends personal Slack DM or email each day
   - "How's paper trading going? Any issues?"
   - Goal: Build relationship, gather real-time feedback

**Success Criteria (Week 9):**
- [ ] 20 users onboarded
- [ ] 18 users (90%) connected brokers successfully
- [ ] 15 users (75%) started paper trading
- [ ] 0 critical bugs reported (blockers escalated immediately)

---

#### Week 10: Alpha Expansion (Next 30 Users) + Iteration

**Recruitment:**
- [ ] Open waitlist to public (limited to 30 spots)
- [ ] Reddit post: "We validated ReFi.Trading with 100+ traders. Here's what we learned."
  - Share validation results (transparency builds trust)
  - CTA: "Join Alpha Wave 1 - last 30 spots"
  
- [ ] Twitter thread: Behind-the-scenes of validation sprint
  - Tease: "60-day validation sprint. 3 experiments. 100+ user interviews. Here's what we built."

**Iteration Based on Week 9 Feedback:**
- [ ] Fix top 3 bugs reported by first 20 users
- [ ] Optimize drop-off points (e.g., if broker connection still at 60%, improve UX)
- [ ] Add FAQ section based on most common questions

**Success Criteria (Week 10):**
- [ ] 50 total users onboarded (20 + 30)
- [ ] 42 users (84%) completed paper trading (7 days)
- [ ] 25 users (50%) went live (initiated live trading)
- [ ] Average NPS: ≥50 (survey sent on Day 7 of paper trading)

---

#### Week 11: WAST Optimization + Retention Focus

**Goal:** Hit 40 Weekly Active Safe Traders (WAST)

**WAST Definition:**
- Unique users who executed ≥1 live trade with valid zk-VaR proof in the last 7 days

**Current Funnel (Projected):**
```
50 alpha users
  → 42 completed paper trading (84%)
    → 25 went live (50% of paper completers)
      → 20 executed ≥1 trade in Week 1 (80% of live users)

WAST = 20 (Week 11)
Target = 40 by Week 12
```

**Tactics to Increase WAST:**

1. **Reactivation Campaign (For Users Stuck in Paper Trading):**
   - Segment: 8 users who completed paper but didn't go live
   - Email: "You crushed paper trading (+$X PnL). Ready to go live?"
   - Offer: 1:1 call with Zeshan to address concerns
   - Goal: Convert 5 of 8 (total live users → 30)

2. **Encourage Daily Activity (For Live Users):**
   - Gamification: Daily login streak badge
   - Email: "Your AI found 2 opportunities today. Check your dashboard."
   - Push notifications: "New trade executed: Bought 5 AAPL @ $178.50"
   - Goal: Increase active rate from 80% to 90%

3. **Referral Program (Soft Launch):**
   - Each alpha user gets 3 invite codes
   - Referred user joins waitlist for Alpha Wave 2 (May 2026)
   - Referrer gets: "Lifetime Pro tier when we launch" (worth $350/mo)
   - Goal: Generate 20 referrals for Wave 2 pipeline

**Success Criteria (Week 11):**
- [ ] WAST increases from 20 → 30 (reactivation campaign)
- [ ] Average trades per active user: 3-5 per week
- [ ] Weekly retention (W1 → W2): ≥40%
- [ ] 20 referrals generated for Alpha Wave 2

---



---



---

## 🔄 SCENARIO B: ITERATE - OPTIMIZE & RETEST

**Conditions:**
- ⚠️ 1-2 experiments validated, but not all 3
- OR: All 3 validated but confidence is 🟡 Medium (not High)
- OR: Validation showed promise but significant gaps remain

**Example Scenarios:**
1. Broker connection validated (70%), but paper-to-live only hit 45%
2. Non-custodial trust validated, but broker connection only hit 52%
3. All 3 experiments hit lower end of targets (60-65%), not confident enough

**Decision:** Don't build full MVP yet. Run 4-6 week iteration sprint to strengthen weak areas.

---

### Iteration Sprint Structure (4-6 Weeks)

**Week 1: Identify Root Causes**

**For Each Weak Experiment:**
- [ ] Review qualitative feedback (interview transcripts)
- [ ] Analyze quantitative drop-off points
- [ ] Form hypothesis: "We think [X] is the blocker because [Y evidence]"

**Example (if Paper-to-Live was weak at 45%):**
> **Hypothesis:** "Paper-to-live conversion was 45% (target: 60%) because:
> 1. Users felt 7 days was too short to build confidence (8/10 non-converters cited this)
> 2. $100 starting cap felt 'pointless' for users with $50K+ accounts (6/10 cited this)
> 3. Email follow-ups felt pushy (5/10 mentioned 'too many emails')"

**Iteration Plan:**
1. **Extend paper trading default to 14 days** (with 7-day opt-in for aggressive users)
2. **Tiered progressive caps based on account size:**
   - <$10K account → Start at $100
   - $10K-$50K → Start at $250
   - >$50K → Start at $500
3. **Reduce email frequency** from 3 follow-ups to 1, softer tone

---

**Week 2: Build Iteration**

- [ ] Implement changes (faster than full MVP build, only modify weak areas)
- [ ] Set up new A/B test (control = original, variant = iteration)
- [ ] Recruit 30 new users (50% control, 50% variant)

**Example Testing Plan:**
- Control group (15 users): Original 7-day paper + $100 cap
- Variant group (15 users): 14-day paper + tiered caps
- Run for 21 days (14 days paper + 7 days conversion window)

---

**Week 3-4: Run Iteration Experiment**

- [ ] Monitor daily (same as Experiment 3 in original validation)
- [ ] Conduct 5 interviews per group (10 total)
- [ ] Track conversion rates in real-time

**Success Criteria for GO:**
- Variant group conversion ≥60% (vs. control ≤50%)
- Qualitative feedback shows improvement
- Confidence level increases to 🟢 High

---

**Week 5: Analysis & Decision**

- [ ] Compare control vs. variant
- [ ] If variant wins: ✅ Proceed to full MVP build with optimized approach
- [ ] If variant still weak: ⚠️ Consider another iteration OR pivot
- [ ] Update roadmap based on learnings

---

**Week 6: Team Alignment & Planning**

- [ ] Share results with team + advisors
- [ ] Decide: GO (build MVP) or PIVOT (fundamental change)
- [ ] If GO: Start Phase 1 (SnapTrade integration) in Week 7
- [ ] If PIVOT: Move to Scenario C planning

---

### Budget for Iteration Sprint

| Item | Cost | Notes |
|------|------|-------|
| Recruitment (ads if needed) | $500 | LinkedIn ads for 30 users |
| User incentives (15 interviews) | $375 | $25 gift cards |
| Tools (Typeform, Retool, etc.) | $0 | Free tiers |
| Contractor (if UI changes needed) | $3,000 | Part-time dev, 2 weeks |
| **Total** | **$3,875** | |

**Timeline:** 4-6 weeks → Then GO/PIVOT decision

---

## 🔀 SCENARIO C: PIVOT - FUNDAMENTAL STRATEGY SHIFT

**Conditions:**
- ❌ 2+ experiments invalidated (<40% conversion)
- OR: All experiments showed <50% conversion
- OR: Qualitative feedback reveals fundamental product misalignment

**Example Scenarios:**
1. Users don't trust broker API connections at all (Exp 1: 35% conversion)
2. zk-proofs added confusion, not trust (Exp 2: 40% comprehension)
3. Users won't go live even after positive paper performance (Exp 3: 30% conversion)

**Decision:** Current approach is not working. Need to fundamentally change strategy.

---

### Pivot Options (Choose One)

#### Option 1: Demo Accounts Only (No Broker Connection)

**Hypothesis:**
> "Users want to see the AI in action but are fundamentally unwilling to connect real brokers. We'll offer demo accounts with simulated capital, monetize via subscriptions."

**Changes:**
- ❌ Remove: Broker connection (SnapTrade integration)
- ❌ Remove: Real capital trading
- ✅ Keep: TD3/PPO RL algorithms, zk-proofs (for demo trades)
- ✅ Add: Simulated brokerage with fake $100K capital
- ✅ Add: Leaderboard (users compete on PnL)

**Revenue Model:**
- Free tier: 1 strategy, $10K demo capital
- Pro tier ($50/mo): 5 strategies, $100K demo capital, priority AI access
- Premium tier ($150/mo): Unlimited strategies, custom model training

**Timeline:** 8 weeks to build (faster than full MVP)

**Risk:** This is not a trading platform anymore—it's an AI demo/education tool. Harder to prove value long-term.

---

#### Option 2: View-Only Analytics Platform

**Hypothesis:**
> "Users don't trust automated execution but want AI-powered insights. We'll build a 'Trading Copilot' that suggests trades, users execute manually."

**Changes:**
- ❌ Remove: Automated trade execution
- ❌ Remove: Progressive caps, zk-proofs (not needed for suggestions)
- ✅ Keep: RL algorithms (generate trade ideas)
- ✅ Add: Trade suggestion feed (push notifications)
- ✅ Add: "One-click execute" button (sends order to broker, user confirms manually)

**Revenue Model:**
- Free tier: 3 trade suggestions/day
- Pro tier ($100/mo): Unlimited suggestions, priority signals
- Premium tier ($300/mo): Custom strategies, backtesting tools

**Timeline:** 6 weeks to build (no execution infrastructure needed)

**Risk:** Commoditized market—many competitors offer trade signals. Hard to differentiate.

---

#### Option 3: B2B SaaS for Small Hedge Funds

**Hypothesis:**
> "Retail traders don't have enough capital to justify our complexity. We'll pivot to institutional clients (funds managing $10M-$100M) who need quant infrastructure but can't afford Bloomberg + in-house data scientists."

**Changes:**
- ❌ Remove: Retail focus (progressive caps, simplified UX)
- ❌ Remove: Non-custodial wallets (institutions use prime brokers)
- ✅ Keep: RL algorithms, backtesting, zk-proofs (for audit trails)
- ✅ Add: White-label solution (fund can brand it)
- ✅ Add: Multi-user RBAC (analysts, traders, compliance officers)
- ✅ Add: Regulatory reporting (CFTC, SEC filings)

**Revenue Model:**
- Base: $5,000/month per fund
- Plus: 5 bps on AUM (e.g., $50M AUM → $25K/year)
- Implementation fee: $20K one-time

**Timeline:** 12 weeks to build (enterprise features take longer)

**Risk:** Longer sales cycles (6-12 months), need legal/compliance expertise. May require Series A before revenue.

---

#### Option 4: Regulated Fund (ReFi Capital)

**Hypothesis:**
> "Users want the performance but don't want to operate the tech themselves. We'll launch a regulated fund (CTA/CPO) that uses our RL algorithms. Users invest, we manage."

**Changes:**
- ❌ Remove: Self-directed platform (users don't log in)
- ❌ Remove: Non-custodial wallets (we custody via prime broker)
- ✅ Keep: RL algorithms (fund's trading strategy)
- ✅ Add: Fund structure (LP units, quarterly redemptions)
- ✅ Add: Prime brokerage relationship (Interactive Brokers, etc.)
- ✅ Add: CFTC/NFA registration (CTA + CPO)

**Revenue Model:**
- Management fee: 2% AUM annually
- Performance fee: 20% of profits above high-water mark
- Minimum investment: $100K per LP

**Timeline:** 6-9 months (regulatory approval is slow)

**Risk:** Very different business model. Capital-intensive. Regulatory complexity. Need to raise AUM to break even.

---

### Pivot Decision Framework

**Decision Matrix:**

| Option | Time to Market | Capital Required | Competitive Moat | TAM | Difficulty |
|--------|---------------|------------------|------------------|-----|-----------|
| 1. Demo Accounts | 8 weeks | Low ($50K) | Low | $50M | Low |
| 2. View-Only Analytics | 6 weeks | Low ($40K) | Low | $200M | Low |
| 3. B2B SaaS for Funds | 12 weeks | Medium ($150K) | Medium | $500M | Medium |
| 4. Regulated Fund | 6-9 months | High ($500K+) | High | $5B+ | High |

**Recommendation Process:**
1. **Week 1:** Founder + advisors debate all 4 options
2. **Week 2:** Interview 10 target customers for *each* pivot option
   - E.g., For Option 3: Interview 10 hedge fund operators
3. **Week 3:** Build lightweight prototypes (landing pages, mockups)
4. **Week 4:** Run lightweight validation (similar to Experiment 1 smoke tests)
5. **Week 5:** Decide on pivot direction or shut down

**Shut Down Criteria:**
- If no pivot option shows ≥60% interest in validation
- If team is misaligned on direction (co-founder conflict)
- If remaining capital <$100K (not enough to execute pivot)

---

### Pivot Budget

| Phase | Cost | Notes |
|-------|------|-------|
| Validation (Weeks 1-4) | $5,000 | User interviews, prototypes |
| Build (Weeks 5-12) | $50K-150K | Depends on pivot option |
| Legal/Regulatory (if needed) | $20K-100K | For Options 3-4 |
| **Total** | **$75K-255K** | |

**Remaining Runway:** [Calculate based on seed funds - validation spend]

---

## 📊 Key Performance Indicators (All Scenarios)

**Track These Weekly (Regardless of GO/ITERATE/PIVOT):**

### North Star Metric
- **WAST (Weekly Active Safe Traders):**
  - Week 1: [X]
  - Week 4: [X]
  - Week 8: [X]
  - Week 12: [X]
  - Target: 40 by Week 12 (GO scenario)

### Activation Funnel
| Stage | Week 1 | Week 4 | Week 8 | Week 12 | Target |
|-------|--------|--------|--------|---------|--------|
| Signup | - | - | - | - | - |
| Broker Connected | - | - | - | - | ≥60% |
| Paper Trading Started | - | - | - | - | ≥92% |
| Completed 7 Days Paper | - | - | - | - | ≥85% |
| Initiated Live Trading | - | - | - | - | ≥60% |
| First Live Trade | - | - | - | - | ≥86% |
| Weekly Active (W1) | - | - | - | - | ≥70% |

### Retention Cohorts
```
Week 1 Cohort: 20 users
  - W1 retention: [X%] (target: ≥70%)
  - W2 retention: [X%] (target: ≥40%)
  - W4 retention: [X%] (target: ≥30%)
  - W12 retention: [X%] (target: ≥20%)

Week 4 Cohort: 30 users
  - W1 retention: [X%]
  - W2 retention: [X%]
  - W4 retention: [X%]
```

### Revenue Metrics (If Monetizing)
- **MRR:** $[X] / $15K (Month 6 target)
- **ARPU:** $[X] / $150 (Starter tier)
- **LTV:CAC Ratio:** [X:1] / 3:1 (target)
- **Payback Period:** [X] months / 6 months (target)

### Product Health
- **NPS:** [X] / 50+ (target)
- **Avg Trades/Week per Active User:** [X] / 5 (target)
- **% Users with Positive PnL:** [X%] / 60%+ (target)
- **Platform Uptime:** [X%] / 99.5%+ (target)
- **Support Response Time:** [X] hours / <2 hours (target)

---

## 🚨 Red Flags & Kill Switches

**Stop and reassess if any of these occur:**

### Technical Red Flags
1. **Proof generation fails >1% of the time**
   - Action: Pause live trading, debug circuit
   - Backup: Revert to manual risk checks

2. **Broker API errors >5% (sustained for 24 hours)**
   - Action: Switch to backup broker (e.g., IBKR → Alpaca)
   - Backup: Notify users, offer manual execution

3. **Smart wallet exploit discovered**
   - Action: IMMEDIATE PAUSE of all live trading
   - Backup: Emergency contract upgrade, user fund recovery

### Business Red Flags
4. **WAST stagnant or declining for 3+ weeks**
   - Action: Run rapid user interviews (20+ in 1 week)
   - Decision: Iterate product or consider pivot

5. **NPS drops below 30**
   - Action: All-hands on support, gather feedback
   - Decision: Product has serious issues, consider halt

6. **Churn >20% monthly**
   - Action: Exit interview every churned user
   - Decision: Product not sticky enough, iterate retention

### Operational Red Flags
7. **Burn rate >$50K/month (pre-revenue)**
   - Action: Cut non-essential spend, extend runway
   - Decision: If <6 months runway, accelerate fundraising

8. **Co-founder misalignment on direction**
   - Action: Facilitated session with advisors
   - Decision: If unresolved, consider acqui-hire or shutdown

9. **Regulatory cease-and-desist from CIRO or CSA**
   - Action: IMMEDIATE HALT of all Canadian operations
   - Backup: Shift to UAE/ADGM markets only

### User Safety Red Flags
10. **User loses >$5K due to platform bug**
    - Action: Immediate incident response, user reimbursement
    - Investigation: Root cause analysis, prevent recurrence
    - Decision: If liability risk is existential, consider shutdown

---

## 📅 Weekly Operating Rhythm (All Scenarios)

**Monday 9:00 AM: Metrics Review (60 mins)**
- Review dashboard: WAST, funnel, retention, NPS
- Identify biggest blocker this week
- Set weekly OKRs (3 max)

**Wednesday 3:00 PM: User Insights Sharing (30 mins)**
- Share quotes from interviews or support tickets
- Discuss: What are users loving? What's frustrating them?
- Prioritize: Which feedback becomes next sprint's focus?

**Friday 4:00 PM: Week in Review (45 mins)**
- Review: Did we hit this week's OKRs?
- Retrospective: What went well? What didn't?
- Plan: What's the focus for next week?

**Monthly (Last Friday): Deep Dive (2 hours)**
- Comprehensive metrics review (full AARRR funnel)
- GO/NO-GO check: Are we on track for targets?
- Roadmap update: Adjust next month's plan based on data

---

## 🎯 Final Recommendations (Based on Your Scenario)



### If You Chose ITERATE:
1. **Be ruthless:** Only fix the *one* biggest blocker, don't boil the ocean
2. **Time-box it:** 4-6 weeks max. If not fixed by then, pivot or shut down
3. **High-bandwidth feedback:** Do 20+ interviews in iteration sprint, not 10
4. **A/B test always:** Run control vs. variant to prove iteration works
5. **Preserve cash:** Iteration budget should be <$5K (use free tools, no contractors)

### If You Chose PIVOT:
1. **Kill your darlings:** If broker connection is the issue, kill it entirely. Don't half-ass the pivot.
2. **Validate before building:** Run smoke tests for new direction (same as Experiment 1)
3. **Be honest with investors:** Tell them early, don't surprise them with pivot in next update
4. **Preserve team morale:** Pivots are hard. Celebrate learnings, not failures.
5. **Set a deadline:** If pivot validation fails in 4 weeks, seriously consider shutdown

---

## 📄 Document Control

**Version:** 1.0  
**Last Updated:** [Insert date]  
**Next Review:** [Weekly, every Monday]  
**Owner:** Zeshan Ahmad (CEO)  
**Approvers:** Daniel Oosthuyzen (CTO), [Board/Advisors if applicable]

**Change Log:**
| Date | Version | Changes | Author |
|------|---------|---------|--------|
| [Date] | 1.0 | Initial roadmap post-validation | Zeshan |
| | | | |
| | | | |

---

## 🔗 Related Documents

- [Hypothesis Prioritization](/tmp/refi-validation/hypothesis-prioritization.md)
- [Experiment Plan](/tmp/refi-validation/experiment-plan.md)
- [Success Metrics](/tmp/refi-validation/success-metrics.md)
- [Smoke Test Plan](/tmp/refi-validation/smoke-test-plan.md)
- [Validation Sprint Plan](/tmp/refi-validation/validation-sprint-plan.md)
- [Experiment Results Log](/tmp/refi-validation/experiment-results-log.md)
- [Dev Phases Technical Spec](/mnt/user-data/uploads/Dev-PhasesV2.pdf)

---

**Remember: This roadmap is a living document. Update it weekly based on learnings. The worst thing you can do is follow a stale plan.**

**The best founders adapt. The best plans enable adaptation.**

---

**Status:** [🟢 ACTIVE / 🟡 UNDER REVIEW / 🔴 PAUSED]  
**Current Phase:** [Phase 1 / Phase 2 / Phase 3 / Iteration / Pivot]  
**Days Since Validation Completed:** [X]  
**Days Until Next Milestone:** [X]

**Next Critical Decision Point:** [Insert date and decision]
