---
layout: page
title: Variational autoencoders for dummies
description: A simple(ish), complete(ish) explanation of the theory behind VAEs
---


We'll use the MNIST digits example here.

## Latent variables

(Explain latent variables and introduce `z`)

## Probability distribution over latent and observable variables

P(x, z) is a _joint distribution_. From it, we can calculate a few
other distributions:

* P(x | z): given a particular z, what is the distribution of x values?

* P(z | x): given a particular x (image), what is the distribution of z values?

* P(x): what is the overall distribution of images?

* P(z): what is the overall distribution of latent variables?

Generative model:
p(x) = int p(x|z) * p(z) dz

Maximize likelihood of data under model:
max(theta) p_theta(x)

p(x) = int p(x,z) dz  # Why not just calculate this?

p(x|z) = p(x, z) / p(z)
p(x|z) = p(x, z) / (int p(x,z) dx)

$$\sigma$$







