---
title: "Dependent type theory"
layout: post
date: 2021-12-05
tag:
- type theory
- tutorial
star: true
category: blog
author: Zilu
katex: yes
description: Note of dependent type theory" by Richard Southwell
---
Reference: [video]

The simple type theory, also known as the lambda calculus with sum, has some limitations. For example, it does not have the proper theory of arithmetic, e.g. we do not have infinite structure that can represent natural numbers. The dependent type theory addresses this concern and allows us to define types which can depend on values. In terms of logic, dependent type theory brings aboard the quantifiers such as there exists and forall.

We denote a type universe using $$U_i$$, $$ U_0: U_1 : U_2 \ldots $$. Consider the following example, which we can also think of as $$ (\lambda x: A).1: A \rightarrow U_i $$. 

$$ x: A \vdash 1 : U_i $$

More generally, if we have $$B : A \rightarrow U_i $$, then B is a *type family* that maps every value of A to a type (indexed by A), $$ B(x): U_i, x: A $$.

### Dependent pair type (Sigma type)

For $$ A \xrightarrow{B} U_i $$, we can form the dependent pair type $$\Sigma_{x: A} B(x) $$, which has members (a, b) where $$a: A, b: B(a) $$. We denote as $$ (a, b): \Sigma_{x: A} B(x) $$. Let $$ A = \{ a_1, a_2, a_3 \}$$, $$B(a_1) = \{ 1, 2 \}$$, $$B(a_2) = \{ 1' \}$$, $$B(a_3) = \{ 1'', 2'', 3'' \} $$. Then some members of the sigma type are $$(a_1, 2), (a_2, 1')$$. We call $$B(a_i)$$  a fiber over $$a_i$$.

The Sigma type has a projection function. 

$$ Pr_1: \Sigma_{x: A}B(x) \rightarrow A$$

The product type is a special case of a Sigma type. If B is constant, then 

$$ \Sigma_{x: A} B \equiv (A \times B) $$

For example, let B={1, 2} and A={$$a_1, a_2, a_3$$}. Then $$A \times B = \{(a_1, 1), (a_1, 2), (a_2, 1), (a_2, 2), (a_3, 1), (a_3, 2) \}$$, which is also the same as $$ \Sigma_{x: A} B$$.

### Dependent function type (Pi type)
The dependent function type $$\Pi_{x:A} B(x)$$ has as value a "function" f sending each a: A to some f(a): B(a). 

### Connection with logic

|Type theory    | Logic       |
|:---           | :----       |
|Q\: U          | Proposition |
|q\: Q          | Evidence    |
|B\: $$A \rightarrow U_i$$ | Predicate on A |
|$$p: \Sigma_{x: A} B(x)$$ | Evidence p that $$\exists (x: A).B(x) $$ |
|$$p: \Pi_{x: A} B(x)$$ | Evidence p that $$\forall (x: A).B(x) $$ |


### Identity type
For a, a': A, we write $$ (a =_A a'): U $$ to denote the identity type. In terms of logic, $$p: (a =_A a')$$ corresponds to p is the evidence that a and a' are propositionally equal. For any $$a: A: U$$, we have $$refl_a: (a =_A a)$$. We can think of $$a =_A a' $$ as a path from a to a'.

We can define the type of semi-group using the following equation. A semi-group is a set and an associative binary relation over the set. In the equation below, an element of a semi-group type consists of a pair $$(A, A \rightarrow (A \rightarrow A))$$ together with the evidence that the relation $$A \rightarrow (A \rightarrow A)$$ is associative.

$$ \Sigma_{A: U} \Sigma_{m: A \rightarrow (A \rightarrow A)} \Pi_{x: A} \Pi_{y:A} \Pi_{z: A} m(x, m(y, z)) =_A m(m(x, y), z) $$

### Path-based induction
Given $$a: A$$, $$ k: \Pi_{a: A}((a =_A x) \rightarrow U)$$ and $$e: k(a, refl_a)$$, we can get $$f: \Pi_{x: A} \Pi_{p: a=x} k(x, p) $$ where $$f(a, refl): \equiv e$$. 

For k, we are associating every path from A with a type. For the path p from a to b, it has type k(b, p). $$p: (a=_A b), k(b, p)$$. We can think of associating every path from a with a proposition that is either true or false. For path from a to a, the proposition is true. The path-based induction says that all paths from a have propositions true.

### Natural number type
Let O: N, $$ succ: N \rightarrow N $$. For $$Q: U, c_0 : Q, c_s: N \rightarrow (Q \rightarrow Q)$$, we have $$f: N \rightarrow Q, f(0) :\equiv c_0, f(succ(n)):\equiv c_s(n, f(n))$$. $$c_s$$ is a time-dependent function; f is also called a primitive recursion.

### Locally cartesian closed categories
For an object A of category C, the slice category C/A has objects of arrows in C, $$ B \xrightarrow{f} A $$ into A. An arrow m from ($$B \xrightarrow{f} A$$) to ($$B' \xrightarrow{f'} A$$) in C/A is $$B \xrightarrow{m} B'$$.

[video]:https://www.youtube.com/watch?v=Wh1QxF5FLJw