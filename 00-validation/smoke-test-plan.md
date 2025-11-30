# Smoke Test Plan - ReFi.Trading Broker Connection Validation

**Team:** ReFi.Trading  
**Product:** ReFi.Trading - Non-Custodial RL Trading Platform  
**Created:** November 28, 2025

---

## Objective

**What We're Testing:**  
Whether power-retail traders and small fund operators in UAE/GCC who are frustrated with manual trading will connect their brokerage account to ReFi.Trading within 7 days of expressing interest.

**Why This Matters:**  
Broker connection is the #1 blocker to validating our core product. Without users granting trading access, we cannot test RL agent performance, generate revenue (execution fees), or prove our value proposition. If <60% of interested users complete broker connection, our entire go-to-market strategy needs to pivot.

---

## Hypothesis

**We believe that** power-retail traders (3+ years experience, $10K+ accounts) and fund operators (<$50M AUM) in the UAE/GCC region who are currently using fragmented tool stacks (costing $300-600/month) and making emotional trading decisions **will** connect their brokerage account via SnapTrade to access our RL-driven, non-custodial trading platform.

**We will know we're right when** 60% or more of users who click "Connect Your Broker in 60 Seconds" on our landing page successfully complete the simulated OAuth flow to the "Connection Successful" screen within 7 days.

---

## Test Design

### The Value Proposition

**Problem we're solving:**  
"You're spending $300-600/month on fragmented tools (TradingView, data feeds, execution platforms) and still making emotional trades that cost you 15-30% in annual returns. You lack the $10M infrastructure budget that hedge funds use to build algorithmic trading systems."

**Solution promise:**
"ReFi.Trading compresses a $10M hedge fund quant desk into a 3-click app. Deploy institutional-grade RL algorithms in under 20 minutes. Your assets stay at your broker (IBKR/Alpaca) - we never take custody. Every trade is verified by zero-knowledge proofs before execution. Start with $100 risk limits, scale to $5000+ as you build confidence."

**Target user:**  
- **Primary:** Power-retail traders in UAE/Saudi/GCC (3+ years trading experience, $10-250K account size, actively trading 3+ times per week)
- **Secondary:** Fund operators with <$50M AUM lacking in-house quant infrastructure
- **Geographic focus:** UAE (ADGM RegLab target), Saudi Arabia, Qatar, Bahrain (English-speaking, crypto-friendly jurisdictions)

---

### Smoke Test Asset Type

**Type:** Landing page with simulated broker connection flow

**Why this type:**
- **Fastest to validate demand (1-2 weeks)** without building full SnapTrade production integration (3-4 weeks)
- **Tests willingness to grant broker access** (our highest-risk assumption) before investing in real OAuth
- **Low friction for users** - takes 60 seconds to click through, doesn't require real credentials
- **Easy to iterate** - can A/B test messaging, broker selection screen, OAuth copy quickly

**Tools:**
- **Landing page:** Webflow (more design flexibility than Carrd for fintech credibility)
- **Mock OAuth:** Custom HTML/CSS (looks real but doesn't actually connect)
- **Analytics:** PostHog (event tracking) + Hotjar (heatmaps, session recordings)
- **Email collection:** Airtable embedded form
- **Survey:** Typeform (post-connection intent survey)

**Time to build:** 6 hours
**Time to run:** 7 days
**Total:** 9 days (Dec 2-13, 2025)

---

## Asset Content

### Headline

**Option A (Problem-First):**  
"Stop Losing 15-30% Returns to Emotional Trading"

**Option B (Solution-First):**  
"Wall Street AI, Radically Accessible"

**Testing:** Will A/B test both (50/50 traffic split) to see which drives higher broker connection rate

**Why these options:**
- Option A addresses pain directly (loss aversion)
- Option B emphasizes democratization (aspirational)
- Both avoid hype ("guaranteed returns") in favor of clear positioning

---

### Subheadline / Value Proposition

"Power-retail traders and small funds spend $300-600/month on fragmented tools (TradingView, data, execution) and still make emotional decisions. ReFi.Trading gives you institutional-grade RL algorithms in 3 clicks. Your assets never leave your broker. Every trade verified by zero-knowledge proofs. Start with $100 caps, scale as you build confidence."

**Character count:** 345 (optimal for scanning, <400 char limit)

---

### Key Benefits (5 bullet points)

- 📊 **Institutional AI in Your Pocket:** TD3/PPO ensemble RL agents trained on 3+ years of walk-forward data. 28% CAGR, 2.07 Sharpe ratio, <7.5% max drawdown in backtests.

- 🔐 **Non-Custodial by Design:** Your assets stay at IBKR/Alpaca. We send orders, you hold keys. ERC-4337 smart contract wallets ensure we can never withdraw funds.

- ✅ **Cryptographically Verified Risk:** Every trade passes a zk-SNARK proof before execution. VaR limits enforced mathematically, not just in software. Audit trail on zkSync Era.

- 🎯 **Progressive Caps = No Fear:** Start with $100 max position. Unlock $500 after Day 3, $5000 after Day 7. Paper trade first, go live when you're ready.

- ⚡ **Deploy in 20 Minutes:** Connect broker (60 seconds) → Select strategy (PPO, TD3, or hybrid) → Set risk limits → Go. No coding, no infrastructure, no $10M budget.

**Why these benefits:**
- Each addresses a specific pain point from user interviews (cost, trust, complexity, fear, time)
- Quantified claims (28% CAGR, <7.5% DD) provide credibility via backtest results
- Technical details (TD3/PPO, zk-SNARK, ERC-4337) signal sophistication to prosumers
- Progressive caps messaging reduces activation friction (tested in Experiment 3)

---

### Social Proof

**Section title:** "Built by Traders Who Felt Your Pain"

**Content:**
- "Based on 10+ interviews with UAE and GCC algo traders about their tool stack frustrations"
- "Backed by Outlier Ventures (leading Web3 accelerator) and Chainlink BUILD program"
- "Adjunct Professor in Blockchain & Cryptography (Georgia State) + 10-year HFT engineer"
- "USPTO Patent Filed: 'System and Method for Non-Custodial, Zero-Knowledge-Verified RL Trading'"

**Why this social proof:**
- User interviews = product-market fit research (not just guessing)
- Outlier Ventures + Chainlink = institutional validation (reduces "is this a scam?" concern)
- Academic/engineering credentials = technical credibility
- USPTO patent = IP moat + serious commitment

---

### Call to Action (CTA)

**Primary CTA button text:** "Connect Your Broker in 60 Seconds"

**Why this CTA:**
- **Action verb ("Connect")** - clearer than vague "Get Started" or "Learn More"
- **Benefit ("Your Broker")** - emphasizes non-custodial (you keep control)
- **Time constraint ("60 Seconds")** - reduces perceived effort
- **Alternative tested:** "See How It Works" (lower commitment, but less targeted)

**After click (simulated flow):**
1. **Broker Selection Screen:**
   - Two options with logos: "Interactive Brokers" | "Alpaca"
   - Under each: "Why choose IBKR?" / "Why choose Alpaca?" (educational tooltips)
   - "Your assets stay at your broker - we send orders, you keep keys"
   
2. **Mock OAuth Authorization:**
   - Looks like real IBKR/Alpaca login
   - **Disclaimer at top:** "This is a demo to test UX - not connecting your real account"
   - Username/password fields (pre-filled with "demo")
   - "Authorize ReFi.Trading" button with scope list: "Read portfolio, Execute trades (with limits)"
   
3. **Connection Successful Screen:**
   - ✅ "Connected to IBKR/Alpaca Demo Account"
   - "Next Steps: Set Your Risk Limits"
   - Dashboard preview showing: Portfolio ($10K), First Trade Recommendation, zk-VaR Proof Status
   - **Post-Connection Survey (2 questions):**
     - Q1: "On a scale 1-10, how likely are you to complete this process with your REAL broker credentials?" (1-10 slider)
     - Q2: "What concerns do you have about connecting your brokerage account?" (open text, 200 char limit)

**What happens after:**
- Immediate email: "Thanks for testing! Here's what happens next in the real flow..." (sets expectations)
- Within 24 hours: Personal email from Zeshan with interview invitation (15 min, $25 gift card offered to first 10)

---

### Wireframe / Design

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[HEADER]
🔹 ReFi.Trading Logo | [About] [How It Works] [Pricing]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[HERO SECTION - Full width, gradient background]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
   STOP LOSING 15-30% RETURNS TO EMOTIONAL TRADING
   
   Power-retail traders and small funds spend $300-600/mo
   on fragmented tools and still make emotional decisions.
   ReFi.Trading gives you institutional-grade RL algorithms
   in 3 clicks.
   
   [Connect Your Broker in 60 Seconds] ← Big CTA button
   
   Your assets never leave your broker | Verified by zk-proofs
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[PROBLEM SECTION - 2 columns]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
   The Quant Infrastructure Gap
   
   Left Column:                   Right Column:
   Hedge Funds Have:             You're Stuck With:
   ✓ $10M quant desks            ❌ $300-600/mo tool sprawl
   ✓ RL algorithms               ❌ Manual TradingView scripts
   ✓ Risk systems                ❌ Emotional decisions
   ✓ 24/7 execution              ❌ Fragmented execution
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[SOLUTION SECTION - 5 benefit cards in grid]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
   How ReFi.Trading Levels the Playing Field
   
   [Card 1: Institutional AI]   [Card 2: Non-Custodial]
   📊 TD3/PPO Ensemble         🔐 Assets at Your Broker
   28% CAGR, 2.07 Sharpe       ERC-4337 Smart Wallets
   
   [Card 3: Verified Risk]      [Card 4: Progressive Caps]
   ✅ zk-SNARK Proofs          🎯 $100 → $500 → $5000
   VaR Enforced On-Chain       Build Confidence Safely
   
   [Card 5: 20-Min Deploy]
   ⚡ Connect → Select → Set → Go
   No Code, No $10M Budget
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[HOW IT WORKS - 3-step visual]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
   Step 1: Connect Broker (60s)  →  Step 2: Set Limits  →  Step 3: Go Live
   [IBKR/Alpaca logos]               [VaR slider visual]      [Dashboard preview]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[SOCIAL PROOF]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
   Built by Traders Who Felt Your Pain
   
   🎓 Adjunct Prof (Blockchain) + 10-Yr HFT Engineer
   🚀 Backed by Outlier Ventures & Chainlink BUILD
   📋 Based on 10+ UAE/GCC Trader Interviews
   🏛️ USPTO Patent Filed (Non-Custodial zk-Verified Trading)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[FINAL CTA SECTION]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
   Ready to Trade Like a Hedge Fund?
   
   Connect your broker. Set your limits. Let the AI trade.
   
   [Connect Your Broker in 60 Seconds] ← Big CTA button
   
   Your assets never leave IBKR/Alpaca
   First 50 alpha users get priority access
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[FOOTER]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
About | Privacy | Terms | Discord | LinkedIn | X
© 2025 ReFi.Trading Inc. | ADGM RegLab Approved
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Design notes:**
- **Mobile-first:** 70%+ traffic expected on mobile (UAE traders check phones constantly)
- **Gradient background:** Purple/blue gradient (crypto aesthetic) for hero section
- **Trust badges:** IBKR/Alpaca logos, Chainlink logo, Outlier Ventures logo
- **Proof screenshot:** Include actual zk-VaR proof visual (builds credibility)
- **No stock photos:** Use actual product screenshots (dashboard, proofs, trades)

---

## Success Criteria

### Primary Metric

**Metric:** Simulated broker connection completion rate

**Success thresholds:**
- **Strong validation (≥75%):** Users are VERY willing to connect - build real SnapTrade integration immediately, this is not a blocker
- **Good validation (60-74%):** Users are willing - proceed with real integration, but monitor closely and optimize messaging
- **Weak signal (40-59%):** Mixed results - need more data or messaging iteration before investing in real integration
- **Invalid (<40%):** Major trust barrier - pivot to demo accounts, view-only mode, or different onboarding strategy

**Minimum sample size:** 100 visitors (±10% margin of error at 95% confidence)

**Calculation:**
```
Completion Rate = (Connection Success / CTA Click) × 100

Where:
- CTA Click = users who clicked "Connect Your Broker in 60 Seconds"
- Connection Success = users who reached "Connection Successful" screen
```

**Why these thresholds:**
- 60% is industry benchmark for "good" activation (top quartile fintech SaaS)
- Our bar is high because broker connection is our core activation, not a nice-to-have
- If <60%, real broker connection (more friction than simulation) will be even lower
- 75%+ would be exceptional, suggests our messaging is very compelling

---

### Secondary Metrics

| Metric | Target | Tool | Why It Matters |
|--------|--------|------|----------------|
| **Post-connection intent score** | Average ≥7/10 | Typeform survey | Validates simulation behavior predicts real behavior. If completion is high but intent is low, users are just clicking through without commitment. |
| **Time on page (landing)** | Median ≥60 seconds | Hotjar | If <30 seconds, users aren't reading value prop - problem is messaging clarity or relevance. |
| **Scroll depth** | ≥75% scroll to bottom | Hotjar | Validates users are engaging with full page, not bouncing after hero section. |
| **Broker preference** | Track IBKR vs. Alpaca ratio | PostHog | Informs which broker to prioritize for real integration. Expect 60/40 IBKR/Alpaca based on UAE market. |
| **Drop-off point** | Identify where users abandon | PostHog funnel | If drop-off is at broker selection (early), problem is trust. If at OAuth (late), problem is perceived complexity. |
| **Traffic source performance** | Compare LinkedIn vs. WhatsApp vs. X | UTM parameters | Identifies highest-quality lead sources for future campaigns. |

---

## Distribution Plan

### Target Channels

**Channel 1: LinkedIn Fintech Groups**

- **Specific tactic:** Post in "UAE FinTech Professionals" (850 members), "GCC Algo Traders" (320 members), "Quantitative Finance Middle East" (540 members)
- **Expected reach:** 500 engaged members (not all 1700 - many inactive)
- **Expected traffic:** 40 visitors (8% CTR - conservative for professional groups)
- **Cost:** $0 (organic posts)
- **Timeline:** Day 1 (Monday) at 9 AM UAE time (peak engagement for professionals)
- **Message:**
  "After interviewing 10+ UAE algo traders, I've learned everyone is spending $300-600/month on fragmented tools (TradingView + data feeds + execution) and still making emotional trades.

  We're building ReFi.Trading to compress a $10M hedge fund quant desk into a 3-click app. Institutional RL algorithms, non-custodial (your assets stay at IBKR/Alpaca), every trade verified by zk-proofs.

  Testing broker connection UX - takes 60 seconds to see if you'd grant trading access: [link]

  Not asking for real credentials - just validating demand before building full integration. First 50 get priority alpha access."

**Why this message works:**
- Opens with research credibility ("interviewed 10+ traders")
- Quantifies pain ($300-600/mo)
- Technical details appeal to sophisticated audience
- Transparency about "testing UX" reduces pressure
- Scarcity ("first 50") creates urgency

---

**Channel 2: UAE/GCC Trader WhatsApp Groups**

- **Specific tactic:** Direct message to "Dubai Crypto Traders" (180 members), "Saudi Algo Trading" (90 members) - both via personal network connections
- **Expected reach:** 270 traders (active groups, high engagement)
- **Expected traffic:** 30 visitors (11% CTR - higher than LinkedIn due to warm network)
- **Cost:** $0 (personal network)
- **Timeline:** Day 2 (Tuesday) at 6 PM UAE time (after market close, when traders relax)
- **Message:**
  "Quick favor from the group - testing broker connection flow for a new algo trading platform I'm building.
  
  Takes 60 seconds to click through a demo (NOT connecting your real broker, just testing UX).
  
  If you've ever been frustrated with TradingView scripts or paying for 5 different tools, this might interest you: [link]
  
  Feedback appreciated! First 10 who complete get a 15-min call to shape the product."

**Why this message works:**
- "Quick favor" = low-pressure ask
- "NOT connecting real broker" = removes fear
- "5 different tools" = relatable pain point
- "First 10...shape the product" = exclusive, co-creation appeal

---

**Channel 3: X (Twitter) + Reddit Algo Trading**

- **Specific tactic:** Thread on X with screenshots + cross-post to r/algotrading (850K members)
- **Expected reach:** 
  - X: 500 impressions (small following, but targeted #AlgoTrading #Fintech hashtags)
  - Reddit: 2000 impressions (top 25% of posts get ~2K views in 24 hours)
- **Expected traffic:** 30 visitors (1.2% CTR - lower than groups, but broader reach)
- **Cost:** $0 (organic)
- **Timeline:** Day 3 (Wednesday) at 2 PM UTC (peak r/algotrading activity)
- **X Thread (6 tweets):**
  
  **Tweet 1:**
  "Wall Street AI, Radically Accessible 🧵
  
  After 10+ interviews with retail algo traders, I learned everyone faces the same problem: spending $300-600/mo on fragmented tools and still making emotional trades.
  
  Here's what we're building to fix it:"
  
  **Tweet 2:**
  "The Problem: You want to trade algorithmically but don't have $10M to build infrastructure.
  
  So you cobble together: TradingView ($60) + data feeds ($150) + execution platform ($100) + backtesting ($90) + risk monitoring ($100).
  
  And you STILL override the algo emotionally."
  
  **Tweet 3:**
  "ReFi.Trading compresses a hedge fund quant desk into a 3-click app.
  
  ✓ Institutional RL algorithms (TD3/PPO ensemble)
  ✓ Non-custodial (assets at YOUR broker)
  ✓ Every trade verified by zk-proofs
  ✓ Start with $100 caps, scale to $5K+
  
  28% CAGR in 3-yr backtests."
  
  **Tweet 4:**
  "Non-custodial is key.
  
  Your assets stay at IBKR/Alpaca. We send orders via SnapTrade, you keep keys.
  
  ERC-4337 smart contract wallets ensure we can NEVER withdraw funds.
  
  Post-FTX, this is the only way retail should do automated trading."
  
  **Tweet 5:**
  "I'm testing broker connection UX before building the full integration.
  
  Takes 60 seconds to see the flow (demo, not real connection): [link]
  
  If you've ever wanted to trade like a quant fund, check it out."
  
  **Tweet 6:**
  "First 50 who complete get priority alpha access.
  
  We're targeting ADGM RegLab launch in UAE first, then global expansion.
  
  Would love your feedback: What would make YOU trust an algo trading platform?"

**Reddit Post Title:** "Building non-custodial RL trading platform - testing broker connection UX (demo, 60 seconds)"

**Reddit Post Body:**
"Hey r/algotrading,
  
I've been interviewing retail algo traders and everyone has the same frustration: spending $300-600/month on fragmented tools (TradingView, data feeds, execution) and still making emotional trades that hurt returns.
  
I'm building ReFi.Trading to compress a $10M hedge fund quant desk into a 3-click app:
- Institutional RL algorithms (TD3/PPO ensemble trained on 3+ years walk-forward)
- Non-custodial (your assets stay at IBKR/Alpaca, we just send orders)
- Every trade verified by zk-SNARK proofs before execution
- Progressive caps ($100 → $500 → $5000) to build confidence
  
Before building the full SnapTrade integration (3-4 week project), I want to validate that broker connection isn't a blocker.
  
I've built a 60-second demo flow (NOT connecting your real broker, just testing UX): [link]
  
Would appreciate feedback:
1. Would you actually connect your real broker to something like this?
2. What would make you trust it?
3. What concerns do you have?
  
First 50 who complete get priority alpha access when we launch in ADGM RegLab (UAE).
  
Tech stack for the curious: Google AI Agent Platform (RL inference), zkSync Era (proof anchoring), ERC-4337 (smart wallets), SnapTrade (broker APIs). Happy to discuss architecture.
  
Thanks!"

**Why this works:**
- Long-form allows technical detail (Reddit rewards depth)
- "Not connecting real broker" repeated (removes fear)
- Asking for specific feedback (not just clicks) = higher engagement
- Tech stack details = credibility with r/algotrading audience
- Mention of Alpaca supports proof that we work with modern APIs

---

### Total Expected Reach

| Channel | Reach | Est. CTR | Est. Visitors |
|---------|-------|----------|---------------|
| LinkedIn Groups | 500 | 8% | 40 |
| WhatsApp Groups | 270 | 11% | 30 |
| X + Reddit | 2500 | 1.2% | 30 |
| **TOTAL** | **3270** | **3.1%** | **100** |

**Confidence level:** Medium-High
- LinkedIn/WhatsApp are warm networks (high confidence)
- X/Reddit are cold but targeted (medium confidence)
- If <80 visitors by Day 5, pivot to paid LinkedIn ads ($50 budget) or extend timeline

---

## Timeline

```
Day 1 (Mon Dec 2):  Build landing page (Webflow) + mock OAuth flow
                    Set up PostHog events + Hotjar heatmaps
                    Test flow end-to-end on mobile + desktop
                    
Day 2 (Tue Dec 3):  Launch to LinkedIn groups (9 AM UAE)
                    Launch to WhatsApp groups (6 PM UAE)
                    
Day 3 (Wed Dec 4):  Launch to X/Reddit (2 PM UTC)
                    Monitor first 24 hours of traffic
                    
Day 4-9:            Daily check: traffic, conversions, drop-offs
                    Respond to all comments/questions within 2 hours
                    DM users who complete flow for interviews
                    
Day 10 (Fri Dec 13): Close experiment
                     Export PostHog funnel data + Hotjar recordings
                     Export Typeform survey responses
                     Compile verbatim comments
                     
Day 11 (Sat Dec 14): Analysis session (Zeshan + Daniel)
                     Decision: Persevere, Pivot, or Iterate?
```

**Start:** Monday, December 2, 2025  
**End:** Saturday, December 14, 2025  
**Duration:** 13 days (includes 1 day buffer)

---

## Follow-Up Plan

### For People Who Complete Simulation (Automated)

**Email 1: Immediate Thank You (triggered on "Connection Successful" screen)**

**Subject:** "You're on the ReFi.Trading Alpha Waitlist"

**Body:**
```
Hi [Name],

Thanks for testing our broker connection flow!

You're one of the first [X] traders interested in bringing hedge fund AI to retail.

What happens next:
- Real SnapTrade integration launches in 3 weeks (early January)
- You'll get priority alpha access (first 50 users)
- We'll reach out within 48 hours for a 15-min feedback call

In the meantime, any questions? Just reply to this email.

Best,
Zeshan Ahmad
Founder, ReFi.Trading

P.S. We're offering $25 Amazon gift cards to the first 10 users who do a 15-min interview. Interested? Book a time: [Calendly link]
```

**Why this works:**
- Immediate confirmation (reduces "did it work?" anxiety)
- Clear next steps (sets expectations)
- Personalized (from founder, not generic support@)
- Incentive for interview (gift card)

---

### For People Who Complete Simulation (Manual, within 24hrs)

**Email 2: Interview Invitation**

**Subject:** "15 minutes to shape ReFi.Trading? ($25 gift card)"

**Body:**
```
Hey [Name],

Thanks again for testing our broker connection flow yesterday.

Since you're one of the first traders to express interest, I'd love 15 minutes of your time to understand:
- What you liked/disliked about the connection flow
- What would make you trust ReFi.Trading with real broker access
- What features would be most valuable to you

As a thank-you, I'll send you a $25 Amazon gift card (first 10 respondents).

When works for you this week?
[Calendly link with UAE/GCC timezone slots]

Also, you'll get:
- First access when we launch in early January
- Direct line to me for feature requests
- Free Pro tier for first 3 months (usually $350/mo)

Sound good?

Best,
Zeshan

P.S. If you're not interested in the call, no worries - you're still on the priority alpha list.
```

**Why this works:**
- Personal (from Zeshan, not automated)
- Clear value exchange (15 min → $25 + benefits)
- Low-pressure (opt-out okay)
- Multiple incentives (gift card, early access, free tier)

---

### For People Who Drop Off

**Email 3: Recovery Campaign (sent 3 days after drop-off)**

**Subject:** "Quick question about ReFi.Trading"

**Body:**
```
Hi [Name],

I noticed you started our broker connection demo but didn't finish.

I'd love to understand why - was it:
- Not clear what we do?
- Concerned about security?
- Just browsing, not ready to commit?
- Something else?

Would really appreciate 30 seconds of feedback: [2-question Typeform]

Thanks,
Zeshan

P.S. If you're still interested, we're launching alpha in early January. The demo is still live: [link]
```

**Why this works:**
- Acknowledges they started (shows attention)
- Multiple-choice options (easy to answer)
- No pressure to complete flow
- Re-engages with reminder

---

## Measurement & Tracking

### Analytics Setup

**PostHog Events Tracked:**

```javascript
// Landing page
posthog.capture('landing_page_viewed', {
  variant: 'A' or 'B',  // headline A/B test
  source: utm_source,
  medium: utm_medium,
  campaign: utm_campaign
})

// CTA interaction
posthog.capture('cta_clicked', {
  cta_location: 'hero' or 'footer',
  cta_text: 'Connect Your Broker in 60 Seconds'
})

// Broker selection
posthog.capture('broker_selected', {
  broker: 'IBKR' or 'Alpaca',
  time_on_selection_screen: seconds
})

// OAuth simulation
posthog.capture('oauth_initiated', {
  broker: 'IBKR' or 'Alpaca'
})

posthog.capture('oauth_completed', {
  broker: 'IBKR' or 'Alpaca',
  time_to_complete: seconds
})

// Success
posthog.capture('connection_success', {
  broker: 'IBKR' or 'Alpaca',
  total_time: seconds,
  survey_submitted: true/false
})

// Survey
posthog.capture('survey_submitted', {
  intent_score: 1-10,
  concerns: [text],
  broker: 'IBKR' or 'Alpaca'
})
```

**Hotjar Setup:**
- Heatmaps: Track where users click, scroll depth
- Session recordings: Watch 20+ sessions to identify friction points
- Funnel tracking: Visualize drop-offs

**UTM Parameters:**
- LinkedIn: `?utm_source=linkedin&utm_medium=group&utm_campaign=smoke_test_broker`
- WhatsApp: `?utm_source=whatsapp&utm_medium=group&utm_campaign=smoke_test_broker`
- X: `?utm_source=twitter&utm_medium=organic&utm_campaign=smoke_test_broker`
- Reddit: `?utm_source=reddit&utm_medium=post&utm_campaign=smoke_test_broker`

**Dashboard:** PostHog custom dashboard showing:
- Real-time visitor count
- Conversion funnel (landing → CTA → broker → OAuth → success)
- Drop-off points highlighted in red
- Traffic sources breakdown
- Time-series chart (visitors over time)

---

## Decision Framework

### Actual Results (Fill in after test)

**Visitors:** [100]  
**CTA Clicks:** [75] (75% clicked "Connect Your Broker")  
**Broker Selected:** [65] (87% of clickers selected a broker)  
**OAuth Initiated:** [58] (89% of selectors started OAuth)  
**Connection Success:** [52] (90% of OAuth starters completed)  
**Overall Conversion:** [52/75 = 69%] (CTA clicks → success)

### Interpretation

**If ≥75% conversion (52+ completions from 75 CTA clicks):**
→ **STRONG VALIDATION** - Users are very willing to grant broker access
→ **Action:** Build real SnapTrade integration immediately (Week 1-2 of MVP sprint)
→ **Next:** Begin Experiment 2 (trust + zk-proof validation) while engineering works on SnapTrade

**If 60-74% conversion (45-51 completions):**
→ **GOOD VALIDATION** - Users are willing, but with some hesitation
→ **Action:** Proceed with real SnapTrade integration, but optimize messaging first
→ **Deep dive:** Interview both completers AND drop-offs to understand barriers
→ **Next:** A/B test different trust messaging (e.g., "Your money never leaves your broker" vs. "Non-custodial = you keep keys")

**If 40-59% conversion (30-44 completions):**
→ **WEAK SIGNAL** - Mixed results, not confident enough to invest in full integration
→ **Action:** Iterate on messaging OR test alternative onboarding (demo accounts, view-only mode)
→ **Deep dive:** Where did drop-offs happen? Broker selection? OAuth screen?
→ **Next:** Re-run experiment with 2-3 different messaging variants, measure which performs best

**If <40% conversion (<30 completions):**
→ **INVALID HYPOTHESIS** - Major trust barrier, current approach won't work
→ **Pivot options:**
  - **Option A:** Offer demo accounts (no broker connection required)
  - **Option B:** View-only mode first (read portfolio, show recommendations, don't trade)
  - **Option C:** Different broker strategy (find broker with simpler OAuth, or manual API key entry)
→ **Next:** User interviews with both completers AND drop-offs to diagnose root cause

---

## Risks & Mitigation

| Risk | Likelihood | Impact | Mitigation Strategy |
|------|------------|--------|---------------------|
| **Users dismiss simulation as "not real"** | High | High | - Add disclaimer: "This is a demo - we want to know if you'd do this with real credentials"<br>- Post-connection survey asks "likelihood to complete with real broker"<br>- Plan to test with REAL SnapTrade for 10 users in follow-up |
| **Can't drive 100 visitors organically** | Medium | High | - Have backup: $50 LinkedIn ad budget if <60 visitors by Day 5<br>- Extend timeline from 7 to 10 days if needed<br>- Activate backup channels: Telegram groups, fintech Discord servers |
| **Drop-off happens before CTA (bounce rate >60%)** | Medium | High | - Track bounce rate separately from conversion rate<br>- If high bounce, problem is value prop/messaging, not connection flow<br>- A/B test different headlines immediately |
| **LinkedIn/WhatsApp groups block posts** | Low | Medium | - Pre-clear posts with group admins (already done for WhatsApp)<br>- Have 2-3 backup groups ready<br>- Pivot to Reddit/X if social channels fail |
| **PostHog tracking fails** | Low | High | - Test events thoroughly pre-launch (send test events, verify they appear)<br>- Manual backup: Typeform form on success screen captures completions<br>- Daily data exports to catch issues early |

---

## Files & Evidence

After test completion:

- **Landing page:** refi.trading/alpha (archived via Wayback Machine)
- **Analytics dashboard:** https://posthog.refi.trading/dashboard/smoke-test-broker
- **Raw data:** `experiment-01-data.csv` (PostHog export)
- **Hotjar recordings:** 20+ session recordings saved
- **Survey responses:** `survey-responses.csv` (Typeform export)
- **Screenshots:** `/evidence/` folder (landing page, OAuth screens, success screen, dashboard)

---

This smoke test will definitively answer: **Will users grant us broker access?** If yes, we build. If no, we pivot. Time to find out.
