
I've just learned that Kubernetes "Helm" is a great technology "to find, share, 
and use software built for Kubernetes" and decide I want to learn how to use 
it. First stop is [their documentation](http://helm.readthedocs.io/en/latest/awesome).
 Near the very start of the page, they mention one of the three core components:

> * The `manifests/` directory contains one or more Kubernetes manifest files.

Later in the page, there are more references to "manifests," which ones get 
special treatment, how some of them should be "keepers," but nothing about what 
they *are*. 

You would think that searching through the Helm docs, the Kubernetes doc, or
Google would turn up something, but no.

[Google doesn't know](Google%20kubernetes%20helm.pdf).

[Kubernetes doesn't know](Kubernetes%20search.pdf).

After a *lot* more digging, I *think* "manifest" refers to any of the general
YAML files used to define Kubernetes resources. I genuinely don't understand
how people get up and running with new technologies.
