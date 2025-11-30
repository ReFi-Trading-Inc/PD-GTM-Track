# Interview Transcript: Power-Retail Trader #02

**Participant:** Power-Retail Trader #2
**Date:** September 15, 2025  
**Duration:** 47 minutes  
**Location:** Dubai, UAE (Video call)  
**Interviewer:** Zeshan Ahmad (CEO)  
**Stage:** Discovery / Experiment 2 (Non-Custodial Trust)

---

## Participant Profile

| Attribute | Details |
|-----------|---------|
| **Age** | 38 |
| **Experience** | 8 years active trading |
| **Account Size** | $85,000 (IBKR) |
| **Primary Assets** | US equities (tech stocks), crypto (BTC, ETH) |
| **Trading Frequency** | 10-15 trades/week |
| **Current Tools** | TradingView Pro, IBKR TWS, Excel for tracking |
| **Professional Background** | Senior Engineer at Aramco (oil & gas) |
| **Location** | Dubai Marina |
| **Annual Income** | $180,000 |

---

## Interview Summary

**Key Quote:**  
> *"After FTX, I'll never give my keys to anyone again. If your platform lets me keep custody while the AI trades for me, that's exactly what I need. But I need to see proof it's working, not just trust you."*

**Validation Insights:**
- ✅ Strong interest in non-custodial solution (trust barrier after FTX)
- ✅ zk-proof concept resonated ("cryptographic safety check" made sense)
- ✅ Willing to start with $100 progressive caps
- ⚠️ Concerned about RL "black box" → wants transparency
- ⚠️ Needs to see backtest results before risking real capital

**ICP Fit:** 🟢 Strong (9/10) - Primary target persona

---

## Full Transcript

**[00:00] Introduction & Warm-up**

**Zeshan:** Thanks for joining me today. I know you're busy, so I appreciate you taking the time. Before we dive in, can you tell me a bit about your trading journey? How did you get started?

**Trader #2:** Sure, happy to help. I started trading about 8 years ago, around 2017. I was working in Houston at the time—Aramco sent me there for a 2-year assignment. I had some extra cash and a colleague introduced me to options trading. Lost $3,000 in my first month [laughs]. That was a wake-up call.

**Zeshan:** Ouch. What changed after that?

**Trader #2:** I got serious. Started reading—Market Wizards, Reminiscences of a Stock Operator, all the classics. Took an online course from Udemy on technical analysis. But the real learning came from just doing it. Thousands of trades. Lots of mistakes. Eventually, I developed a system that works for me—mostly momentum trading on tech stocks. Tesla, Nvidia, Apple. Things I understand.

**[05:12] Current Trading Setup**

**Zeshan:** Walk me through your current setup. What tools are you using?

**Trader #2:** I wake up at 6 AM Dubai time—that's when New York opens. I've got three monitors set up in my home office. First monitor is TradingView with my charts—I use a custom indicator I built based on RSI and MACD. Second monitor is Interactive Brokers Trader Workstation—that's where I actually execute trades. Third monitor is just news—Bloomberg, Twitter, sometimes CNBC if something big is happening.

**Zeshan:** What does a typical trading day look like?

**Trader #2:** I scan for setups from 6 to 7 AM. I'm looking for stocks that gapped up or down overnight with volume. If I see a setup that fits my rules, I'll place a trade. Usually 2-3 trades in the morning session. Then I step away, go to work—I can't be glued to screens all day. I'll check positions around lunch, maybe adjust stop-losses. Then I close everything before US market close. I don't hold overnight unless it's a strong trend.

**Zeshan:** How much time does this take weekly?

**Trader #2:** [Pauses] Honestly? Way more than I want. Probably 15-20 hours a week. The analysis alone is 10 hours. Then there's the emotional energy—watching positions, second-guessing entries, kicking myself when I exit too early. It's exhausting.

**[11:34] Pain Points & Frustrations**

**Zeshan:** You mentioned emotional energy. Tell me more about that.

**Trader #2:** This is the hardest part of trading. I have a system that works on paper—I've backtested it, it has a 58% win rate, average R:R of 1:1.8. But in real-time, I deviate. I see Tesla down 3% and I think "this is the dip!"—even though my system says wait for confirmation. Or I'm up $800 on a trade and I exit because I'm scared it'll reverse. Then it runs another $1,200 without me.

**Zeshan:** So discipline is the issue?

**Trader #2:** Discipline is *the* issue. Not just for me—for everyone. We're human. We're wired to panic when we see red, to get greedy when we see green. The best traders are machines. That's why I'm interested in what you're building.

**Zeshan:** Have you tried any automation before?

**Trader #2:** I tried MT4 expert advisors a few years ago. Total disaster. The EAs were garbage—probably scams. I lost $2,000 testing them on real capital. Since then, I've been skeptical of anything "automated." But I know institutional traders use algorithms. I just can't afford a quant team.

**[18:22] FTX / Custody Concerns**

**Zeshan:** Let's talk about FTX. You mentioned earlier you'll never give up custody again. What happened?

**Trader #2:** [Deep sigh] I had $12,000 in FTX. Not a huge amount, but it stung. I was using it for crypto trading—faster than moving USD to Kraken every time. Then November 2022 happened. One day I woke up and couldn't withdraw. Just... locked. Gone.

**Zeshan:** Did you get anything back?

**Trader #2:** I'm in the bankruptcy process. Maybe I'll see 30 cents on the dollar in 5 years. Maybe. But it's not even about the money anymore—it's about the principle. These platforms asked us to trust them, and they betrayed that trust. Sam Bankman-Fried was on CNBC talking about "effective altruism" while he was stealing our money.

**Zeshan:** How did that change your approach?

**Trader #2:** Everything went to self-custody. I moved my crypto to a Ledger hardware wallet. My equities are at Interactive Brokers—at least that's regulated and audited. I don't care if a platform offers 10% yield—if it means giving up my keys, I'm not interested.

**Zeshan:** So if a trading platform asked for your API keys...

**Trader #2:** [Interrupts] No. Absolutely not. Not unless it's read-only and I can revoke it instantly. Even then, I'd be nervous. The only reason I'd consider it is if there's no other way. But if there's a way to trade *without* giving control of my account... that's what I want.

**[26:45] Introducing Non-Custodial + zk-Proofs Concept**

**Zeshan:** That's exactly what we're building. Let me show you a quick video—it's 3 minutes—that explains how it works. [Shares screen, plays Experiment 2 video]

**Trader #2:** [Watching intently]

**[Video ends at 30:12]**

**Zeshan:** Okay, so that was a lot. Before I ask questions, what's your gut reaction?

**Trader #2:** [Long pause] Honestly? This is exactly what I've been wanting. The non-custodial part solves my biggest fear. I keep my assets at IBKR, you just send instructions. If your platform goes down or gets hacked, I still have my money. That's huge.

**Zeshan:** And the zk-proof part—the "cryptographic safety check"?

**Trader #2:** I'll be honest, I don't fully understand the math. Something about zero-knowledge proofs, Groth16... [laughs] way over my head. But I get the concept: before every trade, the system proves it's within my risk limits. And I can verify that proof. It's like a safety lock.

**Zeshan:** Do you need to understand the math?

**Trader #2:** No. I don't understand how HTTPS encryption works either, but I trust it when I see the lock icon in my browser. Same thing here—if I see a green checkmark that says "Verified ✓" and I know it's cryptographically enforced, that's enough.

**Zeshan:** Would you trust this more than a regular "AI risk check" without proofs?

**Trader #2:** Yes. 100%. Because anyone can *say* they're checking risk. But if it's cryptographic and on-chain, you can't fake it. That's the difference between FTX saying "we have reserves" versus Kraken publishing a Merkle tree proof of reserves. One is just words. The other is math.

**[34:56] Progressive Caps & Paper Trading**

**Zeshan:** Let's talk about going live. Imagine you've used the platform in paper trading for 7 days. You've seen the AI make 15 trades, your paper account is up 6%. You feel good. Now we say: "You can go live, but you start with a $100 maximum trade size on Day 1."

**Trader #2:** $100? [Laughs] That's nothing. I have $85,000 in my account.

**Zeshan:** That's the point. It's a safety mechanism. Day 1: $100 max. Day 3: $500 max. Day 7: $5,000 max. After 2 weeks, we remove the training wheels.

**Trader #2:** [Pauses] Okay, I see what you're doing. You're protecting me from myself. And probably protecting *you* from liability. If someone loses $10,000 on Day 1 because the AI glitched, that's a lawsuit. But if they lose $100? That's acceptable risk.

**Zeshan:** Exactly. Would you be comfortable starting at $100?

**Trader #2:** Honestly? Yes. Even though it feels "too small," psychologically it makes sense. If I see it work with $100, then $500, then $5,000... by the time I'm at unrestricted, I've built trust through proof. That's smart. I'd probably do the same thing if I were you.

**Zeshan:** Some people said $100 is *too* small. They want $250 or $500 to start. What do you think?

**Trader #2:** Maybe tier it based on account size. Someone with $5,000 in their account? $100 is fine. Someone with $200,000? Let them start at $500. But honestly, even for me, I'd rather start small. It's only 2 weeks. I can wait.

**[40:18] Concerns & Objections**

**Zeshan:** What would make you hesitate to use this?

**Trader #2:** Three things. One: I want to see real backtest results. Not just "we have a 2.07 Sharpe ratio"—I want to see the trades. Dates, tickers, entry, exit, P&L. Full transparency.

**Zeshan:** We can provide that. What else?

**Trader #2:** Two: What happens if the AI goes rogue? Like, what if there's a bug and it tries to place a $50,000 trade on some penny stock? Even with proofs, software has bugs.

**Zeshan:** That's where the broker integration matters. Interactive Brokers has their own risk controls—position limits, margin requirements. And the proof system would reject anything outside your VaR limit. So there are multiple layers. But you're right—bugs can happen. That's why we start with paper trading and small caps.

**Trader #2:** Okay. Three: Regulatory risk. What if CIRO in Canada or the SEC says "this is illegal" and shuts you down? Then what happens to my trading?

**Zeshan:** Your capital stays at your broker—nothing changes there. In the worst case, we shut down and you go back to manual trading. You don't lose access to your funds. But we're designing this to be compliant from Day 1. Non-custodial reduces regulatory risk significantly.

**Trader #2:** [Nods] That makes sense.

**[44:03] Willingness to Pay**

**Zeshan:** Last question: If this existed today and worked as described, what would you pay per month?

**Trader #2:** [Thinks] For something that saves me 15 hours a week and removes emotional trading? Honestly, $300-$500 a month. Maybe more if the performance is good. I currently pay $180/month for TradingView Pro and data feeds. If your platform replaces that *and* trades for me, $500 is reasonable.

**Zeshan:** What if I said $150/month for a Starter tier—limited to one asset class—or $350/month for Pro with multi-asset?

**Trader #2:** I'd go Pro. $350 is nothing if it works. That's like... 3 good trades. If you save me even 5 hours a week, my time alone is worth $500/month. So $350 is a no-brainer.

**[46:30] Closing**

**Zeshan:** This was incredibly valuable. Thank you. One last thing: if we launch an alpha in January, would you want to join?

**Trader #2:** 100%. Just send me the invite. I'll test it, give you honest feedback, and if it works, I'll spread the word in the Dubai trading community. We have a WhatsApp group with about 40 active traders. If this is legit, word will travel fast.

**Zeshan:** That would be amazing. I'll be in touch. Thanks again.

**Trader #2:** My pleasure. Good luck with the build.

---

## Key Takeaways

### ✅ Strong Validation Signals

1. **Non-Custodial is Non-Negotiable**
   - FTX trauma is real and persistent
   - API key access to broker is maximum acceptable risk
   - Willing to sacrifice features for custody control

2. **zk-Proofs Add Trust (Even Without Understanding)**
   - "Like HTTPS lock icon" analogy worked perfectly
   - Green checkmark ✓ is sufficient UX
   - Cryptographic > "trust us" messaging

3. **Progressive Caps are Smart (Despite Initial Resistance)**
   - $100 feels small but psychologically sound
   - Tiering by account size is a good idea
   - Willing to wait 2 weeks to build trust

4. **Willingness to Pay is High**
   - $350/month for Pro tier is "no-brainer"
   - Time savings alone justifies cost
   - Value = hours saved + emotion removed + performance

### ⚠️ Concerns to Address

1. **Backtest Transparency**
   - Provide full trade log (date, ticker, P&L)
   - Not just aggregate statistics
   - Monthly transparency reports in alpha

2. **Bug Risk & Kill Switch**
   - Emphasize multi-layer safety (proofs + broker limits)
   - Clear kill switch communication
   - Insurance/guarantee for alpha users?

3. **Regulatory Uncertainty**
   - Highlight non-custodial = lower regulatory risk
   - Show compliance roadmap (CIRO, SEC, ADGM)
   - Worst case = platform shuts down, but capital is safe

### 🎯 ICP Confirmation

**This is the bullseye customer:**
- 5+ years trading experience (knows the pain)
- $50K-$100K account size (meaningful but not institutional)
- UAE location (ADGM regulatory clarity)
- Tech-savvy (understands APIs, proofs, wallets)
- Professional income (can afford $350/mo easily)
- FTX-burned (custody paranoia is an advantage for us)
- Community connector (40-person WhatsApp group)

### 📊 Experiment 2 Data Point

**Pre-Video Trust (1-5 scale):**
- ReFi.Trading: 3/5 (neutral, hadn't heard of us)
- Non-custodial concept: 5/5 (strongly interested)

**Post-Video Trust (1-5 scale):**
- ReFi.Trading: 5/5 (would join alpha immediately)
- zk-Proof concept: 4/5 (trusts it, doesn't need to understand math)

**Trust Lift:** +2 points (aligned with experiment target)

**Comprehension Test Score:** 5/5 (100%)

---

## Recommended Actions

1. **Add to Alpha Wave 1** - Priority invite (top 10)
2. **Feature in marketing** - Quote about FTX + custody
3. **Connect to Dubai community** - Potential for 10+ referrals
4. **Follow up in January** - Personal outreach before launch

---

**Interviewer Notes:**
- Power-Retail Trader #2 is articulate, thoughtful, and represents our ICP perfectly
- His objections are rational and addressable
- Strong validation signal for product direction
- High likelihood of becoming an evangelist if product delivers

**Status:** ✅ Strong ICP Fit | 🟢 Alpha Candidate
