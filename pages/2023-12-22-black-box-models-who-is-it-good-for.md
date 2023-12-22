@def title = "Black Box Models: Who Is It Good For?"
@def hasmath = true
@def hascode = true
@def date = Date(2023, 10, 26)

&#8287;
&#8287;

**[\col{black}{cd ..}](/)**

**\alignright{ {{date}} }**

# {{title}}

Lately in data science there has been a demand for machine learning models like random forests, anything gradient boosted, neural networks, etc to be interpretable. Because the output of these models are not comprehensible to humans (compared to say, linear regression), methods like SHAP values, partial dependency plots, and so on rose in popularity so the results could be interpreted post-hoc.

Which got me thinking: if they aren't inherently interpretable, then how did these black box models get popular in the first place?

I think it's clear that interpretability is inherently desirable for anyone looking to solve real world tasks. So from the start, black box models have to compensate in other areas to compete with so called "white box" models like regression and decision trees.

The edge for black boxes can be the following:

1. It **can be more accurate** than white boxes. This is the most commonly cited reason for picking black boxes.
2. It **can take up less resources**. This applies when the white box models are simulations. Even neural networks can be the faster and more efficient option compared to it. [Recent developments in weather forecasting](https://www.ft.com/content/ca5d655f-d684-4dec-8daa-1c58b0674be1) are a good example of this.
3. It **can scale compared to manual methods**. This is especially relevant for machine learning in vision, audio, and NLP because every human i.e. everyone is the domain expert (in these fields, ML’s goal is to catch up to human accuracy). So a black box's edge here is doing like 5 guys’ work from one guy’s input.

Note for the above, when I say _can_, I do mean it, it's not like white boxes can't edge out black boxes in those areas.

## But We're Here for the Who

I had the outline for this article done and was in the middle of writing when a question popped up: "Where's the heart in this?" Because it seemed like there was a richer story that I was missing.

The answer I found for that was the people. This article started with asking when are black box models useful, but a more enticing question was: _what kind of person_ would find black box models useful?

At first glance, the edge for black box models I listed earlier seems to answer the question. Yet when a person tries to wield the model for those reasons, its lack of interpretability can be fatal:

1. For use cases like fraud detection & medical imaging, identifying why the results are what they are is as important as accuracy; it dictates the action taken afterwards (and given the stakes, interested parties can force this in the form of compliance requirements)
2. Compute-intensive simulations are necessary for furthering domain understanding. Black boxes are at best complements for an audience of average joes looking for applied use cases, but it can't replace the tools or knowledge of domain experts.
3. For non-tabular machine learning, it can be hard to justify replacing humans when we are the standard for performance. The reason to do so is usually unit economics, so black boxes don't have a definitive edge over white boxes here either.

Now, with interpretabiliy methods rising in popularity, you might think the above concerns will become moot and everyone will adopt them. But I want to focus on the moment before this: there was a long stretch of time when the data science community didn't saw fit to include interpretability methods as part of their basic toolkit, but did so with black box models. Why was that the case?

## Coda

The closest thing to an answer I've found is that:

1. Data science as a field just hasn't displayed the ability to account for itself. There's a short [blog post](https://dpananos.github.io/posts/2023-09-11-right/) from Demetri Pananos which you should read, where he laments that errors in data science don't fail the people who commit them, and that the profession as a whole might be a bullshit job.

2. This is downstream from the first one but is worth eking out as its own point: data science being not good at catching or even having a tangible conception of failure makes it very convenient as uh... useful idiot in tool form (if there's a word for this please let me know). This is where things take a more sinister turn. Earlier this year, WIRED and Lighthouse Reports published [an investigation](https://www.wired.com/story/welfare-state-algorithms/) into Rotterdam's welfare algorithm which was built by consulting firm Accenture and was intended to catch fraud. What they found wasn't pretty. The algorithm discriminates applicants based on ethnicity and gender, which is illegal when done directly, but using those traits as part of a model is a legal gray area. Where does interpretability fit into this? Well, most governments wouldn't give access for third party scrutiny. And that's before trying to interpret the model's results (Rotterdam's algorithm used random forest). This is where the term 'black box' we've been using needs to be expanded. An inherently uninterpretable model is a black box, but so is an interpretable model that's kept under lock and key. It didn't matter if Accenture used linear regression when relevant parties can't access the model to interpret it. Rotterdam allowed the investigation team to examine their algorithm & data. What happens behind the doors of those who didn't?

So, black box models... it's good for, at best: "consumers". I could use the phrase "users of the model" but that doesn't capture how little interest this group has in the workings of the model. At worst? it's for people too ignorant or dumb to notice, or people who make shit up, or people in power who don't want to explain themselves.
