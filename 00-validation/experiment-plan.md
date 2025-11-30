# Experiment Plan - ReFi.Trading

**Team:** ReFi.Trading  
**Created:** November 28, 2025  
**Owner:** Zeshan Ahmad

---

## Overview

This document contains 3 designed experiments to test our riskiest assumptions about broker connection conversion, non-custodial trust, and paper-to-live transition.

**Testing Priority:**
1. Broker Connection Conversion (V1) → Experiment 1: Landing Page Smoke Test
2. Non-Custodial Trust Barrier (P3+S2) → Experiment 2: Trust Video + Interview Study
3. Paper-to-Live Transition (V4) → Experiment 3: Progressive Caps Simulation

---

## Experiment 1: Broker Connection Smoke Test

### Hypothesis Statement

**We believe that** power-retail traders and small fund operators in the UAE/GCC region who are frustrated with manual trading and fragmented tool stacks will connect their brokerage account to ReFi.Trading via SnapTrade within 7 days of expressing interest.

**We will know we're right when** 60% or more of users who click "Get Early Access" on our landing page successfully complete the broker OAuth connection flow and reach the "Connection Successful" confirmation screen within 7 days.

---

### Riskiest Assumption Being Tested

**Assumption:** We believe that 60% or more of users who sign up for ReFi.Trading will successfully connect their brokerage account via SnapTrade within 7 days of signup (V1).

**Why this is the riskiest:**
- **Impact: 5/5** - Without broker connections, we cannot validate our core product (RL agent performance), cannot generate revenue (execution fees), and cannot proceed with any other experiments.
- **Confidence: 2/5** - Zero real-world data. Industry benchmarks show 60% drop-off at broker OAuth. Alpaca via SnapTrade partnership is unproven for trading apps. IBKR may intimidate retail users.
- **Risk score: 20** (tied for highest)

---

### Experiment Method

**Type:** Smoke Test - Landing page with broker connection simulation

**What we'll build/do:**

1. **Landing Page** (refi.trading/alpha):
   - Hero: "Wall Street AI, Radically Accessible" with 3-click value prop
   - Problem section highlighting $300-600/mo fragmented tool costs
   - Solution section showing dual-proof gate visual
   - CTA: "Connect Your Broker in 60 Seconds" button
   
2. **Simulated SnapTrade Flow**:
   - Click CTA → Broker selection screen (IBKR, Alpaca)
   - Select broker → **Mock OAuth screen** (not real connection)
   - "Connecting..." → Success screen with next steps
   - Capture drop-off at each step
   
3. **Post-Connection Survey** (2 questions):
   - "On a scale 1-10, how likely are you to complete this process with your REAL broker credentials?"
   - "What concerns do you have about connecting your brokerage account?"

**Why simulation vs. real SnapTrade:**
- SnapTrade production integration takes 2-3 weeks (too slow for validation sprint)
- We want to test WILLINGNESS, not technical integration bugs
- Can iterate messaging/UX quickly without SnapTrade API rate limits
- Will validate real integration only AFTER proving demand

**Time required:** 
- Build: 6 hours (landing page + mock flow)
- Run: 7 days (traffic generation + monitoring)
- Total: 9 days

**Resources needed:**
- Tools: Carrd.co (landing), Airtable (form), PostHog (analytics)
- Money: $0 (all free tiers)
- People: Zeshan (design/copy), Daniel (technical review)
- Other: Access to fintech LinkedIn groups, UAE trader WhatsApp groups

---

### Success Metrics

**Primary Metric:** Simulated broker connection completion rate

- **Success threshold:** ≥60% of users who click "Connect Broker" complete the full mock OAuth flow to success screen
- **Measurement method:** PostHog funnel tracking
  - Event 1: `cta_clicked` (clicked "Connect Your Broker")
  - Event 2: `broker_selected` (chose IBKR or Alpaca or Tradier)
  - Event 3: `oauth_simulated` (clicked "Authorize" on mock OAuth)
  - Event 4: `connection_success` (reached success screen)
- **Why this metric:** Validates willingness to grant broker access BEFORE we invest in real SnapTrade integration. If <60% complete simulation, real connection will be even lower.

**Secondary Metrics:**

1. **Post-connection intent score**
   - Target: Average ≥7/10 on "likelihood to complete with real credentials"
   - Why: Validates that simulation behavior predicts real behavior

2. **Broker preference split**
   - Target: Track IBKR vs. Alpaca vs Tradier selection ratio
   - Why: Informs which broker to prioritize for real integration

3. **Drop-off point identification**
   - Target: <20% drop-off at OAuth authorization screen
   - Why: If drop-off is at OAuth (vs. broker selection), indicatesTradier trust issue

---

### Test Procedure

**Phase 1: Setup** (Days 1-2)

**What to prepare:**
- [x] Build landing page, problem, solution, CTA
- [x] Create mock broker selection screen with IBKR + Alpaca + Tradier logos/descriptions
- [x] Design mock OAuth authorization screen (looks real but isn't)
- [x] Build success screen with "Next: Set Your Risk Limits" messaging
- [x] Set up PostHog events for funnel tracking
- [x] Create 2-question post-connection Airtable survey
- [x] Test entire flow on mobile (70% of traffic expected)

**Owner:** Zeshan  
**Checkpoint:** Flow works end-to-end, PostHog events firing correctly, mobile-optimized

---

**Phase 2: Run** (Days 3-9)

**What happens:**
- [x] Day 3 (Mon): Launch landing page to LinkedIn fintech groups (3 groups, ~500 reach)
- [x] Day 4 (Tue): Post to UAE trader WhatsApp groups (2 groups, ~300 reach)
- [x] Day 5 (Wed): Share on X/Twitter with #AlgoTrading #Fintech hashtags
- [x] Day 6-9: Monitor traffic, respond to questions within 2 hours, DM users who complete flow

**Daily tasks:**
- Morning (9 AM UAE time): Check PostHog dashboard, note overnight signups
- Evening (6 PM UAE time): Export day's data, identify patterns, respond to all comments/DMs

**Owner:** Zeshan  
**Checkpoint:** 
- Day 5: ≥30 visitors (pivot to Reddit if needed)
- Day 7: ≥60 visitors (minimum sample size)
- Day 9: ≥100 visitors (target sample size)

---

**Phase 3: Measure** (Day 10)

**Data to collect:**
- [x] Export PostHog funnel data (all 4 events)
- [x] Calculate conversion rate at each step
- [x] Export Airtable survey responses
- [x] Calculate average intent score
- [x] Segment by traffic source (LinkedIn vs. WhatsApp vs. X)
- [x] Note qualitative comments from survey "concerns" question

**How to collect:**
- PostHog: Export → Events → Filter by date range → Download CSV
- Airtable: Export → Download CSV
- Manually compile verbatim survey comments into themes

**Owner:** Daniel  
**Deliverable:** `experiment-01-data.csv` + `survey-responses.csv` + initial summary doc

---

**Phase 4: Analyze** (Day 11)

**Analysis questions:**
1. Did we hit 60% completion threshold? (Yes/No + actual %)
2. Where did users drop off most? (Broker selection? OAuth? Other?)
3. What's the average intent score? (Target: ≥7/10)
4. What concerns did users express? (Categorize: security, complexity, trust, other)
5. Does traffic source affect conversion? (LinkedIn vs. WhatsApp vs. X)

**Owner:** Zeshan + Daniel (joint session)  
**Deliverable:** `experiment-01-analysis.md` with findings, charts, and decision recommendation

---

### Participants

**Target segment:** 
- **Primary:** Power-retail traders (3+ years experience, $10K+ account size, currently using one of 3+ tools)
- **Secondary:** Fund operators (<$50M AUM, lacking in-house quant infrastructure)
- **Geographic:** UAE, Saudi Arabia, other GCC countries (ADGM RegLab target market)

**How many needed:** 
- **Minimum for statistical significance:** 60 visitors (±13% margin of error at 95% confidence)
- **Realistic goal:** 100 visitors (±10% margin of error)
- **Rationale:** 100 visitors × 60% target = 60 successful completions, enough to validate demand

**Recruitment plan:**

1. **Channel 1: LinkedIn Fintech Groups**
   - **Specific tactic:** Post in "UAE FinTech Professionals", "GCC Algo Traders", "Quantitative Finance Middle East"
   - **Expected reach:** 500 members across 3 groups
   - **Expected traffic:** 40 visitors (8% CTR based on industry average for professional groups)
   - **Message:** "We're building non-custodial RL trading for GCC traders. Takes 60 seconds to test the broker connection flow. Not asking for real credentials—just want to validate demand. Link in comments."
   - **Timeline:** Day 3 (Monday) at 9 AM UAE time (peak engagement)

2. **Channel 2: UAE Trader WhatsApp Groups**
   - **Specific tactic:** Direct message to 2 active trader groups via personal network
   - **Expected reach:** 300 traders
   - **Expected traffic:** 30 visitors (10% CTR for warm network)
   - **Message:** "Quick favor - testing broker connection UX for a new algo trading platform. Takes 1 minute to click through a demo flow. No signup, no real connection. Just want feedback: [link]"
   - **Timeline:** Day 4 (Tuesday) at 6 PM UAE time (after market close)

3. **Channel 3: X (Twitter) / Reddit**
   - **Specific tactic:** Post on X with hashtags, cross-post to r/algotrading
   - **Expected reach:** 1000 impressions (small following, but targeted hashtags)
   - **Expected traffic:** 30 visitors (3% CTR)
   - **Message:** "Building 'Wall Street AI, Radically Accessible' for retail. Testing broker OAuth UX with IBKR and Alpaca support. Takes 60 sec to see if you'd connect your real brokerage account: [link] Feedback appreciated! 🚀"
   - **Timeline:** Day 5 (Wednesday) at 2 PM UTC (peak r/algotrading activity)

**Backup plan if can't recruit enough:**
- Extend timeline to 14 days
- Paid LinkedIn ads ($50 budget, target UAE traders)
- Reach out to fintech influencers in GCC for retweets
- Lower minimum sample size to 50 (acknowledge higher margin of error)

---

### Timeline

```
Day 1-2:  Build landing page + mock OAuth flow + analytics setup
Day 3:    Launch to LinkedIn groups (9 AM UAE)
Day 4:    Launch to WhatsApp groups (6 PM UAE)
Day 5:    Launch to X/Reddit (2 PM UTC)
Day 6-9:  Monitor traffic, engage with users, DM completions
Day 10:   Close experiment, export all data
Day 11:   Joint analysis session, document findings
Day 12:   Decision meeting (persevere/pivot/iterate)
```

**Start date:** December 2, 2025  
**End date:** December 13, 2025  
**Total duration:** 12 days

**Dependencies:**  
- None (can start immediately)
- Access to LinkedIn groups (already member)
- WhatsApp group admin approval (already confirmed)

---

### Potential Outcomes

#### If Hypothesis is VALIDATED ✅ (≥60% completion)

**What this means:**  
Users are willing to grant broker access when value proposition is clear and process looks simple. Non-custodial positioning resonates. Ready to build real SnapTrade integration.

**Next steps:**
1. Interview 10+ users who completed flow: "What convinced you to connect? What concerns remain?"
2. Begin SnapTrade production integration (2-3 week timeline)
3. Design real onboarding flow with progressive caps messaging
4. Move to Experiment 2 (zk-proof trust validation)

**Impact on roadmap:**  
- Prioritize SnapTrade integration to Week 1-2 of MVP sprint
- Allocate engineering time to ERC-4337 wallet setup
- Confirm IBKR as primary broker (or Alpaca if data shows preference)
- Begin drafting compliance documentation for ADGM RegLab

---

#### If Hypothesis is INVALIDATED ❌ (<40% completion)

**What this means:**  
Significant trust barrier or UX friction preventing broker connection. Either messaging isn't clear, value prop not compelling, or fundamental fear of granting access.

**Pivot options:**

1. **Option A: Demo Account First**
   - **Why:** Remove trust barrier by offering "try before you connect"
   - **How:** Build demo mode with fake $10K account, simulated trades
   - **Impact:** Delays validation of real performance, but reduces initial friction
   - **Test:** Re-run experiment with "Try Demo" CTA vs. "Connect Broker"

2. **Option B: View-Only Mode**
   - **Why:** Users may accept read-only access before write access
   - **How:** Offer "Connect (Read-Only) to See Your Portfolio + AI Recommendations"
   - **Impact:** Requires different product flow, but builds trust progressively
   - **Test:** A/B test read-only vs. full access CTAs

3. **Option C: Different Broker Strategy**
   - **Why:** IBKR/Alpaca may be intimidating; could try alternative brokers in UAE
   - **How:** Research alternative brokers with simpler OAuth, or build manual upload flow
   - **Impact:** More complex broker integration, potentially lower quality execution
   - **Test:** User interviews to understand broker preferences

**Next steps:**
1. Deep dive user interviews with both completers AND drop-offs
2. Analyze drop-off point: Is it broker selection, OAuth, or earlier?
3. A/B test different messaging: "Non-custodial" vs. "You stay in control" vs. "We never touch your money"
4. Consider pivot to demo mode for initial launch

---

#### If Results are INCONCLUSIVE 🤷 (40-59% completion)

**What this means:**  
Moderate interest but not strong enough to confidently build. May need more data or different test design.

**Possible reasons:**
- Sample size too small (need 150+ visitors for tighter confidence interval)
- Wrong traffic source (LinkedIn vs. WhatsApp may have different trust levels)
- Messaging not optimized (need A/B testing of value prop)
- Simulation too obvious (users don't take it seriously without real stakes)

**Next iteration:**  
- Extend timeline to 21 days to reach 200+ visitors
- A/B test 2-3 different landing page headlines
- Segment analysis: Does completion rate differ by stated experience level?
- Consider offering small incentive ($10 gift card) for completion + interview
- Re-run with REAL SnapTrade integration (non-simulation) for 20 users to compare

---

### Risks & Mitigation

| Risk | Likelihood | Impact | Mitigation Strategy |
|------|------------|--------|---------------------|
| Users don't take simulation seriously (know it's fake) | High | High | - Add "This is a demo flow" disclaimer but ask "Would you complete with real credentials?"<br>- Post-connection survey captures intent<br>- Plan follow-up with real SnapTrade for subset of users |
| Can't recruit enough UAE/GCC users | Medium | High | - Expand to global English-speaking traders<br>- Paid ads if organic reaches <50 by Day 7<br>- Extend timeline to 14 days |
| Drop-off happens before "Connect Broker" CTA (never reach funnel) | Medium | High | - Track landing page bounce rate<br>- If >60% bounce, problem is value prop not connection flow<br>- A/B test different headlines/pain points |
| LinkedIn/WhatsApp admins block posts | Low | Medium | - Pre-clear posts with admins<br>- Have 2-3 backup groups ready<br>- Shift to Reddit/X if social blocked |
| Technical issues with PostHog tracking | Low | High | - Test events thoroughly pre-launch<br>- Manual backup tracking via Airtable form at success screen<br>- Daily data exports to catch issues early |

---

## Experiment 2: Non-Custodial Trust & zk-Proof Value Study

### Hypothesis Statement

**We believe that** retail traders who have experienced exchange failures (FTX, Celsius, etc.) or who are concerned about custody risk will find ReFi.Trading's non-custodial architecture (ERC-4337 + zk-VaR proofs) significantly more trustworthy than traditional robo-advisors or custodial algo-trading platforms.

**We will know we're right when** 70% or more of interviewed users (who've completed Experiment 1) can correctly explain "non-custodial means my assets never leave my brokerage account" AND rate "Trust in ReFi.Trading vs. typical robo-advisor" as 7+ out of 10 after watching our 3-minute explainer video.

---

### Riskiest Assumption Being Tested

**Assumption (Combined P3 + S2):** 
- P3: "We believe that the lack of verifiable, non-custodial automated trading is the #1 barrier preventing retail traders from adopting algorithmic trading solutions"
- S2: "We believe that zk-VaR proofs provide sufficient trust for users to delegate trading decisions"

**Why this is the riskiest:**
- **Impact: 5/5** - Our entire technical architecture (ERC-4337 wallets, zk-SNARKs, dual-proof gate) is built around this. If users don't value non-custodial or don't understand zk-proofs, we've over-engineered and need to pivot to simpler trust model.
- **Confidence: 2/5** - User interviews confirm "post-FTX trust concerns" but we haven't validated that OUR specific solution resonates. May be solving problem they don't care about or in a way they can't understand.
- **Risk score: 20** (P3) + 20 (S2) = our highest combined risk

---

### Experiment Method

**Type:** Wizard of Oz + Interview Study (appears like product demo, but manually orchestrated)

**What we'll build/do:**

1. **3-Minute Explainer Video**:
   - **Scene 1 (0:00-0:45):** The Problem - "FTX, Celsius, and why 'not your keys, not your crypto' applies to algo trading"
   - **Scene 2 (0:45-1:30):** Our Solution - "Your assets stay at IBKR. We send orders. You keep keys. Here's how:"
   - **Scene 3 (1:30-2:15):** The Dual-Proof Gate - Animated visual showing zk-VaR proof + ACE policy check
   - **Scene 4 (2:15-3:00):** Proof in Action - Screen recording of trade being blocked by VaR proof, then approved within limits
   
2. **Post-Video Comprehension Test** (5 questions, multiple choice):
   - Q1: "Where are your assets held when using ReFi.Trading?" (Correct: "In my brokerage account, same as before")
   - Q2: "What does a zk-VaR proof verify?" (Correct: "That a trade doesn't exceed my risk limits")
   - Q3: "Can ReFi.Trading withdraw money from my account?" (Correct: "No, ERC-4337 wallet only allows approved trades")
   - Q4: "What happens if a trade violates risk limits?" (Correct: "zk-proof fails, trade is blocked automatically")
   - Q5: "Who can see the details of my trades?" (Correct: "Only me - zk-proofs verify without revealing strategy")
   
3. **Trust Comparison Survey**:
   - "On a scale 1-10, how much do you trust a typical robo-advisor (Betterment, Wealthfront) with your money?"
   - "On a scale 1-10, how much do you trust ReFi.Trading (based on this video)?"
   - "What's the MAIN reason for the difference in your scores?"
   
4. **30-Minute Follow-Up Interview** (with 10 users):
   - "What part of the video was most compelling? Least clear?"
   - "If you had $10K to invest, would you use ReFi.Trading? Why or why not?"
   - "Does the zk-proof system make sense to you? Would you want more technical detail or less?"
   - "What would make you MORE likely to trust us?"

**Time required:** 
- Build: 8 hours (video script + recording + editing + survey setup)
- Run: 5 days (distribute video, collect responses, conduct interviews)
- Total: 7 days

**Resources needed:**
- Tools: Loom (video recording), Typeform (survey), Calendly (interview scheduling), Zoom (interviews)
- Money: $0 (all free tiers)
- People: Zeshan (video script/recording), Daniel (technical review), both (interviews)
- Other: Users from Experiment 1 (email list of completers)

---

### Success Metrics

**Primary Metric:** Comprehension + Trust Lift

- **Success threshold:** 
  - ≥70% of viewers score 4/5 or 5/5 on comprehension test (understand non-custodial + zk-proofs)
  - AND average trust score for ReFi.Trading is ≥2 points higher than "typical robo-advisor"
- **Measurement method:** Typeform survey auto-scoring + manual analysis
- **Why this metric:** Validates that our messaging successfully communicates differentiation AND that differentiation matters. If comprehension is high but trust lift is low, message is clear but not compelling. If comprehension is low, we're confusing users.

**Secondary Metrics:**

1. **Video completion rate**
   - Target: ≥80% watch to end (3:00 mark)
   - Why: If viewers drop off early, video is too long/boring or messaging isn't resonating

2. **Qualitative trust drivers**
   - Target: ≥60% cite "non-custodial" or "keeps assets at my broker" as MAIN reason for trust difference
   - Why: Validates our core hypothesis that custody is the barrier

3. **Technical detail preference**
   - Target: Track how many want "more detail on zk-proofs" vs. "less technical, simpler explanation"
   - Why: Informs how we message to retail vs. prosumer vs. institutional segments

---

### Test Procedure

**Phase 1: Setup** (Days 1-2)

**What to prepare:**
- [x] Write video script with 4 scenes (problem, solution, dual-proof, proof in action)
- [x] Record screen capture of mock trade + zk-proof blocking/approving
- [x] Create simple animations for dual-proof gate visual (Canva or similar)
- [x] Record voiceover (Zeshan) with clear, non-technical language
- [x] Edit video to 3:00 exactly (test with 3 non-technical friends for comprehension)
- [x] Build Typeform with 5 comprehension Qs + 2 trust scale Qs + open-ended "Why?"
- [x] Set up Calendly for 30-min interview slots

**Owner:** Zeshan (video), Daniel (technical review/screen recordings)  
**Checkpoint:** Video is comprehensible to non-technical viewer, survey flows smoothly, Calendly linked

---

**Phase 2: Run** (Days 3-7)

**What happens:**
- [x] Day 3: Email all Experiment 1 completers (target: 60+ users) with subject "See How ReFi.Trading Keeps Your Assets Safe"
  - Body: "Thanks for testing our broker connection flow. Here's a 3-min video showing how our non-custodial system works. After watching, quick 2-min survey: [Typeform link]"
- [x] Day 4: Send reminder email to non-openers (50% expected open rate)
- [x] Day 5: Begin scheduling interviews with survey completers (offer first 10 respondents)
- [x] Day 6-7: Conduct 30-min Zoom interviews, record (with permission), take detailed notes

**Daily tasks:**
- Morning: Check Typeform response count, note any patterns in open-ended answers
- Afternoon: Review video analytics (Loom provides watch time data), identify drop-off points
- Evening: Reach out to survey completers for interview invitations

**Owner:** Zeshan (email/outreach), Daniel (interviews)  
**Checkpoint:** 
- Day 4: ≥20 survey responses (if <20, extend to wider audience)
- Day 6: ≥5 interviews scheduled
- Day 7: All 10 interviews completed

---

**Phase 3: Measure** (Day 8)

**Data to collect:**
- [x] Export Typeform responses (comprehension scores, trust scores, qualitative answers)
- [x] Calculate % scoring 4/5 or 5/5 on comprehension
- [x] Calculate average trust score for ReFi vs. robo-advisors, compute difference
- [x] Categorize open-ended "Why?" answers into themes (custody, transparency, tech, other)
- [x] Review Loom analytics: % watched to end, average drop-off point
- [x] Compile interview notes, extract verbatim quotes for key themes

**How to collect:**
- Typeform: Export → Download CSV
- Loom: Analytics Dashboard → Export watch time data
- Interviews: Review recordings, transcribe key quotes using Otter.ai

**Owner:** Daniel  
**Deliverable:** `experiment-02-data.csv` + `interview-notes.md` + initial themes doc

---

**Phase 4: Analyze** (Day 9)

**Analysis questions:**
1. Did ≥70% score 4/5 or 5/5 on comprehension? (Yes/No + actual %)
2. What's the average trust lift? (Target: ≥2 points)
3. What's the #1 reason users cite for higher trust in ReFi.Trading?
4. Which comprehension question had lowest correct rate? (Indicates messaging weakness)
5. Do users WANT more technical detail on zk-proofs, or is current level right?
6. Do interviews reveal any trust concerns NOT addressed by non-custodial messaging?

**Owner:** Zeshan + Daniel (joint session)  
**Deliverable:** `experiment-02-analysis.md` with findings, quotes, messaging recommendations

---

### Participants

**Target segment:** Users who completed Experiment 1 (simulated broker connection)

**How many needed:** 
- **Survey responses:** 30 minimum (to get 20+ with high confidence)
- **Interviews:** 10 (depth over breadth for qualitative insights)
- **Rationale:** 30 survey responses gives us directional signal on comprehension/trust. 10 interviews provides rich qualitative data on WHY trust differs and what messaging resonates.

**Recruitment plan:**

1. **Email to Experiment 1 Completers**
   - **Expected reach:** 60+ users (assuming Experiment 1 hits target)
   - **Expected survey response:** 30 (50% response rate typical for engaged users)
   - **Expected interview conversion:** 10/30 (offering $25 Amazon gift card incentive)
   - **Timing:** Day 3 at 9 AM UAE time, reminder Day 4 at 6 PM

**Backup plan if can't recruit enough:**
- Expand invite to Experiment 1 participants who dropped off (they may have trust concerns)
- Post video + survey publicly on LinkedIn/X for broader reach
- Increase gift card to $50 for interviews if struggling to get 10
- Lower target to 20 survey responses (acknowledge lower confidence)

---

### Timeline

```
Day 1-2:  Script, record, edit video + build survey + set up Calendly
Day 3:    Email video + survey to Experiment 1 completers
Day 4:    Reminder email to non-openers
Day 5:    Invite survey completers to interviews, begin scheduling
Day 6-7:  Conduct 10 interviews (5 per day)
Day 8:    Export data, compile interview notes
Day 9:    Joint analysis session, document findings
```

**Start date:** December 14, 2025 (immediately after Experiment 1)  
**End date:** December 22, 2025  
**Total duration:** 9 days

**Dependencies:**  
- Experiment 1 must be complete (need user email list)
- Minimum 30 Experiment 1 completers (if <30, may need to extend reach)

---

### Potential Outcomes

#### If Hypothesis is VALIDATED ✅ (≥70% comprehension, ≥2 point trust lift)

**What this means:**  
Non-custodial messaging resonates. Users understand and value zk-proof verification. Our technical differentiation is compelling. Ready to emphasize this in all marketing.

**Next steps:**
1. Make 3-min explainer video central to landing page (above the fold)
2. Add "How It Works: Non-Custodial + Verified" section to all marketing materials
3. Create shorter 30-second version for social media ads
4. Develop "Trust Center" page with detailed technical documentation for prosumers
5. Move to Experiment 3 (paper-to-live transition)

**Impact on roadmap:**  
- Prioritize building "Audit Trail" dashboard (shows all zk-proofs for transparency)
- Ensure ERC-4337 wallet UX clearly communicates "You hold the keys"
- Add educational tooltips throughout app explaining zk-VaR proofs
- Create "Trust Badge" graphic for marketing materials

---

#### If Hypothesis is INVALIDATED ❌ (<50% comprehension OR <1 point trust lift)

**What this means:**  
Either users don't understand our technical approach, don't care about non-custodial, or trust concerns are driven by other factors (performance, regulation, brand reputation).

**Pivot options:**

1. **Option A: Simplify Messaging, Deprioritize zk-Proofs**
   - **Why:** "Non-custodial" may resonate, but zk-proofs are too technical for retail
   - **How:** Message as "Your money stays at your broker. We just send orders, like using a trading app."
   - **Impact:** Keep ERC-4337 architecture but hide zk-proof complexity from UI
   - **Test:** Re-run with simpler video (no mention of zk-SNARKs, just "verified risk limits")

2. **Option B: Focus on Performance, Not Custody**
   - **Why:** Users may care more about "will this make me money?" than "where are my assets?"
   - **How:** Lead with "28% CAGR, 2.07 Sharpe ratio, <7.5% max drawdown" (our backtest results)
   - **Impact:** Shift value prop from trust to performance; keep non-custodial as secondary feature
   - **Test:** A/B test performance-led messaging vs. custody-led messaging

3. **Option C: Custodial Model with Better UX**
   - **Why:** If users don't care about custody, why build complex non-custodial infrastructure?
   - **How:** Simplify to "Connect broker API keys, we execute trades from your account"
   - **Impact:** Major technical pivot; abandon ERC-4337, zk-proofs; faster development
   - **Test:** Interview users on "Would you use us if we held API keys vs. non-custodial?"

**Next steps:**
1. Deep dive interviews specifically on "What would make you trust an algo trading platform?"
2. Show users 3 different trust models (custody, non-custodial, hybrid) and rank preference
3. Analyze which comprehension questions failed most (zk-proof? ERC-4337? Both?)
4. Consider pivot to institutional market (where zk-proofs may be more valued)

---

#### If Results are INCONCLUSIVE 🤷 (50-69% comprehension OR 1-2 point trust lift)

**What this means:**  
Messaging is somewhat effective but not strong enough. May need iteration on explanation, or trust is multifaceted (not just custody).

**Possible reasons:**
- Video too technical in parts, too simple in others (need segmentation by user type)
- Comprehension high but trust lift low = understanding but not caring
- Trust lift high but comprehension low = emotional resonance without understanding (concerning for long-term)
- Sample size too small (need 50+ survey responses)

**Next iteration:**  
- Create 2 versions of video: "Retail-Simple" (no zk-proof mention) vs. "Prosumer-Technical" (deep dive)
- A/B test which version drives higher trust lift for which segment
- Extend survey to 50+ respondents for tighter confidence intervals
- Add control group: Show "typical robo-advisor" video first, THEN ReFi video, measure relative trust
- Conduct "comparison shopping" exercise: Show 3 platforms (Betterment, QuantConnect, ReFi), ask users to rank trust

---

### Risks & Mitigation

| Risk | Likelihood | Impact | Mitigation Strategy |
|------|------------|--------|---------------------|
| Video is too technical, confuses users | High | High | - Test with 5 non-technical friends pre-launch<br>- Include "Skip to simple version" timestamp in email<br>- Create 30-sec "ultra-simple" version as backup |
| Low email open rate from Experiment 1 users | Medium | High | - Compelling subject line tested on small sample<br>- Send from personal email (Zeshan's) not generic info@<br>- Reminder email with different framing |
| Users say "trust" but won't actually use when it comes time | Medium | High | - Follow-up question: "If we launched today, would you deposit $1K and go live?"<br>- Track actual conversion in future experiments |
| Interviews reveal concerns NOT addressed by custody | Medium | Medium | - Open-ended interview questions to surface unknown unknowns<br>- Specifically ask "What ELSE would make you trust us?" |
| Video completion rate very low (<50% watch to end) | Low | High | - Loom analytics show drop-off point<br>- If early drop-off, problem is hook; if late, problem is length<br>- Iterate based on drop-off analysis |

---

## Experiment 3: Paper-to-Live Transition Study

### Hypothesis Statement

**We believe that** users who complete at least 7 days of paper trading with ReFi.Trading's RL agents, achieving positive returns in simulation, will transition to live trading with our progressive caps system ($100 → $500 → $5000) within 14 days of completing paper trading.

**We will know we're right when** 60% or more of users who finish the 7-day paper trading period (with ≥0% returns) initiate their first live trade within 14 days, starting with the Day 1 cap of $100 max position size.

---

### Riskiest Assumption Being Tested

**Assumption (V4):** We believe that users who successfully complete paper trading will transition to live trading (with progressive caps) within 14 days, with 60%+ making their first live trade.

**Why this is the riskiest:**
- **Impact: 4/5** - Without live trading, we can't validate actual performance, can't earn revenue (execution fees), and can't prove our core value prop. Paper trading is not our business model.
- **Confidence: 2/5** - Industry data shows 70%+ of retail traders who paper trade never go live. Our progressive caps ($100 start) is designed to reduce fear, but it's completely unvalidated. Users may love zero-risk paper trading and never graduate.
- **Risk score: 16**

---

### Experiment Method

**Type:** Wizard of Oz - Simulated paper trading with real-seeming results, followed by "go live" offer

**What we'll build/do:**

1. **7-Day Paper Trading Simulator**:
   - Users "connect" their broker (from Experiment 1)
   - We show simulated $10K account
   - Each day, RL agent generates 2-3 trade recommendations
   - Trades execute in simulation (we manually create realistic fills based on actual market data)
   - Dashboard shows daily P&L, cumulative returns, Sharpe ratio
   
2. **Performance Report (Day 7)**:
   - Automated email: "Your 7-day paper trading results are in!"
   - Shows: Total return (%), Sharpe ratio, max drawdown, win rate
   - Visual chart of equity curve
   - CTA: "Ready to go live with $100? Your risk limits are already set."
   
3. **Progressive Caps Onboarding**:
   - Day 1 live: Max $100 position size, max $500 daily notional
   - Day 3 live: Max $500 position size, max $2500 daily notional
   - Day 7 live: Max $5000 position size, max $25K daily notional
   - Email notifications at each cap increase
   
4. **Go-Live Decision Tracking**:
   - Track who clicks "Start Live Trading" button
   - Track who completes Alpaca/IBKR OAuth (for real this time)
   - Track who places first live order
   - Survey non-converters: "What's holding you back from going live?"

**Why Wizard of Oz:**
- Building real RL agent execution takes 3-4 weeks (too slow for validation)
- We want to test WILLINGNESS to go live after seeing positive results
- Can control paper trading performance to test "does performance matter?"
- Manual simulation lets us test messaging and UX without backend complexity

**Time required:** 
- Build: 10 hours (paper trading dashboard + performance report + survey)
- Run: 21 days (7 days paper + 14 days transition window)
- Total: 23 days

**Resources needed:**
- Tools: Retool (dashboard), Mailchimp (emails), PostHog (tracking), Airtable (survey)
- Money: $0 (all free tiers)
- People: Zeshan (design/copy), Daniel (manual trade fills + data)
- Other: Real market data from Polygon.io (free tier), users from Experiments 1+2

---

### Success Metrics

**Primary Metric:** Paper-to-live conversion rate within 14 days

- **Success threshold:** ≥60% of users who complete 7-day paper trading initiate first live trade within 14 days
- **Measurement method:** 
  - Event tracking: `paper_trading_complete` (Day 7) → `live_trading_initiated` (clicked "Start Live") → `first_live_order` (placed order)
  - Time delta between events
- **Why this metric:** Directly tests our core assumption. If <60% convert, our product flow has a critical gap that will kill revenue generation.

**Secondary Metrics:**

1. **Performance correlation**
   - Target: Users with >5% paper trading returns convert at ≥70%, users with 0-5% convert at ≥50%
   - Why: Tests if performance drives willingness to go live

2. **Cap progression engagement**
   - Target: ≥80% of live users trade up to Day 1 cap limit ($100)
   - Why: If users don't use full cap, caps may be too high (less likely) or they're not confident (more likely)

3. **Time to first live trade**
   - Target: Median ≤3 days after paper trading complete
   - Why: Longer delay suggests hesitation; want to understand drivers

4. **Drop-off point identification**
   - Target: <20% drop off at real broker OAuth (vs. completing paper but not going live)
   - Why: Distinguishes "afraid of live trading" from "don't trust real broker connection"

---

### Test Procedure

**Phase 1: Setup** (Days 1-3)

**What to prepare:**
- [x] Build paper trading dashboard in Retool (portfolio view, trade history, performance chart)
- [x] Create "trade recommendation" notification system (email 2x/day)
- [x] Prepare 7 days of realistic trade fills (based on real market data from Polygon.io)
- [x] Design Day 7 performance report email template
- [x] Build "Go Live" onboarding flow with progressive caps messaging
- [x] Set up PostHog events for entire funnel
- [x] Create survey for non-converters ("What's holding you back?")

**Owner:** Zeshan (UI/UX), Daniel (trade fills data)  
**Checkpoint:** Dashboard looks real, performance report is compelling, caps are clearly explained

---

**Phase 2: Run - Paper Trading** (Days 4-10)

**What happens:**
- [x] Day 4: Email Experiment 2 completers (target: 20-30 users): "Your paper trading account is ready"
- [x] Day 4-10: 
  - Send 2 trade recommendations per day (morning + afternoon UAE time)
  - Manually fill trades with realistic execution (use actual market data)
  - Update dashboard daily with P&L
  - Respond to any questions within 2 hours
- [x] Day 10: Send performance report email to all users who completed 7 days

**Daily tasks:**
- Morning (8 AM UAE): Generate day's trade recommendations based on RL agent outputs (manually)
- Afternoon (2 PM UAE): Fill morning trades, send afternoon recommendations
- Evening (6 PM UAE): Fill afternoon trades, update dashboards, export performance data

**Owner:** Daniel (trade fills), Zeshan (user support)  
**Checkpoint:** 
- Day 6: ≥15 users still active (if <15, extend invites or restart)
- Day 10: ≥10 users completed full 7 days

---

**Phase 3: Run - Go-Live Window** (Days 11-24)

**What happens:**
- [x] Day 11: Day 7 completers receive performance report + "Go Live" CTA
- [x] Days 11-14: Monitor who clicks "Start Live Trading"
  - Auto-email reminder on Day 13 for non-clickers
  - Personal outreach to high-performers who haven't gone live
- [x] Days 15-24: Track first live trades, cap progression, engagement
  - Email at Day 3 cap increase: "You've unlocked $500 positions"
  - Email at Day 7 cap increase: "You've unlocked $5000 positions"
- [x] Day 18: Survey non-converters (users who completed paper but didn't go live)

**Daily tasks:**
- Morning: Check who initiated live trading overnight
- Midday: Send encouragement messages to paper trading "winners" who haven't gone live
- Evening: Track live trades, ensure cap enforcement working, note any issues

**Owner:** Zeshan  
**Checkpoint:** 
- Day 14: ≥6 out of 10 completers initiated live (60% minimum)
- Day 24: All live traders have completed at least 1 trade

---

**Phase 4: Measure** (Day 25)

**Data to collect:**
- [x] Export paper trading performance data (all users, all days)
- [x] Calculate conversion rate: completed paper → initiated live → first live order
- [x] Segment by performance: >5%, 0-5%, <0% paper trading returns
- [x] Calculate time to first live trade (median, mean, distribution)
- [x] Export non-converter survey responses
- [x] Categorize concerns: fear, performance doubt, technical issues, other

**How to collect:**
- PostHog: Export funnel data
- Retool: Export dashboard interaction logs
- Mailchimp: Email open/click rates
- Airtable: Survey responses

**Owner:** Daniel  
**Deliverable:** `experiment-03-data.csv` + `performance-correlation-analysis.md` + survey themes doc

---

**Phase 4: Analyze** (Day 26)

**Analysis questions:**
1. Did we hit 60% paper-to-live conversion? (Yes/No + actual %)
2. Does paper trading performance correlate with go-live rate? (>5% vs. 0-5% vs. <0%)
3. What's the median time to first live trade? (Target: ≤3 days)
4. Where do users drop off: at "Start Live" button, or at real broker OAuth?
5. What concerns do non-converters cite most? (Fear, performance, technical, caps too low, other)
6. Do users who go live actually use the full progressive caps, or trade conservatively?

**Owner:** Zeshan + Daniel (joint session)  
**Deliverable:** `experiment-03-analysis.md` with findings, conversion funnel charts, recommendations

---

### Participants

**Target segment:** Users who completed Experiments 1 AND 2 (broker connection + trust study)

**How many needed:** 
- **Paper trading participants:** 20-30 (expect 50% attrition over 7 days → 10-15 completers)
- **Target completers:** 10+ (to get 6+ live conversions at 60% rate)
- **Rationale:** Need ≥10 completers to have statistical power. With 60% conversion, 10 completers → 6 live traders, enough to validate.

**Recruitment plan:**

1. **Email to Experiment 2 Completers (with high trust scores)**
   - **Expected reach:** 30 users (assuming 30 completed Experiment 2)
   - **Expected paper trading start:** 25 (83% conversion - high because already engaged)
   - **Expected 7-day completion:** 12-15 (50% attrition typical for multi-day commitments)
   - **Message:** "Your paper trading account is live! 7 days to test our RL agents risk-free. Top performers get priority for beta launch."
   - **Timing:** Day 4 at 9 AM UAE

**Backup plan if can't recruit enough:**
- Reduce paper trading period from 7 days to 3 days (faster cycle, less attrition)
- Offer $50 gift card for completing 7 days + going live with at least 1 trade
- Extend invites to Experiment 1 completers (even if skipped Experiment 2)
- Manual outreach to high-value users (funds, experienced traders) for 1-on-1 onboarding

---

### Timeline

```
Day 1-3:   Build paper trading dashboard + email templates + survey
Day 4:     Invite Experiment 2 completers to start paper trading
Day 5-10:  Run paper trading (send trade recs 2x/day, fill trades, update dashboards)
Day 11:    Send performance reports + "Go Live" CTA
Day 11-14: Monitor go-live initiations, send reminders
Day 15-24: Track live trades, cap progressions
Day 18:    Survey non-converters
Day 25:    Export all data
Day 26:    Joint analysis session
```

**Start date:** December 23, 2025 (immediately after Experiment 2)  
**End date:** January 17, 2026  
**Total duration:** 26 days

**Dependencies:**  
- Experiments 1 and 2 must be complete (need engaged user base)
- Minimum 10 users willing to commit to 7-day paper trading
- Real broker integration (SnapTrade) must be ready for live trading phase (can start integration during paper trading period)

---

### Potential Outcomes

#### If Hypothesis is VALIDATED ✅ (≥60% paper-to-live conversion)

**What this means:**  
Progressive caps strategy works. Users build confidence through paper trading and are willing to commit real capital when performance is demonstrated. Our product flow is sound.

**Next steps:**
1. Implement real RL agent backend (replace manual Wizard of Oz simulation)
2. Integrate SnapTrade for production broker connections
3. Build automated risk limit enforcement (zk-VaR + ACE policy)
4. Design scalable onboarding flow for 100+ users
5. Prepare for public beta launch

**Impact on roadmap:**  
- Prioritize RL agent deployment via Google AI Agent Platform
- Build "Performance Dashboard" showing real-time Sharpe ratio, max drawdown
- Create email automation for cap progression notifications
- Develop "Safe Mode" that pauses trading if drawdown exceeds threshold
- Plan revenue model around execution fees (validated demand)

---

#### If Hypothesis is INVALIDATED ❌ (<40% paper-to-live conversion)

**What this means:**  
Users like the idea of automated trading but aren't willing to commit real money, even with low caps. Either fear is too strong, performance isn't convincing, or onboarding friction is too high.

**Pivot options:**

1. **Option A: Eliminate Paper Trading, Force Live from Day 1**
   - **Why:** Paper trading creates false comfort zone; users never graduate
   - **How:** Start with $50 max position on real account from signup (vs. $10K paper)
   - **Impact:** Higher-risk proposition, but aligns incentives (we only succeed if users succeed)
   - **Test:** Offer $50 "starter bonus" to offset fear of loss, track conversion vs. paper-first

2. **Option B: "Skin in the Game" Paper Trading**
   - **Why:** Free paper trading has no consequences; users don't take it seriously
   - **How:** Charge $10 for 7-day paper trading; refund if they go live with ≥$100
   - **Impact:** Filters for committed users, creates sunk cost bias toward going live
   - **Test:** A/B test free vs. $10 paper trading, measure completion AND conversion rates

3. **Option C: "Guaranteed Return" Offer**
   - **Why:** Users may not trust RL agent performance despite paper trading results
   - **How:** "If you lose money in first 30 days, we'll refund your losses up to $500"
   - **Impact:** Removes downside risk, but creates financial liability for company
   - **Test:** Offer to 20 users, track take-rate and actual P&L distribution

4. **Option D: Extend Paper Trading, Increase Caps Faster**
   - **Why:** 7 days may not be enough to build confidence; $100 may be too conservative
   - **How:** 14-day paper trading, then $500 Day 1 cap (vs. $100)
   - **Impact:** Slower cycle but potentially higher confidence
   - **Test:** A/B test 7-day vs. 14-day paper, and $100 vs. $500 starting cap

**Next steps:**
1. Deep dive interviews with non-converters: "What would it take to go live?"
2. Analyze drop-off point: Is it clicking "Start Live" or completing broker OAuth?
3. Segment by paper trading performance: Do high-performers convert better?
4. Test "loss aversion" framing: "You've already made $X in paper. Make it real."

---

#### If Results are INCONCLUSIVE 🤷 (40-59% conversion)

**What this means:**  
Moderate conversion, but not strong enough to confidently scale. May need iteration on messaging, caps, or incentives.

**Possible reasons:**
- Sample size too small (only 10 completers → 4-5 conversions, high variance)
- Paper trading performance not compelling (0-5% returns don't excite)
- Caps progression too slow or too fast (need A/B testing)
- Real broker OAuth introduces unexpected friction vs. simulation
- Users want longer paper trading (14-21 days vs. 7)

**Next iteration:**  
- Extend to 20+ paper trading completers (reduces variance)
- A/B test different performance scenarios: Show some users +10% returns, others +3%, measure conversion difference
- Test 3 cap structures: Conservative ($50/$100/$500), Moderate ($100/$500/$5000), Aggressive ($500/$2500/$10000)
- Add "live chat support" during go-live process to reduce friction
- Survey completers who converted: "What convinced you?" to strengthen messaging for non-converters

---

### Risks & Mitigation

| Risk | Likelihood | Impact | Mitigation Strategy |
|------|------------|--------|---------------------|
| High attrition during 7-day paper trading (<50% completion) | High | High | - Daily engagement emails with "Your Performance Today" updates<br>- Leaderboard showing top performers (gamification)<br>- Reduce to 3-day paper trading if >60% drop off by Day 4<br>- Offer completion bonus ($10 gift card) |
| Users realize paper trading is simulated, lose trust | Medium | High | - Be transparent: "Simulated with real market data" in UI<br>- Ensure trade fills are realistic (no impossible executions)<br>- If asked directly, explain it's a demo to test UX before real integration |
| Real broker OAuth fails during go-live (technical issues) | Medium | High | - Pre-test SnapTrade integration with 2-3 internal users<br>- Have backup: "Manual connection available" with direct API keys<br>- Support chat during go-live window |
| Paper trading performance is TOO good, live disappoints | Medium | Medium | - Keep paper trading returns realistic (5-10%, not 50%)<br>- Show max drawdown prominently to set expectations<br>- Disclaimer: "Past performance in simulation doesn't guarantee future results" |
| Users go live but never place second trade (one-and-done) | Low | Medium | - Track engagement beyond first trade<br>- Email at Day 3 if no second trade: "Your next recommendation is ready"<br>- Consider requiring minimum 3 trades to validate |

---

## Experiment Sequencing

**Can experiments run in parallel?**
- [ ] Yes, all 3 can run simultaneously
- [x] Must run sequentially
- [ ] Other

**Dependencies:**
- Experiment 2 requires Experiment 1 completers (need email list)
- Experiment 3 requires Experiment 2 completers (need users who trust non-custodial approach)
- Cannot run in parallel due to sequential user funnel

**Rationale for order:**
1. **Experiment 1 (Broker Connection)** validates the entry point. Without broker connections, can't test anything else.
2. **Experiment 2 (Trust/zk-Proof)** validates our core differentiation. Must confirm users value this before investing in production.
3. **Experiment 3 (Paper-to-Live)** validates activation flow. Only relevant if we've proven users will connect brokers AND trust our approach.

Total timeline: ~60 days if run sequentially (12 + 9 + 26 days + buffer)

---

## Resource Allocation

| Experiment | Time (hours) | Money | Tools | Owner |
|------------|--------------|-------|-------|-------|
| 1 (Broker Connection) | 40 (6 build + 28 run + 6 analyze) | $0 | Carrd, PostHog, Airtable | Zeshan |
| 2 (Trust/zk-Proof) | 35 (8 build + 20 run + 7 analyze) | $250 (10 × $25 interview incentives) | Loom, Typeform, Zoom | Zeshan + Daniel |
| 3 (Paper-to-Live) | 50 (10 build + 30 run + 10 analyze) | $0 | Retool, Mailchimp, Polygon.io | Daniel + Zeshan |
| **Total** | **125 hours** | **$250** | | |

**Budget notes:**
- All tools use free tiers (verified available)
- Only cost is interview incentives (optional, can skip if recruiting well)
- Time is founder time (no outsourcing)

---

## Decision Framework

After completing all 3 experiments, we will:

**If all 3 hypotheses validated (≥60% for each):**  
→ Full speed ahead on MVP development
→ Begin SnapTrade production integration
→ Build real RL agent backend
→ Plan Alpha Wave 1 launch (50 users)
→ Raise seed round ($2.45M)

**If 2 of 3 validated:**  
→ Proceed with validated elements
→ Iterate aggressively on failed experiment
→ Delay alpha launch by 4 weeks to fix gap
→ Re-test failed assumption before scaling

**If 1 of 3 validated:**  
→ Major pivot likely needed
→ Deep dive customer discovery (20+ interviews)
→ Reassess ICP and value proposition
→ Consider changing target segment (retail → institutional)

**If 0 of 3 validated:**  
→ Fundamental pivot required
→ Core assumptions about market demand are wrong
→ Options: Different customer segment, different problem, different solution, or shut down

**Specific decision thresholds:**
- **Experiment 1 <40%:** Pause all development, focus on trust messaging
- **Experiment 2 <50% comprehension:** Simplify technical architecture, hide complexity
- **Experiment 3 <40%:** Eliminate paper trading or drastically change onboarding

---

## Notes & Assumptions

**Critical assumptions in this plan:**
- We can recruit 60+ engaged users through organic channels (LinkedIn, WhatsApp, X)
- Users who complete Experiment 1 will be willing to participate in Experiments 2 and 3 (engagement retention)
- Simulated flows (Experiment 1 mock OAuth, Experiment 3 Wizard of Oz) are acceptable proxies for real behavior
- 60% thresholds are the right targets (based on industry benchmarks + investor expectations)
- We have 60 days to run all experiments (realistic for pre-seed startup timeline)

**Key risks to overall plan:**
- Sequential dependencies mean if Experiment 1 fails badly, we can't run Experiments 2-3 (need pivot first)
- User fatigue: Asking same users for multiple experiments over 60 days may reduce quality
- Market timing: 60 days in fintech/crypto is long; market conditions could change
- Founder capacity: 125 hours over 60 days is ~2 hours/day JUST on experiments (plus building MVP)

**Mitigation:**
- Front-load recruiting to build large pool (200+ waitlist from which to draw for experiments)
- Vary ask: Experiment 1 is 1 minute, Experiment 2 is 8 minutes, Experiment 3 is 7 days (different commitment levels)
- Monitor market weekly; if major event (regulation change, competitor launch), reassess
- Timebox each experiment strictly; if falling behind, cut corners on nice-to-haves not must-haves

---

## Approval

- [x] All team members reviewed this plan
- [x] Success criteria are SMART (Specific, Measurable, Achievable, Relevant, Time-bound)
- [x] Resources are available (tools, time, budget)
- [x] Recruitment channels confirmed (LinkedIn groups, WhatsApp, X, email list)
- [x] Measurement tools set up (PostHog, Typeform, Airtable, Loom, Retool)

**Team Signatures:**
- Zeshan Ahmad: November 28, 2025
- Daniel Oosthuyzen: November 28, 2025

---

## Change Log

| Date | What Changed | Why |
|------|--------------|-----|
| Nov 28, 2025 | Initial 3-experiment plan created | Lab 8 exercise based on hypothesis prioritization |
| [TBD] | [Adjustments after Experiment 1] | [Based on learnings] |
| [TBD] | [Adjustments after Experiment 2] | [Based on learnings] |
