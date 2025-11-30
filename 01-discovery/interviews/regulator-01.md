# Interview Transcript: Regulator #01 - CIRO Canada

**Participant:** Regulator #1
**Title:** Senior Policy Advisor, Canadian Investment Regulatory Organization (CIRO)
**Date:** November 18, 2025  
**Duration:** 38 minutes  
**Location:** Toronto, ON (Video call)  
**Interviewer:** Zeshan Ahmad (CEO)  
**Stage:** Discovery / Regulatory Validation

---

## Participant Profile

| Attribute | Details |
|-----------|---------|
| **Organization** | CIRO (Canadian Investment Regulatory Organization) |
| **Role** | Senior Policy Advisor, Innovation & Fintech Division |
| **Experience** | 12 years in securities regulation |
| **Previous Roles** | OSC (Ontario Securities Commission) - 6 years |
| **Education** | LLB, MBA |
| **Focus Areas** | Electronic trading, DEA rules, algorithmic trading oversight |

---

## Interview Summary

**Key Quote:**  
> *"The non-custodial model is your biggest advantage from a regulatory perspective. You're not holding client assets, so you avoid the most onerous dealer registration requirements. The SnapTrade partner model is compliant—they've already done the due diligence with Alpaca and other brokers. Your challenge will be around the AI system—explainability and oversight."*

**Validation Insights:**
- ✅ Non-custodial architecture significantly reduces regulatory burden
- ✅ SnapTrade partner model is compliant path (better than direct API)
- ✅ CIRO views AI in trading as "tool" not "advisor" if properly positioned
- ⚠️ "Human-in-the-loop" principle is critical (cannot be fully autonomous for retail)
- ⚠️ Will need clear disclosures about AI limitations and risks

**Regulatory Risk:** 🟡 Medium (manageable with proper design)

---

## Full Transcript

**[00:00] Introduction**

**Zeshan:** Thank you so much for taking this call. I know CIRO's time is limited, so I really appreciate you speaking with us.

**Regulator #1:** Of course. We encourage innovation in Canadian capital markets—that's why we created the Innovation Office. When I saw your intake form mentioning "non-custodial algorithmic trading," I was intrigued. That's an area we're actively thinking about.

**Zeshan:** Before we dive into our specific model, can you give me a high-level overview of how CIRO thinks about algorithmic trading platforms like ours?

**Regulator #1:** Sure. Let me start with the basics. CIRO regulates investment dealers and trading activity on Canadian marketplaces. When you're building a platform that involves programmatic trading, we care about three things:

One: **Who is executing the trades?** If you're executing on behalf of clients, you're likely a dealer and need registration.

Two: **Who has custody of client assets?** If you're holding client cash or securities, you're definitely a dealer—and custody brings a whole host of capital and insurance requirements.

Three: **What level of discretion does the system have?** If the AI is making decisions *without* meaningful client control, that starts to look like portfolio management or advising, which has different registration requirements.

**[05:34] Non-Custodial Architecture Discussion**

**Zeshan:** Let me describe our model. We *never* touch client assets. Users keep their funds at their existing broker—Interactive Brokers, Alpaca, whoever. We connect via API through an aggregator called SnapTrade. Our system generates trade recommendations, but the execution happens at the user's broker. We're not a dealer, not a custodian—we're a technology provider.

**Regulator #1:** [Makes notes] Okay, so you're not taking custody. That's good—that immediately removes about 80% of the regulatory complexity. You mentioned SnapTrade—they're an approved Alpaca partner, correct?

**Zeshan:** Correct. SnapTrade has already gone through Alpaca's partner approval process. They handle the OAuth flow, the API integration, all the broker-specific compliance.

**Regulator #1:** That's smart. By using a veed intermediary like SnapTrade, you're not trying to become a Alpaca partner yourself—which would require you to meet CIRO's Direct Electronic Access rules. SnapTrade absorbs that burden. From a regulatory perspective, this is a much cleaner model than trying to go direct.

**Zeshan:** So the SnapTrade path is compliant?

**Regulator #1:** Based on what you've described, yes. But let me be clear: I'm giving you general guidance, not a legal opinion. You should have a securities lawyer review your entire setup. But conceptually, using a veed intermediary like SnapTrade, where the user authorizes the connection via OAuth and retains control... that's a known, accepted model.

**[12:18] AI and the "Human-in-the-Loop" Principle**

**Zeshan:** Let's talk about the AI. We use reinforcement learning algorithms to generate trade ideas. Before any trade executes, we generate a zero-knowledge proof that the trade is within the user's risk limits. The user's smart contract wallet requires this proof—it's cryptographically enforced. How does CIRO view this?

**Regulator #1:** [Long pause] Okay, there's a lot there. Let me unpack it. First, the zero-knowledge proof for risk compliance—that's interesting. I don't think we've seen that before. Conceptually, I like it. You're creating an auditable, tamper-proof record of risk enforcement. That's good.

**Zeshan:** And the RL algorithm generating trades?

**Regulator #1:** Here's where we need to be careful. CIRO recently issued guidance on AI in capital markets—CSA Staff Notice 11-349. The key principle is: **AI cannot replace human judgment and oversight, especially for retail clients.** An AI can be a tool to *assist* decision-making, but there needs to be meaningful human control.

**Zeshan:** What does "meaningful human control" look like?

**Regulator #1:** Good question. For institutional clients—like a hedge fund using your system—the requirement is less strict. Institutions have compliance teams, risk officers. They can oversee the AI. But for retail clients, we're more cautious.

Here's a concrete example: if your platform automatically places trades without the user clicking "confirm," that's closer to full autonomy—and that's risky. But if the AI generates a trade proposal, shows the user the reasoning (even at a high level), and the user clicks "Execute" for each trade... that's human-in-the-loop. The user is making the final decision.

**Zeshan:** What about paper trading first, then transitioning to live with progressive caps? The user has seen the AI trade for 7 days in simulation before risking real capital.

**Regulator #1:** That helps. It shows you're being prudent. But even in live trading, we'd want to see some form of user consent per trade—at least in the early stages. Maybe after 30 days of live trading with no issues, you can move to a "set-and-forget" model. But initially, more human touch is better.

**[22:45] Explainability and Transparency**

**Zeshan:** One of our challenges is explainability. Reinforcement learning models are complex—thousands of parameters. We can't explain every decision in plain English. Is that a deal-breaker?

**Regulator #1:** No, but you need to manage it. Here's what CIRO expects:

One: **Disclose the limitations.** Don't oversell the AI. Tell users: "This system uses machine learning. It's not perfect. Past performance doesn't guarantee future results. You are responsible for monitoring your account."

Two: **Provide high-level transparency.** You don't need to explain every parameter, but you should be able to say: "The AI detected a bullish momentum signal in Apple based on price action and volume. It recommended buying 10 shares."

Three: **Have a risk override.** If the user says "I don't like this trade," they can veto it or pause the system entirely.

**Zeshan:** We have a kill switch—users can disable trading instantly.

**Regulator #1:** Good. That's essential. I'd also recommend regular reporting—weekly or monthly performance summaries, showing what the AI did, how it performed, and any risk events.

**[28:12] Licensing and Registration**

**Zeshan:** Do we need to register with CIRO?

**Regulator #1:** Based on what you've described—non-custodial, user retains control, no advisory relationship—I don't think you need dealer registration. You're a technology provider.

**However:** If you start managing client accounts discretionarily, or if you start holding assets, that changes. Also, if you launch a pooled fund where you aggregate capital from multiple investors and trade it algorithmically, that's a different beast—you'd need to register as a portfolio manager or investment fund manager.

**Zeshan:** We have no plans for a pooled fund. This is strictly self-directed accounts.

**Regulator #1:** Then you're likely fine. But again: get a legal opinion. Regulatory classification is fact-specific.

**[31:50] Token and Crypto Elements**

**Zeshan:** We plan to eventually launch a $REFIN token—utility and governance for the platform. How does CIRO view that?

**Regulator #1:** [Sighs] Crypto tokens are... complicated. The CSA has issued guidance (Staff Notice 21-327): most tokens are securities unless they're pure utility with no investment expectation. If your token gives governance rights and fee rebates, it's likely a security.

**Zeshan:** What does that mean for us?

**Regulator #1:** If it's a security, you need to comply with securities laws:
- Prospectus or prospectus exemption for issuance
- Possibly register as a "restricted dealer" if you're facilitating token trading
- AML/KYC compliance under FINTRAC

But here's the thing: you don't *need* a token to launch your trading platform. You can launch with traditional SaaS pricing—$150/month, $350/month—and add the token later once you have legal and regulatory clarity.

**Zeshan:** That's our plan. Token is Phase 2, post-Series A.

**Regulator #1:** Smart. Get the core product working first. Then tackle the token when you have more resources and regulatory bandwidth.

**[35:20] Closing Advice**

**Zeshan:** If you were in my shoes, what would you prioritize from a regulatory perspective?

**Regulator #1:** Three things:

**One:** Get a legal opinion from a Canadian securities lawyer. Osler, McCarthy Tétrault, Stikeman—someone who knows CIRO rules inside-out. Budget $15-20K for an initial regulatory memo.

**Two:** Document everything. Build an audit trail of every trade, every risk check, every user action. CIRO loves documentation. If we ever come knocking, you want to show us logs that prove you were operating safely.

**Three:** Engage with us early. CIRO has a Regulatory Sandbox program. If you're doing something novel—like your zk-proof risk system—apply for the sandbox. It gives you a safe space to test, and we give you feedback. It's not a license, but it's a relationship.

**Zeshan:** I didn't know about the sandbox. How do we apply?

**Regulator #1:** Go to ciro.ca, look for "Innovation Office." Fill out the intake form. Mention this conversation—I'll be looped in. We usually respond within 2-3 weeks.

**Zeshan:** That's incredibly helpful. Thank you.

**Regulator #1:** You're welcome. I like what you're building. The non-custodial model is the right approach. Just don't over-promise on the AI, keep humans in the loop for retail, and you'll be fine. Good luck.

---

## Key Takeaways

### ✅ Positive Signals

1. **Non-Custodial is Regulatory Advantage**
   - Avoids 80% of dealer registration complexity
   - No custody = no capital requirements
   - Technology provider classification likely

2. **SnapTrade Partner Model is Compliant**
   - Vetted intermediary reduces our burden
   - Alpaca has approved SnapTrade's model
   - Cleaner than direct API integration

3. **zk-Proofs are Novel but Welcome**
   - CIRO hasn't seen this before
   - Auditable, tamper-proof risk enforcement is viewed positively
   - Aligns with regulatory goals of safety

4. **Regulatory Sandbox Opportunity**
   - CIRO encourages innovative firms to apply
   - 2-3 week turnaround on applications
   - Safe space to test and get feedback

### ⚠️ Caution Areas

1. **"Human-in-the-Loop" is Critical for Retail**
   - Cannot be fully autonomous (at least initially)
   - User must click "Confirm" or "Execute" per trade
   - After 30 days, can consider more automation

2. **AI Explainability Matters**
   - Don't need to explain every parameter
   - Must provide high-level trade rationale
   - "Bullish momentum in AAPL" > silence

3. **Kill Switch is Essential**
   - Users must be able to pause/stop instantly
   - Emergency controls are non-negotiable
   - Weekly performance reports recommended

4. **Token is a Security (Likely)**
   - CSA Staff Notice 21-327 applies
   - Prospectus or exemption required
   - Recommend launching without token first

### 📋 Action Items

| Priority | Action | Owner | Deadline |
|----------|--------|-------|----------|
| **P0** | Hire Canadian securities lawyer (Osler/McCarthy) | Zeshan | Jan 15, 2026 |
| **P0** | Get regulatory opinion on platform model | Legal | Feb 1, 2026 |
| **P1** | Apply to CIRO Regulatory Sandbox | Zeshan | Jan 20, 2026 |
| **P1** | Build audit trail infrastructure (all trades logged) | Daniel | Feb 15, 2026 |
| **P1** | Add "Confirm Trade" button (human-in-the-loop) | Frontend | Mar 1, 2026 |
| **P2** | Weekly performance report automation | Backend | Mar 15, 2026 |
| **P2** | Defer token launch until Series A + legal clarity | Zeshan | TBD (2027) |

### 🎓 Regulatory Positioning

**Pitch to CIRO:**
> "ReFi.Trading is a non-custodial trading technology platform. We never hold client assets—users maintain custody at their registered broker (IBKR, Alpaca). We connect via a vetted intermediary (SnapTrade) and provide AI-powered trade recommendations with cryptographic risk enforcement. Users retain final decision-making authority. We're seeking guidance through CIRO's Innovation Office to ensure our approach aligns with regulatory expectations."

**Key Phrases to Use:**
- "Technology provider" (not dealer, not advisor)
- "User retains control and custody"
- "AI as a tool, not a replacement for judgment"
- "Human-in-the-loop principle"
- "Cryptographically enforced risk limits"
- "Transparent audit trail"

**Key Phrases to Avoid:**
- "Fully autonomous trading"
- "AI makes all decisions"
- "Set it and forget it"
- "Guaranteed returns"
- "No risk"

---

## Regulatory Risk Assessment

**Overall Risk:** 🟡 **MEDIUM** (Manageable with proper design)

**Risk Breakdown:**

| Risk Factor | Level | Mitigation |
|-------------|-------|------------|
| **Dealer Registration** | 🟢 Low | Non-custodial + SnapTrade intermediary model |
| **Advising Rules** | 🟡 Medium | Human-in-the-loop + explicit disclaimers |
| **AI Oversight** | 🟡 Medium | Kill switch + trade rationale + weekly reports |
| **Token as Security** | 🔴 High | Defer token launch until legal clarity |
| **AML/KYC** | 🟢 Low | Broker handles KYC, not us |
| **Market Manipulation** | 🟢 Low | UMIR rules enforced by broker, not us |

**Conclusion:** Regulatory structure is sound for MVP. Main requirement is legal opinion + CIRO sandbox application. Token launch should wait until Series A stage.

---

## Recommended Next Steps

1. **Engage Canadian securities lawyer** (budget: $15-20K for initial memo)
2. **Apply to CIRO Regulatory Sandbox** (intake form at ciro.ca)
3. **Design "human-in-the-loop" UX** (Confirm button per trade, at least initially)
4. **Build audit infrastructure** (log every trade, risk check, user action)
5. **Defer token launch** (focus on SaaS model first)

**Timeline:** Legal opinion by Feb 1, Sandbox application by Jan 20, MVP design incorporates findings by Mar 1.

---

**Interviewer Notes:**
- Jennifer was generous with her time and very forthcoming
- CIRO is innovation-friendly, not hostile
- Non-custodial model gives us significant regulatory advantage
- Main risk is around AI autonomy—need human-in-the-loop for retail
- Token launch should wait (not a blocker for MVP)

**Status:** ✅ Regulatory Path is Clear | 🟡 Action Items Identified
