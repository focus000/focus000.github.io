---
layout: post
title:  "Wagner–Fischer algorithm's proof"
date:   2021-10-15 01:14:53 +0800
categories: algorithm
---
# Wagner–Fischer algorithm's proof

## Introduction

[Wagner–Fischer algorithm](https://en.wikipedia.org/wiki/Wagner–Fischer_algorithm) can calculate [Levenshtein distance](https://en.wikipedia.org/wiki/Levenshtein_distance), now we give the description.

**Wagner–Fischer algorithm:** let $a \coloneqq a_1\dots a_m$ and $b \coloneqq b_1\dots b_n$ are strings, and the Levenshtein distance of $a$ and $b$ is denote as $d_{mn}$, then we have
$$
{\displaystyle {\begin{aligned}d_{i0}&=\sum _{k=1}^{i}w_{\mathrm {del} }(a_{k}),&&\quad {\text{for}}\;1\leq i\leq m\\d_{0j}&=\sum _{k=1}^{j}w_{\mathrm {ins} }(b_{k}),&&\quad {\text{for}}\;1\leq j\leq n\\d_{ij}&={\begin{cases}d_{i-1,j-1}&{\text{for}}\;a_{i}=b_{j}\\\min {\begin{cases}d_{i-1,j}+w_{\mathrm {del} }(a_{i})\\d_{i,j-1}+w_{\mathrm {ins} }(b_{j})\\d_{i-1,j-1}+w_{\mathrm {sub} }(a_{i},b_{j})\end{cases}}&{\text{for}}\;a_{i}\neq b_{j}\end{cases}}&&\quad {\text{for}}\;1\leq i\leq m,1\leq j\leq n.\end{aligned}}}
$$
where $w_{del}, w_{ins}$ and $w_{sub}$ means the operator of delete, insert and substitute a character.

## Proof of Wagner–Fischer algorithm

Indeed, caculate $d_{i0}$ and $d_{0j}$ is trivial. Now we generate to $d_{ij}$.

**For $a_i = b_j$**, we have
$$
d_{ij} = d_{i-1, j-1}.
$$

**proof:** First of all,
$$
d_{ij} \leq d_{i-1, j-1}
$$
is trivial. Then we denote that $w_*$ is one of the three operatoprs, $w_{del}, w_{ins}$ and $w_{sub}$. Since $w_*$ can only change one character, and these operaters are commutative with each other, we can find a sequence of operator $w*$ change $a_i$ to $b_j$, which can write as
$$
\prod^m w_*(a_k) \prod^n w_*(a_{last}) = b, \tag{*}
$$
where $a_{last}$ is the last element of $a$, and $\forall k \neq last$, and $m + n = d_{ij}$. Since $w_*(a_k)$ won't change $a_{last}$, and vice versa. We have
$$
d_{i-1, j-1} \leq m \leq d_{ij}.
$$
Hence we have $d_{ij} = d_{i-1, j-1}$.

**For $a_i \neq b_j$**, $w_*$ is commutative, we have

$$
w_{ins}(a_{last})w_{ins}(a_{last}) = w_{ins}(a_{last})w_{ins}(a_{last-1}), \\
w_{del}(a_{last})w_{del}(a_{last}) = w_{del}(a_{last-1})w_{del}(a_{last}), \\
w_{sub}(a_{last})w_{sub}(a_{last}) = w_{sub}(a_{last}), \\
w_{ins}(a_{last})w_{del}(a_{last}) = \empty, \\
w_{del}(a_{last})w_{ins}(a_{last}) = \empty \text{ or } w_{sub}(a_{last}), \\
w_{ins}(a_{last})w_{sub}(a_{last}) = w_{ins}(a_{last}), \\
w_{sub}(a_{last})w_{ins}(a_{last}) = w_{ins}(a_{last})w_{sub}(a_{last-1}), \\
w_{del}(a_{last})w_{sub}(a_{last}) = w_{del}(a_{last-1})w_{sub}(a_{last}), \\
w_{sub}(a_{last})w_{del}(a_{last}) = w_{del}(a_{last}), \\
$$

hence in $(*)$, $n = 1$ or $0$, when $a_i \neq b_j$, the last character of string $a$ must be modified, so $n = 1$, it means $a_i$ must be insert, delete or substitute, we have

$$
d_{ij} \geq \min {\begin{cases}d_{i-1,j}+w_{\mathrm {del} }(a_{i})\\d_{i,j-1}+w_{\mathrm {ins} }(b_{j})\\d_{i-1,j-1}+w_{\mathrm {sub} }(a_{i},b_{j})\end{cases}}.
$$

On the other side,

$$
d_{ij} \leq \min {\begin{cases}d_{i-1,j}+w_{\mathrm {del} }(a_{i})\\d_{i,j-1}+w_{\mathrm {ins} }(b_{j})\\d_{i-1,j-1}+w_{\mathrm {sub} }(a_{i},b_{j})\end{cases}},
$$

is trivial, we have

$$
d_{ij} = \min {\begin{cases}d_{i-1,j}+w_{\mathrm {del} }(a_{i})\\d_{i,j-1}+w_{\mathrm {ins} }(b_{j})\\d_{i-1,j-1}+w_{\mathrm {sub} }(a_{i},b_{j})\end{cases}},
$$

where $a_i \neq b_j$. Now we complete the proof of Wagner–Fischer algorithm.