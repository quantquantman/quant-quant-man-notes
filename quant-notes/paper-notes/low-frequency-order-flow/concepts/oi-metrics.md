# Metrics

### Metrics 總整理

#### 訂單不平衡 (Order Imbalance)

此類指標衡量市場中買方和賣方發起的交易壓力差異。

| Metric Name                         | 公式                                                                                                                                                              |
| ----------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 基於交易筆數 (Number of Trades Based)     | $$I_{NUM} = \frac{\text{No. of buyer-initiated trades} - \text{No. of seller-initiated trades}}{\text{Total no. of trades}}$$                                   |
| 基於交易股數 (Share Volume Based)         | $$I_{SHR} = \frac{\text{No. of buyer-initiated shares} - \text{No. of seller-initiated shares}}{\text{Total no. of shares traded}}$$                            |
| 基於交易金額 (Dollar Volume Based)        | $$I_{VALUE} = \frac{\text{Buyer-initiated \$ volume} - \text{Seller-initiated \$ volume}}{\text{Total \$ volume}}$$                                             |
| 標準化訂單不平衡 (Standardized, $$SOI$$)    | $$SOI_{it} = \frac{BP_{it} - BP_{mt}}{\sigma(BP_{it})}$$, where $$BP_{it}$$is the buy proportion for stock$$i$$, $$BP_{mt}$$ is the market-wide buy proportion. |
| 低頻估計 (Low-Frequency Estimate, LFOI) | $$x = \frac{\Delta P}{\lambda}$$, where $$x$$= net order flow,$$\Delta P$$= price change,$$\lambda$$= illiquidity proxy (e.g.,$$1/\text{TURN}$$, BASPRD)        |

#### 資訊不對稱與價格效率 (Asymmetric Information & Price Efficiency)

此類指標衡量市場中知情交易的可能性、價格反映資訊的效率以及相關風險。

| Metric Name                           | 公式                                                                                                                  |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| 訂單不平衡波動率 (VOIB)                       | $$VOIB_m = \text{StdDev}(\text{Daily } OIB_d)_{\text{for month } m}$$                                               |
| 訂單不平衡波動率衝擊 (SVOIB)                    | $$SVOIB_t = VOIB_t - \text{MovingAverage}(VOIB_{t-1, \dots, t-k})$$                                                 |
| 成交量變異係數 (VCV)                         | $$VCV_{it} = \frac{\hat{\sigma}_{V(i,t-20:t)}}{\hat{\mu}_{V(i,t-20:t)}}$$                                           |
| 預測可能性 (Predictive Likelihood, $$pl$$) | $$pl_{t} = \text{RollingAvg}_{d=t-19 \dots t} \left( p(oib_{d} \| oib_{d\|d-1}, \sigma^{2}(oib_{d\|d-1})) \right)$$ |
| 絕對轉換自我相關係數 ($$abs\_ac$$)              | $$\|\frac{1 + ac_{it}}{1 - ac_{it}}\|$$where$$ac_{it}$$ is 20-day rolling return autocorrelation.                   |
| 變異數比率 ($$vratio$$)                    | $$\|1 - \frac{2 \cdot var[ret_{it}^{(1)}]}{var[ret_{it}^{(2)}]}\|$$                                                 |

#### 流動性 (Liquidity)

此類指標衡量在不顯著影響資產價格的情況下進行交易的難易程度。

| Metric Name                | 公式                                                           |
| -------------------------- | ------------------------------------------------------------ |
| 報價價差 (Quoted Spread)       | $$\frac{ask - bid}{midpoint}$$                               |
| 有效價差 (Effective Spread)    | $$2 \times \frac{\lvert price - midpoint \rvert}{midpoint}$$ |
| 訂單簿深度不平衡 (Depth Imbalance) | $$\frac{ask\_depth - bid\_depth}{ask\_depth + bid\_depth}$$  |

#### 市場活動與關注度 (Market Activity & Attention)

此類指標衡量特定股票的交易活躍程度或受投資者關注的程度。

| Metric Name           | 公式                                                                                 |
| --------------------- | ---------------------------------------------------------------------------------- |
| 標準化異常散戶成交量 ($$SARV$$) | $$SARV_{it} = \frac{(v_{it} - \bar{v}_{it, t-45:t-6})}{\sigma(v_{it, t-45:t-6})}$$ |

***

### 2015-Order flow imbalance effects on the German stock market

| Metric Name                                      | 經濟意涵                                                  | 公式                                                                                                                                             |
| ------------------------------------------------ | ----------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| Order Imbalance ($$I_{it}$$)                     | 衡量在給定期間內市場買單和賣單之間的差異，代表市場上的買賣壓力。                      | $$I_{it} = \frac{\text{No. of buyer-initiated trades}_{i,t} - \text{No. of seller-initiated trades}_{i,t}}{\text{Total no. of trades}_{i,t}}$$ |
| Daily Log Returns ($$R_{it}$$)                   | 股票的每日報酬率，使用買賣報價的中間價計算，以避免買賣價差跳動 (bid-ask bounce) 的影響。 | $$R_{it} = \log\left(\frac{ask_{i,t} + bid_{i,t}}{ask_{i,t-1} + bid_{i,t-1}}\right)$$                                                          |
| Abnormal Market Capitalization ($$C_{i,t}^{a}$$) | 捕捉公司規模對訂單不平衡與報酬關係的U形效應，其中非常小和非常大的股票表現出更高的敏感度。         | $$C_{i,t}^{a} := \lvert C_{i,t} - (NT)^{-1}\sum_{i=1}^{N}\sum_{t=1}^{T}C_{i,t} \rvert$$                                                        |

***

### 2016-Estimating Order Imbalance Using Low Frequency Data

| Metric Name                           | 經濟意涵                                                         | 公式                                                                                                                         |
| ------------------------------------- | ------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------- |
| Low-Frequency Order Imbalance (LFOI)  | 根據Kyle (1985) 模型估計的淨訂單流，其中價格影響是訂單不平衡和市場非流動性的乘積。此指標僅使用日度數據計算。 | $$x = \frac{\Delta P}{\lambda}$$where$$x$$= net order flow,$$\Delta P$$= price change,$$\lambda$$ = illiquidity            |
| Turnover-based LFOI (TLFOI1)          | 使用收盤對收盤交易報酬率和成交量週轉率計算的LFOI。                                  | Daily risk-adjusted close-to-close transaction return $$\times$$ TURN                                                      |
| Turnover-based LFOI (TLFOI2)          | 使用開盤對收盤中間價報酬率和成交量週轉率計算的LFOI。                                 | Daily risk-adjusted open-to-close mid quote return $$\times$$ TURN                                                         |
| Bid-Ask Spread-based LFOI (BALFOI1)   | 使用收盤對收盤交易報酬率和買賣價差計算的LFOI。                                    | $$\frac{\text{Daily risk-adjusted close-to-close transaction return}}{\text{BASPRD}}$$                                     |
| Bid-Ask Spread-based LFOI (BALFOI2)   | 使用開盤對收盤中間價報酬率和買賣價差計算的LFOI。                                   | $$\frac{\text{Daily risk-adjusted open-to-close mid quote return}}{\text{BASPRD}}$$                                        |
| High-Low Spread-based LFOI (HLLFOI1)  | 使用收盤對收盤交易報酬率和高低價差計算的LFOI。                                    | $$\frac{\text{Daily risk-adjusted close-to-close transaction return}}{\text{HLSPRD}}$$                                     |
| High-Low Spread-based LFOI (HLLFOI2)  | 使用開盤對收盤中間價報酬率和高低價差計算的LFOI。                                   | $$\frac{\text{Daily risk-adjusted open-to-close mid quote return}}{\text{HLSPRD}}$$                                        |
| High Frequency Order Imbalance (HFOI) | 根據Lee and Ready (1991) 算法，使用高頻數據計算的淨訂單不平衡，按總發行股數進行縮放。        | $$\frac{\text{Total buyer-initiated shares} - \text{Total seller-initiated shares}}{\text{Number of shares outstanding}}$$ |
| PS measure                            | 遵循Pastor and Stambaugh (2003) 的每日淨訂單不平衡指標，即由報酬正負號決定的美元交易量。   | sign(daily close-to-close transaction return) $$\times$$ daily dollar trading volume                                       |

***

### 2018-ISO Order Imbalances and Individual Stock Returns

| Metric Name              | 經濟意涵                  | 公式                                                                                                        |
| ------------------------ | --------------------- | --------------------------------------------------------------------------------------------------------- |
| Order Imbalance (Trades) | 基於買入和賣出交易數量的標準化訂單不平衡。 | $$\frac{\text{Number of Buys} - \text{Number of Sells}}{\text{Number of Buys} + \text{Number of Sells}}$$ |
| Order Imbalance (Volume) | 基於買入和賣出數量的標準化訂單不平衡。   | $$\frac{\text{Quantity Bought} - \text{Quantity Sold}}{\text{Quantity Bought} + \text{Quantity Sold}}$$   |

***

### 2019-Predictability of Order Imbalance Market Quality and Equity Cost of Capital

| Metric Name                                             | 經濟意涵                                           | 公式                                                                                                                                                                       |
| ------------------------------------------------------- | ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Total Order Imbalance ($$oib_{it}^{tot}$$)              | 每日買方發起的美元交易量減去賣方發起的美元交易量，再除以總美元交易量。            | $$\frac{\text{Buyer-initiated \$ volume} - \text{Seller-initiated \$ volume}}{\text{Total \$ volume}}$$                                                                  |
| Predictive Likelihood ($$pl_t$$)                        | 衡量未來一天訂單不平衡可預測性的指標，來自於動態線性模型的擬合優度。值越高表示可預測性越高。 | $$\tilde{p}l_{t} = p(oib_{t} \| oib_{t\|t-1}, \sigma^{2}(oib_{t\|t-1}))$$where$$p(\cdot)$$ is the Normal PDF. The metric used is a 20-day rolling average of this value. |
| Quoted Spread ($$qspread_{it}$$)                        | 流動性指標，衡量被動交易者進行一來回交易的成本。                       | $$\frac{ask_{it} - bid_{it}}{midpoint_{it}}$$                                                                                                                            |
| Effective Spread ($$espread_{it}$$)                     | 流動性指標，衡量交易價格與當時買賣報價中間價差距的兩倍。                   | $$2 \times \frac{\lvert price_{it} - midpoint_{it} \rvert}{midpoint_{it}}$$                                                                                              |
| Absolute Transformed Autocorrelation ($$abs\_ac_{it}$$) | 價格效率的代理指標，基於每日股票報酬的自我相關性。                      | $$\lvert \frac{1 + ac_{it}}{1 - ac_{it}} \rvert$$where$$ac_{it}$$ is 20-day rolling autocorrelation.                                                                     |
| Variance Ratio ($$vratio_{it}$$)                        | 價格效率的代理指標。對於隨機遊走的過程，此比率應為1。偏離1表示可預測性。          | $$\lvert 1 - \frac{2 \cdot var[ret_{it}^{(1)}]}{var[ret_{it}^{(2)}]} \rvert$$                                                                                            |
| Depth Imbalance ($$dib_{it}$$)                          | 衡量限價訂單簿中買單與賣單掛單量的懸殊程度。                         | $$\frac{ask\_depth_{it} - bid\_depth_{it}}{ask\_depth_{it} + bid\_depth_{it}}$$                                                                                          |

***

### 2019-Order Flow Volatility and Equity Costs of Capital

| Metric Name                                     | 經濟意涵                       | 公式                                                                                                                                      |
| ----------------------------------------------- | -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| Order Imbalance (Shares) ($$OIB\_SHR$$)         | 基於買入和賣出股票數量的訂單不平衡。         | $$\frac{\text{number of shares bought} - \text{number of shares sold}}{\text{number of shares bought} + \text{number of shares sold}}$$ |
| Order Imbalance (Trades) ($$OIB\_NUM$$)         | 基於買入和賣出交易筆數的訂單不平衡。         | $$\frac{\text{number of buy trades} - \text{number of sell trades}}{\text{total number of trades}}$$                                    |
| Volatility of Order Imbalance (VOIB)            | 訂單流的波動性，被提出作為信息不對稱成本的代理指標。 | Monthly standard deviation of the daily OIB.                                                                                            |
| Shocks to Volatility of Order Imbalance (SVOIB) | 訂單不平衡波動性的創新或非預期變化。         | $$VOIB_t - \text{6-month moving average of } VOIB_{t-1}$$                                                                               |

***

### 2022-Order Imbalance and stock returns: Evidence from the Finnish stock market

| Metric Name                                   | 經濟意涵                                                     | 公式                                                                                                                                            |
| --------------------------------------------- | -------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| Share-based Order Imbalance ($$I\_SHR_{it}$$) | 買方發起的交易股數減去賣方發起的交易股數，佔總交易股數的比例。                          | $$I\_SHR_{it} = \frac{\text{Shares traded by buyers}_{it} - \text{Shares traded by sellers}_{it}}{\text{Total shares traded}_{it}}$$          |
| Trade-based Order Imbalance ($$I\_NUM_{it}$$) | 買方發起的交易筆數減去賣方發起的交易筆數，佔總交易筆數的比例。                          | $$I\_NUM_{it} = \frac{\text{Trades initiated by buyers}_{it} - \text{Trades initiated by sellers}_{it}}{\text{Total number of trades}_{it}}$$ |
| Volume Coefficient of Variation (VCV)         | 一種衡量信息不對稱性的指標，假設訂單流不平衡衡量了知情交易。它是成交量在一個月滾動窗口內的後向標準差除以平均值。 | $$VCV_{i,t} = \frac{\hat{\sigma}_{V(i,t+d)}}{\hat{\mu}_{V(i,t+d)}}$$where$$d = [-20, 0]$$                                                     |

***

### 2023-Resolving a Paradox: Retail Trades Positively Predict Returns but Are Not Profitable

| Metric Name                                         | 經濟意涵                                             | 公式                                                                                                                                                                                          |
| --------------------------------------------------- | ------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Standardized Order Imbalance ($$SOI_{it}$$)         | 一個標準化的訂單不平衡指標，它考慮了市場整體的趨勢和觀察到的交易數量，從而更可靠地評估散戶情緒。 | $$SOI_{it} = \frac{BP_{it} - BP_{mt}}{\sigma(BP_{it})}$$, where $$BP_{it}$$is the buy proportion for stock$$i$$and$$\sigma(BP_{it}) = \frac{1}{v_{it}}\sqrt{(v_{it})(BP_{mt})(1-BP_{mt})}$$ |
| Standardized Abnormal Retail Volume ($$SARV_{it}$$) | 衡量某一天某支股票的散戶交易量相對於其近期歷史水平的異常程度。                  | $$SARV_{it} = \frac{(v_{it} - \bar{v}_{it})}{\sigma(v_{it})}$$, where the mean and standard deviation are calculated over days t-45 to t-6.                                                 |
| Buy-Sell Imbalance ($$BSI_{it}$$)                   | 一個簡單、未經標準化的訂單不平衡指標，基於買入比例。                       | $$BSI_{it} = \frac{\text{Buys} - \text{Sells}}{\text{Buys} + \text{Sells}}$$                                                                                                                |

***

### 2024-Trade Size Based Order Imbalance and the Cross-Section of Stock Returns

| Metric Name           | 經濟意涵                                               | 公式                                                                                               |
| --------------------- | -------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| Share Trade Imbalance | 買入和賣出交易之間的差異，按總交易數量進行縮放，並針對特定的交易規模類別（例如，中型交易）進行計算。 | $$\text{Share Trade Imbalance} = \frac{\text{Buys} - \text{Sells}}{\text{Buys} + \text{Sells}}$$ |

***

