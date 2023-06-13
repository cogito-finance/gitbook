---
description: An in-depth explanation of Cogito's core concepts
---

# Capital Adequacy Ratio

One of the key characteristics of the protocol is that when users deposit crypto assets and mint tracercoins, the underlying crypto assets are split in two reserves. This split is determined by the **Capital Adequacy Ratio (CAR)**.&#x20;

The CAR is the core essence of Cogito that provides pragmatic guidance for treasury allocation, risk management, token buyback, and protocol growth. It ensures that capital of the protocol is kept at a level sufficient to absorb losses and counteract negative events, in order to protect users and ensure stability.

As mentioned earlier, the reserve consists of a liquid and illiquid component. We assign a risk discounting factor for each asset based on the associated risks and liquidity. The discounting factors are based on three major risks:&#x20;

* Counterparty risk associated with stablecoins, i.e. a counterparty (e.g. a farming or a lending protocol) fails to repay the full amount of USDC we’ve deposited.
* Market risk associated with losses due a decrease in the value of investments. It applies to all trading book products.&#x20;
* Operational risk resulting from inadequate or failed internal processes, people and systems, or from external events, for example hacking or exploits to our system.&#x20;

The Cogito team has developed a scorecard system to determine the discounting factors, where metrics include project performance, historical price volatility, track record of security, and other factors. The scorecard will be managed by the Cogito treasury investment board and be updated regularly for public review.

Similarly, the liability of the protocol is assigned a time factor depending on the tenor of deposits placed in the ADP. The CAR is calculated as follows:

$$
CapitalAdequacyRatio(CAR) = \frac{RiskWeightedCapital}{TenorWeightedDebt} = \frac{\sum\nolimits_{i}^n A_i*df_i }{\sum\nolimits_{j}^m L_j*tw_j * e }
$$

$$A_i$$ is  is the market value of asset i in the reserve.

​$$df_i$$is the respective discounting factor for asset $$i$$.

$$L_j$$is the amount of tracercoins outstanding.

$$tw_j$$is the time weighting factor of a given tracercoin.

​$$e$$ is the exchange rate of the tracercoin to stablecoins

## ​CAR in practice

As an illustration, assume the reserve includes a liquid reserve of 100 USDC, an illiquid reserve of 100 USDC deposit in a credited platform (e.g. AAVE) for 6 months, and an illiquid reserve of BTC with a market value of 100 USDC. On the other hand, outstanding tracercoin is 300 GCOIN, of which 100 in users' wallets, 200 in ADP for 12 months. GCOIN price is 1.02 USDC.

We establish that liquid reserves have a 100% discounting factor, meaning we don’t discount it at all. Medium-term investments ( 6 monthsTenor<12 months) have a 95% discounting factor and blue-chip risky assets have a 60% discounting factor. Meanwhile, liabilities with 1-year tenor carry a time factor of 88%, i.e. we discount it by 12%, which is the Time Value of Money (TVM) indicating the current value of future cash flows.

| Illiquid reserve - USDC deposit for 6 months | 100 \* 95% = 95             |
| -------------------------------------------- | --------------------------- |
| Illiquid reserve - BTC                       | 100 \* 60% = 60             |
| GCOIN in the user's wallet                   | 100 \* 100% = 100           |
| GCOIN deposited for 12 months                | 200 \* 88% = 176            |
| Total Risk-Weighted Asset (USDC)             | 100 + 95 + 60 = 255         |
| Total Tenor Weighted Liability (USDC)        | (100 + 176) \* 1.02 = 281.5 |
| CAR                                          | 255 / 281.5 = 90.6%         |

CAR directly impacts the risk tolerance and investment decisions of the protocol. The ASF monitors the CAR continuously and adjusts strategies through what we call a “defensive mechanism” to ensure the CAR is kept at a satisfactory level.

During the full collateralization phase, the CAR is expected to be running between 90% to 110%. When the CAR is much higher (>110%), the ASF will allocate more reserves to illiquid components, and invest in higher risk protocols or assets to generate higher yields. When the CAR drops below 90%, the program will be more risk-off and invest in safer products; in the meantime, the protocol will divert the ongoing revenue to liquid reserves to supplement capital. If the CAR drops further to below 75%, the protocol will halt interest distribution and build up reserves until the CAR recovers. In drastic scenarios where the CAR drops below 50% — even though this may not warrant a depeg or failure of the tracercoins — we will trigger the distribution of retained profits or sell off reserves to defend the CAR. When the system is running as a risk-weighted-reserve, we aim to achieve a CAR ratio of at least 75%, which is the safety ratio to prevent substantial bank runs in most of our stress tests. This is much more prudent than traditional banks where regulation requires the banks’ CAR (which is defined similarly as our approach) to be only a minimum of 8%!
