# ReFi.Trading MVP Definition
**Version:** 1.0  
**Target Launch:** Week 12 (February 2026)  
**Success Criterion:** 40+ WAST (Weekly Active Safe Traders)

---

## MVP Philosophy

**Riskiest Assumptions to Test:**
1. Will power-retail traders actually connect their brokers via OAuth?
2. Do zk-proofs build enough trust to overcome "black box AI" fear?
3. Will users transition from paper trading to live trading with real money?

**MVP = Minimum LOVABLE Product**
- Not "barely functional"—polished enough that users want to show friends
- Not "feature-complete"—deliberately limited to test core assumptions
- Not "throw-away code"—production-quality architecture that scales

**12-Week Build Sprint:** $70.5K budget (2.9% of $2.45M seed round)

---

## In-Scope Features (MVP)

### Core User Journey (Must-Have)
1. ✅ **Landing page** with clear value prop + alpha waitlist
2. ✅ **Sign-in with Ethereum (SIWE)** for wallet-based auth
3. ✅ **Broker connection** via SnapTrade OAuth (IBKR, Alpaca, Kraken, Coinbase)
4. ✅ **Paper trading dashboard** (7-14 days, 50 simulated orders minimum)
5. ✅ **zk-VaR proof verification** (<3ms generation, visual checkmark)
6. ✅ **ERC-4337 smart wallet** (deployed on zkSync Era testnet)
7. ✅ **Progressive caps system** ($100 → $500 → $5K)
8. ✅ **Human-in-the-loop UX** (click "Confirm" per trade)
9. ✅ **Live trading dashboard** (first real money trades)
10. ✅ **Kill switch** ("Pause All Trading" always visible)

### Supporting Infrastructure (Must-Have)
11. ✅ **PostgreSQL database** (users, accounts, trades, proofs)
12. ✅ **Redis cache** (hot portfolio data, API rate limiting)
13. ✅ **Event sourcing** (append-only log of all actions)
14. ✅ **PostHog analytics** (funnel tracking: signup → broker connect → paper → live)
15. ✅ **Email automation** (daily recap at 6 PM user time, welcome sequence)
16. ✅ **Grafana dashboard** (uptime, latency, proof gen p95, WAST)
17. ✅ **Status page** (public uptime monitoring)

### AI/Risk Layer (Must-Have)
18. ✅ **2 pre-trained RL models** (PPO for conservative, TD3 for aggressive)
19. ✅ **Regime detection** (trending/mean-reverting/high-vol/low-vol)
20. ✅ **zk-VaR circuit** (8 state variables, Circom, <65k constraints)
21. ✅ **SnarkJS proof worker** (WASM backend for speed)
22. ✅ **Proof anchoring** (zkSync Era L2 batch poster, 1 proof per trade)

### 2 Asset Classes (MVP)
23. ✅ **US Equities** (via IBKR/Alpaca)
24. ✅ **Crypto spot** (via Kraken/Coinbase, BTC, ETH, top 10 by market cap)

---

## Out-of-Scope Features (Phase 2+)

### Deferred to Post-MVP
- ❌ Custom risk parameter editor (use pre-set Conservative/Moderate/Aggressive)
- ❌ Options trading (complex, regulatory scrutiny, defer to Month 6+)
- ❌ Futures (same reason as options)
- ❌ Mobile app (web-first for alpha, mobile in Phase 2)
- ❌ Social features (leaderboards, copy trading—regulatory complexity)
- ❌ Referral program (focus on organic first)
- ❌ Custom model training (enterprise feature, Phase 3)
- ❌ Multi-user RBAC (enterprise feature, Phase 3)
- ❌ Token integration ($REFIN deferred to post-Series A 2027)
- ❌ DePIN node operator dashboard (Phase 4)
- ❌ Strategy Marketplace SDK (Phase 5)

### Deliberately Limited Scope
- **1 market regime detection algo** (not 5)—sufficient to prove concept
- **2 RL policies** (not 10)—enough for A/B test, not overwhelming
- **No customization** (users pick Conservative/Moderate/Aggressive, not tune parameters)
- **Email-only support** (no live chat, no Slack yet)
- **Single geography** (UAE/GCC focus for alpha)

---

## MVP User Stories

### Story 1: Power-Retail Trader #2
**Goal:** Trade US equities with AI assistance while keeping custody at IBKR

**Flow:**
1. Trader #2 visits refi.trading from LinkedIn ad
2. Reads hero: "Wall Street AI, Radically Accessible"
3. Clicks "Join Alpha Waitlist" → enters email
4. Receives "You're In! Next Steps" email within 1 hour
5. Week later: "Your Alpha Access is Ready" email
6. Clicks link → lands on /login
7. "Sign in with Ethereum" → connects MetaMask
8. Prompted: "Connect Your Broker" → clicks IBKR logo
9. SnapTrade OAuth redirect → logs into IBKR → approves read/write access
10. Returns to ReFi dashboard → sees "Portfolio Synced: $85K"
11. Selects risk profile: "Moderate (VaR ≤ 5%)"
12. Selects strategy: "TD3 Momentum Equity"
13. Starts paper trading → 50 simulated orders over 7 days
14. Dashboard shows: +$1,240 paper PnL, 2.1 Sharpe, -3.2% max DD
15. Day 8: Prompted "Ready for Live Trading? Start with $100 limit."
16. Clicks "Go Live" → 5-step checklist (set daily limit, confirm risk, enable kill switch, verify email, accept terms)
17. First real trade: AAPL 5 shares @ $180 = $900
18. AI proposes trade → 2-second proof generation → ✅ "Risk proof verified"
19. Trader #2 clicks "Confirm Trade"
20. Order sent to IBKR → filled at $180.05 → confirmation in dashboard
21. Daily recap email 6 PM: "Today's Activity: 1 trade, +$12.50 PnL"
22. Over 2 weeks: caps increase to $500, then $5K
23. Trader #2 invites 3 friends from WhatsApp trading group

**Success Criterion:** Trader #2 executes ≥3 trades/week for 4 consecutive weeks = ACTIVE SAFE TRADER ✅

---

## Technical Architecture (MVP)

### Frontend (Next.js 14+ App Router)
- **Framework:** Next.js with TypeScript, Tailwind CSS, shadcn/ui components
- **State Management:** Zustand (lightweight, no Redux complexity)
- **Web3:** Wagmi + RainbowKit (wallet connection), Viem (blockchain interactions)
- **Analytics:** PostHog (events, funnels, session replay)
- **Hosting:** Vercel (auto-deploy from GitHub main branch)

### Backend (NestJS)
- **Framework:** NestJS (Node.js, TypeScript, modular architecture)
- **Database:** PostgreSQL 15+ (Supabase or Railway)
- **Cache:** Redis 7+ (Upstash serverless)
- **Queue:** BullMQ (background jobs: proof generation, email sending, broker sync)
- **File Storage:** IPFS (Filebase for model checkpoints + proof metadata)
- **Hosting:** Railway or Fly.io (auto-scale, easy DB backups)

### Blockchain Layer
- **L2:** zkSync Era testnet for MVP (mainnet in Week 16)
- **Smart Contracts:**
  - ERC-4337 Account Abstraction wallet (Biconomy SDK)
  - Proof Verifier contract (verifies zk-SNARK from Groth16)
  - Batch Poster (anchors trade proofs on-chain)
- **Oracle:** Chainlink Price Feeds (if needed for DeFi integration Phase 2)

### AI/ML Layer
- **Models:** Pre-trained PyTorch models exported to TorchScript (deterministic inference)
- **Inference:** Python microservice (FastAPI) called via gRPC from NestJS backend
- **Proof Generation:** Rust-based Circom circuit compiled to WASM via SnarkJS
- **Data Pipeline:** Polygon.io for equities tick data, Kraken/Coinbase WebSockets for crypto

### Integration Layer
- **Broker API:** SnapTrade unified SDK (IBKR, Alpaca, Kraken, Coinbase)
- **Email:** Resend or SendGrid (transactional emails, daily recaps)
- **Monitoring:** Grafana Cloud (metrics), Sentry (error tracking), BetterStack (uptime)

---

## MVP Data Model (PostgreSQL)

### Core Tables

**users**
- id (UUID, PK)
- wallet_address (ETH address, unique, indexed)
- email (encrypted)
- created_at, updated_at
- alpha_wave (1 or 2)
- referral_code (unique, generated on signup)

**broker_connections**
- id (UUID, PK)
- user_id (FK → users)
- broker (enum: IBKR, Alpaca, Kraken, Coinbase)
- snaptrade_user_id (from SnapTrade)
- snaptrade_user_secret (encrypted)
- status (enum: connected, disconnected, error)
- connected_at, last_synced_at

**portfolios**
- id (UUID, PK)
- user_id (FK → users)
- broker_connection_id (FK → broker_connections)
- total_value_usd (decimal)
- cash_balance_usd (decimal)
- positions (JSONB: [{symbol, quantity, cost_basis, current_value}])
- updated_at (cache invalidation timestamp)

**trades**
- id (UUID, PK)
- user_id (FK → users)
- broker_connection_id (FK → broker_connections)
- symbol (e.g., AAPL, BTC)
- side (enum: buy, sell)
- quantity (decimal)
- limit_price (decimal, nullable)
- status (enum: proposed, proof_verified, submitted, filled, rejected, cancelled)
- proof_hash (SHA256 of zk-SNARK proof, nullable)
- zksync_tx_hash (nullable, anchored proof)
- ai_confidence_score (float 0-1)
- regime (enum: trending, mean_reverting, high_vol, low_vol)
- created_at, filled_at

**risk_profiles**
- id (UUID, PK)
- user_id (FK → users)
- profile_name (enum: Conservative, Moderate, Aggressive)
- max_var_pct (decimal, e.g., 0.03 = 3%)
- max_position_size_pct (decimal, e.g., 0.10 = 10%)
- max_daily_trades (integer)
- leverage_allowed (boolean, false for MVP)

**progressive_caps**
- id (UUID, PK)
- user_id (FK → users)
- current_day (integer, days since go-live)
- max_trade_size_usd (decimal, e.g., 100)
- max_daily_notional_usd (decimal, e.g., 500)
- updated_at

**event_log** (append-only, event sourcing)
- id (UUID, PK)
- user_id (FK → users, nullable for system events)
- event_type (enum: user_signup, broker_connected, trade_proposed, proof_generated, trade_filled, etc.)
- event_data (JSONB, full event payload)
- created_at (indexed for time-series queries)

---

## MVP API Endpoints (NestJS)

### Authentication
- `POST /auth/siwe/nonce` - Get SIWE nonce
- `POST /auth/siwe/verify` - Verify signed message, create session
- `POST /auth/logout` - Destroy session

### Broker Integration (via SnapTrade)
- `GET /brokers` - List supported brokers
- `POST /brokers/connect` - Get SnapTrade OAuth redirect URL
- `GET /brokers/callback` - Handle OAuth callback
- `GET /brokers/connections` - List user's connected brokers
- `DELETE /brokers/connections/:id` - Disconnect broker

### Portfolio
- `GET /portfolio` - Get current portfolio (cached, 4x/day sync)
- `POST /portfolio/sync` - Force sync from broker (rate-limited)

### Trading
- `POST /trades/propose` - AI proposes trade based on strategy
- `GET /trades/:id/proof` - Get zk-VaR proof for trade
- `POST /trades/:id/confirm` - User confirms trade (human-in-the-loop)
- `GET /trades` - List user's trade history
- `GET /trades/:id` - Get trade details + proof URL

### Risk & Strategy
- `GET /risk-profiles` - List available risk profiles
- `POST /risk-profiles/select` - Set user's risk profile
- `GET /strategies` - List available RL strategies (PPO, TD3)
- `POST /strategies/select` - Set user's active strategy

### Analytics (Internal)
- `GET /metrics/wast` - Weekly Active Safe Traders count
- `GET /metrics/funnel` - Conversion funnel (signup → broker → paper → live)

---

## MVP Success Metrics (Week 12 Targets)

### North Star Metric
- **WAST (Weekly Active Safe Traders):** ≥40
  - Definition: User who executed ≥1 trade with zk-proof verification in past 7 days

### Acquisition
- **Alpha Signups:** 50 (target), 75 (stretch)
- **Sources:** LinkedIn (40%), Reddit AMAs (30%), Referrals (20%), Other (10%)

### Activation
- **Broker Connect Rate:** ≥78% (validated in Experiment 1)
- **Time to First Trade:** ≤14 days median (7 days paper, 7 days live ramp)

### Retention
- **Week-over-Week:** ≥40% (W1→W2 retention)
- **Monthly Churn:** <5%

### Revenue (MVP = $0 Revenue, Proof-of-Value Only)
- **Willingness-to-Pay Confirmed:** ≥60% say "yes" to $350/month in exit survey
- **First Paying Users:** Week 13+ (post-alpha graduation)

### Product Health
- **NPS:** ≥50
- **Aggregate PnL:** ≥60% users positive
- **Support Tickets:** <2 per user (indicates good UX)
- **Critical Bugs:** 0 (system down, data loss, security breach)

### Technical Health
- **Uptime:** ≥99.5%
- **Proof Gen p95:** <3ms
- **Order-to-Fill p95:** <150ms
- **Broker API Error Rate:** <1%

---

## MVP Launch Checklist (Week 12)

### Pre-Launch (Weeks 9-11)
- [ ] 50 alpha invites sent (email + LinkedIn DM)
- [ ] All critical bugs resolved (P0 = none, P1 = ≤3)
- [ ] Load testing completed (100 concurrent users, no degradation)
- [ ] Security audit checklist completed (OWASP Top 10, no criticals)
- [ ] Backup & restore tested (database, Redis, smart contracts)
- [ ] Status page live (status.refi.trading)
- [ ] Support email monitored (support@refi.trading, <24h response SLA)
- [ ] Legal terms finalized (Terms of Service, Privacy Policy, Risk Disclosure)

### Launch Day (Week 12, Day 1)
- [ ] Deploy to production (Vercel frontend, Railway backend, zkSync mainnet)
- [ ] Send "We're Live!" email to 50 alpha users
- [ ] Post launch thread on Twitter (with screenshots + demo video)
- [ ] Publish launch blog post on refi.trading/blog
- [ ] Monitor Grafana dashboard continuously (first 24 hours)
- [ ] Founders available for emergency hotfixes (on-call)

### First Week (Week 12, Days 2-7)
- [ ] Daily standup at 9 AM MT / 11 PM SGT (30 min check-in)
- [ ] User interviews (5 users, 30 min each, gather feedback)
- [ ] Bug triage daily (P0 immediate, P1 within 48h, P2 backlog)
- [ ] Metrics dashboard review daily (WAST, funnel, uptime)
- [ ] Send personalized thank-you emails to first 10 active traders

---

## Risk Mitigation (MVP-Specific)

### Risk: Low Alpha Signup Rate
**Mitigation:**
- Pre-launch: Power-Retail Trader #2's 40-person WhatsApp group warm intro
- Week 9: Open waitlist to LinkedIn followers (3K+)
- Week 10: Reddit AMA on r/algotrading (50K+ members)
- Week 11: Influencer partnership (1 micro-influencer, $2K budget)

### Risk: High Broker Connect Drop-Off
**Mitigation:**
- Implement trust-building video (Experiment 3.1 from validation plan)
- Guided 3-step flow with progress bar
- Live chat support during onboarding (Intercom, first 2 weeks)

### Risk: Users Don't Go Live After Paper Trading
**Mitigation:**
- Progressive caps de-risked ($100 start felt safe in 12/14 interviews)
- Email nudge on Day 7: "Ready to go live? Start with just $100."
- Show paper trading PnL prominently (build confidence)

### Risk: zk-Proof Generation Latency Exceeds 3ms
**Mitigation:**
- Circuit optimized to <65k constraints (tested in dev)
- WASM backend pre-compiled (faster than native in some cases)
- Fallback: If >5ms, show warning but allow trade (don't block user)
- Phase 2: GPU-accelerated proof generation (DePIN nodes)

---

## Post-MVP Roadmap Teaser

**Week 13-16: Polish & Scale**
- Fix top 10 bugs from alpha feedback
- Add custom risk parameter editor (user-requested feature)
- Launch mobile-responsive PWA (not native app yet)
- Onboard Alpha Wave 2 (next 50 users)

**Month 5-6: Revenue Launch**
- Implement Stripe billing (Starter $150, Pro $350, Prime $995)
- First paying customers (graduate from alpha)
- Target: $50K MRR by Month 6

**Month 7-12: Scale to $3M ARR**
- Options trading support (via IBKR)
- 5 RL policy library (add RVI-Q, A3C, SAC)
- Social features (leaderboards, copy top performers WITH risk proofs)
- Fund Lite tier early access (2-3 pilot fund customers)

---

## Document Control

**Version:** 1.0  
**Date:** November 28, 2025  
**Next Review:** Week 4 (mid-sprint check-in)  
**Owners:** Zeshan Ahmad (Product), Daniel Oosthuyzen (Technical)  
**Approval:** Both founders signed off November 27, 2025

---

**"Ship fast, learn faster. 40 WAST or bust."**

*— ReFi.Trading MVP Definition v1.0*
