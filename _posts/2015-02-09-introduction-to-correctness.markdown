---
layout: post
title:  "Introduction to Software Correctness"
date:   2015-02-09 21:35:17
categories: computer science
---
Software correctness is a neat way to tie specifications to code implementation. Correctness by construction helps you be absolutely sure your code performs according to specifications. The computer science construct often used for this is Hoare Triples. This [Microsoft Research Labs Video](https://www.youtube.com/watch?v=spcfzbisBv4) has piqued my interest in the practical aspects of Invariants so I thought I'd give a simple overview of Hoare Triples.

Hoare triples are usually written in the format of {P}S{Q} where P is the precondtion and Q is the postcondition. Let's take for example:

`
{P}
x := y + 1
{x > 5}
`

The goal is to find the weakest precondition that creates a correct program.

Using the [assignment axiom](https://www.dropbox.com/s/oc3ax256a10jkpk/Designprocessesforsoftwaredevelopment.pdf?dl=0) we substitute the precondition for the postcondtion, pretty simple:

`
{x > 5}[x := y + 1]
`

Which results in:

`
{y + 1 > 5} = {y > 4}
`

This is our weakest predicate P. Of course, this is a fairly trivial example, but I hope it gets you started in predicate logic and hoare triple notation. For more information I recommend reading "What Computing is All About".