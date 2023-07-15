@def title = "A Short Cautionary Tale When Backtesting Strategies"
@def hasmath = true
@def hascode = true
@def date = Date(2023, 7, 15)

&#8287;
&#8287;

**[\col{black}{cd ..}](/)**

\alignright{ {{date}} }

## {{title}}

back then, someone on Twitter shared a backtest on using 200-day moving averages (200MA) as a buy/sell signal for the S&P500 compared to simply buying and holding it.

~~~
<img src="/assets/backtesting-tale/robertotalamas_backtest.png">
<img src="/assets/backtesting-tale/robertotalamas_backtest_chart.png">
<img src="/assets/backtesting-tale/robertotalamas_backtest_code.png">
<div style="text-align: center;">
    <a href="https://twitter.com/RobertoTalamas/status/1598353728922329089" target="_blank" style="color:grey;">
        https://twitter.com/RobertoTalamas/status/1598353728922329089
    </a>
</div>
~~~

looks really good! but a while later, macrocephalopod (a popular account on the quant side
of twitter, or fintwit for short) quote-tweeted it.

~~~
<img src="/assets/backtesting-tale/macrocephalopod_quote.png">
<div style="text-align: center;">
    <a href="https://twitter.com/macrocephalopod/status/1598573871271235586" target="_blank" style="color:grey;">
        https://twitter.com/macrocephalopod/status/1598573871271235586
    </a>
</div>
~~~

so what went wrong?

## backtesting (properly) is hard

doing data analysis/data mining/statistical inference with market data can seem frictionless. 
you pull the data, do whatever transforms or comparisons or charts you want, pattern found, edge discovered, model established, and boom: you got a research paper or a empirically tested strategy ready for live trading.

but the process belies how little of the overall market dynamic that data is capturing, and that lack of friction means it's easy for subtle mistakes to creep in to your model.

credit where it's due for OP RobertoTalamas, sharing his code to the public is an admirable move, 
especially on twitter where cheap dunks are commonplace. and the octopus recognized it too:

~~~
<img src="/assets/backtesting-tale/macrocephalopod_reply.png">
<div style="text-align: center;">
    <a href="https://twitter.com/macrocephalopod/status/1598579432905637888" target="_blank" style="color:grey;">
        https://twitter.com/macrocephalopod/status/1598579432905637888
    </a>
</div>
~~~

this is actually relevant to our discussion: part of how to stave off these errors is a workflow that leads you to confront the assumptions behind your model of reality head on, rather than hand-waving it.

this involves feedback. in finance, more often than not this takes the form of "finding out" after "f**king around". it also helps to be surrounded by people who view you in good faith and are willing to give advice.

case in point:

~~~
<img src="/assets/backtesting-tale/jessicanutt96_reply.png">
<div style="text-align: center;">
    <a href="https://twitter.com/JessicaNutt96/status/1598583153198776320" target="_blank" style="color:grey;">
        https://twitter.com/JessicaNutt96/status/1598583153198776320
    </a>
</div>
~~~

## back to the code

so this is a common mistake in simulations: look-ahead bias.
it's when a model uses data that shouldn't be available at its time. for example, 
using earnings reports for a period when that data hasn't been reported (maybe not even determined yet) to the public.

in backtesting, this can inflate trading performance since the strategy uses info that other participants
in the simulation couldn't possibly have. or as a mutual jokingly described it: "my alpha is my time machine".

the code's mistake is on this line. for context, snp['S&P500'] contains closing prices for the S&P500.

~~~
<img src="/assets/backtesting-tale/robertotalamas_backtest_code_line.png"
    style="border-radius:0px;"
>
~~~

as anyone who's traded stocks will know, you can't trade using the day's closing price because... _the market's closed_.
this bleeds into not one, but two issues with the trade signal:
- on Day 1, we only get the day's 200MA after market close, so we have to wait until Day 2 to use it
- on Day 2, we have the 200MA, but our trade signal compares that to the closing price, so... we wait again until Day 2 closes to compare Day 1's 200MA with Day 2's closing price. but when do we trade?
- finally on Day 3, we can act on our trade signal.

yes, there is supposed to be a two day lag between signal generation and trade execution. 

it's one of the pitfalls of using close-to-close data. if we want to backtest a trade signal that's actionable on the same day,
we'd need more granular data than daily prices. sourcing that may cost money, and it's harder to process, 
but yahoo finance's intraday price data is unreliable, so it's for you decide whether the cost and operational toll is worth it.