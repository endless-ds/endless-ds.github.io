@def title = "Advanced Portfolio Management by Giuseppe Paleologo (2021)"
@def hasmath = true
@def hascode = true

&#8287;
&#8287;

**[\col{black}{cd ..}](/)**

# {{title}}

~~~
<div class="img-og">
    <img src="/assets/notes/adv-portfolio-mgmt-paleologo-2021.jpg" style="width:55%;">
</div>
~~~

---

### ~~~<span style="background-color: #E9F3F7">1. For Whom? Why? And How?</span>~~~

- This book is for people at the intersection of (equity) fundamental analysis & quantitative research.
- **Good trading ideas are useless without a portfolio that survives adversity.**
- Readers who don’t have access to risk models can still get a lot out of this book.
  - Managers with _**effective heuristics**_ can be successful without checking their factor risk decomposition every minute.

---

### ~~~<span style="background-color: #E9F3F7">2. The Problem: From Ideas to Profit</span>~~~

- **There is no master theory (yet) of portfolio management.**
- Simulations & historical tests should be looked at for limit-testing, but not for confirmation.
- The problem (or steps) dealt in each chapter:
  - **All valuations are relative**, but to what? (ex. a stock vs its environment) _(ch. 3,4,5)_
  - **Sizing position** for your investment: is conviction the only factor? how do other assets in the portfolio affect this size? _(ch. 6)_
  - **A strategy’s performance**: stock selection, position sizing, and timing skills. How to quantify and improve upon them? _(ch. 8)_
  - **Transaction costs** when picking trade opportunities _(sec. 8.2.1, 8.3)_
  - Determine **rules for risk management** that allow various trading ideas while controlling risk _(ch.7)_
  - Survival is based on avoiding your capital’s critical limit (often via **stop-loss policies**) _(ch.9)_
  - How to decide **leverage** (for managers who are also fund owners) _(ch. 10)_
  - Analyze **alternative data** _(sec. 8.4)_

---

### ~~~<span style="background-color: #E9F3F7">3. A Tour of Risk and Performance</span>~~~

- A stock index provides a _benchmark_ to compare one’s investment, being a summary of the market (or specific sector).
  - Factor models make them rigorous and extend them to allow decomposition.
- A stock’s return can be written with the linear regression $r = \alpha + \beta \times m + \varepsilon$
  - $r$ is stock return, $\alpha$ is alpha (intercept), $\beta$ is beta (slope), $m$ is market return, $\varepsilon$ is noise (idiosyncratic or specific or residual return)
  - **The term $\alpha + \varepsilon$ is only dependent on the company being examined.**
  - For expected returns, the equation becomes (_expected return_) = (_alpha_) + (_beta_) × (_expected market return_)
- **Estimates of $\alpha$ tend to be highly variable** (and often the error is bigger than the estimate itself), unlike estimates of $\beta$ which are relatively stable.
