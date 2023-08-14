@def title = "Notes on Causal Graphs (for the DAGless)"
@def hasmath = true
@def hascode = true
@def date = Date(2023, 8, 4)

&#8287;
&#8287;

__**[\col{black}{cd ..}](/)**__

**\alignright{ {{date}} }**

# {{title}}

The following consists of my notes on understanding causal graphs, presented in a way nearly devoid of statistics. My experience with them so far has led me to write in this manner, because:

1. Causal graphs are not formed by statistics but by domain knowledge, and
2. Despite this, somehow the literature on causal inference I've come across express these graphs with the language of probabilities.

So without further ado:

\toc

## DAG Notation

It is very intuitive for people to depict causality using graphs. The specific type commonly used for causal inference are called __DAGs__ (Directed Acyclic Graph). 

In it, __nodes__ represent random values of the variables we're interested in, and __arrows__ represent causal effect between two variables in the arrow's direction. 

By using DAGs, we presume several ideas about the nature of what we're graphing:

1. Causality runs in one direction (forward in time). There are no two-way arrows or cycles in a DAG.
2. The arrows in a DAG indicate _presence_ of causal pathways between the nodes.
3. A lack of arrows indicate _absence_ of causal pathways between the nodes.

~~~
<div class="img-small">
    <img src="/assets/DAGs-for-DAGless/1.png">
</div>
<div style="text-align: center; font-size: 0.85em;">
    <snap style="color:grey;">
        A simple DAG for "X causes Y"
    </snap>
</div>
~~~

## Causal Effect & Mediator

Causal effects happen in two ways: they are either direct, or mediated by another node. In the latter case, the middle node can be called a _mediator_.

~~~
<div class="img-small">
    <img src="/assets/DAGs-for-DAGless/2.png">
</div>
<div style="text-align: center; font-size: 0.85em;">
    <snap style="color:grey;">
        Here, M is a mediator between X and Y
    </snap>
</div>
~~~

In this DAG, while X directly causes M, it doesn't directly cause Y; the lack of an arrow between X and Y makes it so that X only causes Y via M.

## Confounding

When a node has causal pathways towards  several nodes, that node is called a _confounder_.

~~~
<div class="img-small">
    <img src="/assets/DAGs-for-DAGless/3.png">
</div>
<div style="text-align: center;">
    <snap style="color:grey; font-size: 0.85em;">
        Here, Z is a confounder to X and Y
    </snap>
</div>
~~~

In this DAG, comparing X to Y is confounded by Z which affects both of them.

Confounders are bedeviling creatures, sometimes existing despite not being observed. If so, this can be reflected in the graph by using dashed arrows.

~~~
<div class="img-small">
    <img src="/assets/DAGs-for-DAGless/4.png">
</div>
<div style="text-align: center;">
    <snap style="color:grey; font-size: 0.85em;">
        This Z is an unobserved confounder to X and Y
    </snap>
</div>
~~~

## Colliders

_Colliders_ are nodes that receive causal pathways from several nodes.

~~~
<div class="img-small">
    <img src="/assets/DAGs-for-DAGless/5.png">
</div>
<div style="text-align: center;">
    <snap style="color:grey; font-size: 0.85em;">
        Both X and Y affect the collider C
    </snap>
</div>
~~~

## Conditioning/Controlling

To _condition_ or _control_ a variable is to lock their values in place, while letting the other variables vary.

## Getting Correlation to be a Sign of Causation

The point of a DAG is to clarify relationships between variables we're interested in, in a way that (and this is where statistics comes into play) lets us infer variations as result of causal effect.

