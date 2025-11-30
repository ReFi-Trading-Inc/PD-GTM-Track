# Technical Architecture Decision Records (ADRs)

## ADR-001: Multi-Broker via SnapTrade (Not Direct Integration)
**Date:** November 20, 2025  
**Status:** ✅ Accepted  
**Decision:** Use SnapTrade as unified broker gateway instead of direct IBKR/Alpaca APIs

**Rationale:**
- SnapTrade is pre-approved Alpaca partner (trading permissions)
- Single integration = 4 brokers (IBKR, Alpaca, Kraken, Coinbase)
- Reduces 8 weeks of OAuth + API implementation to 2 weeks
- SOC 2 Type II certified (compliance requirement)
- $1.50/user/month cost acceptable vs. engineering time saved

**Consequences:**
- ✅ Faster time-to-market (6 weeks saved)
- ✅ Compliant Alpaca access (otherwise unavailable)
- ⚠️ New dependency on SnapTrade (mitigated via direct IBKR backup plan)
- ⚠️ Per-user cost vs. free direct API (acceptable at current scale)

---

## ADR-002: zkSync Era for L2 (Not Optimism or Arbitrum)
**Date:** November 22, 2025  
**Status:** ✅ Accepted  
**Decision:** Deploy smart contracts + proof anchoring on zkSync Era

**Rationale:**
- Native zk-rollup architecture (vs. optimistic rollups)
- Aligns with zk-SNARK proof strategy (zkSync = zk-native)
- Lower gas costs than Ethereum mainnet ($0.05 vs. $5 per proof)
- ERC-4337 account abstraction support (via zkSync SDK)
- Strong ecosystem growth (Matter Labs $250M funding)

**Consequences:**
- ✅ Cost-effective proof anchoring at scale
- ✅ Native zk-proof compatibility
- ⚠️ Less mature than Optimism (accepted risk for cost savings)
- ⚠️ Potential migration to Ethereum mainnet Phase 4 if needed

---

## ADR-003: PostgreSQL + Redis (Not MongoDB + In-Memory)
**Date:** November 18, 2025  
**Status:** ✅ Accepted  
**Decision:** PostgreSQL for primary DB, Redis for caching/sessions

**Rationale:**
- ACID compliance critical for financial data (trades, balances)
- JSONB support = flexible schema where needed (portfolio positions)
- Supabase/Railway managed hosting = easy backups + scaling
- Redis = battle-tested for caching (4x/day broker syncs)
- NoSQL (MongoDB) unnecessary complexity for our relational data model

**Consequences:**
- ✅ Data integrity guaranteed (no lost trades)
- ✅ Familiar SQL tooling for team
- ✅ Easy migration to RDS/CloudSQL if scaling beyond 10K users
- ⚠️ Write-heavy workloads may need sharding Phase 3+ (acceptable)

---

## ADR-004: Pre-Trained Models (Not Real-Time Training)
**Date:** November 25, 2025  
**Status:** ✅ Accepted  
**Decision:** Deploy pre-trained RL models (PPO, TD3) for MVP, defer online learning

**Rationale:**
- 3.1-year backtest validation: 28% CAGR, 2.07 Sharpe (proven models)
- Real-time training = complex infrastructure (GPU clusters, data pipeline)
- MVP goal = prove non-custodial + zk-proofs, not cutting-edge RL
- Custom model training = enterprise feature ($10K setup fee) Phase 3

**Consequences:**
- ✅ Faster MVP (no training infrastructure needed)
- ✅ Predictable performance (validated backtest results)
- ⚠️ Models don't adapt to changing markets (mitigated via quarterly retraining)
- ⚠️ Competitive disadvantage vs. adaptive algos (Phase 2 roadmap item)

---

## ADR-005: Email-Only Support (Not Live Chat) for MVP
**Date:** November 27, 2025  
**Status:** ✅ Accepted  
**Decision:** Support via email (support@refi.trading) with 24-hour SLA, no live chat

**Rationale:**
- Alpha = 50 users, manageable via email
- Live chat = $500/month (Intercom) + 24/7 coverage burden
- Email = asynchronous, allows thoughtful responses
- Slack community (post-Week 9) provides peer support

**Consequences:**
- ✅ Cost savings ($6K/year)
- ✅ Founders can handle support directly (build empathy)
- ⚠️ Slower response time (acceptable for alpha, upgrade Phase 2)
- ⚠️ May frustrate users expecting instant support (set expectations upfront)

---

## ADR-006: Next.js + Vercel (Not React SPA + AWS)
**Date:** November 15, 2025  
**Status:** ✅ Accepted  
**Decision:** Next.js 14+ App Router on Vercel for frontend

**Rationale:**
- Server-side rendering (SSR) = better SEO for landing page
- Built-in API routes = simpler backend-for-frontend pattern
- Vercel auto-deploy from GitHub main = zero DevOps overhead
- Edge functions = low-latency for global users (UAE, Canada, USA)

**Consequences:**
- ✅ Fast development velocity (hot reload, TypeScript support)
- ✅ Zero infrastructure management (Vercel handles CDN, SSL, scaling)
- ⚠️ Vendor lock-in to Vercel (mitigated via Next.js portability)
- ⚠️ Cost scales with traffic ($20/mo free → $1K+/mo at scale, acceptable)

---

## Decision Log
| ADR | Decision | Date | Status | Owner |
|-----|----------|------|--------|-------|
| 001 | SnapTrade API | Nov 20 | ✅ Accepted | Zeshan |
| 002 | zkSync Era L2 | Nov 22 | ✅ Accepted | Daniel |
| 003 | PostgreSQL + Redis | Nov 18 | ✅ Accepted | Daniel |
| 004 | Pre-Trained Models | Nov 25 | ✅ Accepted | Daniel |
| 005 | Email-Only Support | Nov 27 | ✅ Accepted | Zeshan |
| 006 | Next.js + Vercel | Nov 15 | ✅ Accepted | Daniel |

**Next ADR:** Week 4 (post-sprint 1 retro)
