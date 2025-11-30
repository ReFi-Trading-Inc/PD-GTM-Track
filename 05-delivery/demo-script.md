# Live Demo Script (15 minutes)

## Slide 1: Landing Page (1 min)
"Here's our landing page. Hero message: 'Wall Street AI, Radically Accessible.' Clear value prop: non-custodial, AI-powered, cryptographically safe. Users click 'Join Alpha' and enter email. We have 50 in alpha now."

## Slide 2: Sign In (30 sec)
"Sign in with Ethereum - connect MetaMask. This is key: wallet = identity, no email/password."

## Slide 3: Broker Connect (2 min)
"First step: connect your broker. We support IBKR, Alpaca, Kraken, Coinbase via SnapTrade. Click IBKR... OAuth flow... user logs in at IBKR, approves read/write access... redirects back. Done. Portfolio synced: $85K."

## Slide 4: Risk Profile Selection (1 min)
"Choose your risk tolerance: Conservative (3% VaR), Moderate (5%), Aggressive (8%). Most users pick Moderate. Let's do that."

## Slide 5: Strategy Selection (1 min)
"Pick your RL strategy. We have PPO (conservative momentum) and TD3 (aggressive momentum). These are pre-trained on 3.1 years of data: 28% CAGR, 2.07 Sharpe. Let's pick TD3."

## Slide 6: Paper Trading (2 min)
"You start in paper trading. The AI proposes trades - here's one: Buy 5 shares AAPL at $180. See the 'Why this trade?' explanation: bullish momentum, VIX low. Over 7 days, you run 50 simulated orders. Dashboard shows PnL, Sharpe, max drawdown."

## Slide 7: Go Live (1 min)
"After 7 days, you're prompted to go live. Progressive caps: Day 1-2 = $100 max, Day 3-6 = $500, Day 7-14 = $5K. Let's start with $100."

## Slide 8: First Real Trade (3 min)
"AI proposes: Buy 5 AAPL at $180 = $900 total. Click 'Confirm'. Watch: zk-VaR proof generates in 2-3 seconds. See the checkmark: ✅ Risk Safety Check Passed. This is the magic - cryptographic proof that your VaR limit wasn't breached. Click 'Confirm Trade'. Order sent to IBKR... filled at $180.05. Confirmation in dashboard. You'll get a daily recap email at 6 PM."

## Slide 9: Audit Trail (1 min)
"Click on the trade. See the proof hash? Links to zkSync Era blockchain explorer. Immutable, auditable, transparent. Regulators love this."

## Slide 10: Kill Switch (30 sec)
"See 'Pause All Trading' in top right? Always visible. One click = all trading stops immediately. Safety first."

## Slide 11: Performance Dashboard (1 min)
"Over 2 weeks: 8 trades, +$342 PnL, 2.1 Sharpe, -2.1% max DD. AI outperformed S&P 500 by 4.2%. Caps increased to $500, then $5K. You're now a full active trader."

## Q&A (remaining time)
Be ready for:
- "How does zk-VaR work?" → High-level: mathematical proof, circuit, on-chain verification
- "What if IBKR goes down?" → Multi-broker redundancy, fallback to Alpaca
- "Regulatory risk?" → Non-custodial = huge advantage, hired counsel, sandbox approved
