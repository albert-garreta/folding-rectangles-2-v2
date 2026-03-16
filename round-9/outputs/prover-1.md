## Read-through / small issue in the current files

One repository issue is still worth flagging explicitly: in `proofs.md`, Lemma 4 has a corrupted line reading `|J_i| 	o E_i \sqcup F_i`. The intended statement is clearly that `J_i = E_i \sqcup F_i`, and several later arguments use exactly that partition. I am not rewriting the file, but this line should be repaired before any verifier relies on it.

---

## New progress: a genuine 5-witness algebraic collapse

The pairwise graph method topped out because it only saw the sets $F_i$. To go beyond that, I looked for a relation that uses the full pointwise structure

- for each hard witness $i$,
- on the large set $J_i = S_0 \cap S_i$,
- the codeword $h_i$ takes one of two values:
  $h_i(x) \in \{ o(x),\ o'(x) + \lambda_i C(x)\}$.

The key new observation is that **five** such points $(\lambda_i,h_i(x))$ always lie on a reducible conic. This gives a concrete $5 \times 5$ determinant relation, and unlike the earlier triple/pairwise identities, it is strong enough to survive root-counting up to rate $r < 61/256 \approx 0.23828$.

I also found a sharp obstruction showing why **four-witness** local polynomial identities cannot possibly do this: any universal 4-witness polynomial relation has degree at least $10$, so root-counting with 4 witnesses is intrinsically too weak well before $r=1/4$.

So the picture is now much cleaner:

- 4-witness local elimination is fundamentally too weak.
- 5-witness local elimination is the first viable order.
- At 5 witnesses one gets a global rank-$4$ collapse, reducing the hard case to a common quadratic relation over the function field.

That is real incremental progress toward the verifier’s requested “global dependency” step.

---

## Setup for the hard regime

I use the same notation as in the verified hard-regime decomposition.

Fix a reference witness $(f_0,\rho_0,g_0)$ with success set $S_0$, $|S_0| \ge T = 127N/128$.

For each other non-exceptional witness $i$, let $S_i$ be its success set, let $J_i = S_0 \cap S_i$, and define the Reed–Solomon codeword

$h_i = \dfrac{g_i-g_0}{\rho_i-\rho_0} \in RS[H^2,k']$.

By the already-established hard-regime structure, there are fixed functions $o,o',C$ on $H^2$ and distinct scalars $\lambda_i$ such that for every $x \in J_i$ one has

$h_i(x) \in \{ o(x),\ o'(x)+\lambda_i C(x)\}$.

Also, since each success set misses at most $N/128$ points, for any finite index set $I$ we have the crude but useful intersection bound

$|S_0 \cap \bigcap_{i \in I} S_i| \ge N - (|I|+1)\cdot N/128$.

In particular, for five witnesses $i_1,\dots,i_5$,

$|S_0 \cap S_{i_1}\cap \cdots \cap S_{i_5}| \ge N - 6N/128 = 61N/64$.

I will use this repeatedly.

---

## Lemma 1: the 5-witness reducible-conic determinant

### Statement

Fix five distinct hard witnesses $i_1,\dots,i_5$. Define

$\Delta_{i_1,\dots,i_5}(x) := \det
\begin{pmatrix}
1 & \lambda_{i_1} & h_{i_1}(x) & \lambda_{i_1} h_{i_1}(x) & h_{i_1}(x)^2 \\
1 & \lambda_{i_2} & h_{i_2}(x) & \lambda_{i_2} h_{i_2}(x) & h_{i_2}(x)^2 \\
1 & \lambda_{i_3} & h_{i_3}(x) & \lambda_{i_3} h_{i_3}(x) & h_{i_3}(x)^2 \\
1 & \lambda_{i_4} & h_{i_4}(x) & \lambda_{i_4} h_{i_4}(x) & h_{i_4}(x)^2 \\
1 & \lambda_{i_5} & h_{i_5}(x) & \lambda_{i_5} h_{i_5}(x) & h_{i_5}(x)^2
\end{pmatrix}$.

Then $\Delta_{i_1,\dots,i_5}(x)=0$ for every $x \in S_0 \cap S_{i_1}\cap \cdots \cap S_{i_5}$.

### Proof

Fix such an $x$.

Write $a = o(x)$, $b = o'(x)$, and $c = C(x)$.

For each $t \in \{1,\dots,5\}$, because $x \in J_{i_t}$, we know that

$h_{i_t}(x) \in \{ a,\ b+\lambda_{i_t} c\}$.

Now consider the polynomial in two variables

$Q_x(\lambda,y) := (y-a)(y-b-\lambda c)$.

Expanding,

$Q_x(\lambda,y) = y^2 - (a+b+\lambda c)y + ab + a c \lambda$.

Hence, for each $t$,

$Q_x(\lambda_{i_t}, h_{i_t}(x)) = h_{i_t}(x)^2 - (a+b+\lambda_{i_t} c)h_{i_t}(x) + ab + a c \lambda_{i_t}$.

But $h_{i_t}(x)$ is either the first root $a$ or the second root $b+\lambda_{i_t}c$, so this quantity is zero.

Therefore the row vector

$(1,\ \lambda_{i_t},\ h_{i_t}(x),\ \lambda_{i_t} h_{i_t}(x),\ h_{i_t}(x)^2)$

is orthogonal to the fixed coefficient vector

$(ab,\ ac,\ -(a+b),\ -c,\ 1)$.

So all five rows lie in a common $4$-dimensional hyperplane of $\mathbb F^5$, and therefore their determinant is zero.

This proves $\Delta_{i_1,\dots,i_5}(x)=0$ on the whole common success set. $\square$

---

## Lemma 2: degree bound for the 5-witness determinant

### Statement

Each $\Delta_{i_1,\dots,i_5}$ is the evaluation on $H^2$ of a polynomial of degree strictly less than $4k'$.

### Proof

Each $h_i$ is a Reed–Solomon codeword of degree less than $k'$ on the domain $H^2$.

So, as a polynomial in the evaluation variable $x$,

- $1$ has degree $0$,
- $\lambda_i$ has degree $0$,
- $h_i$ has degree less than $k'$,
- $\lambda_i h_i$ has degree less than $k'$,
- $h_i^2$ has degree less than $2k'$.

In any monomial term in the determinant expansion, exactly one entry is chosen from each column. Therefore every determinant monomial contains

- one factor from the $h_i^2$ column, contributing degree less than $2k'$,
- one factor from the $h_i$ column, contributing degree less than $k'$,
- one factor from the $\lambda_i h_i$ column, contributing degree less than $k'$,
- and two constant-degree factors from the first two columns.

Hence every monomial term has degree strictly less than $2k' + k' + k' = 4k'$.

Therefore $\Delta_{i_1,\dots,i_5}$ has degree strictly less than $4k'$. $\square$

---

## Corollary 3: identically vanishing 5-witness minors for $r<61/256$

### Statement

Assume $r = k'/N < 61/256$.

Then for every five hard witnesses $i_1,\dots,i_5$, the determinant $\Delta_{i_1,\dots,i_5}$ vanishes identically as a polynomial on $H^2$.

### Proof

By Lemma 1, $\Delta_{i_1,\dots,i_5}$ vanishes on the set $S_0 \cap S_{i_1}\cap \cdots \cap S_{i_5}$.

As noted above, this set has size at least $61N/64$.

By Lemma 2, $\deg \Delta_{i_1,\dots,i_5} < 4k' = 4rN$.

If $r < 61/256$, then $4rN < 61N/64$.

A nonzero polynomial of degree less than $4k'$ cannot vanish on more than $4k'-1$ points of the Reed–Solomon evaluation domain. Since $\Delta_{i_1,\dots,i_5}$ vanishes on at least $61N/64 > 4k'$ points, it must be the zero polynomial.

So every such $5 \times 5$ determinant vanishes identically. $\square$

---

## First structural consequence: a rank-$4$ collapse

### Statement

Under the same hypothesis $r<61/256$, for every $x \in H^2$, the row vectors

$(1,\lambda_i,h_i(x),\lambda_i h_i(x),h_i(x)^2)$

have rank at most $4$.

Equivalently, over the function field of $H^2$, the family of vectors

$(1,\lambda_i,h_i,\lambda_i h_i,h_i^2)$

spans a space of dimension at most $4$.

### Proof

Every $5 \times 5$ minor of the matrix with these rows is exactly one of the determinants from Corollary 3, hence vanishes identically.

A matrix has rank at most $4$ if and only if all its $5 \times 5$ minors vanish.

Therefore the rank is at most $4$ pointwise and over the function field. $\square$

---

## Proposition 4: explicit quadratic collapse, conditional on one nonzero $4 \times 4$ minor

The previous corollary gives a rank bound. The next step is to turn it into an explicit formula.

### Statement

Assume $r<61/256$.

Suppose there exist four hard witnesses, relabelled $1,2,3,4$, such that the determinant

$\Gamma(x) := \det
\begin{pmatrix}
h_1(x) & \lambda_1 h_1(x) & -1 & -\lambda_1 \\
h_2(x) & \lambda_2 h_2(x) & -1 & -\lambda_2 \\
h_3(x) & \lambda_3 h_3(x) & -1 & -\lambda_3 \\
h_4(x) & \lambda_4 h_4(x) & -1 & -\lambda_4
\end{pmatrix}$

is not the zero polynomial.

Then there exist rational functions $P,Q,R,S$ on $H^2$ such that for every hard witness $i$ one has the identity

$h_i^2 - (P+\lambda_i Q)h_i + R + \lambda_i S = 0$.

Moreover, these $P,Q,R,S$ can be chosen with common denominator $\Gamma$.

### Proof

Define the $4 \times 4$ matrix

$A :=
\begin{pmatrix}
h_1 & \lambda_1 h_1 & -1 & -\lambda_1 \\
h_2 & \lambda_2 h_2 & -1 & -\lambda_2 \\
h_3 & \lambda_3 h_3 & -1 & -\lambda_3 \\
h_4 & \lambda_4 h_4 & -1 & -\lambda_4
\end{pmatrix}$

and the column vector

$b := (h_1^2,h_2^2,h_3^2,h_4^2)^T$.

By hypothesis, $\det A = \Gamma$ is not identically zero, so $A$ is invertible over the function field. Define

$(P,Q,R,S)^T := A^{-1} b$.

By construction, for $j=1,2,3,4$ we have

$P h_j + Q \lambda_j h_j - R - S \lambda_j = h_j^2$,

which is the same as

$h_j^2 - (P+\lambda_j Q)h_j + R + \lambda_j S = 0$.

Now let $i$ be any other hard witness. Consider the $5 \times 5$ determinant

$\det
\begin{pmatrix}
h_1 & \lambda_1 h_1 & -1 & -\lambda_1 & h_1^2 \\
h_2 & \lambda_2 h_2 & -1 & -\lambda_2 & h_2^2 \\
h_3 & \lambda_3 h_3 & -1 & -\lambda_3 & h_3^2 \\
h_4 & \lambda_4 h_4 & -1 & -\lambda_4 & h_4^2 \\
h_i & \lambda_i h_i & -1 & -\lambda_i & h_i^2
\end{pmatrix}$.

This is just a column permutation of the determinant from Corollary 3, so it vanishes identically.

Write the last row as $u_i := (h_i,\lambda_i h_i,-1,-\lambda_i)$. Then the determinant above has block form

$\det \begin{pmatrix} A & b \\ u_i & h_i^2 \end{pmatrix}$.

Since $A$ is invertible over the function field, the Schur complement formula gives

$\det \begin{pmatrix} A & b \\ u_i & h_i^2 \end{pmatrix}
= \det(A)\cdot \left(h_i^2 - u_i A^{-1} b\right)$.

The left-hand side is identically zero, and $\det(A)=\Gamma$ is not identically zero. Therefore

$h_i^2 - u_i A^{-1} b = 0$.

But $A^{-1}b = (P,Q,R,S)^T$, so this becomes

$h_i^2 - (P+\lambda_i Q)h_i + R + \lambda_i S = 0$.

This holds for every hard witness $i$, completing the proof. $\square$

---

## Corollary 5: a clean reduction to a “square specialization” problem

### Statement

Under the assumptions of Proposition 4, let

$\mathcal D(\lambda) := (P+\lambda Q)^2 - 4(R+\lambda S)$

viewed as a quadratic polynomial in $\lambda$ with coefficients in the function field.

Then for every hard witness $i$, the specialization $\mathcal D(\lambda_i)$ is a square in the function field.

### Proof

From Proposition 4,

$h_i^2 - (P+\lambda_i Q)h_i + R + \lambda_i S = 0$.

Multiply by $4$ and complete the square:

$(2h_i - P - \lambda_i Q)^2
= (P+\lambda_i Q)^2 - 4(R+\lambda_i S)
= \mathcal D(\lambda_i)$.

Hence $\mathcal D(\lambda_i)$ is the square of the rational function $2h_i - P - \lambda_i Q$. $\square$

### Why this matters

This gives a concrete next subproblem:

> Bound the number of constants $\lambda$ such that the quadratic-in-$\lambda$ function-field polynomial $\mathcal D(\lambda)$ takes a square value.

I have not solved that subproblem in this round, but the reduction is rigorous and much sharper than before.

---

## Second structural consequence: the complementary Möbius-collapse case

If Proposition 4 cannot be triggered, then all $4 \times 4$ minors of the smaller matrix already vanish.

### Statement

Assume $r<61/256$. If every $4 \times 4$ minor of the matrix with rows $(1,\lambda_i,h_i,\lambda_i h_i)$ vanishes identically, then there exist rational functions $A,B,C,D$, not all zero, such that for every hard witness $i$,

$A + B\lambda_i + C h_i + D \lambda_i h_i = 0$.

Equivalently, whenever $C + D\lambda_i \not\equiv 0$,

$h_i = -\dfrac{A+B\lambda_i}{C+D\lambda_i}$.

So in this case all hard witnesses lie on a single Möbius family in the parameter $\lambda_i$.

### Proof

If every $4 \times 4$ minor vanishes identically, then the row-rank of the matrix with rows $(1,\lambda_i,h_i,\lambda_i h_i)$ is at most $3$ over the function field.

Therefore there is a nonzero vector $(A,B,C,D)$ in the left kernel, which gives

$A + B\lambda_i + C h_i + D \lambda_i h_i = 0$

for every $i$.

Rearranging gives the stated Möbius form whenever the denominator is nonzero. $\square$

### A resolved subcase

If in this Möbius-collapse case one actually has $D=0$, then

$h_i = u + v\lambda_i$

for some rational functions $u,v$.

Since two distinct $h_i$ are Reed–Solomon codewords and the $\lambda_i$ are distinct constants, it follows that $u,v$ are also Reed–Solomon codewords.

Using $\lambda_i = 1/(\rho_i-\rho_0)$, we get

$g_i = g_0 + (\rho_i-\rho_0)h_i = (g_0+v) + (\rho_i-\rho_0)u$,

so the $g_i$ lie on a single affine line in $RS[H^2,k']$.

By the existing affine-line multiplicity lemma already in `proofs.md`, this immediately gives at most $4$ such parameters.

So one genuine degeneration subcase of the rank-collapse is already closed.

---

## A sharp obstruction: 4-witness local identities cannot work

This is the negative result I think is most important for steering the next rounds.

The verifier suggested trying “triple rank relations” or “global affine-dimension collapse.” The following lemma shows that any attempt to force a **single low-degree universal polynomial identity on four witnesses** is doomed.

### Definition

Fix four distinct constants $\lambda_1,\lambda_2,\lambda_3,\lambda_4$.

Let $\mathcal A_4 \subseteq \mathbb F^4$ be the set of all quadruples $(y_1,y_2,y_3,y_4)$ for which there exist scalars $a,b,c$ and bits $\varepsilon_1,\dots,\varepsilon_4 \in \{0,1\}$ such that

$y_t = a + \varepsilon_t (b+c\lambda_t)$ for all $t$.

This is exactly the local 4-witness model coming from the hard decomposition after freezing a coordinate $x$.

For a triple $i,j,k$, write

$L_{ijk}(y) := \det
\begin{pmatrix}
1 & \lambda_i & y_i \\
1 & \lambda_j & y_j \\
1 & \lambda_k & y_k
\end{pmatrix}$.

This is a nonzero linear form in the variables $y_i,y_j,y_k$.

### Lemma 6: any universal 4-witness polynomial has degree at least 10

If a polynomial $F(y_1,y_2,y_3,y_4)$ vanishes on all of $\mathcal A_4$, then $F$ is divisible by

$\prod_{1 \le i < j \le 4} (y_i-y_j)\cdot \prod_{1 \le i < j < k \le 4} L_{ijk}(y)$.

In particular, every nonzero such $F$ has degree at least $6+4=10$.

### Proof

I prove first that each pair-equality hyperplane is contained in $\mathcal A_4$.

Fix a pair, say $(1,2)$. Take any quadruple with $y_1=y_2$.

Set $a := y_1 = y_2$, choose $\varepsilon_1=\varepsilon_2=0$, and choose $\varepsilon_3=\varepsilon_4=1$.

We need $b,c$ such that

$y_3 = a + b + c\lambda_3$ and $y_4 = a + b + c\lambda_4$.

Since $\lambda_3 \ne \lambda_4$, this is a $2 \times 2$ linear system with a unique solution $(b,c)$. Hence every point on the hyperplane $y_1=y_2$ lies in $\mathcal A_4$.

The same argument works for every pair $(i,j)$, so every hyperplane $y_i-y_j=0$ is contained in $\mathcal A_4$.

Now I prove that each triple-collinearity hyperplane is also contained in $\mathcal A_4$.

Fix a triple, say $(1,2,3)$. Take any quadruple satisfying $L_{123}(y)=0$.

Then the three points $(\lambda_1,y_1)$, $(\lambda_2,y_2)$, $(\lambda_3,y_3)$ are collinear in the affine plane. So there exist scalars $\alpha,\beta$ such that

$y_t = \alpha + \beta \lambda_t$ for $t=1,2,3$.

Now set $a := y_4$, choose $\varepsilon_4=0$, and choose $\varepsilon_1=\varepsilon_2=\varepsilon_3=1$.

We want

$y_t = a + b + c\lambda_t$ for $t=1,2,3$.

This is achieved by taking $c=\beta$ and $b=\alpha-a$.

Therefore every point on the hyperplane $L_{123}(y)=0$ lies in $\mathcal A_4$.

The same holds for every triple $(i,j,k)$.

So $F$ vanishes on each of the six hyperplanes $y_i-y_j=0$ and on each of the four hyperplanes $L_{ijk}(y)=0$.

A polynomial vanishing on a hyperplane defined by a nonzero linear form must be divisible by that linear form. Therefore $F$ is divisible by each of the ten linear factors above.

These ten factors are pairwise nonassociated because they define ten distinct hyperplanes. Hence their product divides $F$.

Therefore $\deg F \ge 10$. $\square$

---

## Numerical consequence of the 4-witness obstruction

This obstruction is not just philosophical; it gives an explicit barrier.

Suppose one hoped to prove a universal 4-witness polynomial identity and then force it to vanish identically by root-counting on the common success set.

For four alternate witnesses plus the reference, the common success intersection has size at least

$N - 5N/128 = 123N/128$.

But Lemma 6 says any universal 4-witness polynomial has degree at least $10$ in the witness values, so after substituting codewords of degree less than $k'$, its $x$-degree is at least about $10k' = 10rN$.

Thus 4-witness root-counting can only possibly work when

$10rN < 123N/128$,

i.e.

$r < 123/1280 \approx 0.09609$.

That is **strictly below** the already-proved $0.13939$ regime. So any local 4-witness elimination strategy is inherently weaker than what is already known.

This is, I think, the cleanest explanation so far of why the previous triple/quadruple local attempts kept stalling.

---

## Summary of what is now rigorously established

In the hard regime, I can now rigorously prove the following:

1. **Five-witness reducible-conic relation.**  
   For any five hard witnesses, the determinant with rows $(1,\lambda_i,h_i,\lambda_i h_i,h_i^2)$ vanishes on their common success set.

2. **Global rank-$4$ collapse for $r<61/256$.**  
   Since the common success set has size at least $61N/64$, this determinant vanishes identically whenever $r<61/256 \approx 0.23828$.

3. **Concrete algebraic dichotomy for $r<61/256$.**  
   Either:
   - all rows $(1,\lambda_i,h_i,\lambda_i h_i)$ have rank at most $3$, giving a Möbius family $h_i = -(A+B\lambda_i)/(C+D\lambda_i)$, or
   - there exist rational functions $P,Q,R,S$ with a common quadratic identity  
     $h_i^2 - (P+\lambda_i Q)h_i + R + \lambda_i S = 0$  
     for every hard witness $i$.

4. **A resolved degeneration.**  
   In the rank-$3$ case, if the denominator does not depend on $\lambda$ (equivalently $D=0$), then the family is affine in $\lambda$, hence the old affine-line multiplicity lemma immediately gives at most $4$ witnesses.

5. **Definitive obstruction to 4-witness universal identities.**  
   Any universal polynomial relation on four witnesses has degree at least $10$, so 4-local root-counting cannot reach anywhere near $r=1/4$.

---

## Why I think this is the right next reduction

This feels like the first truly “global” collapse that is both explicit and auditable:

- it uses five witnesses simultaneously,
- it produces an honest polynomial-matrix rank condition,
- it gets all the way to $r<61/256 \approx 0.23828$,
- and it pinpoints the remaining issue as a very concrete function-field specialization problem.

What remains unresolved in this round is the final step from

- Möbius family, or
- common quadratic identity with square discriminant at many constants $\lambda_i$,

to an absolute $O(1)$ bound on the number of witnesses.

But this is now a much more rigid target than the previous set-overlap picture.

---

## Suggested next steps

I think the next iteration should focus on one of these two sharply formulated subproblems:

1. **Quadratic-family case.**  
   Study the quadratic function-field polynomial  
   $\mathcal D(\lambda) = (P+\lambda Q)^2 - 4(R+\lambda S)$  
   and bound the number of constants $\lambda$ for which $\mathcal D(\lambda)$ is a square in the function field.

2. **Möbius-family case.**  
   In the relation $h_i = -(A+B\lambda_i)/(C+D\lambda_i)$, show that if this quotient is a Reed–Solomon codeword for many distinct constants $\lambda_i$, then either it reduces to the affine case $D=0$ or only $O(1)$ values of $\lambda_i$ are possible.

If useful, I can spend the next round attacking one of those two reduced problems directly.