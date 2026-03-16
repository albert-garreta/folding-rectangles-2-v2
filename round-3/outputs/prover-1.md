## New rigorous progress: a hard-regime packing lemma, and an exact obstruction to the current pairwise-intersection plan

I think there is one clean thing we can add now which is both rigorous and directly relevant to the remaining obstacle.

The current notes repeatedly return to the hard-regime sets $D_i$ / $F_i$ and their pairwise intersections. There is a precise second-moment inequality available here. Once written out, it shows exactly what threshold on pairwise intersections would suffice for a constant bound, and it also shows why the naive version of this plan cannot close the problem by itself.

---

## 1. Setup for the hard regime

I will use the notation already present in `proofs.md`.

Let $N = n' = |H^2|$, so $k' = N/4$ and $T = 127N/128$.

Fix a rectangle $R(a,b)$ and a reference successful witness triple $(f_0,\rho_0,g_0)$, with success set

$S_0 = \{x \in H^2 : \operatorname{Fold}[f_0,\rho_0](x) = g_0(x)\}$,

so $|S_0| \ge T$.

For each $x \in S_0$, let $(e(x),o(x))$ denote the even/odd data of the branch chosen by $f_0$ at $x$, and let $(e'(x),o'(x))$ denote the even/odd data of the opposite branch at $x$.

Define the branch-gap function on $S_0$ by

$C(x) = e'(x) - e(x) + \rho_0 \bigl(o'(x)-o(x)\bigr)$.

Equivalently, $C(x)$ is the difference between the opposite branch fold-value and the chosen branch fold-value at parameter $\rho_0$.

Now let $\rho_1,\dots,\rho_m$ be distinct parameters in $X_R \setminus \{\rho_0\}$, and for each $i$ choose a successful witness triple $(f_i,\rho_i,g_i)$ with success set $S_i$.

Define

$h_i = \dfrac{g_i-g_0}{\rho_i-\rho_0} \in \operatorname{RS}[H^2,k']$,

and let $D_i \subseteq S_0 \cap S_i$ be the coordinates where $f_i$ chooses the branch opposite to the one chosen by $f_0$.

---

## 2. Lemma: the $D_i$ are large, and pairwise intersections are controlled by RS-correlation of $C$

### Lemma
With the notation above, the following hold.

1. For every $i$, we have $|D_i| > \dfrac{31}{64} N$.

2. If we set $\lambda_i = (\rho_i-\rho_0)^{-1}$, then for every $x \in D_i$,
   $h_i(x) = o'(x) + \lambda_i C(x)$.

3. Define
   $\Gamma(C) = \max_{q \in \operatorname{RS}[H^2,k']} |\{x \in S_0 : q(x)=C(x)\}|$.
   Then for every distinct $i,j$,
   $|D_i \cap D_j| \le \Gamma(C)$.

### Proof

#### Step 1: the overlap $S_0 \cap S_i$ is large

Since $|S_0| \ge T$ and $|S_i| \ge T$, inclusion-exclusion gives

$|S_0 \cap S_i| \ge 2T - N = 2 \cdot \frac{127}{128}N - N = \frac{63}{64}N$.

Let me write

$J_i = S_0 \cap S_i$,

so $|J_i| \ge 63N/64$.

#### Step 2: same-branch coordinates are sparse

Consider the set

$P_i = \{x \in S_0 : h_i(x) = o(x)\}$.

I claim that $|P_i| < N/2$.

To prove this, define a codeword on $H$ by

$r_i(Y) = \bigl(g_0 - \rho_0 h_i\bigr)(Y^2) + Y h_i(Y^2)$.

Since $g_0,h_i \in \operatorname{RS}[H^2,k']$, both terms have degree $<k$, so $r_i \in \operatorname{RS}[H,k]$.

Now fix any $x \in P_i$, and write $x=h^2$. Because $x \in S_0$, the reference witness $f_0$ uses the branch with even/odd data $(e(x),o(x))$, so

$g_0(x) = e(x) + \rho_0 o(x)$.

Since $x \in P_i$, we also have $h_i(x)=o(x)$. Therefore

$r_i(h) = \bigl(g_0(x)-\rho_0 o(x)\bigr) + h\,o(x) = e(x)+h\,o(x) = f_0(h)$,

and similarly

$r_i(-h) = \bigl(g_0(x)-\rho_0 o(x)\bigr) - h\,o(x) = e(x)-h\,o(x) = f_0(-h)$.

So for every $x \in P_i$, the function $f_0$ agrees with the codeword $r_i$ on both roots $\pm h$.

Hence

$\operatorname{agr}(f_0,r_i) \ge 2|P_i|$.

But $f_0$ is $1/2$-far from $\operatorname{RS}[H,k]$, so its agreement with every codeword is strictly less than $n/2 = N$. Therefore

$2|P_i| < N$,

which gives

$|P_i| < \frac{N}{2}$.

#### Step 3: same-branch coordinates inside $J_i$ lie in $P_i$

Take any $x \in J_i$ where $f_i$ chooses the same branch as $f_0$.

At such an $x$, both witnesses use the same branch data $(e(x),o(x))$, so

$g_0(x) = e(x) + \rho_0 o(x)$,
and
$g_i(x) = e(x) + \rho_i o(x)$.

Subtracting gives

$g_i(x)-g_0(x) = (\rho_i-\rho_0)o(x)$,

hence

$h_i(x) = \frac{g_i(x)-g_0(x)}{\rho_i-\rho_0} = o(x)$.

So every same-branch coordinate in $J_i$ belongs to $P_i$.

Since $D_i$ is the opposite-branch part of $J_i$, we get

$|D_i| \ge |J_i| - |P_i| > \frac{63}{64}N - \frac12 N = \frac{31}{64}N$.

This proves part 1.

#### Step 4: formula for $h_i$ on $D_i$

Fix $x \in D_i$.

By definition of $D_i$, the witness $f_i$ chooses the opposite branch at $x$, so

$g_i(x) = e'(x) + \rho_i o'(x)$,

while the reference witness gives

$g_0(x) = e(x) + \rho_0 o(x)$.

Subtracting,

$(\rho_i-\rho_0) h_i(x) = g_i(x)-g_0(x) = e'(x)-e(x) + \rho_i o'(x) - \rho_0 o(x)$.

Rewrite the right-hand side as

$(\rho_i-\rho_0)o'(x) + \bigl(e'(x)-e(x)+\rho_0(o'(x)-o(x))\bigr)$,

which is

$(\rho_i-\rho_0)o'(x) + C(x)$.

Dividing by $\rho_i-\rho_0$ gives

$h_i(x) = o'(x) + \lambda_i C(x)$,

where $\lambda_i = (\rho_i-\rho_0)^{-1}$.

This proves part 2.

#### Step 5: pairwise intersections are agreement sets with codewords

Take distinct $i,j$.

For any $x \in D_i \cap D_j$, part 2 gives

$h_i(x) = o'(x) + \lambda_i C(x)$,
and
$h_j(x) = o'(x) + \lambda_j C(x)$.

Subtracting,

$h_i(x)-h_j(x) = (\lambda_i-\lambda_j) C(x)$.

Since $\rho_i \ne \rho_j$, we also have $\lambda_i \ne \lambda_j$. Therefore, on $D_i \cap D_j$,

$C(x) = q_{ij}(x)$,

where

$q_{ij} = \frac{h_i-h_j}{\lambda_i-\lambda_j}$.

Because $h_i,h_j \in \operatorname{RS}[H^2,k']$, the quotient $q_{ij}$ also lies in $\operatorname{RS}[H^2,k']$.

Thus $C$ agrees with a Reed-Solomon codeword on all of $D_i \cap D_j$, so by definition of $\Gamma(C)$,

$|D_i \cap D_j| \le \Gamma(C)$.

This proves part 3. $\square$

---

## 3. Second-moment consequence

The previous lemma gives a clean packing inequality.

### Corollary
Let $\alpha = 31/64$, and let $\gamma = \Gamma(C)/N$.

If $\Gamma(C) < \alpha^2 N$, equivalently $\gamma < \alpha^2 = 961/4096$, then

$m \le \frac{\alpha-\gamma}{\alpha^2-\gamma}$.

In particular, under any bound of the form $\Gamma(C) \le \beta N$ with $\beta < 961/4096$, the number of non-reference successful parameters is $O(1)$.

### Proof

For each $x \in H^2$, let

$r(x) = |\{i : x \in D_i\}|$.

Then

$\sum_{x \in H^2} r(x) = \sum_{i=1}^m |D_i| > \alpha m N$.

Also,

$\sum_{x \in H^2} \binom{r(x)}{2} = \sum_{1 \le i < j \le m} |D_i \cap D_j| \le \Gamma(C)\binom{m}{2}$.

Now use the identity

$\sum_x \binom{r(x)}{2} = \frac12 \left(\sum_x r(x)^2 - \sum_x r(x)\right)$.

By Cauchy-Schwarz,

$\sum_x r(x)^2 \ge \dfrac{\left(\sum_x r(x)\right)^2}{N}$.

So if $M = \sum_x r(x)$, then

$\sum_x \binom{r(x)}{2} \ge \frac12\left(\frac{M^2}{N} - M\right)$.

Now $M > \alpha m N$. If $m \ge 2$, then $\alpha m > 1/2$, so the function $u \mapsto u^2/N - u$ is increasing at $u=M$. Hence

$\frac{M^2}{N} - M \ge \alpha^2 m^2 N - \alpha m N$.

Therefore

$\Gamma(C)\binom{m}{2} \ge \sum_x \binom{r(x)}{2} \ge \frac12\bigl(\alpha^2 m^2 N - \alpha m N\bigr)$.

Multiply by $2$:

$\Gamma(C)(m^2-m) \ge \alpha^2 m^2 N - \alpha m N$.

Rearrange:

$0 \ge (\alpha^2 N - \Gamma(C))m^2 - (\alpha N - \Gamma(C))m$.

Since $m>0$, this is

$0 \ge m\bigl((\alpha^2 N - \Gamma(C))m - (\alpha N - \Gamma(C))\bigr)$.

If $\alpha^2 N - \Gamma(C) > 0$, then

$m \le \frac{\alpha N - \Gamma(C)}{\alpha^2 N - \Gamma(C)} = \frac{\alpha-\gamma}{\alpha^2-\gamma}$.

This proves the corollary. $\square$

---

## 4. Exact obstruction: this plan cannot be completed using only generic RS agreement of $C$

This is the key point.

### Lemma
For every function $C : S_0 \to \mathbb{F}$, one always has

$\Gamma(C) \ge k' = \frac{N}{4}$.

### Proof

Choose any subset $A \subseteq S_0$ of size $k'$.

Because $|S_0| \ge T = 127N/128 > N/4 = k'$, such a subset exists.

The Reed-Solomon code $\operatorname{RS}[H^2,k']$ has dimension $k'$, and evaluation on any $k'$ distinct points is an isomorphism onto $\mathbb{F}^{A}$. Therefore there exists a unique codeword $q \in \operatorname{RS}[H^2,k']$ such that

$q(x) = C(x)$ for all $x \in A$.

Hence

$|\{x \in S_0 : q(x)=C(x)\}| \ge |A| = k'$,

so $\Gamma(C) \ge k'$. $\square$

### Numerical consequence

Now compare the two thresholds:

- the second-moment packing argument needs
  $\Gamma(C) < \alpha^2 N = \frac{961}{4096}N \approx 0.234619\,N$;

- but interpolation always gives
  $\Gamma(C) \ge k' = \frac14 N = \frac{1024}{4096}N = 0.25\,N$.

Since

$\frac{961}{4096} < \frac{1024}{4096}$,

the required inequality is universally impossible.

So there is a precise, rigorous obstruction:

> Any hard-regime argument that uses only the facts
> 1. $|D_i| > 31N/64$, and
> 2. $D_i \cap D_j$ is contained in an agreement set of $C$ with some Reed-Solomon codeword,
>
> cannot by itself yield a constant bound, because the generic interpolation lower bound on $\Gamma(C)$ is already above the critical second-moment threshold.

This is, I think, the cleanest formal explanation of the barrier noted informally in `notes.md`.

For the target parameter $N = 2^{19}$, the gap is

$\left(\frac14 - \frac{961}{4096}\right)N = \frac{63}{4096}N = 8064$

coordinates.

So a pairwise-intersection strategy would need to save at least $8064$ coordinates below the generic interpolation bound before the second-moment count can even start to force a constant bound.

---

## 5. A small extra structural identity that may be useful later

The codewords arising from pairwise intersections are not arbitrary.

For distinct $i,j$, define

$q_{ij} = \frac{h_i-h_j}{\lambda_i-\lambda_j} \in \operatorname{RS}[H^2,k']$.

Then for any distinct $i,j,k$,

$(\lambda_i-\lambda_j)q_{ij} + (\lambda_j-\lambda_k)q_{jk} + (\lambda_k-\lambda_i)q_{ki} = 0$.

This is immediate from the definition, since the left side is

$(h_i-h_j) + (h_j-h_k) + (h_k-h_i) = 0$.

So the family $\{q_{ij}\}$ satisfies a cocycle-type linear relation. This is one concrete piece of extra structure that is not captured by the raw bound $|D_i \cap D_j| \le \Gamma(C)$.

I do not yet see a complete argument from this identity alone, but it suggests a more promising direction: the $q_{ij}$ that approximate $C$ on the intersections come from a highly constrained low-rank family, not from an arbitrary list of Reed-Solomon codewords.

---

## 6. What this says about the current notes / proofs

I think the main thing that should be made explicit in the current writeup is:

- The hard-regime pairwise-intersection approach naturally leads to the parameter
  $\Gamma(C) = \max_q \operatorname{agr}(C,q)$.

- The second-moment threshold for constant packing is exactly $\Gamma(C) < (31/64)^2 N = 961N/4096$.

- But for any function $C$, one always has $\Gamma(C) \ge k' = N/4 = 1024N/4096$ by plain interpolation.

So if the intended hard-regime closure is “show $|D_i \cap D_j|$ is controlled by $\Gamma(C)$ and then apply counting,” that route is formally blocked unless one uses additional algebraic structure beyond generic RS agreement.

That is not just a heuristic issue; it is a rigorous obstruction.

---

## 7. Concrete next steps

Here are two next steps that now seem sharply formulated.

1. **Exploit structure of the family $q_{ij}$, not just their existence.**  
   The cocycle relation above is one simple identity. A stronger version might show that many large intersections force the $h_i$ to lie in a low-dimensional affine subspace, after which one could try to generalize the affine-line counting lemma.

2. **Strengthen intersection control in a way that beats interpolation.**  
   Since $\Gamma(C) \ge k'$, any successful argument must use more than “$D_i \cap D_j$ is an agreement set with some codeword.”  
   One needs an additional restriction, for example:
   - only certain codewords can arise as $q_{ij}$,
   - or the intersections $D_i \cap D_j$ are not arbitrary agreement sets,
   - or many pairwise intersections must be compatible in a way that forces an affine-line collapse.

If useful next round, I can try to turn the cocycle identity into a more explicit “low-dimensional affine-space reduction” statement for triples or quadruples of witnesses.