## What I checked first

There are two file-quality issues worth flagging before the new mathematics.

1. `output.md` is badly corrupted near the end and currently contains unrelated non-mathematical text. It is not auditable in its present form.

2. In the draft lemma labeled “Lemma 13” in the task statement, the last numerical step
   `$130/62 \approx 2.09 \le 2$`
   is false. So that lemma cannot be used as written.

The new argument below is designed to be independent of those corrupted portions.

---

## Main new progress

I think there is a clean way to push the proven rate regime strictly beyond the previously recorded threshold $r < (31/96)^2 \approx 0.104$.

The new bound I get is:

- for every rate
  $r = k/n = k'/n' < r_*$
- where
  $r_* = \left(\frac{95 - 8\sqrt{79}}{64}\right)^2 \approx 0.13939$,

one gets a constant bound $|X_{R(a,b)}| = O_r(1)$ for every rectangle.

What is nice is that this proof seems to bypass the old moderate/hard split entirely once a single reference witness is fixed. It uses only:

- the clean affine-line multiplicity lemma already in `proofs.md` (Lemma 3 there),
- a simple “fractional Johnson” counting lemma for subsets,
- and the basic same-branch / opposite-branch decomposition relative to a reference witness.

So this looks both stronger and cleaner.

---

## Notation for this round

Let

- $N = n' = |H^2|$,
- $r = k'/N = k/n$,
- $T = 127N/128$,
- $A = 2T/N - 1 = 63/64$.

Thus for any two successful witnesses, the overlap of their good folding sets is at least $AN$.

Fix a rectangle $R(a,b)$. Assume $X := X_{R(a,b)}$ is nonempty, and choose one reference element $\rho_0 \in X$ with a corresponding witness triple $(f_0,\rho_0,g_0)$ and agreement set $S_0 \subseteq H^2$, with $|S_0| \ge T$.

For each other $\rho_i \in X \setminus \{\rho_0\}$, choose one witness triple $(f_i,\rho_i,g_i)$ and let

- $S_i$ be its agreement set, so $|S_i| \ge T$,
- $J_i = S_0 \cap S_i$, so $|J_i| \ge 2T-N = AN$,
- $\lambda_i = 1/(\rho_i-\rho_0)$,
- $h_i = (g_i-g_0)/(\rho_i-\rho_0) \in RS[H^2,k']$.

---

## Lemma 1: fractional Johnson bound for subsets

**Claim.** Let $U$ be a finite set of size $N$. Let $A_1,\dots,A_m \subseteq U$ satisfy

- $|A_i| \ge \alpha N$ for every $i$,
- $|A_i \cap A_j| \le \beta N$ for every $i \ne j$,

with $\alpha^2 > \beta$.

Then
$ m \le \frac{\alpha-\beta}{\alpha^2-\beta}$.

### Proof

For each $x \in U$, define
$r_x = |\{i : x \in A_i\}|$.

Then

- $\sum_{x \in U} r_x = \sum_{i=1}^m |A_i| \ge m\alpha N$.

By Cauchy–Schwarz,

- $\sum_{x \in U} r_x^2 \ge \frac{(\sum_x r_x)^2}{N} \ge m^2 \alpha^2 N$.

Now
$\sum_{1 \le i < j \le m} |A_i \cap A_j| = \sum_{x \in U} \binom{r_x}{2} = \frac{1}{2}\left(\sum_x r_x^2 - \sum_x r_x\right)$.

Hence

- $\sum_{1 \le i < j \le m} |A_i \cap A_j| \ge \frac{1}{2}(m^2\alpha^2 - m\alpha)N$.

On the other hand, the pairwise intersection hypothesis gives

- $\sum_{1 \le i < j \le m} |A_i \cap A_j| \le \beta N \binom{m}{2} = \frac{1}{2}\beta m(m-1)N$.

Comparing the two bounds and dividing by $\frac{1}{2}mN > 0$, we get

- $m\alpha^2 - \alpha \le \beta(m-1)$.

So

- $m(\alpha^2-\beta) \le \alpha-\beta$.

Since $\alpha^2 > \beta$, we may divide and obtain

- $m \le \frac{\alpha-\beta}{\alpha^2-\beta}$.

This proves the lemma. ∎

---

## Corollary 2: explicit list bound for Reed–Solomon at agreement $>\sqrt r$

This is the same counting lemma applied to agreement sets of codewords with a fixed received word.

**Claim.** Let $w : H^2 \to \mathbb F$ be arbitrary. Let $q_1,\dots,q_m \in RS[H^2,k']$ be distinct codewords, each agreeing with $w$ on at least $\beta N$ coordinates, where $\beta^2 > r$.

Then
$ m \le L_r(\beta) := \frac{\beta-r}{\beta^2-r}$.

### Proof

For each $i$, let
$A_i = \{x \in H^2 : q_i(x) = w(x)\}$.

Then $|A_i| \ge \beta N$.

If $i \ne j$, then on $A_i \cap A_j$ we have $q_i = q_j$. Since $q_i-q_j$ is a nonzero polynomial of degree $< k'$, it has at most $k'-1 < rN$ zeros on $H^2$. Therefore
$|A_i \cap A_j| < rN$,
and in particular
$|A_i \cap A_j| \le rN$.

Apply Lemma 1 with $\alpha=\beta$ and $\beta=r$. We obtain
$ m \le \frac{\beta-r}{\beta^2-r}$.

This proves the corollary. ∎

### Comment

This gives an elementary substitute for Guruswami–Sudan in the range $\beta > \sqrt r$. I think this is useful in its own right.

---

## Lemma 3: direct reference decomposition into same-branch and opposite-branch sets

This is the structural piece that seems to make the rest go through cleanly.

**Claim.** For each witness index $i$, there exists a partition
$J_i = E_i \sqcup F_i$
such that:

1. $|J_i| \ge AN = 63N/64$.

2. On $E_i$, one has $h_i = o$.

3. On $F_i$, one has $h_i = o' + \lambda_i C$ for a fixed received word $C : H^2 \to \mathbb F$ depending only on the reference witness, not on $i$.

4. $|E_i| < N/2$.

Consequently, for every $i$,
$|F_i| > AN - N/2 = 31N/64$.

### Proof

For each $x \in S_0$, let the branch used by the reference witness $f_0$ be called the “reference branch”. Denote its even/odd parts at $x$ by $e(x), o(x)$. Denote the other branch’s even/odd parts by $e'(x), o'(x)$.

Define
$C(x) = e'(x)-e(x) + \rho_0 (o'(x)-o(x))$.

Now fix $i$. Since $|S_0|, |S_i| \ge T$, we have
$|J_i| = |S_0 \cap S_i| \ge 2T-N = AN$.

For each $x \in J_i$, there are two cases.

### Case 1: same branch

Suppose witness $i$ also uses the reference branch at $x$. Then
$g_0(x) = e(x) + \rho_0 o(x)$
and
$g_i(x) = e(x) + \rho_i o(x)$.

Subtracting gives
$g_i(x)-g_0(x) = (\rho_i-\rho_0)o(x)$.

By definition of $h_i$,
$(\rho_i-\rho_0)h_i(x) = g_i(x)-g_0(x)$,
so
$h_i(x) = o(x)$.

Let $E_i$ be the set of such $x$.

### Case 2: opposite branch

Suppose witness $i$ uses the opposite branch at $x$. Then
$g_i(x) = e'(x) + \rho_i o'(x)$.

So
$(\rho_i-\rho_0)h_i(x) = g_i(x)-g_0(x) = e'(x)-e(x) + \rho_i o'(x) - \rho_0 o(x)$.

Rewrite the right-hand side as
$(\rho_i-\rho_0)o'(x) + C(x)$.

Hence
$h_i(x) = o'(x) + \lambda_i C(x)$,
where $\lambda_i = 1/(\rho_i-\rho_0)$.

Let $F_i$ be the set of such $x$.

This proves $J_i = E_i \sqcup F_i$ and the asserted formulas on the two parts.

It remains to show $|E_i| < N/2$.

On $E_i$, we have $h_i=o$, so the codeword
$p_i(Y) = (g_0 - \rho_0 h_i)(Y^2) + Y h_i(Y^2)$
matches the reference witness $f_0$ on both roots above each $x \in E_i$. Therefore
$\operatorname{agr}(f_0,p_i) \ge 2|E_i|$.

Since $f_0$ is $1/2$-far from $RS[H,k]$, it cannot agree with any codeword on $n/2$ or more coordinates. Hence
$2|E_i| < n/2$,
that is,
$|E_i| < n/4 = N/2$.

Therefore
$|F_i| = |J_i|-|E_i| > AN - N/2 = 31N/64$.

This proves the lemma. ∎

---

## Type A / Type B split

Fix a real number $\beta$ satisfying

- $\sqrt r < \beta < 1/2$,
- and later we will also require $(A-\beta)^2 > \beta$.

We split the non-reference witnesses into:

- **Type A:** $|E_i| > \beta N$,
- **Type B:** $|E_i| \le \beta N$.

Let
$\alpha = A-\beta = 63/64 - \beta$.

Then every Type B witness satisfies
$|F_i| \ge \alpha N$.

---

## Lemma 4: Type A witnesses are constant in number

**Claim.** The number of Type A witnesses is at most
$4L_r(\beta) = 4\frac{\beta-r}{\beta^2-r}$.

### Proof

If $i$ is Type A, then by Lemma 3 the codeword $h_i$ agrees with the received word $o$ on more than $\beta N$ points.

By Corollary 2, there are at most $L_r(\beta)$ distinct possible codewords $h_i$.

Now fix one such codeword $h$. Any witness with this slope satisfies
$g = g_0 + (\rho-\rho_0)h = (g_0-\rho_0 h) + \rho h$.

So all corresponding pairs $(\rho,g)$ lie on one affine line in the $(\rho,g)$-parameterization. By the already proved affine-line multiplicity lemma from `proofs.md` (Lemma 3 there), there are at most $4$ such parameters $\rho$.

Therefore the total number of Type A witnesses is at most
$4L_r(\beta)$.

∎

---

## Lemma 5: bounded degree in the Type B overlap graph

Define a graph $G_B$ on the Type B witnesses by joining $i$ and $j$ if
$|F_i \cap F_j| > \beta N$.

**Claim.** Every vertex of $G_B$ has degree at most
$3L_r(\beta)$.

### Proof

Fix a Type B witness $i$.

For any neighbor $j$ of $i$, define
$C_{ij} = \frac{h_i-h_j}{\lambda_i-\lambda_j}$.

This is a codeword in $RS[H^2,k']$ because $h_i,h_j$ are codewords and $\lambda_i \ne \lambda_j$.

Now on $F_i \cap F_j$, Lemma 3 gives

- $h_i = o' + \lambda_i C$,
- $h_j = o' + \lambda_j C$.

Subtracting,
$h_i - h_j = (\lambda_i-\lambda_j)C$.

Hence on $F_i \cap F_j$,
$C_{ij} = C$.

Since $j$ is a neighbor of $i$, we have $|F_i \cap F_j| > \beta N$. Thus $C_{ij}$ agrees with the fixed received word $C$ on more than $\beta N$ coordinates.

By Corollary 2, there are at most $L_r(\beta)$ possible values of $C_{ij}$ as $j$ varies over the neighbors of $i$.

So it remains to show that for each fixed codeword $c$, there are at most $3$ neighbors $j$ with $C_{ij}=c$.

Fix such a codeword $c$. Then for every such $j$,
$h_j = h_i + (\lambda_j-\lambda_i)c$.

Define
$\phi = h_i - \lambda_i c$
and
$u = g_0 + c - \rho_0 \phi$.

Then for every such $j$,
$g_j = g_0 + (\rho_j-\rho_0)h_j$,
and using $(\rho_j-\rho_0)\lambda_j=1$, we compute
$g_j = g_0 + (\rho_j-\rho_0)(\phi + \lambda_j c) = g_0 + (\rho_j-\rho_0)\phi + c = u + \rho_j \phi$.

So all these witnesses lie on the same affine line $u+\rho\phi$.

Also $\rho_i$ itself lies on this same line, because
$u + \rho_i \phi = g_i$.

By the affine-line multiplicity lemma (Lemma 3 in `proofs.md`), there are at most $4$ valid parameters on this line in total. Since one of them is $\rho_i$, there are at most $3$ others.

Thus each of the at most $L_r(\beta)$ possible values of $c$ contributes at most $3$ neighbors, and therefore
$\deg_{G_B}(i) \le 3L_r(\beta)$.

This proves the claim. ∎

---

## Lemma 6: any independent set of Type B witnesses is constant in size

**Claim.** Assume $\alpha^2 > \beta$. Then every independent set in $G_B$ has size at most
$\frac{\alpha-\beta}{\alpha^2-\beta}$.

### Proof

Let $I$ be an independent set of vertices in $G_B$.

By definition of independence, if $i \ne j$ are in $I$, then
$|F_i \cap F_j| \le \beta N$.

Since every Type B witness satisfies $|F_i| \ge \alpha N$, the family $\{F_i : i \in I\}$ satisfies the hypotheses of Lemma 1.

Therefore
$|I| \le \frac{\alpha-\beta}{\alpha^2-\beta}$.

∎

---

## Proposition 7: explicit constant bound for all witnesses

**Claim.** Suppose $\beta$ satisfies

- $\sqrt r < \beta < 1/2$,
- $\alpha = 63/64 - \beta$,
- $\alpha^2 > \beta$.

Then
$|X| \le 1 + 4L_r(\beta) + (3L_r(\beta)+1)\frac{\alpha-\beta}{\alpha^2-\beta}$.

In particular, $|X| = O_r(1)$.

### Proof

We already bounded the number of Type A witnesses by $4L_r(\beta)$.

Now consider the Type B graph $G_B$.

From Lemma 5, its maximum degree satisfies
$\Delta(G_B) \le 3L_r(\beta)$.

From Lemma 6, its independence number satisfies
$\alpha(G_B) \le \frac{\alpha-\beta}{\alpha^2-\beta}$.

Any graph with maximum degree $\Delta$ is $(\Delta+1)$-colorable, so one color class has size at least $|V|/(\Delta+1)$. Equivalently,
$|V| \le (\Delta+1)\alpha(G)$.

Applying this to $G_B$ gives
$|V(G_B)| \le (3L_r(\beta)+1)\frac{\alpha-\beta}{\alpha^2-\beta}$.

Finally, add the reference witness $\rho_0$. Thus
$|X| \le 1 + 4L_r(\beta) + (3L_r(\beta)+1)\frac{\alpha-\beta}{\alpha^2-\beta}$.

This proves the proposition. ∎

---

## The new rate threshold

The proposition applies whenever there exists $\beta$ with

- $\sqrt r < \beta$,
- and $(63/64 - \beta)^2 > \beta$.

Since the function
$f(\beta) = (63/64 - \beta)^2 - \beta$
is strictly decreasing on $[0,1]$, such a $\beta$ exists if and only if
$\sqrt r < \beta_*$,
where $\beta_*$ is the smaller root of
$(63/64 - \beta)^2 = \beta$.

Solving,
$\beta_* = \frac{95 - 8\sqrt{79}}{64} \approx 0.373351$.

Therefore the method proves the following.

---

## Theorem 8: improved local rectangle bound for all rates below about $0.13939$

**Claim.** Let $r = k/n = k'/n'$. If
$r < r_* := \left(\frac{95 - 8\sqrt{79}}{64}\right)^2 \approx 0.13939$,
then for every rectangle $R(a,b)$ one has
$|X_{R(a,b)}| = O_r(1)$.

### Proof

Choose any $\beta$ with
$\sqrt r < \beta < \beta_*$.

Then by definition of $\beta_*$,
$(63/64 - \beta)^2 > \beta$.

So the hypotheses of Proposition 7 are satisfied, and therefore $|X_{R(a,b)}|$ is bounded by a constant depending only on $r$.

∎

---

## Why I think this is a real improvement

The previous verified milestone in the notes/verifier summary was the regime
$r < (31/96)^2 \approx 0.104$.

The argument above raises that to
$r < 0.13939$.

Also, the proof is quite clean:

- no interleaved-RS machinery,
- no cocycle argument,
- no moderate/hard split appears necessary in the proved range,
- and the only nontrivial previously proved input is the affine-line multiplicity lemma.

So I think this is a substantial simplification as well as an improvement in range.

---

## Important obstacle: this method seems intrinsically capped near $0.146$

This is also useful to record, because it says what must change if we want to approach $1/4$.

The only place the rate enters is through the existence of $\beta$ satisfying

- $\beta > \sqrt r$,
- and $(A-\beta)^2 > \beta$ with $A = 1-2\delta_0$.

In our case $A=63/64$.

Even in the hypothetical best case $\delta_0=0$, one would only get $A=1$, so the condition becomes
$(1-\beta)^2 > \beta$.

The smaller root is
$\beta = \frac{3-\sqrt{5}}{2} \approx 0.381966$,
which means
$r < \left(\frac{3-\sqrt{5}}{2}\right)^2 \approx 0.1459$.

So:

- this entire “Type A / Type B + pairwise fractional-Johnson + affine-line multiplicity” mechanism cannot possibly get anywhere near $r=1/4$;
- it tops out below $0.146$, even if $\delta_0$ were ideal.

I think this is the right diagnosis of where the next genuinely new idea is needed.

---

## Small numerical sanity checks

- If $r=0.13$, then $\sqrt r \approx 0.3606$. Taking $\beta=0.37$ gives
  $\alpha = 63/64 - 0.37 = 0.614375$,
  and $\alpha^2 \approx 0.3775 > 0.37$.
  So the theorem applies.

- If $r=0.15$, then $\sqrt r \approx 0.3873$. Any admissible $\beta$ must exceed $0.3873$, but then
  $\alpha = 63/64 - \beta < 0.5971$,
  so $\alpha^2 < 0.3566 < \beta$.
  Hence this method fails there, exactly as the theoretical cap predicts.

These checks are consistent with the threshold $r_* \approx 0.13939$.

---

## Suggested next steps

1. **Audit-ready insertion into the proof pipeline.**
   The cleanest thing to verify next is Proposition 7 above, since it depends only on:
   - the reference decomposition in Lemma 3 here,
   - the already established affine-line multiplicity lemma,
   - and the elementary subset-packing Lemma 1.

2. **Use this to replace the corrupted theorem section.**
   Right now the theorem in `proofs.md` is unreadable. The argument above is short enough to stand as a clean replacement.

3. **For progress beyond $0.13939$, do not push this same mechanism harder.**
   The cap near $0.146$ shows that pairwise overlap information is not enough. The next step must exploit some stronger algebraic dependence among the family of cross-factors $C_{ij}$, probably via:
   - triple relations,
   - low-rank/interleaving structure,
   - or a global affine-dimension collapse.

If useful next round, I can try to formalize Proposition 7 into a file-ready theorem statement with every dependency spelled out exactly.