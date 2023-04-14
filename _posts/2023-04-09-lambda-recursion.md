---
title:  "The LAMBDA Manifesto"
excerpt: "The most powerful function in Google Sheets."
header:
  teaser: "assets/images/sword.JPG"
tags:
  - lambda
  - formula
toc: true
--- 

### Introduction

This is not a tutorial. This is a rant.

This manifesto is dedicated to `LAMBDA`, an egregiously undervalued function. Since its introduction on August 24, 2022, it has been relegated to use as a mere auxiliary to the `LAMBDA` Helper Functions, or LHFs. However, this reductionist perspective trivializes `LAMBDA` qua `LAMBDA` in its floccinaucinihilipilification. The objective, therefore, is to recast `LAMBDA` as the apotheosis of spreadsheet formulae in its own right.

### The Underestimation of LAMBDA

Here is a selection of opinions taken from some of the most venerated Google Sheets users.

> The use case for the LAMBDA function is to work with other lambda helper functions, like MAP, REDUCE, SCAN, MAKEARRAY, BYCOL, and BYROW.
> 
> LAMBDA functions themselves are challenging to use and not very intuitive compared to regular functions.

- [Ben L. Collins of The Collins School of Data](https://www.benlcollins.com/spreadsheets/lambda-function/)

> The below LAMBDA function examples are to make you understand its usage. At this level, you may even surprise; why this function is even required. \[sic]
> 
> You would only understand the real potential of the LAMBDA function in Google Sheets when you use it together with its helper functions.

- [Prashanth K V of InfoInspired](https://infoinspired.com/google-docs/spreadsheet/how-to-use-the-lambda-function-in-google-sheets-standalone/)

Arguably the only correct sentiment expressed here is that `LAMBDA` can be challenging to use. The rest? Utter falsehood.

Let's go back to the year 1936.

### Lambda Calculus

`LAMBDA` finds its roots in the pioneering work of Alonzo Church. Church developed a system called lambda calculus while tackling the *Entscheidungsproblem*, a foundational problem in the still-nascent field of computer science.

Let's start by taking it apart. Lambda calculus has three types of so-called lambda terms:

`x`
: A variable.

`λx.M`
: An abstraction. `M` itself must be a lambda term. Variable `x` becomes bound to the expression (i.e. its scope is limited to `M`).

`M N`
: An application. Both `M` and `N` must be lambda terms. It's easiest to think of this as applying function `M` to argument(s) `N`.

Arguably the most important concept of these is the *abstraction*. Take a standard mathematical function, such as `f(x) = x^2 + 2`. An analogous expression using lambda terms would be `λx.(x^2 + 2)`. In this case, `(x^2 + 2` is a lambda term on its own. Using the above notation, it is the `M` in the abstraction.

Note how the `f` disappeared. In lambda calculus, all functions are anonymous, devoid of traditional variable-bound names.

This brings us to *application*. Let's say we want to input `4` into the function. For standard function notation, that would simply be `f(4)`. In lambda calculus, we must instead say `(λx.(x^2 + 2))(4)`.

Note the parentheses. The same expression can be simply written as `λx.(x^2 + 2)) 4`; however, we can more clearly identify each distinct lambda term. Here, we have the lambda term `M` as an abstraction with `λx`, and lambda term `N` as 4. Again, compare this structure to the above, and you'll find that it ultimately follows the form of an application.

This is akin to the `LAMBDA` formula in Google Sheets, where functions can be created and invoked without explicit names, following a similar notation to lambda calculus. For instance, the formula `=LAMBDA(x, x^2 + 2)(4)` evokes an analogous implementation. This integration enables users to harness the potential of lambda calculus for practical applications.

While this connection may not appear immediately useful, Church's lambda calculus is a formal system that can express any computable function. The equivalent computational power between lambda calculus and Turing machines implies that lambda calculus, therefore, is Turing-complete—a property initially recognized in the seminal Church-Turing thesis.

### Lambda Calculus in Google Sheets

Firstly, to dismiss the notion that the sole use case of `LAMBDA` is with LHFs.

Here's a basic description of each LHF using lambda calculus. For the purposes of this demonstration, let us call the anonymized function `f`.

`MAP`
: `∀A[i,j] ∈ array ↦ (λx.f)(A[i,j])`

`REDUCE`
: `(λg.g(g initial_value 1))(λgan.if n > |array| then a else (g g (λxy.f)(a array[n]) n+1))`

`SCAN`
: `∀A[i,j] ∈ array ↦ (λg.g(g initial_value 1))(λgan.if n > i+j*i then a else (g g (λxy.f)(a array[n]) n+1))`

`MAKEARRAY`
: `∀A[i,j] ∈ A ∈ M(m,n) ↦ (λx.f)(A[i,j])`

`BYCOL`
: `∀A[*,j] ∈ array ↦ (λx.f)(A[*,j])`

`BYROW`
: `∀A[i,*] ∈ array ↦ (λx.f)(A[i,*])`

You'll note that most of the functions utilize `↦`, or the maplet. Mapping is built into lambda notation.

So what does this mean? Well, for starters, it means that we can fully emulate any of the LHFs *with `LAMBDA` alone*. This mere fact indicates a complete role reversal; suddenly, it is the LHFs that are auxilliary to `LAMBDA`, as opposed to vice versa.

You can find proof of this in [this](https://docs.google.com/spreadsheets/d/1Jw8fbGWoMI9M5vwb11tkg67Mleozq4Q-9kyhf_3nT6Q/edit?usp=sharing) workbook. I've also opted to not use `MAP` as the maplet can be emulated using recursion and array construction.

While this is very interesting, `LAMBDA` also has the capability for unbounded recursion. If `REDUCE` is a `FOR` loop, `LAMBDA` recursion is a `WHILE`. This behavior is not achievable otherwise. This capability is especially notable as its interactions with hardcoded `LAMBDA` calculation limits diverge from standard conventions.

That's all from me. Catch y'all on the flip side,

- Astral
