+++
title = "An analogy"
description = "Eating fruit or eating an apple is contravariant to fruit or an apple"
date = 2021-06-10
draft = false
slug = "eating-fruit"

[taxonomies]
categories = ["data","category-theory"]
tags = ["solid", "variance", "functors","liskov"]

[extra]
comments = true
+++

# An analogy between programming and statistics

## Introduction

Since some time machine learning and especially deep learning are growing ever more powerfull. Organizations are using these tools more and more. As they go mainstream and grow more powerfull there is however a counterforce with growing concerns about the fairness and explainability of these algorithms. Mainly of what the bias is of these blackbox models. One of the main advocates is Judea Pearl with causal inference as to making prior beliefs more explicit. For me the explicit modelling of prior beliefs for causal inference reminds me of the compile time type checking that is supported in programming languages like Csharp, Java, C++, Haskell, etc. Furthermore there is the trend of differentiable programming. Machine learning and deep learning frameworks like tensorflow and pytorch traditionally are implemented as a dialect or a domain specific language in the high level scripting language python. Similarly several statistical and machine learning models were implemented in the statistical programming language R. The secret sauce here is that they very much depend on libraries in C++ or Fortran for speed and typechecking while it depends on the scripting languages for conciseness and flexibility. This leads to a set of problems like library lock-in, lack of support of the language (for e.g. bound checks). By using real programming language constructs instead of framework dialects you get support for type checking, debugging, IDE support so alround transferable knowledge about the language and it's tooling (and also cheaper to find people and not having to retrain them so they can work with it). [It is also noted](http://colah.github.io/posts/2015-09-NN-Types-FP/) that composition of the different layers in deep learning is akin to programming language constructs from functional programming. So more and more there is work being done on introducing first class language support for differentiation to programming languages like:
  
- Python language with [JAX](https://github.com/google/jax)
- Swift lanugage with the [Swift for Tensorflow experiment](https://github.com/tensorflow/swift) which is now being directly integrated in the Swift compiler
- Julia language with [zygote](https://fluxml.ai/Zygote.jl/latest/)
- CLR language like Csharp with [PartyDonk](https://github.com/partydonk/partydonk/) by the samen guy that did the mono project.
- [Deeplearning.scala](https://index.scala-lang.org/thoughtworksinc/deeplearning.scala/any/1.0.0-M0?target=_2**.11**)
- etc.

> Deep Learning est mort. Vive Differentiable Programming! [Yann LeCun](https://www.facebook.com/yann.lecun/posts/10155003011462143)

That's why I think that it is usefull to revisit the Classical Design Patterns of object oriented software engineering and exploring how they relate to fundamental statistical principles. The gang of four patterns design patterns are a bit verbose and typically the most known ones are among the mnemonic SOLID. One of the most striking I find is with the L of this mnemonic which is the Liskov substituion principle. Object oriented programming is a subset of functional programming. If you consider objects of a class just as partially applied functions with as partially applied arguments the identity of the object. That's why I will try to use Category Theory since this is the fundament of most functional programming languages like haskell, ML, Fsharp, Scala etc. Category theory is a rather abstract subject in mathematics but is used to bridge the gap between seamingly unrelated branches of mathematics (famously the Curry-Howard isomorphism that relates type theory and proof theory).

## Liskov substitution principle

data abstraction and polymorphism

"Putting an apple in a fruit basket" is covariant. "Going to a fruit orchard and plucking an apple" is contravariant. You can put fruit in the fruit basket, but you can't put fruit in the apple basket. You can pluck an apple at the apple orchard but you won't get any other fruit.

## Variance and covariance in statistics

bias
corellation 
animal breeding variance covariance matrix
variance is information
regression analysis: regression around a mean
bias variance trade off 

## Functor in Category theory

lawvere 
equivariance
representation theory
algebraic topology
structure preserving map
map SQL select