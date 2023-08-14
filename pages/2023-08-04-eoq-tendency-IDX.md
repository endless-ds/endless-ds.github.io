@def title = "End of Quarter Tendency in IDX Composite Index"
@def hasmath = true
@def hascode = true
@def date = Date(2023, 8, 4)

&#8287;
&#8287;

**[\col{black}{cd ..}](/)**

**\alignright{ {{date}} }**

# {{title}}

I wanted to investigate a seasonal pattern in my country's stock market that I've heard rumors of. Supposedly, when a quarter's about to end, funds managers and company owners want to show good performance in their holdings, so the stocks get played around by "dealers" to go up.

It's worth noting that in Indonesia, the popular approaches to equity are fundamental or technical approaches, or the "Bandarmologi" approach (translated literally as "dealerology", it's part behavioral finance, part IDing market actors, part dubious stuff that might be banned in other countries). Quantitative approaches on the other hand, not so much.

One consequence of this is different explanations for the same phenomenon: where one practitioner sees dealers in price movement, another might see genuine if temporary demand increase (this is also my position).

Back to the topic, I pulled IDX Composite index prices from 2010 to now, and checked close-to-close returns on the last business day of each quarter. I picked this because it's more actionable than daily returns (only luck gets you filled on the day's open).

From 2010 to 2019, there is a __77.5%__ chance you get a successful trade with an average return of __0.5%__. But from 2020 to Q2 2023, the odds are only __43%__ with __0.16%__ average return. Why the changes after 2019? Besides COVID dragging prices down in 2020, my best guess for the subsequent years is [the recent increase in retail money entering the market](https://www.cnbcindonesia.com/market/20220114152218-17-307432/investor-ritel-memang-naik-tapi-yang-aneh-aneh-makin-banyak), which would obfuscate the fund managers' effect.