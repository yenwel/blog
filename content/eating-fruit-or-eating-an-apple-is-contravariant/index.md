+++
title = "Eating fruit"
description = "eating fruit or eating an apple is contravariant to fruit or an apple"
date = 2021-06-10
draft = false
slug = "eating-fruit"

[taxonomies]
categories = ["data","category-theory"]
tags = ["solid", "variance", "functors","liskov"]

[extra]
comments = true
+++

# introduction

Since some time machine learning and especially deep learning are growing ever more powerfull. Organization in private and the public sector are using these tools more and more. As they go mainstream and grow more powerfull there is however a counterforce with growing concerns about the fairness and explainability of these algorithms. Mainly of what the bias is of these blackbox models. One of the main advocates is Judea Pearl with causal inference as to making bias more explicit. Furthermore there is the trend of differentiable programming. Machine learning and deep learning algorithms where implemented as a dialect of domain specific language in the high level scripting language python. Similarly several statistical and machine learning models were implemented in the statistical programming language R. The secret here is that they very much depend on libraries in C++ or fortran. 

Julia lang

making CLR languages differentiable

JAX

Swift tensorflow

automatic differentation: applying the chain rule untill you end up with

That's why I think that it is usefull to revisit the classical Design Patterns of object oriented software engineering en exploring how they relate to fundamental statistical principles. The gang of four patterns design patterns are a bit verbose and typically the most known ones are among the mnemonic SOLID. One of the most striking I find is with the L of this mnemonic which is the Liskov substituion principle. Object oriented programming is a subset of functional programming. If you consider objects for example just as partially applied functions with the as partially applied arguments the identity of the object. That's why I will try to use Category Theory since this is the fundament of most functional programming languages like haskell, ML, Fsharp, Scala etc. Category theory is a rather abstract subject in mathematics but is used to bridge the gap between seamingly unrelated branches of mathematics (famously the curry howard isomorphism that related ). There are higher order theories o

# Liskov substitution principle

data abstraction and polymorphism

"Putting an apple in a fruit basket" is covariant. "Going to a fruit orchard and plucking an apple" is contravariant. You can put fruit in the fruit basket, but you can't put fruit in the apple basket. You can pluck an apple at the apple orchard but you won't get any other fruit.

# Variance and covariance in statistics

bias
corellation 
animal breeding variance covariance matrix
variance is information
regression analysis: regression around a mean
bias variance trade off 

# Functor in Category theory

lawvere 
equivariance
representation theory
algebraic topology
structure preserving map
map SQL select