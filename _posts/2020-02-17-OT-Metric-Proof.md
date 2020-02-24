---
layout: post
title: The Wasserstein Metric is, in fact, a Metric
date:   2020-02-17 12:00:00 +1100
icon: /post_assets/2020-02-17/icon.png
---
<!--more-->

## Post Overview:
In this shorter post, we'll prove that that $W_p$ is indeed a metric on $\mathcal{P}(\Omega)$. This is a result that I referenced in my previous post in a rather hand-wavey fashion, and I feel like the proof is accessible enough for me to walk through it in this post. The goal of this post is to help me develop a better understanding of the Wasserstein metric and its properties, as it is foundational to the study of OT.

___
### Background and Motivation:
The theorem in question essentially states that the $p$-Wasserstein metric is a metric under certain conditions. That is, it satisfies the properties of non-negativity and reflexivity, as well as the triangle inequality. This theorem was originally proven by Cedric Villani in his 2003 book entitled ["Topics in Optimal Transport"](https://bookstore.ams.org/gsm-58) [Theorem 7.3]. Fun fact, Villani (Fields Medalist in 2010) almost ran for mayor in Paris this year.

Here is our set-up: let $\Omega$ be a [Polish space](https://en.wikipedia.org/wiki/Polish_space) endowed with a metric $D$, and let $p \in \mathbb{R}^+$. Then, let $$ \mathcal{T}_p(\mu, \nu) $$ be the cost of the optimal tranport plan of moving $\mu$ to $\nu$ on $\Omega$ (it is known that such a plan must exist on a Polish space, but we will not prove that here). We then have that $W_p = \mathcal{T}_p^{1/p}$, and recall that $$ W_p(\mu, \nu) := \Big(\inf_{P \in \Pi(\mu, \nu)}{\int_{\Omega \times \Omega}{D(x,y)^{p}dP(x,y)}}\Big)^{1/p} $$. Let $\mathcal{P}_p(\Omega)$ be the set of all probability measures on $\Omega$ with finite $p$-th moments. We can now state the theorem formally. 

___
### Theorem and Proof
__Theorem__: _For every $p \geq 1$, $W_p = \mathcal{T}_p^{1/p}$ defines a metric on $\mathcal{P}_p(\Omega)$. i.e.,_

1. $W_p \geq 0$
2. $W_p(\mu, \nu) = 0$ _iff_ $\mu = \nu$
3. For all $(\mu_1, \mu_2, \mu_3) \in \mathcal{P}_p(\Omega)$, $W_p(\mu_1, \mu_3) \leq W_p(\mu_1, \mu_2) + W_p(\mu_2, \mu_3)$.


_Proof:_ 
1. First, we note that $W_p$ is trivially non-negative because $D$ is a metric on $\Omega$ and the infimum of the integral of the product of $D$ with any finite probability measure $P$ must also be non-negative.
2. Becase the cost $c$ of pushing any measure $\mu$ onto itself is $0$, it must be the case that $W_p(\mu, \mu) = 0$. Now, for $\mu, \nu \in \mathcal{P}(\Omega)$, asuume that $W_p(\mu, \nu) = 0$. Then, let $\pi$ be a plan of optimal transport from $\mu$ to $\nu$ (again, it is known that such a plan must exist, but the proof is omitted here). That is, $\int_{\Omega \times \Omega}{Dx,y)^{p}d\pi(x,y)} = 0$, which implies that $\pi$ is supported on the diagonal $\Delta := \\{ (x, y) \in \Omega \times \Omega\ \mid x = y \\}$. Then, for any continuous function $\phi$ defined on $\Omega$, we have the following:

    $$\int{\phi d\mu} = \int{\phi(x) d\pi} = \int{\phi(y) d\pi} = \int{\phi d\nu}$$  

    This implies that $\mu = \nu$, so we have shown that $W_p(\mu, \nu) = 0 \text{ iff } \mu = \nu$.
3. Now we must prove the triangle inequality. To do so, we must use the Gluing Lemma, which will allows us to "glue" together two transport plans that share a common marginal. (Quick terminology note: $\pi \in \Pi(\mu, \nu)$ means that $\mu$ is the first marginal of $\pi$ and $\nu$ is the second. The term "marginal" refers to the destination of a pushed-forward probability measure). Here is the statement of the lemma:   

    __The Gluing Lemma__: _Let $\mu_1, \mu_2, \mu_3$ be probability measures supported in Polish spaces $\Omega_1, \Omega_2, \Omega_3$, respectively, and let $$\pi_{12} \in \Pi(\mu_1, \mu_2)$$ and $$\pi_{23} \in \Pi(\mu_2, \mu_3)$$ be two transport plans. Then, there exists a probability measure $\pi \in \Pi(\Omega_1 \times \Omega_2 \times \Omega_3)$ with marginals $$\pi_{12}$$ on $$\Omega_1 \times \Omega_2$$ and $$\pi_{23}$$ on $$\Omega_2 \times \Omega_3$$.

    I was first introduced to this lemma in a [topological setting](https://en.wikipedia.org/wiki/Pasting_lemma) with continuous functions, but its application here is pretty slick. This lemma essentially states the following: if we're given three probability measures in three spaces, as well an optimal plan to transport measure 1 to measure 2 and an optimal plan to transport measure 2 to measure 3, then we can "glue" our two plans together to obtain a new (not necessarily optimal) plan defined on the product of the three spaces with the marginals of the glued-together plans left intact.

    Now, let $$ \mu_1, \mu_2, \mu_3 \in \mathcal{P}_p(\Omega )$$, $\pi_{12}$ an optimal transport plan between $\mu_1$ and $\mu_2$, and $\pi_{23}$ an optimal transport plan between $\mu_2$ and $\mu_3$. For each $\mu_i$, let $\Omega_i$ denote the support of $\mu_i$. Define $\pi$ as it is defined in the Gluing Lemma, and let $\pi_{13}$ be the marginal of $\pi$ on $\Omega_1 \times \Omega_3$.
    Then, we obtain the following (excuse the image formatting, MathJax can't handle the align environment):


    <div class="img-container">
    <img src="/post_assets/2020-02-17/triangle_ineq_latex.png" style="height:500px">
    </div>

    Where the above equalities are obtained from the following facts and properties: $\pi_{13}$ is a transport plan on $\Omega_1 \times \Omega_3$ $$(*)$$, the marginal properties of measures $$(**)$$, the [Minkowski Inequality](https://en.wikipedia.org/wiki/Minkowski_inequality) of $L^p(\Omega^3, \pi)$ $$(***)$$, and $\pi_{12}$ and $\pi_{23}$ are optimal transport plans $$(****)$$. $\square$

___
### Afterthoughts:
This post ended up being a bit more abstract than I had originally intended, but I think that working to understand this proof has helped me to understand the most important aspects of the Wasserstein distance. This is also an interesting proof; the triangle inequality proof is really non-trivial and the use of the Gluing Lemma is clever. In future posts, I'll be pushing forward into new OT material and hopefully exploring some of the computational aspects of the Wasserstein distance.