---
title: Metropolis Sampler Demo
math: true
---

# The Ole' Metropolis Sampler

Its a tale as old as time. A bayesian statistician wants to estimate the posterior distribution of some model (s)he's planning to fit to data, how do they do it?
Thankfully there are all manner of ways to sample from the posterior distribution ranging from the most convenient - analytically tractible posterior distributions - to the 
slightly less convenient - [reversible jump](https://en.wikipedia.org/wiki/Reversible-jump_Markov_chain_Monte_Carlo) [random partition](https://arxiv.org/abs/1506.04696) [expectation propagated](https://en.wikipedia.org/wiki/Expectation_propagation) [Hamiltonian Markov Chain](https://en.wikipedia.org/wiki/Hamiltonian_Monte_Carlo) fanciness. 

Among the simpler, yet still very useful, methods lies the Metropolis sampler.

