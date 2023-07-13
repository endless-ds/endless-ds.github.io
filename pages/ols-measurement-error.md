@def title = "How Measurement Error Affects OLS"
@def hasmath = true
@def hascode = true
@def date = Date(2023, 7, 13)

&#8287;
&#8287;

**[\col{black}{cd ..}](/)**

\alignright{ {{date}} }

## {{title}}

this is another data science question I saw on twitter:

~~~
<div class="img-small">
    <img src="/assets/ols-measurement-error/ryxcommar_ols_q.png">
</div>
<div style="text-align: center;">
    <a href="https://twitter.com/ryxcommar/status/1551262675342045184" target="_blank" style="color:grey;">
        https://twitter.com/ryxcommar/status/1551262675342045184 (account privated as of writing)
    </a>
</div>
~~~

with some corrections:
~~~
<div class="img-small">
    <img src="/assets/ols-measurement-error/ryxcommar_q_correction_1.png">
</div>
~~~
&#8287;
~~~
<div class="img-small">
    <img src="/assets/ols-measurement-error/ryxcommar_q_correction_2.png">
</div>
~~~

basically we're trying to answer how $\alpha$, $\beta$, etc changes if errors are added to the $y$ values.

note that ryxcommar's notation for normal distribution is $N(\mu,\sigma)$ instead of $N(\mu,\sigma^2)$. we'll be using this for the answer.

so $y^* = \alpha + \beta x + \epsilon + u$ where $u$ is measurement error distributed $N(2,2)$

since $x$ isn't affected by the measurement error, $\beta$ is also unaffected.

which means $u$ only affects $\alpha$ & $\epsilon$.

OLS residuals always have mean $0$, because the constant is carried over to the $\alpha$ term. so $\alpha^* = \alpha + 2$. and $\epsilon^* \sim N(0,1) + N(0,2) \sim N(0,\sqrt{5}) + cov(e,u)$. this is why the second correction is nice to have, so $\epsilon \sim N(0,\sqrt{5})$

in conclusion:
- $\alpha^* = \alpha + 2$
- $\beta^* = \beta$
- $\mu^* = \mu = 0$
- $\sigma^* = \sqrt{\sigma + 2^2}$