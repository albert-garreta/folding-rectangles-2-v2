## New rigorous progress: the Möbius branch is already $O(1)$

I think one of the verifier’s two remaining tasks can now be closed completely:

> **Claim.** In the rank-$\le 4$ regime of Lemmas 5–9, the **Möbius alternative** from Lemma 7 contributes at most a constant number of witnesses. In fact, the number of non-reference witnesses in the Möbius branch is at most $4$.

This is a genuine strengthening of `proofs.md`: Lemma 7 gives the Möbius parametrization abstractly over the function field, but for counting we need a **degree-controlled polynomial null relation**. That is the key new ingredient below.

---

## Setup for the lemma

Fix the reference witness $(f_0,\rho_0,g_0)$, and for each alternate witness write

- $h_i = (g_i-g_0)/(\rho_i-\rho_0) \in RS[H^2,k']$,
- $\lambda_i = (\rho_i-\rho_0)^{-1}$.

Let $N=|H^2|$, $r=k'/N$, and $A=63/64$ as in `proofs.md`.

From Lemma 4, for each non-exceptional witness $i$ we have a partition
$J_i = E_i \sqcup F_i$,
where

- on $E_i$, $h_i = o$,
- on $F_i$, $h_i = o' + \lambda_i L$,

for fixed polynomials $o,o',L \in RS[H^2,k']$, and
$|J_i| \ge A N$.

Here I renamed the fixed branch-offset polynomial from `proofs.md` to $L$ to avoid clashing with Möbius coefficients.

---

## Proposition: Möbius branch has size at most $4$

### Statement

Assume $r<61/256$, and suppose a family of non-reference witnesses lies in the Möbius branch of Lemma 7. Then the number of such witnesses is at most $4$.

---

## Proof

### Step 1: the easy rank-$\le 2$ subcase already collapses to an affine line

Suppose first that the vectors
$(1,\lambda_i,h_i,\lambda_i h_i)$
span dimension at most $2$ over the function field.

Then the projected triples $(1,\lambda_i,h_i)$ also span dimension at most $2$. Since the first two coordinates $1,\lambda_i$ are linearly independent as functions of $i$ (the $\lambda_i$ are distinct constants), it follows that there exist $u,v \in \mathbb{F}(x)$ such that for every $i$,
$h_i = u + v\lambda_i$.

Now $u$ and $v$ are linear combinations of two distinct $h_i$’s, so in fact $u,v \in RS[H^2,k']$.

Therefore
$g_i = g_0 + (\rho_i-\rho_0)h_i = g_0 + (\rho_i-\rho_0)u + v = (g_0+v-\rho_0 u) + \rho_i u$.

So all the codewords $g_i$ lie on a single affine line $u_0 + \rho_i \phi$ in $RS[H^2,k']$. By Lemma 3 of `proofs.md`, there are at most $4$ such parameters $\rho_i$.

So the only case left is when the span of $(1,\lambda_i,h_i,\lambda_i h_i)$ has dimension exactly $3$.

---

### Step 2: construct a degree-controlled null relation

Assume now the span has dimension exactly $3$.

Choose three witnesses, say $i=1,2,3$, whose row vectors
$(1,\lambda_i,h_i,\lambda_i h_i)$
span this $3$-dimensional space over $\mathbb{F}(x)$.

Let $\alpha,\beta,\gamma,\delta \in \mathbb{F}[x]$ be the signed $3\times 3$ minors obtained from the $3\times 4$ matrix with rows
$(1,\lambda_1,h_1,\lambda_1 h_1)$,
$(1,\lambda_2,h_2,\lambda_2 h_2)$,
$(1,\lambda_3,h_3,\lambda_3 h_3)$,
by deleting columns $1,2,3,4$ respectively.

By the standard cofactor identity, the vector $(\alpha,\beta,\gamma,\delta)$ is orthogonal to each of these three rows. Since those rows span the entire row space, it is orthogonal to every row. Hence for every witness $i$ we have the polynomial identity
$\alpha + \beta \lambda_i + \gamma h_i + \delta \lambda_i h_i = 0$.

Equivalently,
$\alpha + \beta \lambda_i + (\gamma + \delta \lambda_i) h_i = 0$.

Now we record the degree bounds.

- In $\alpha$ and $\beta$, every determinant term contains exactly two $h$-type factors, so
  $\deg \alpha < 2k'$ and $\deg \beta < 2k'$.
- In $\gamma$ and $\delta$, every determinant term contains exactly one $h$-type factor, so
  $\deg \gamma < k'$ and $\deg \delta < k'$.

These bounds are crucial.

---

### Step 3: define the two “identity sets” where multiplicity can be large

For a point $x \in H^2$, let
$t_E(x) = |\{i : x \in E_i\}|$,
$t_F(x) = |\{i : x \in F_i\}|$,
and $t(x)=t_E(x)+t_F(x)$.

We define two subsets of $H^2$.

#### The $E$-identity set

Let
$Z_E = \{x : \alpha(x)+o(x)\gamma(x)=0 \text{ and } \beta(x)+o(x)\delta(x)=0\}$.

If $x \notin Z_E$ and $x \in E_i$, then $h_i(x)=o(x)$, so the null relation becomes
$\alpha(x)+o(x)\gamma(x) + \lambda_i(\beta(x)+o(x)\delta(x)) = 0$.

This is a nonzero linear equation in the constant $\lambda_i$, because $x\notin Z_E$. Therefore it has at most one solution. Hence for every $x \notin Z_E$,
$t_E(x) \le 1$.

#### The $F$-identity set

Let
$Z_F = \{x : \alpha(x)+o'(x)\gamma(x)=0,\ \beta(x)+o'(x)\delta(x)+L(x)\gamma(x)=0,\ L(x)\delta(x)=0\}$.

If $x \notin Z_F$ and $x \in F_i$, then $h_i(x)=o'(x)+\lambda_i L(x)$, so the null relation becomes
$\alpha(x)+o'(x)\gamma(x) + \lambda_i(\beta(x)+o'(x)\delta(x)+L(x)\gamma(x)) + \lambda_i^2 L(x)\delta(x)=0$.

Since $x\notin Z_F$, this is a nonzero polynomial in $\lambda_i$ of degree at most $2$. Therefore it has at most two solutions. Hence for every $x \notin Z_F$,
$t_F(x) \le 2$.

Combining the two bounds, if $x \notin Z_E \cup Z_F$, then
$t(x) \le 3$.

---

### Step 4: averaging forces one of the identity sets to be huge

Let $m$ be the number of witnesses in the Möbius branch.

If $m \le 4$, we are done. So suppose for contradiction that $m \ge 5$.

Since each $|J_i| \ge A N$ with $A=63/64$, we have
$\sum_{x \in H^2} t(x) = \sum_{i=1}^m |J_i| \ge m A N$.

On the other hand, writing $Z = Z_E \cup Z_F$, we have

- $t(x) \le m$ for $x \in Z$,
- $t(x) \le 3$ for $x \notin Z$.

So
$\sum_{x \in H^2} t(x) \le m|Z| + 3(N-|Z|) = 3N + (m-3)|Z|$.

Therefore
$m A N \le 3N + (m-3)|Z|$,

so
$|Z| \ge \frac{mA-3}{m-3}N$.

Since $A=63/64$ and $m\ge 5$, the right-hand side is minimized at $m=5$, giving
$|Z| \ge \frac{5\cdot 63/64 - 3}{2}N = \frac{123}{128}N$.

Hence one of $Z_E,Z_F$ has size at least half of this:
$\max(|Z_E|,|Z_F|) \ge \frac{123}{256}N$.

Because $r<61/256$, we have
$2k' = 2rN < \frac{122}{256}N < \frac{123}{256}N$.

So one of $Z_E$ or $Z_F$ has size strictly bigger than $2k'$.

---

### Step 5: whichever identity set is large, it globalizes by degree

We now use the degree bounds from Step 2 and the fact that $o,o',L$ all have degree $<k'$.

The polynomials defining $Z_E$ are

- $\alpha + o\gamma$, of degree $<2k'$,
- $\beta + o\delta$, of degree $<2k'$.

Indeed $\deg \alpha,\deg \beta <2k'$ and $\deg(o\gamma),\deg(o\delta) <2k'$.

Similarly, the polynomials defining $Z_F$ are

- $\alpha + o'\gamma$, degree $<2k'$,
- $\beta + o'\delta + L\gamma$, degree $<2k'$,
- $L\delta$, degree $<2k'$.

Therefore:

- if $|Z_E|>2k'$, then both $\alpha + o\gamma$ and $\beta + o\delta$ vanish identically;
- if $|Z_F|>2k'$, then $\alpha + o'\gamma$, $\beta + o'\delta + L\gamma$, and $L\delta$ all vanish identically.

We now handle the two cases.

---

### Step 6: if $Z_E$ is large, the family collapses to $h_i=o$ except possibly one witness

Assume $|Z_E|>2k'$. Then
$\alpha + o\gamma \equiv 0$
and
$\beta + o\delta \equiv 0$.

Substitute these into the null relation:
$\alpha + \beta \lambda_i + (\gamma+\delta\lambda_i)h_i = 0$.

We get
$(\gamma+\delta\lambda_i)(h_i-o)=0$
as a polynomial identity in $x$.

Since $\mathbb{F}[x]$ is an integral domain, for each fixed $i$ either

- $\gamma+\delta\lambda_i \equiv 0$, or
- $h_i \equiv o$.

If $\delta=0$, then $\gamma \neq 0$ because otherwise also $\alpha=\beta=0$, contradicting nontriviality of the null relation. So in this subcase every witness satisfies $h_i=o$.

If $\delta \neq 0$, then $\gamma+\delta\lambda_i \equiv 0$ can hold for at most one constant $\lambda_i$, because the $\lambda_i$ are distinct. So all but at most one witness satisfy $h_i=o$.

Now if $h_i=o$, then
$g_i = g_0 + (\rho_i-\rho_0)o = (g_0-\rho_0 o) + \rho_i o$.

Also the reference codeword $g_0$ itself lies on the same affine line:
$g_0 = (g_0-\rho_0 o) + \rho_0 o$.

Hence the reference witness together with all non-exceptional witnesses lie on one affine line in $RS[H^2,k']$. By Lemma 3, there are at most $4$ corresponding parameters in total. Therefore there are at most $3$ non-reference non-exceptional witnesses, and after adding the possible one exceptional witness we get
$m \le 4$.

This contradicts $m\ge 5$.

---

### Step 7: if $Z_F$ is large, the family collapses to $h_i=o'+\lambda_i L$ (or $h_i=o'$ if $L=0$)

Assume $|Z_F|>2k'$. Then
$\alpha + o'\gamma \equiv 0$,
$\beta + o'\delta + L\gamma \equiv 0$,
and
$L\delta \equiv 0$.

There are two subcases.

#### Subcase 7a: $L \not\equiv 0$

Then $L\delta \equiv 0$ forces $\delta \equiv 0$.

So the null relation becomes
$\alpha + \beta \lambda_i + \gamma h_i = 0$,
and using the two identities above we get
$\gamma(h_i - o' - \lambda_i L)=0$.

Again $\gamma \neq 0$ (otherwise all coefficients are zero), so for every $i$,
$h_i = o' + \lambda_i L$.

Therefore
$g_i = g_0 + (\rho_i-\rho_0)(o' + \lambda_i L) = g_0 + (\rho_i-\rho_0)o' + L = (g_0 + L - \rho_0 o') + \rho_i o'$.

So all these witnesses lie on a single affine line in $RS[H^2,k']$. By Lemma 3, there are at most $4$ such parameters. Hence $m\le 4$.

#### Subcase 7b: $L \equiv 0$

Then the $F$-branch identity reduces to
$h_i = o'$ on $F_i$, and the same computation as in Step 6 gives
$(\gamma+\delta\lambda_i)(h_i-o')=0$.

So again all but at most one witness satisfy $h_i=o'$. For those witnesses,
$g_i = g_0 + (\rho_i-\rho_0)o' = (g_0-\rho_0 o') + \rho_i o'$,

and now the reference codeword $g_0$ also lies on this line. Lemma 3 again gives at most $4$ total parameters on the line, so there are at most $3$ non-reference non-exceptional witnesses plus at most one exceptional witness. Hence $m\le 4$.

So in every subcase we contradict $m\ge 5$.

This finishes the proof.

---

## Consequence

This completely closes the verifier’s Step 2:

- the **continuous Möbius family** cannot contribute more than a constant number of parameters;
- in fact, the Möbius branch contributes at most $4$ non-reference witnesses.

So, after this round, the only genuinely unresolved branch is the **quadratic / square-specialization branch** from Lemma 9.

---

## What this reveals about the remaining square-specialization step

There is a useful structural takeaway.

The same per-coordinate multiplicity idea also works formally in the quadratic branch. If
$h_i^2 - (P+\lambda_i Q)h_i + R + \lambda_i S = 0$,
then at a fixed point $x$:

- the condition that the $E$-root $h_i=o$ works is linear in $\lambda_i$,
- the condition that the $F$-root $h_i=o' + \lambda_i L$ works is quadratic in $\lambda_i$.

So outside a corresponding union of two identity sets, one again gets at most $3$ witnesses per coordinate. The averaging argument would again force a very large identity set.

The remaining obstacle is now very crisp:

- in the Möbius case, I produced polynomial coefficients $\alpha,\beta,\gamma,\delta$ of degree $<2k'$, so a large identity set globalizes immediately;
- in the quadratic case, `proofs.md` does not yet provide an equally good **degree-controlled polynomial normalization** for $P,Q,R,S$.

With naive Cramer/minor formulas, the degrees look too large. So the remaining task is essentially:

> Find a normalization of the quadratic relation whose relevant coefficient polynomials have degree $<123N/256$ (ideally $<2k'$), or replace the degree-count with a different global argument.

That is a much sharper target than before.

---

## Small repository note

A concrete issue in the current files:

- `output.md` still advertises only the older $R<0.13939$ result as the “Current Main Result”.
- But `proofs.md` plus the verifier already support the stronger structural reduction up to $r<61/256$, and the proposition above removes the Möbius subcase entirely.

So `output.md` is now stale relative to the verified state of the project.

---

## Suggested next move

The next round should focus only on the quadratic branch and try to prove one of the following:

1. a low-degree polynomial normalization of the quadratic identity;
2. or a direct counting lemma for constant specializations $\lambda_i$ making the discriminant a square, using the same “large identity set” philosophy.

I can work out that quadratic identity-set framework explicitly next if useful.