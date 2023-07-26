@def title = "Paper Read - Improved Price Oracles: Constant Function Market Makers by Angeris and Chitra (2020)"
@def hasmath = true
@def hascode = true
@def date = Date(2023, 7, 15)

&#8287;
&#8287;

**[\col{black}{cd ..}](/)**

\alignright{ {{date}} }

## {{title}}

As I read more into quantitative finance & people within the space, it was inevitable that I'd come across crypto. Personally I'm on the [web3 is going just great](https://web3isgoinggreat.com/) and [Line Goes Up](https://www.youtube.com/watch?v=YQ_xWvX1n9g&ab_channel=FoldingIdeas) side of things, but this nifty little structure caught my interest research-wise.

### Background

So traditionally, "market-maker" meant actors that profit on the bid-ask spread in exchanges. But constant function market makers (CFMMs) are more comparable to order books which match orders among its participants. Basically, they're not actors on the exchange, they *are* the exchange.

A simple example of CFMM involves two assets, like in Uniswap. Users put coin $\alpha$ into reserve $R_{\alpha}$ and get coin $\beta$ from reserve $R_{\beta}$ (and vice versa). When generalized, it is possible to trade a basket of assets into the reserves for another basket of assets.



### Definition

CFMMs mathematically are defined by the trading function

$
\varphi(R,\Delta,\Lambda)
$

where $R$ = reserves, $\Delta$ = asset input, $\Lambda$ = asset output.

Trade is accepted only if the trading function has the same result as before the trade:

$
\varphi(R,\Delta,\Lambda) = \varphi(R,0,0)
$

i.e. it stays *constant*. Hence the name.

