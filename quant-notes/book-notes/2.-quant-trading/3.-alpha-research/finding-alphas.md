# Finding Alphas

### Info

* **Author:** Igor Tulchinsky
* **Publisher:** Wiley
* **Publication Year:** 2019 (Second Edition)

### Summary

"Finding Alphas" is a practical guide by Igor Tulchinsky and practitioners from WorldQuant, detailing the process of creating quantitative trading strategies known as alphas. The book covers the entire workflow, from data research and model development to backtesting and avoiding common biases. Ultimately, it provides a collection of professional insights and techniques for discovering predictive signals in financial data.

### 1. The Big Picture: Core Concepts

#### Quick Guide (Chapter Map)

* Part I: Introduction: Definition of an alpha, its lifecycle, and the stop-loss mindset.
* Part II: Design & Evaluation: Alpha design, backtesting, overfitting, risk factors, and robustness.
* Part III: Extended Topics: Alphas from alternative data (news, options, etc.).
* Part IV: WebSim™: A deep dive into the simulation platform.
* Part V: A Final Word: Habits of successful quantitative researchers.

#### What is an Alpha?

* Multiple Equivalent Definitions:
  * A forecast of future returns for individual securities.
  * A set of portfolio holdings that changes over time.
  * A well-founded fundamental viewpoint.
* Characteristics of a Good Alpha:
  * Simple and interpretable.
  * Strong in-sample Sharpe ratio.
  * Insensitive to small changes in parameters or data.
  * Robust across different universes and regions.
* The Algorithmic Design Process (Iterative):
  1. Observe data patterns.
  2. Formulate a hypothesis (as a formula).
  3. Convert the formula into portfolio holdings.
  4. Test its performance.
  5. If effective, submit and deploy. Then, repeat the cycle.

#### Summary in a Sentence

* An alpha is an interpretable forecast, validated by rigorous backtesting, managed with risk and cost discipline, and strengthened through diversification and robustness engineering. Tools like WebSim simply make this process faster and more systematic.

### 2. From Idea to Implementation

#### Alpha Types & Information Frequency

* By Asset Class:
  * Stocks, ETFs, Currencies, Futures, Options, Bonds, etc.
* By Rebalancing Frequency:
  * Intraday: (e.g., 1, 5, or 15 minutes, or event-triggered).
  * Daily: (e.g., Delay 0, Delay N, MOO/MOC).
  * Weekly/Monthly.
* Common Information Sources:
  * Price/Volume, Fundamentals, Macroeconomic Data, Text, Multimedia.

#### From Idea to Alpha (Implementation Workflow)

* Lifecycle:
  * Data → Model (Alpha) → Price Forecast.
  * _Note:_ Data quality directly impacts output. Be mindful of alpha decay and crowding.
* Example Steps:
  1. Formulate Hypothesis: e.g., `Alpha = -(1-week returns)`.
  2. Refine & Enhance: e.g., apply sector-neutralization.
  3. Convert to Holdings: Define position sizing based on alpha values.
  4. Run Robustness Checks: Verify key metrics across different conditions.

### 3. Validation and Risk Management

#### Backtesting and Its Limitations

* Purpose: A screening and comparison tool, not a final investment decision.
* Key Limitations:
  * Changing market structures.
  * Unrealistic assumptions (transaction costs, market impact).
  * Look-ahead bias.
  * High risk of overfitting.
* Core Metrics:
  * Information Ratio (IR), Sharpe Ratio, Turnover, Correlation.

#### Overfitting: The Key Risk

* Symptoms & Pitfalls:
  * "Finding" a high Sharpe ratio on a short sample after many tries.
  * Spurious correlations in random data.
  * Academic publication bias.
* Avoidance Strategies:
  * Strict Out-of-Sample (OOS) testing.
  * Cross-validation and regularization.
  * Model simplicity and unit consistency.

#### Evaluation & Selection Criteria

* IR (Information Ratio): Measures forecast consistency.
* Sharpe Ratio: On WebSim, requires high thresholds (e.g., $$ $\ge 3.95$ $$ for Delay-0) to pass.
* Margin (Profit per $ Traded): Reflects sensitivity to transaction costs.
* Uniqueness (Decorrelation): Low correlation with existing alphas is highly valued.
* Turnover & Liquidity: Strive for a balance between profitability and scalability.

#### Risk and Drawdown Management

* Definition:
  * Drawdown: The percentage decline from a performance peak.
* Control Methods:
  * Set exposure limits (single security, sector).
  * Neutralize factor exposures (beta, styles).
  * Use take-profit and stop-loss orders.
* The Stop-Loss Mindset:
  * Before launching, define the maximum acceptable loss and an exit plan.

### 4. Data, Automation, and Advanced Topics

#### Data and Signals

* Core Principle: Data is the foundation of alpha research.
* Robustness Techniques:
  * Ranking, Quantiles, Z-scoring, Truncation/Winsorizing.
* Automated Search:
  * Components: Input data, search algorithm, signal testing framework.
  * Key Insight: A longer test period isn't always better due to changing market dynamics.

### 5. Tools & Practical Application

#### WebSim™ (Implementation & Interpretation)

* Purpose: A cloud-based backtesting platform for rapid idea validation.
* Key Features:
  * Accepts expressions or Python code.
  * Provides instant feedback on PnL, Sharpe, Turnover.
  * Manages the OOS testing pipeline.
* Interpreting Results:
  * Sharpe Bracket: Grades alphas from "Spectacular" to "Poor".
  * Alpha Repository: Allows filtering and analysis of all submitted alphas.
  * Book Size: Fixed at $20M with 2x leverage.

#### Practical Checklist

1. Define universe, frequency, and delay.
2. Write an interpretable expression matching your hypothesis.
3. Apply neutralization and/or scaling.
4. Review key backtest metrics (IR, Sharpe, Turnover, Margin, Drawdown).
5. Validate across different samples, universes, and regions.
6. Submit for OOS testing based on platform thresholds.
7. Manage risk with exposure limits and stop-loss rules.
8. Avoid Overfitting through strict discipline and simple models.
