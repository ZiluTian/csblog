---
title: "Simple type theory"
layout: post
date: 2021-11-27
tag:
- type theory
- tutorial
star: true
category: blog
author: Zilu
katex: yes
description: Note of Simple type theory" by Richard Southwell
---
Reference: [video]

In this [video], Dr. Southwell discussed the simple type theory and its relationship with intuitionistic logic (in what follows, we refer to it simply as logic) and category theory. Simple type theory is the *minimal* language to describe bicartesian closed categories [bicartesian-closed-category]. The *Set*, *Graph*, and *Function* categories are some examples of bicartesian closed category. The simple type theory is also called *lambda calculus with sum*. 

### Types
- $$O$$ is the **empty type**. In set theory, the empty set; in category theory, the initial object; in logic, the false proposition.
- $$1$$ is the **unit type**. In set theory, the singleton set; in category theory, the terminal object; in logic, the true proposition.
- $$A, B, \ldots$$ are the base types. In category theory, they are objects other than initial and terminal objects in the bicartesian closed category.
- **Product type**, $$ A \times B $$. In set theory, the cartesian product; in category theory, the product of objects; in logic, A and B.
- **Sum type**, $$ A + B $$. In set theory, the sum of sets; in category theory, the co-product of objects; in logic, A or B.
- **Function type**, $$ (A \rightarrow B) $$. In set theory, the set of functions from A to B; in category theory, the exponential object $$B ^ A$$; in logic, A implies B.

Type declaration is of form 

$$ x: A $$

In set theory, x is a value in set A; in category theory, x is an arrow into A; in logic, A is a proposition and x is the proof of that proposition.

**Context** is a list of type declarations for variables, often denoted with $$ \Gamma, \Delta $$. A context provides background for particular judgements. A **judgement** is of following form. 

$$x_1: A_1, x_2: A_2, \ldots, x_n: A_n \vdash r: B $$

In the context specified in the left, we have term *r* of type B. *r* may depend on the variables in the context. In set theory, we can think of it as a function, $$A_1 \times A_2 \times \ldots A_n \rightarrow B$$. When r=*, B=$$1$$. In category theory, we can think of it as an arrow. In logic, if we have a proof $$x_1$$ of proposition $$A_1, \ldots $$ and a proof $$x_n$$ of proposition $$A_n$$, then we have a proof $$r$$ of proposition $$B$$.

### Inference rules
#### Case rule

$$ \over x_1: A_1, x_2: A_2, \ldots, x_n: A_n \vdash x_i : A_i $$

which is also written as

$$ \over \Gamma, x_i: A_i, \Delta \vdash x_i: A_i $$

In set theory, we can think of it as projection function associated with product, $$ A_1 \times \ldots \times A_i \ldots \xrightarrow{\pi_i} A_i $$. In logic, we can think of it as for a list of proof for propositions, and amongst them is proof $$x_i$$ of proposition $$A_i$$, then it entails that we have a proof $$x_i$$ of proposition $$A_i$$.

#### Weakening rule

$$
\Gamma, \Delta \vdash b: B
\over \Gamma, x: A, \Delta \vdash b: B
$$

**Weakening** rule states that we can add variables to context. The analogy in proof and set theory can be easily obtained as shown in rule 2. For example, consider $$ \Gamma = z : L, \Delta = \{\}$$. Then 
$$ z: L \vdash b: B $$
corresponds to 
$$L \xrightarrow{b} B$$
and 
$$z: L, x: A \vdash b: B$$ 
corresponds to 
$$ L \times A \xrightarrow{\pi_1} L \xrightarrow{b} B$$

#### Unit introduction rule

$$\over \Gamma \vdash * : 1 $$

In any context, * is of unit type. In logic, for any context, we always have the proof that proposition true is true. In set theory, we can always produce a value * of type 1. For example, when $$ \Gamma = x : A $$, then we have the unique function from set A to the singleton set that sends all elements of A to *.

#### Product introduction rule

$$
\Gamma \vdash a: A \quad \Gamma \vdash b: B
\over \Gamma \vdash <a, b>: A \times B
$$

Let $$\Gamma = x: H$$. In category theory, it corresponds to the following product. 

$$ H \xrightarrow{b} B, H \xrightarrow{a} A, H \xrightarrow{<a, b>} A \times B $$

For logic, it means that having evidence $$x$$ of proposition $$H$$ entails that we have evidence $$ a $$ of proposition $$A$$ and evidence $$b$$ of proposition $$B$$, then we can form the evidence $$<a, b>$$ of the proposition A *and* B.

#### Product elimination rules

$$
\Gamma \vdash p: A \times B
\over \Gamma \vdash fst(p): A
$$

In logic, if we have a proof for proposition A and B, then we have a proof fst(p) for proposition A. (If A *and* B is true, then A is true)

$$
\Gamma \vdash p: A \times B
\over \Gamma \vdash snd(p): B
$$

#### Function introduction rule

$$
\Gamma, x: A \vdash b: B
\over \Gamma \vdash (\lambda x: A).b : A \rightarrow B
$$

The function introduction rule allows us to think of a function from A to B as a value of function type. In logic, if we have proof x of proposition A that entails proof b of proposition B, then we have a proof of proposition A implies B. In category theory, it corresponds to the currying map or transpose associated with exponential objects (ref: [bicartesian-closed-category], [exponential-object-wiki]). For $$ \Gamma = z: H, H \times A \xrightarrow{b} B, H \xrightarrow{\bar{b}} B^A $$.

#### Function elimination rules

$$
\Gamma \vdash f: A \rightarrow B \quad \Gamma \vdash a: A
\over \Gamma \vdash f(a): B
$$

In set theory, if we have a function from set A to B and a value of A, then we can operate the function on the value and obtains a value f(a) of set B. In logic, if we have a proof f of proposition A implies B and a proof A is true, then we have a proof of B is true. In category theory, it corresponds to evaluation arrow associated with the exponential object, $$ B^A \times A \xrightarrow{e} B $$.

$$
\overline{g: A \rightarrow B, x: A \vdash g: A \rightarrow B}  \quad \overline{ g: A \rightarrow B, x: A \vdash x: A} 
\over g: A \rightarrow B, x: A \vdash g(x): B
$$

With the typing rules described so far, we can convert between the following forms.

$$ z: H, x: A \vdash b: B $$

$$ \vdash k: H \rightarrow (A \rightarrow B) $$ 

$$ \rho: H \times A \vdash \beta: B $$

#### Empty elimination
An empty type does not have an introduction rule, but we can use the empty type.

$$
\Gamma \vdash e: 0
\over \Gamma \vdash abort_A(e): A
$$

In logic, if you have a proof of false proposition, then you can have a proof of any other proposition.

#### Empty uniqueness
If we did have a value of the empty type, then the output is any value of the target type.

$$
\Gamma \vdash e: O \quad \Gamma \vdash x: A
\over \Gamma \vdash abort_A(e) \equiv x: A
$$

#### Sum introduction
Left injection function

$$
\Gamma \vdash a: A
\over \Gamma \vdash inl_{A+B}(a): A + B
$$

Right injection function

$$
\Gamma \vdash b: B
\over \Gamma \vdash inr_{A+B}(b): A + B
$$

#### Sum elimination

$$
\Gamma \vdash s: A+B \quad \Gamma, x: A \vdash u: C \quad \Gamma, y: B \vdash v: C
\over \Gamma \vdash match(s, x.u, y.v): C
$$

The expression $$ x.u $$ binds variable $$x$$ to value $$u$$.

#### Sum computations

Doing a match function after a left injection gives us u.

$$
\Gamma \vdash a: A \quad \Gamma, x: A \vdash u: C \quad \Gamma, y: B \vdash v: C
\over \Gamma \vdash match[inl_{A+B}(a), x.u, y.v] \equiv u[a/x]:C
$$

Similarly for a right injection.

$$
\Gamma \vdash b: B \quad \Gamma, x: A \vdash u: C \quad \Gamma, y: B \vdash v: C
\over \Gamma \vdash match[inr_{A+B}(a), x.u, y.v] \equiv v[b/y]:C
$$

#### Sum uniqueness

$$
\Gamma \vdash s: A+B \quad \Gamma, h: A+B \vdash m: C
\over \Gamma match(s, x.m[inl_{A+B}(x)/h], y.m[inr_{A+B}(y)/h]) \equiv m[s/h]: C
$$


Here are some structural rules.
#### Cut rule

$$
\Gamma \vdash a: A \quad \Gamma, x: A, \Delta \vdash b: B
\over \Gamma, \Delta \vdash b[a/x]
$$

The notation $$b[a/x]$$ represents that we replace all free occurrences of $$x$$ with $$a$$ in term $$b$$. If no free variables of $$a$$ becomes bound in the term $$b$$ after substitution, then we say $$a$$ is free for $$x$$ in $$b$$. 

#### Contract rule

$$
\Gamma, x: A, y: A \Delta \vdash b: B
\over \Gamma, x:A, \Delta \vdash b[x/y]
$$

**Reflexive**

$$
\Gamma, x: A
\over \Gamma \vdash a \equiv a:A
$$

**Symmetric**

$$
\Gamma \vdash a \equiv a': A
\over \Gamma \vdash a' \equiv a: A
$$

**Transitive**

$$
\Gamma \vdash a \equiv a': A \quad \Gamma \vdash a' \equiv a'': A
\over \Gamma \vdash a \equiv a'': A
$$

#### Unit uniqueness

$$
\Gamma \vdash v: 1
\over \Gamma \vdash v \equiv * : 1
$$

#### Product computation

$$
\Gamma \vdash a: A \quad \Gamma \vdash b: B
\over \Gamma \vdash fst(<a, b>) \equiv a: A
$$

$$
\Gamma \vdash a: A \quad \Gamma \vdash b: B
\over \Gamma \vdash snd(<a, b>) \equiv b: B
$$

#### Product uniqueness

$$
\Gamma \vdash p: A\times B
\over \Gamma \vdash p \equiv <fst(p), snd(p)>: A \times B
$$

#### Function computation

$$
\Gamma, x: A \vdash b: B \quad \Gamma \vdash a: A
\over \Gamma \vdash [(\lambda x: A).b](a) \equiv b[a/x]: B
$$

#### Function uniqueness

$$
\Gamma \vdash f: A \rightarrow B
\over \Gamma \vdash f \equiv (\lambda x : A).[f(x)]: A \rightarrow B
$$

$$
\Gamma \vdash f: A \rightarrow B \quad \Gamma \vdash a \equiv a': A
\over \Gamma \vdash f(a) \equiv f(a'): B
$$

$$
\Gamma, x: A \vdash b \equiv b': B
\over \Gamma \vdash \lambda x.b \equiv \lambda x.b': A \rightarrow B
$$

[video]:https://www.youtube.com/watch?v=EEz8DGIjXQI
[bicartesian-closed-category]:http://zll22.user.srcf.net/talks/2011-12-01-CategoricalLogic.pdf
[exponential-object-wiki]:https://en.wikipedia.org/wiki/Exponential_object