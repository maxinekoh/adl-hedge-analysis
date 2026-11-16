# ADL Hedge Analysis

**What happens to a spot–perpetual hedge when auto-deleveraging closes part of the short?** This notebook measures the exposure left behind and how it affects profit and loss (P&L) if the price moves again.

![Line chart showing incremental P&L for a fully hedged portfolio and portfolios whose short hedge was reduced by 25%, 50%, or 100%. A larger reduction means greater sensitivity to subsequent Bitcoin price moves.](figures/hedge-sensitivity.png)

## Worked example

Start with **1 BTC of spot** and an equal short in a linear BTC perpetual. At the point of auto-deleveraging (ADL), BTC is priced at **$90,000**. If ADL closes **50%** of the short while the spot position stays open:

| Metric | Result |
| --- | ---: |
| Remaining short | 0.50 BTC |
| Net long exposure | 0.50 BTC |
| Value of net exposure at the ADL price | $45,000 |
| Additional P&L if BTC falls another 5% | −$2,250 |
| Illustrative cost to restore the hedge at 50 basis points | $225 |

The 50 basis points are applied once to the missing short’s $45,000 notional at the ADL price. The table treats continued exposure and immediate re-hedging as separate scenarios.

## Explore or run

- [Open the notebook](adl_hedge_analysis.ipynb) to see the formulas, four scenarios, and chart.
- To rerun it locally, install the requirements and start Jupyter from the repository folder.

```sh
python -m pip install -r requirements.txt
python -m notebook adl_hedge_analysis.ipynb
```

Change the starting inputs in the notebook, then run all cells. It regenerates the chart at `figures/hedge-sensitivity.png`.

## Scope

The model uses illustrative inputs and assumes equal initial long and short quantities, a linear perpetual, and matching spot and perpetual price moves. Incremental P&L starts at the ADL price. Funding, basis, execution timing, ADL settlement prices, and venue-specific rules are outside the model. The $225 re-hedging cost uses an assumed rate. The results do not estimate historical losses.

This analysis extends the worked example in Maxine Koh Xin Yi’s *The Price of Solvency: When the Exchange Survives, but the Hedge Doesn't* (Blockchain @ NTU, October 2026).
