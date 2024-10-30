---
layout: post
title: "Musings on the Erdős Number"
date: 2019-12-17 12:00:00
categories: blog
tags: academia, mathematics
---

I came across the Erdős number a long time ago and found it a fun and interesting concept. Just last week I saw someone writing about it on Twitter and I got curious about whether I have a finite Erdős number.

<!-- more -->

The [Erdős number](https://en.wikipedia.org/wiki/Erdos_number) describes the collaborative distance between Paul Erdős and other people, via authorship of mathematical (academic) publications. Paul Erdős himself has an Erdős number of 0 and someone's Erdős number is defined as `k+1` where `k` is the lowest Erdős number of any co-author. So, Erdős' co-authors have an Erdős number of 1 and so on. If there is no chain connecting someone to Erdős, their number is undefined or infinite.

## Musings

Since Paul Erdős passed away, the number of people with an Erdős number 1 is fixed at 511 and the number of living people with this number can only decrease. This also means that the lowest Erdős number one can attain is 2. As long as there are people with an Erdős number of 1 alive, the number of people with an Erdős number of 2 can still increase, but I hypothesise that the rate at which this is happening will slow down as the number of living people with Erdős number 1 (in other words: the chance of collaborating with someone with Erdős number 1) decreases. There will be a tipping point at which the death rate among people with an Erdős number of 2 overtakes the rate at which new collaborators with an Erdős number of 2 and thus, the number of living people with Erdős number 2 will decrease. It would be interesting to see how the distributions of Erdős numbers (held by living people) changes over time and to estimate how the prospects of attaining an Erdős number of 2 changes with it.

## My Erdős Number

Since I have one academic publication, at the time of writing, I wanted to figure out whether my Erdős number would be finite. To do this, I used the [collaboration distance](https://mathscinet.ams.org/mathscinet/freetools/collab-dist) tool on MathSciNet (American Mathematical Society). I started my search with the co-authors of my paper. According to this tool, J.A. Burgoyne has an Erdős number of 6 (see table 1), while Henkjan Honing isn't in the database. This gives me a finite Erdős number of (at most) 7.

Author                | Coauthored with       | Identifier | Topic/field
:---------------------|:----------------------|:-----------|:-------------
Nelson Mooren         | John Ashley Burgoyne  |            | Music cognition
John Ashley Burgoyne  | Ichiro Fujinaga       | MR312014   | Computational musicology
Ichiro Fujinaga       | Jorge Calvo-Zaragoza  | MR3673874  | Image analysis
Jorge Calvo-Zaragoza  | Colin de la Higuera   | MR3737504  | Finite state automata
Colin de la Higuera   | John Shawe-Taylor     | MR2804605  | Machine translation
John Shawe-Taylor     | Christopher D. Godsil | MR0897237  | Graph theory
Christopher D. Godsil | Paul Erdős            | MR0957190  | Graph theory/combinatorics

MathSciNet only lists mathematical papers, there are bound to be some gaps in the data. My work, and that of my co-authors, is centred on the field of music cognition. So after this initial search, I figured I could do better. To this end, I looked at some (high-profile) co-authors of both Henkjan Honing and J.A. Burgoyne using Google Scholar, hoping to find different links connecting me to Erdős.

Looking at J.A. Burgoyne's co-authors, I found that I have (at least) two paths that give me an Erdős number of 6, namely:

Author               | Coauthored with      | Identifier | Topic/field
:--------------------|:---------------------|:-----------|:-------------
Nelson Mooren        | John Ashley Burgoyne |            | Music cognition
John Ashley Burgoyne | Lawrence K. Saul     |            | Various
Lawrence K. Saul     | Sam T. Roweis        | MR2050880  | Unsupervised learning
Sam T. Roweis        | Leonard M. Adleman   | MR1655281  | Computational biology
Leonard M. Adleman   | Andrew M. Odlyzko    | MR0717715  | Prime factorisation
Andrew M. Odlyzko    | Paul Erdős           | MR0535395  | Number theory

and:

Author               | Coauthored with      | Identifier | Topic/field
:--------------------|:---------------------|:-----------|:-------------
Nelson Mooren        | John Ashley Burgoyne |            | Music cognition
John Ashley Burgoyne | Max Welling          |            | Deep learning
Max Welling          | John S. Lowengrub    | MR3001289  | Gaussian modelling
John S. Lowengrub    | Joseph B. Keller     | MR1864363  | Physics
Joseph B. Keller     | Persi W. Diaconis    | MR1918049  | Mathematical physics
Persi W. Diaconis    | Paul Erdős           | MR2126886  | Mathematics

Even better, I found a path that gets my Erdős number down to 5:

Author               | Coauthored with      | Identifier | Topic/field
:--------------------|:---------------------|:-----------|:-------------
Nelson Mooren        | John Ashley Burgoyne |            | Music cognition
John Ashley Burgoyne | Remco C. Veltkamp    |            | Music information retrieval
Remco C. Veltkamp    | Mark T. de Berg      | MR2159527  | Algorithm theory
Mark T. de Berg      | Boris Aronov         | MR2414676  | Computational geometry
Boris Aronov         | Paul Erdős           | MR1289067  | Combinatorics

In conclusion: my Erdős number is (at most) 5 and four paths connect me to Erdős, with 17 unique authors. All of these paths run via JAB. Aside from JAB, there are no other duplicate authors in the (known) graph connecting me to Erdős.
