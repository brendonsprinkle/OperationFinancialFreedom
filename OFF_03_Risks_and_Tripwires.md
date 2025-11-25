# Operation Financial Freedom — Risks and Tripwires

Trading is as much about managing downside as it is about seeking upside.  This document catalogues the major risks you face and defines clear “tripwire” conditions that trigger automatic actions (halt, review, revert to paper).  Review and update this list regularly.

## Market Risks

* **Alpha decay and crowding:** Strategies that perform well today may stop working as more participants exploit the same edge.  Monitor returns and stop trading if the edge deteriorates or becomes negative for an extended period (e.g. three consecutive months of losses).
* **Regime shifts and structural changes:** Bull/bear cycles, regulatory changes (e.g. new taxes on crypto), and major macro events can make historical data irrelevant.  Recognise when conditions change (e.g. volatility doubles, funding rates flip sign) and re‑evaluate your models.
* **Exchange/counterparty risk:** Exchanges can freeze withdrawals, suffer hacks or insolvency (e.g. FTX, LUNA).  Diversify across venues and never leave large balances on a single platform.
* **Liquidity shocks and black swans:** Sudden price gaps or flash crashes can wipe out leveraged positions and cause large slippage.  Avoid excessive leverage and use conservative position sizes to weather shocks.

## Model Risks

* **Overfitting:** Complex models, especially neural networks and RL agents, can capture noise rather than signal.  If a strategy performs exceptionally well in sample but poorly out of sample, suspect overfitting and simplify.
* **Unrealistic backtests:** Failing to include fees, slippage, latency or realistic execution results in misleading backtests.  Backtest only with conservative assumptions.
* **Parameter sensitivity:** Strategies like Avellaneda–Stoikov are highly sensitive to volatility or order arrival estimates.  Re‑estimate parameters regularly and have fallback defaults.
* **Reward hacking in RL:** Agents may learn to exploit the reward function in unintended ways (e.g. generating volume without profit).  Inspect behaviour and adjust rewards accordingly.

## Operational Risks

* **API outages and rate limits:** Exchange APIs may go down or throttle you.  Implement retry logic with exponential backoff and alerting when too many errors occur.
* **Coding bugs and logic errors:** A single bug can cause unintended trades (e.g. order quantity mis‑scaled).  Write unit tests for critical functions and peer‑review any code changes.  
* **Bad parameter changes:** Changing a stop‑loss threshold or position size without testing can blow up a strategy.  Always test changes in paper mode first.
* **Infrastructure failures:** VPS crash, network outage or power loss can leave positions unmonitored.  Deploy redundant systems or at least fail‑safe orders (e.g. fixed stop‑loss orders placed directly on the exchange).

## Psychological & Behavioural Risks

* **Over‑trading and revenge trading:** It’s tempting to “tweak” strategies after a loss.  Stick to the plan; adjust only after thorough analysis.
* **Loss aversion and fear of missing out:** Taking profits too early or entering trades prematurely can reduce your edge.  Follow pre‑defined rules.
* **Burnout:** Running bots and monitoring markets is time‑consuming.  Schedule rest, use automation for alerts and set boundaries (e.g. no manual trades outside strategy rules).

## Tripwires

Tripwires are pre‑defined thresholds that automatically trigger actions without human emotion.  Set them conservatively at first and adjust as you gain experience.

1. **Max Drawdown:** If cumulative drawdown on a strategy exceeds *X%* of deployed capital (suggested range: 10–20%), halt all new trades, close open positions and switch the strategy back to paper trading for review.
2. **Divergence from Backtest:** If live PnL over a 1‑month period deviates by more than *Y%* (e.g. 20%) from the expected range (based on backtest distribution), suspend the strategy and investigate causes (data drift, market changes).
3. **API Error Spike:** If the bot records more than N API errors or failed orders in a day (choose N based on normal error rate), pause trading and send an alert.  Resume only after verifying API and code health.
4. **Exchange Incident:** If an exchange announces solvency issues, major hacks or prolonged outages, immediately withdraw funds and stop trading on that venue.
5. **Slippage Spike:** If average slippage doubles relative to baseline (e.g. >0.5% per trade), reduce position sizes or pause trading until liquidity normalises.

*TODO: choose specific values for X (max drawdown), Y (divergence threshold) and N (API error threshold) based on your risk appetite.*

## Final Advice

No model or strategy will save you from poor risk management.  The best way to “avoid blowing up” is to assume you will be wrong at times and design for that outcome.  Document every change, test thoroughly and take breaks.  Remember that preserving capital enables you to stay in the game long enough for modest edges to compound.
