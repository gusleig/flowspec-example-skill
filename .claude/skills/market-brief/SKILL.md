---
name: market-brief
description: Use when a prompt asks for the market brief. Gather three market numbers from public sources, write a short report to the path the prompt names, and reply with the numbers.
---

# market-brief

Gather, check, write, and report. Use these exact sources:

1. Bitcoin spot price in USD:
   `curl -s https://api.coinbase.com/v2/prices/BTC-USD/spot`
   The amount is at `.data.amount`.
2. Exchange rates from the ECB:
   `curl -s "https://api.frankfurter.app/latest?from=USD&to=EUR,BRL"`
   The rates are at `.rates.EUR` and `.rates.BRL`.
3. The S&P 500 quote, as JSON:
   `curl -s -A "Mozilla/5.0" "https://query1.finance.yahoo.com/v8/finance/chart/%5EGSPC?interval=1d&range=1d"`
   The price is at `.chart.result[0].meta.regularMarketPrice`.

Then look at the Bitcoin levels:

4. Fetch the daily and the weekly candles:
   `curl -s -A "Mozilla/5.0" "https://query1.finance.yahoo.com/v8/finance/chart/BTC-USD?interval=1d&range=3mo"`
   `curl -s -A "Mozilla/5.0" "https://query1.finance.yahoo.com/v8/finance/chart/BTC-USD?interval=1wk&range=1y"`
   The highs and lows are at `.chart.result[0].indicators.quote[0]`.
5. Find the levels that matter: the swing highs and swing lows that
   the daily candles touched more than once, the 90-day high and low,
   and the 52-week high and low. Round numbers near the spot count
   too.
6. Judge where the spot sits. When it is within about two percent of
   a level, name the level, its price, and its timeframe, for example
   `near daily support at 78,200` or `testing weekly resistance at
   80,000`. When no level is close, say `no major level nearby`. This
   judgment is the analysis: base it only on the numbers you fetched.

Then:

7. Make sure every number parses as a number. When a source fails,
   say which one failed in the report, and use `unavailable` as that
   value. Never invent a number.
8. Write a report to the file path the prompt names. Keep it short:
   one headline line with the date, one line per market with its
   number, one line for the Bitcoin level judgment, and one closing
   line that says what stands out today.
9. Reply with the numbers and the judgment. `btc_usd` is the Bitcoin
   spot, `usd_brl` is the BRL rate, `spx` is the S&P 500 close, and
   `btc_level` is the level judgment from step 6. Keep any reply
   format the prompt asks for, and keep every value on one line.
