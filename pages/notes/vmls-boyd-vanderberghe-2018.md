@def title = "Vectors, Matrices, Least Squares by Boyd, Vanderberghe (2018)"
@def hasmath = true
@def hascode = true

&#8287;
&#8287;

**[\col{black}{cd ..}](/)**

**\alignright{ Book Notes }**

# {{title}}

~~~
<div class="img-og">
    <img src="/assets/notes/vmls-boyd-vanderberghe-2018.jpg" style="width:55%;">
</div>
~~~

_Python & Julia notebooks are available [here](https://github.com/vbartle/VMLS-Companions)_

---
### ~~~<span style="background-color: #E9F3F7">Part I : Vectors</span>~~~
---

### ~~~<span style="background-color: #E9F3F7">1. Vectors</span>~~~

- A vector is an ordered, finite list of numbers.
  - In coding, it is usually represented by arrays or lists (and not tuples).
- Vector notations can wildly differ among authors, so caution is advised.
- Some notations don’t distinguish between a 1-vector and scalars (numbers). In coding, they’re in different data structures.
- There’s vectors like zero, unit, one, sparse vectors.
- Adding/subtracting vectors is different from stacking their contents.
- The **inner product** (or **dot product**) of n-vectors $x$ and $y$ is written as $x^Ty$
- _Sparse vectors_ reduce computation time; both Python and Julia have them as dedicated data structures.

---

### ~~~<span style="background-color: #E9F3F7">2. Linear Functions</span>~~~

- Functions that take in vectors are simply written as $f(x)$ with $x$ as an n-vector.
- Example: inner product function $f(x) = a^Tx$
  - Can be seen as a weighted sum of elements of $x$
- A **linear function** $f(x)$ is when:
  - $f(ax) = af(x)$  for scalar $a$ and n-vector $x$
  - $f(x+y) = f(x) + f(y)$ for n-vectors $x$ and  $y$
- Example: _mean_() is a linear function, _max_() is not, _median_() is not.
- A differentiable function (doesn't need to be linear) can be approached by a linear function with Taylor approximation.
- Regression can be written with vectors as $f(x) = x^T\beta + v$  (an affine function)

---

### ~~~<span style="background-color: #E9F3F7">3. Norm and Distance</span>~~~

- The (Euclidean) _**norm**_ of an n-vector $x$ is  $||x|| = \sqrt{x_{1}^2+x_{2}^2+...+x_{n}^2}$
  - Also written as  $||x|| = \sqrt{x^Tx}$
  - **_Norm_ is more general than “length”.**
- The triangle inequality for _norms_:  $||x+y|| \leq ||x|| + ||y||$
- The RMS of a vector can be calculated by its norm:  $rms(x) = \frac{||x||}{\sqrt{n}}$
- Chebyshev’s inequality states that the number of entries of an n-vector $x$ with absolute value $\geq a$ is no more than $\frac{||x||^2}{a^2}$ 
  - Chebyshev’s inequality (stats version): the percentage of entries of an n-vector $x-\mu$ with absolute value $\geq k\sigma$ is no more than $\frac{1}{n}\frac{||x-\mu||^2}{(k\sigma)^2} = \frac{1}{k^2}$ 
- The (Euclidean) **distance** of two vectors $x$ and $y$ is $dist(x) = ||x-y||$
- **Average, RMS, and standard deviation**:  $rms(x)^2 = avg(x)^2 + std(x)^2$
- We can standardize a vector by subtracting its $avg()$ and dividing by $std()$, these are called z-scores.
- The angle between two vectors $x$ and $y$ is  $\theta = arccos(\frac{a^Tb}{||a||\,       ||b||})$
- The **correlation coefficient** between two vectors $x$ and $y$ is $\rho = \frac{(x-avg(x))^T(y-avg(y))}{||x-avg(x)||\,||y-avg(y)||}$

---

### ~~~<span style="background-color: #E9F3F7">4. Clustering</span>~~~

- **Clustering outside of simple cases:**
  - In almost all applications $n$ is larger than 2 (we can’t just scatterplot the values).
  - There will be some or even many points between clusters.
  - In real examples the best number of $k$ clusters will be less clear.
- Formalizing a clustering objective:
  - All vectors $x_i$ get clustered into clusters $c$ , where $c_{i}$ is the group where $x_i$ is assigned to.
  - With each cluster $c$ there is a *group representative* $z_{c_{i}}$ (doesn’t need to be one of $x_i$) which is close to each vectors $x_{i}$ in that group (small distance $||x_{i} - z_{c_{i}}||$ ).
  - $J^{clust}$ = **mean squared distance** of each vector to their group representative
- **Optimal clustering is minimizing objective** $J^{clust}$, but this is computationally impractical outside of small problems.
- $k$**_-means_ is suboptimal but finds very good clustering** (close to smallest $J^{clust}$)
  - Algorithm: given vectors $x_i$ and initial list of *group representatives* $z_{c_{i}}$ , repeat steps 1 & 2 until convergence
    1. Given $z_{c_{i}}$ , find best cluster assignments for each $x_i$
    2. For each cluster, set each group representative $z_{c_{i}}$ into mean of vectors in group
  - **The algorithm is a heuristic.** Different initial representatives can result in different clustering and final value of $J^{clust}$
  - The resulting representatives $z_1,…,z_k$ are quite interpretable. Example: if 4th part of vector is age, then $(z_3)_4$ = 37.8 tells us average age of group 3 is 37.8

---

### ~~~<span style="background-color: #E9F3F7">5. Linear Independence</span>~~~

- A collection of n-vectors $a_1,a_2,...,a_k$ is **linearly independent** if $\sum_{i=1}^{k}\beta_ia_i = 0$ only holds up for $\beta_1 = \beta_2 = ... = \beta_k = 0$.
- Like linear dependence, linear independence is an attribute of a _collection of vectors_, not individual vectors.
- **Independence-dimension inequality**: A linearly independent collection of n-vectors can have at most $n$ elements.
    - A collection of $n$ linearly independent n-vectors is called a **basis**.
- A collection of n-vectors $a_1,a_2,...,a_k$ is **orthonormal** if each vector pair is orthogonal ($a_i \perp a_j$ for $i \neq j$) and $||a_i|| = 1$
- **Gram-Schmidt algorithm** can be used to determine if a collection of vectors is linearly independent.
    - It finds the first vector $a_j$ that is a linear combination of previous vectors $a_1,…, a_{j-1}$
    - Step 1: _Orthogonalization_:  $\tilde{q_i} = a_i - (q^T_1 a_i)q_1 - … - (q^T_{i-1} a_i)q_{i-1}$
    - Step 2: _Test for linear dependence_:  if $\tilde{q_i} = 0$ , quit.
    - Step 3: _Normalization_: $q_i = \tilde{q_i}/||\tilde{q_i}||$

---
### ~~~<span style="background-color: #E9F3F7">Part II : Matrices</span>~~~
---
coming soon...

---
### ~~~<span style="background-color: #E9F3F7">Part III : Least Squares</span>~~~
