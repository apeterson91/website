---
title: The Metropolis Sampler 
math: true
summary: A quick demo and backstory on the first MCMC method
---

# The Ole' Metropolis Sampler

Its a tale as old as time. A bayesian statistician wants to estimate the posterior distribution of some model (s)he's planning to fit to data, how do they do it?
Thankfully there are all manner of ways to sample from the posterior distribution ranging from the most convenient - analytically tractible posterior distributions - to the 
slightly less convenient - [reversible jump](https://en.wikipedia.org/wiki/Reversible-jump_Markov_chain_Monte_Carlo) [random partition](https://arxiv.org/abs/1506.04696) [expectation propagated](https://en.wikipedia.org/wiki/Expectation_propagation) [Hamiltonian Markov Chain](https://en.wikipedia.org/wiki/Hamiltonian_Monte_Carlo) fanciness. 

The very first to be developed among the  numerical sampling techniques was the Metropolis sampler. And while it is certainly simpler compared to the more 
complex methods that are under active development today, it nevertheless remains very useful. I hope to convince you, dear reader, as to why it is still useful to know the Metropolis Sampler and how to use it in this modern era of "Big Data".

To give some brief history, which I will unabashedly adapt from the  well curated [wikipedia article](https://en.wikipedia.org/wiki/Metropolis%E2%80%93Hastings_algorithm#History) on the subject,
Nicholas Metropolis was working at the famous Los Alamos National Laboratory when he was prompted by John von Neumann to develop a tractable model for thermonuclear reactions. What he and the [Blumenthals](https://en.wikipedia.org/wiki/Equation_of_State_Calculations_by_Fast_Computing_Machines) ended up publishing became one of the most popular algorithms in human science - the original [paper](https://scholar.google.com/scholar?hl=en&as_sdt=0%2C39&q=Equation+of+State+Calculations+by+Fast+Computing+Machines&btnG=) has roughly 40,000 citations! While there's still more to this story to hear, including some [controversy](https://en.wikipedia.org/wiki/Metropolis%E2%80%93Hastings_algorithm#History) over who should get credit for what, I'll leave the links for those interested to explore, so this post can remain focused on the mechanics and demonstration of the technique. 

## Mechanics 
So how does it work? It starts with a distribution $p(x)$ that one wants to model. This could be the result of solving a differential equation, as in the physics Metropolis was interested in, or as is more typically the case in 
statistics, the product of some conditional probability structure. The famous Bayes law states this eloquently:

$$
p(\theta|x) = p(x|\theta)p(\theta)
$$
