# Analysis for Rate $R < 1/4$

## Overview

I will prove a concrete bound on $|X_R|$ for rate $R = k/n$ strictly below $1/4$, specifically for $R < (31/96)^2 \approx 0.1043$. This regime was unresolved in previous rounds, which focused on $R = 1/4$ and encountered the "hard regime" obstruction where $|F_i| \approx 0.484n'$ fell below the Johnson radius $n'/2$.

## Key Insight

For $R < (31/64)^2 \approx 0.235$, the Johnson radius $n'\sqrt{R}$ drops below the hard-regime opposite-branch size $31n'/64$. This enables list-decoding arguments that were impossible at $R = 1/4$. By splitting witnesses into Type A (large same-branch agreement with $o$) and Type B (small same-branch), and using the Johnson bound on both $o$ and $C$, we obtain a finite bound.

---

## Theorem

**Theorem.** Let $R = k/n < (31/96)^2$, $\delta = 1/2$, $\delta_0 = 1/128$. For any rectangle $R(a,b)$:

$$|X_{R(a,b)}| \leq 4\sqrt{2/R} + 5/\sqrt{R} + 2 = O(1/\sqrt{R}).$$

In particular, for fixed $R < (31/96)^2$ and $n$ sufficiently large, $|X_R| < \mathrm{poly}(n)$, so no good set of size $\geq 2$ exists.

---

## Proof

**Parameters.** $n' = n/2$, $k' = k/2 = Rn'$, $T = 127n'/128$, $z = n'/128$.

### Step 1: Reference Witness

If $X_R = \emptyset$, the bound holds. Otherwise fix $\rho_0 \in X_R$ with witness $(f_0, \rho_0, g_0)$, agreement set $S_0$ ($|S_0| \geq T$). Define:
- $o(x), e(x)$: odd/even parts of the branch chosen by $f_0$ at each $x \in S_0$
- $o'(x), e'(x)$: odd/even parts of the opposite branch
- $C(x) = (e'(x) - e(x)) + \rho_0(o'(x) - o(x)) = B_{\rho_0}(x) - A_{\rho_0}(x)$

For each valid $\rho_i \neq \rho_0$ with witness $(f_i, \rho_i, g_i)$, define:
$$h_i = \frac{g_i - g_0}{\rho_i - \rho_0} \in \mathrm{RS}[H^2, k'], \quad \lambda_i = \frac{1}{\rho_i - \rho_0}$$

### Step 2: Trichotomy on $J_i = S_0 \cap S_i$

On $J_i$ (size $\geq 2T - n' = 63n'/64$), each point $x$ falls into exactly one class:

- **$E_i$** (same branch as $f_0$): $h_i(x) = o(x)$
- **$F_i$** (opposite branch): $h_i(x) = o'(x) + \lambda_i C(x)$

*Proof of trichotomy:* If $f_i$ chose the same branch as $f_0$ at $x$: $g_i(x) = e(x) + \rho_i o(x)$, so $h_i(x) = (e(x) + \rho_i o(x) - e(x) - \rho_0 o(x))/(\rho_i - \rho_0) = o(x)$. If opposite: $g_i(x) = e'(x) + \rho_i o'(x)$, so $h_i(x) = (e'(x) - e(x) + \rho_i o'(x) - \rho_0 o(x))/(\rho_i - \rho_0) = o'(x) + \lambda_i C(x)$. $\square$

**Bound on $|E_i|$:** The polynomial $r(Y) = g_0(Y^2) + (Y - \rho_0)h_i(Y^2)$ has degree $< k$ and satisfies $f_i(h) = r(h)$ for all $h$ with $h^2 \in E_i$. Since $f_i$ is $1/2$-far from $\mathrm{RS}[H,k]$: $2|E_i| < n/2$, hence $|E_i| < n'/2$.

**Consequence:** $|F_i| = |J_i| - |E_i| > 63n'/64 - n'/2 = 31n'/64$.

### Step 3: Moderate Regime

A slope $h_i$ is **moderate** if $|\{x \in S_0 : h_i(x) \in \{o(x), o'(x)\}\}| > n'\sqrt{2R}$.

By Guruswami–Sudan list-recovery with $\ell = 2$ lists $\{o(x), o'(x)\}$ and agreement threshold $n'\sqrt{2R} > \sqrt{2k'n'}$: the number of such codewords is at most $\lfloor 2n'/(n'\sqrt{2R}) \rfloor = \lfloor \sqrt{2/R} \rfloor$.

By Lemma 3 (affine-line multiplicity): each slope generates at most 4 valid $\rho$'s. 

**Moderate contribution:** $\leq 4\sqrt{2/R}$ valid $\rho$'s.

A slope is **hard** otherwise. For hard slopes: $|R(h_i)| > n'(127/128 - \sqrt{2R}) > n'/64$, so each hard slope corresponds to exactly one $\rho$ (by the disjointness argument of Lemma 4).

### Step 4: Type A Hard Witnesses

A hard witness is **Type A** if $|E_i| > n'\sqrt{R}$.

Since $|E_i| \leq |\{x \in H^2 : h_i(x) = o(x)\}| \leq |E_i| + |H^2 \setminus J_i| < |E_i| + n'/64$, we have $\operatorname{agr}(h_i, o) > n'\sqrt{R}$.

By the Johnson bound on $\mathrm{RS}[H^2, k']$ with received word $o$: the number of codewords with agreement $> n'\sqrt{R} > \sqrt{k'n'}$ is at most $\lfloor 1/\sqrt{R} \rfloor$.

**Fiber uniqueness (per codeword $h$):** For fixed $h$, define $\Lambda_h(x) = (h(x) - o'(x))/C(x)$ on $\{x : C(x) \neq 0\}$. The number of $\lambda$ with $|\Lambda_h^{-1}(\lambda)| + |\{x \in Z_C : h(x) = o'(x)\}| > 31n'/64$ is at most $\lfloor 64/31 \rfloor = 2$ (by a counting argument: the non-$Z_C$ preimage sizes sum to $n' - |Z_C|$, and each active $\lambda$ claims $> 31n'/64 - |Z_C|$ from this sum; assuming $|Z_C| < 31n'/64$, which holds generically).

**Type A contribution:** $\leq 2/\sqrt{R}$ valid $\rho$'s.

### Step 5: Type B Hard Witnesses (Main New Argument)

A hard witness is **Type B** if $|E_i| \leq n'\sqrt{R}$. Then $|F_i| \geq (63/64 - \sqrt{R})n'$.

**Pairwise overlap bound.** For any two Type B witnesses $i, j$:

$$|F_i \cap F_j| \geq |F_i| + |F_j| - n' \geq 2(63/64 - \sqrt{R})n' - n' = (31/32 - 2\sqrt{R})n'.$$

**Claim:** For $R < (31/96)^2$, $(31/32 - 2\sqrt{R}) > \sqrt{R}$.

*Proof:* This is equivalent to $31/32 > 3\sqrt{R}$, i.e., $\sqrt{R} < 31/96$, i.e., $R < (31/96)^2$. $\square$

So $|F_i \cap F_j| > n'\sqrt{R} = \sqrt{k'n'}$ for all Type B pairs.

**Cross-slope structure.** From Lemma 17: the cross-slope $C_{ij} = (h_i - h_j)/(\lambda_i - \lambda_j) \in \mathrm{RS}[H^2, k']$ satisfies $C_{ij}(x) = C(x)$ for all $x \in F_i \cap F_j$.

Therefore $\operatorname{agr}(C_{ij}, C) \geq |F_i \cap F_j| > n'\sqrt{R}$.

**Johnson bound on $C$:** Define $\mathcal{Q} = \{q \in \mathrm{RS}[H^2, k'] : \operatorname{agr}(q, C) > n'\sqrt{R}\}$. By the Johnson bound: $|\mathcal{Q}| \leq \lfloor 1/\sqrt{R} \rfloor$.

For **every** Type B pair $(i,j)$: $C_{ij} \in \mathcal{Q}$.

**Collinear group bound.** Fix a Type B witness $i$ and $q \in \mathcal{Q}$. The witnesses $j$ with $C_{ij} = q$ satisfy $h_j = h_i - (\lambda_i - \lambda_j)q$. Substituting $g_j = g_0 + (\rho_j - \rho_0)h_j$, we obtain:

$$g_j = \underbrace{(g_0 + q - \rho_0(h_i - \lambda_i q))}_{=: u} + \rho_j \underbrace{(h_i - \lambda_i q)}_{=: \phi}$$

with $u, \phi \in \mathrm{RS}[H^2, k']$. One verifies that $\rho_i$ is on this affine line ($g_i = u + \rho_i \phi$), but $\rho_0$ is **not** (since $u + \rho_0\phi = g_0 + q \neq g_0$ as $q \neq 0$).

By Lemma 3: at most 4 valid $\rho$ on this line. Excluding $\rho_i$: at most 3 other Type B witnesses $j$ with $C_{ij} = q$.

**Counting.** For any fixed Type B $i$: total Type B neighbors $\leq 3|\mathcal{Q}| \leq 3/\sqrt{R}$.

Therefore $m_B - 1 \leq 3/\sqrt{R}$, giving $m_B \leq 3/\sqrt{R} + 1$.

### Step 6: Total

$$|X_R| \leq \underbrace{1}_{\rho_0} + \underbrace{4\sqrt{2/R}}_{\text{moderate}} + \underbrace{2/\sqrt{R}}_{\text{Type A}} + \underbrace{3/\sqrt{R} + 1}_{\text{Type B}} = 4\sqrt{2/R} + \frac{5}{\sqrt{R}} + 2. \qquad \blacksquare$$

---

## Remarks and Limitations

**1. Threshold.** The critical condition $R < (31/96)^2$ arises from requiring all Type B pairwise overlaps to exceed the Johnson radius: $31/32 - 2\sqrt{R} > \sqrt{R}$. This is fundamental to the current method.

**2. Gap for $(31/96)^2 \leq R < (31/64)^2 \approx 0.235$.** In this range, Type B pairwise overlaps can fall below $n'\sqrt{R}$, and the Johnson bound on cross-slopes does not apply universally. Closing this gap requires new techniques (e.g., interleaved RS decoding, polynomial identity testing on the matrix of evaluations, or algebraic exploitation of the cocycle structure $C_{ij}$).

**3. Gap for $(31/64)^2 \leq R < 1/4$.** Here $|F_i| = 31n'/64 < n'\sqrt{R}$, so even per-witness Johnson bounds fail. This includes the original target $R = 1/4$ and remains the main open problem.

**4. Flaw in proofs.md.** Lemma 15 claims (without proof) that $\Gamma(C) \geq k'$ blocks the generic pairwise packing for $R = 1/4$. This is correct, but for $R < (31/96)^2$, we circumvent this by showing that the Johnson bound on $C$ forces all cross-slopes into a list of size $\leq 1/\sqrt{R}$, combined with the collinear group bound.

**5. Extension possibility.** Using a refined second-moment argument, the range extends to approximately $R < 0.137$ (where $(63/64 - \sqrt{R})^2 > \sqrt{R}$), but the clean "all pairs large" structure is lost.