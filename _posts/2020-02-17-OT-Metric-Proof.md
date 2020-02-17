---
layout: post
title: The Wasserstein Metric is, in fact, a Metric
date:   2020-02-17 12:00:00 +1100
---
<!--more-->

## Post Overview:
In this shorter post, we'll prove that that $W_p$ is indeed a metric on $\mathcal{P}(\Omega)$. This is a result that I referenced in my previous post in a rather hand-wavey fashion, and I feel like the proof is accessible enough for me to walk through it in this post. The goal of this post is to help me develop a better understanding of the Wasserstein metric and its properties, as it is foundational to the study of OT.

___
### Background and Motivation:
The theorem in question essentially states that the $p$-Wasserstein metric is a metric under certain conditions. That is, it satisfies the properties of non-negativity and reflexivity, as well as the triangle inequality. This theorem was originally proven by Cedric Villani in his 2003 book entitled ["Topics in Optimal Transport"](https://bookstore.ams.org/gsm-58) [Theorem 7.3].

Here is our set-up: let $\Omega$ be a polish space endowed with a metric $D$, and let $p \in \mathbb{R}^+$. Then, define the cost function $c$ as such: $c(x,y) := D(x,y)^p$ and let $$ \mathcal{T}_p(\mu, \nu) $$ be the cost of the optimal tranport plan of moving $\mu$ to $\nu$ on $\Omega$ (it is known that such a plan must exist on a Polish space, but we will not prove that here). We then have that $W_p = \mathcal{T}_p^{1/p}$, and recall that $$ W_p(\mu, \nu) := \Big(\inf_{P \in \Pi(\mu, \nu)}{\int_{\Omega \times \Omega}{c(x,y)dP(x,y)}}\Big)^{1/p} $$. Let $\mathcal{P}_p(\Omega)$ be the set of all probability measures on $\Omega$ with finite $p$-th moments. We can now state the theorem formally. 

___
### Theorem and Proof
__Theorem__: _For every $p \geq 1$, $W_p = \mathcal{T}_p$ defines a metric on $\mathcal{P}_p(\Omega)$. i.e.,_

1. $W_p \geq 0$
2. $W_p(\mu, \nu) = 0$ _iff_ $\mu = \nu$
3. $\forall (\mu, \nu, \omega) \in \mathcal{P}_p(\Omega)$, $W_p(\mu, \omega) \leq W_p(\mu, \nu) + W_p(\nu, \omega)$.


_Proof:_ 
1. First, we note that $W_p$ is trivially non-negative because $D$ is a metric on $\Omega$ and the infimum of the integral of the product of $D$ with any finite probability measure $P$ must also be non-negative.
2. Becase the cost $c$ of pushing any measure $\mu$ onto itself is $0$, it must be the case that $W_p(\mu, \mu) = 0$. Now, for $\mu, \nu \in \mathcal{P}(\Omega)$, asuume that $W_p(\mu, \nu) = 0$. Then, let $\pi$ be a plan of optimal transport from $\mu$ to $\nu$ (again, it is known that such a plan must exist, but the proof is omitted here). That is, $\int_{\Omega \times \Omega}{c(x,y)d\pi(x,y)} = 0$, which implies that $\pi$ is supported on the diagonal $\Delta := \{ (x, y) \in \Omega \times \Omega\ \mid x = y \}$. Then, for any continuous function $\phi$ defined on $\Omega$, we have the following:  

    $$ \int{\phi d\mu} = \int{\phi(x) d\pi} = \int{\phi(y) d\pi} = \int{\phi d\nu}$$  

    This implies that $\mu = \nu$, so we have proven that $W_p(\mu, \nu) = 0 \text{ iff } \mu = \nu$.
3. Now we must prove the triangle inequality. To do so, we must use the Gluing Lemma, which will allows us to "glue" together two transport plans that share a common marginal. (Quick terminology note: $\pi \in \Pi(\mu, \nu)$ means that $\mu$ is the first marginal of $\pi$ and $\nu$ is the second). Here is the statement of the lemma:   

    __The Gluing Lemma__: _Let $\mu_1, \mu_2, \mu_3$ be probability measures supported in Polish spaces $\Omega_1, \Omega_2, \Omega_3$, respectively, and let $$\pi_{12} \in \Pi(\mu_1, \mu_2)$$ and $$\pi_{23} \in \Pi(\mu_2, \mu_3)$$ be two transport plans. Then, there exists a probability measure $\pi \in \Pi(\Omega_1 \times \Omega_2 \times \Omega_3)$ with marginals $$\pi_{12}$$ on $$\Omega_1 \times \Omega_2$$ and $$\pi_{23}$$ on $$\Omega_2 \times \Omega_3$$.

With this lemma in hand, ...

### Sources:
- https://www.math.u-psud.fr/~filippo/Wp.pdf
- https://people.math.gatech.edu/~gangbo/Cedric-Villani.pdf