---
date: 2019-12-13
title: "The Curious Case of the Collapsing Concentration Parameter: Part III"
summary: "The mysteries multiply as we look through the literature but some answers are still forthcoming."
tags: ["Dirichlet Process","Bayesian NonParametrics"]
author: "Adam Peterson"
markup: mmark
image:
  placement: 1
  caption: ""
  focal_point: "Center"
  preview_only: false
---


In the Curious Case of the Collapsing Concentration Parameter: Parts I and II we learned about the Dirichlet Process(DP), a cool
tool for clustering data, and an odd phenomena that occurs whenever you have a model that easily captures the data. Specifically,
we saw that the concentration parameter $\alpha$ collapses at zero under specific conditions and what that means in terms of
the model's parametric interpretation. In this post we'll return to the history of the DP, looking at its original construction,
the key developments and patterns of use that have been made along the way and attempt to close this series with some thoughtful reflection from 
everything we've learned.


## The DP's Start

The Dirichlet Process was first introduced, as we discussed during part I, in a 1973 paper by Thompson S. Ferguson. In this original paper,
Ferguson did not even use the parameterization with the concentration parameter that we have been using and that is most commonplace today. 
Instead, he implicitly set this value to one and instead denoted $\alpha$ as the base measure. Here's the full original quote from the paper:

> Let $\mathcal{X}$ be a space and $\mathcal{A}$ be a $\sigma$-field of subsets, and let $\alpha$ be a finite non-null measure on ($\mathcal{X},\mathcal{A})$.
> Then a stochastic process P indexed by elements $A$ of $\mathcal{A}$, is said to be a Dirichlet Process on $(\mathcal{X},\mathcal{A})$ with parameter $\alpha$
> if for any measurable partition ($A_1,...,A_k$) of $\mathcal{X}$, the random vector $(P(A_1),...,P(A_k))$ has a Dirichlet Distribution with parameter $(\alpha(A_1),...,\alpha(A_k))$.

Furthermore, we can see later in Ferguson's development that he specifically wants to allow the parameters of the Dirichlet **Distribution**, not the process, (confusingly, these are also usually denoted as a vector parameter, $\alpha_1,...,\alpha_k$)
to be zero. Quoting from Section 2 of Ferguson's paper:

> The Dirichlet Distribution. The discussion of this section is well known but our definition of the Dirichlet distribution is slightly more general than the usual one...
> We define the Dirichlet distribution slightly more generally than in Wilks[11], by allowing some of the variables to be degenerate at zero...
> Use of the notation $\mathcal{D}(\alpha_{1},...,\alpha_{k})$ is taken to imply that $\alpha_{j} \geq 0 \forall j$ and $\alpha_{j} >0$ for some $j$.[^1]

Again this doesn't mean that $\alpha=0$  *a priori* is okay, as it will still result in a degenerate distribution. However, it seems that 
Ferguson is explicitly allowing these values to be zero in the posterior, as long as some of the weights $\pi_{l}$ from  estimation are non-zero, as they were in our simulation.

While Ferguson's paper doesn't even mention the concentration parameter as its own entity, let alone estimating it, we still learned some worthwhile tidbits in its pages. 
To learn more about the concentration parameter specificaclly, we'll now travel forward in time about 30 years, to discuss two papers by Ishwaran and 
James. 


## The DP's $\alpha$ Update


While Ferguson would eventually introduce the concentration parameter as we know it in a later [paper](https://www.sciencedirect.com/science/article/pii/B9780125893206500186), our journey is 
going to fast forward to a 2000 [article](https://academic.oup.com/biomet/article/87/2/371/221380) by Ishwaran and Zarepour, where the method[^2] of updating $\alpha$ is introduced.
In this paper, we find the authors discussing some interesting numerical issues:

> Selecting an appropriate prior for $\alpha$ is critical to the model's performance, since the value for $\alpha$ is directly related to the number of distinct $Y_i$ values. 
> We use a Gamma($\nu_1,\nu_2)$ prior, which has been used by Escobar & West (1995) in density estimation problems involving the Dirichlet process. 
> A gamma prior is appropriate because of its flexibility. For example, to discourage small and large values for $\alpha$ we choose large values for both $\nu_1$ and $\nu_2$. 

This is an interesting sentence because (1) it shows that someone else has encountered some issues with $\alpha$ and (2)  the author argues for setting $\alpha$'s' prior on the basis of computational motivation rather than substantive or 
"subject-matter" grounds. This is not something that statisticians are usually comfortable with[^3]. Their concern with computation is further underscored by their recognition of numerical problems in the Discussion:

> With a large value of $N$ (the number of DP truncated components), it can sometimes happen that a few $p_{k}$ values become extremely small, and this can lead to serious numerical problems when running the Metropolis step;... 
> Small $p_{k}$ values are still an issue in evaluating the conditional distributions (3) and (31) (refer to equations in the text) for $\alpha$ in the DP($\alpha H$) and $\mathcal{B}(\alpha,1,H)$ processes.
> However, there is a simple way to increase the numerical stability if we remember that the current value for $p$ is sampled from a generalised Dirichlet Distribution. Since the value of $p$ is constructed in terms of 
> $V_{k}$ beta random variables in (25) it means that we can re-express the conditional distribution for $\alpha$ in terms of $V_{k}$ ...[^4].

The authors then add the same equation we have in part II, for sampling updates from the posterior distribution of $\alpha$. So, not a great help to us in our present computational predicament, but it does
give us more information on why $\alpha|- \to 0$ and some previous attempts to address it. 

We now turn to two last papers that use the Dirichlet Process in published papers, in order to see how they handle the same concentration parameter problems we have, so we can learn from them by example.


## Simulated and Real: The DP's Current Use

Fast forwarding even closer to the present, we'll look at two papers that use the Dirichlet Process in their extension work. Specifically, we'll look at the [Nested Dirichlet Process](https://amstat.tandfonline.com/doi/abs/10.1198/016214508000000553)
by Rodriguez et al. and [Clustering Distributions with the Marginalized Nested Dirichlet Process](https://onlinelibrary.wiley.com/doi/abs/10.1111/biom.12778) by Zuanetti et al.
Both of these are chosen mainly for convenience, since I happened to run into them in the course of my research and because they both show an interesting use of the concentration parameter and the concentration parameter prior in their work[^5].


We'll skip over the novelty of their new extension, since we're mainly interested in what they're doing with the concentration parameters in the DP. These two particular papers 
each look at a DP that uses another DP as its base measure, so there are two concentration parameters to consider, $\alpha$ and $\beta$. In the first paper, Rodriguez et al.
have the following setting for their concentration parameters in the simulations:

> The precision parameters $\alpha$ and $\beta$ were both fixed to 1 ....

Similarly in the Marginalized Nested Dirichlet Process paper: 

> The total mass parameters $\alpha$ and $\beta$ are both fixed to 1.

If we look at the data analysis in each paper, we find that Rodriguez et al.  uses informative priors, as Ishwaran and Zarepour discussed, while Zuanetti keeps $\alpha=\beta =1$:

> Finally, we set $\alpha,\beta \sim \text{G}(3,3)$ a priori, implying that $E[\alpha] = E[\beta] = 1$ ( a common choice in the literature) and $P(\alpha >3) = P(\beta >3) \approx 0.006$ - Rodriguez et al.


I don't know about you, but all of this reading left me with a lot of questions. For example, in the Zuanetti et al. paper, they discuss how sampling for $\alpha$ and $\beta$ can be implemented for their model, but they don't do it themselves,
so they leave their concentration parameters fixed at 1. In the Rodriguez et al. paper, they set a fairly informative prior on $\alpha$, $\beta$, in their 
data application without any justification beyond saying that the mean is a common choice in the literature. After working through the DP as we have and seeing the tendency of $\alpha$ to collapse, I can't help but wonder if 
the authors here assign $\alpha, \beta$ an informative prior, or simply keep it fixed, in order to "sweep the numerical issue" under the table so they don't have to explain it. I'm also surprised that reviewers did not ask them
to justify the use of these priors in either substantive or computational terms. 

I'm obviously a bit perplexed, but other readers may think that this isn't unreasonable. I'll leave you to draw your own conclusions. 
For now, I think it's time we take a step back, think about what we learned to take away from all of this.


## Lessons Learned in the Process of Learning about the Dirichlet Process

In this post we delved through several different articles in the DP literature that described the initial construction of the DP and how it uses a non-traditional 
Dirichlet Distribution, concerns with the numerical process of updating $\alpha$ and, finally, the manner in which $\alpha$ is currently used or updated in the literature.
We found that, ever since an inference producedure for $\alpha$ was implemented, there have been numerical concerns about $\alpha$, though it is not clear, to me at least,
that these issues neccessarily result in invalid model inference. Further, it seems plausible that authors in this field try to work their way around these issues either by
restricting the concentration parameters to be fixed, or by setting informative priors. I don't think either of these approaches are "bad", as the model typically performs
well in any of these settings, at least when there is a sufficient sample size.  However, I do think that everything we've discovered thus far does merit some new work on the Dirichlet Process' theoretical construction and what role
the concentration parameter plays in its' behavior.

Regarldess of what work may remain to be done, I thank you for joinging me on this journey.
I hope, dear reader, that you've enjoyed this expedition into the dark nether realms of statistical research in Bayesian NonParametrics and that you've 
learned something about the Dirichlet Process, the "process" of research itself and all the mysteries you can find diving down a rabbit hole in search for a collapsed concentration parameter


[^1]: In the quote, the $\alpha$s mentioned are now scalar variables defined on $[0,\infty)$, rather than the non-null finite measure.
[^2]: Are there other ways of updating $\alpha$? Yes! In fact there are, though this method requires an entirely different sampler that's been shown to be less efficient (both statistically and computationally). See [Escobar and West (1995)](https://www.tandfonline.com/doi/abs/10.1080/01621459.1995.10476550) for more.
[^3]: See the first chapter of Bayesian Data Analysis by Gelman et al. for a discussion of priors.
[^4]: The non numerical parentheses are mine, added to clarify things.
[^5]: If you, dear reader, come across an article that shows a similar or different setting of the concentration parameter, I would be interested to hear it.
