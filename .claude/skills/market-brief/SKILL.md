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

Then:

4. Make sure every number parses as a number. When a source fails,
   say which one failed in the report, and use `unavailable` as that
   value. Never invent a number.
5. Write a report to the file path the prompt names. Keep it short:
   one headline line with the date, one line per market with its
   number, and one closing line that says what stands out today.
6. Reply with the three numbers. `btc_usd` is the Bitcoin spot,
   `usd_brl` is the BRL rate, and `spx` is the S&P 500 close. Keep
   any reply format the prompt asks for, and keep every value on one
   line.
