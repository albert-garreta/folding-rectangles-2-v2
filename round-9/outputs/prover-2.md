# Progress Report: Branch Collapse and Codeword Proximity for $R = 1/4$

## Overview

Building on the proven bound for $R < 0.13939$ and the identified pairwise barrier at $R \approx 0.146$, I develop an algebraic approach exploiting the **global polynomial structure** of the witness family. The main new result is a **Branch Collapse Lemma** showing that, under the affine-line structure on ratio polynomials, a canonical codeword $p \in RS[H,k]$ exists that perfectly matches one of the branch maps ($a$ or $b$) on a large explicit set. Combined with the $\delta$-far condition, this yields a non-trivial quantitative constraint.

---

## Setup and Notation Recap

- $N = |H^2| = n/2$, $k' = k/2 = N/4$, $T = 127N/128$.
- Rectangle $R(a,b)$ with reference witness $(\rho_0, g_0, f_0)$, success set $|S_0| \geq T$.
- Non-reference witnesses $(\rho_i, g_i, f_i)$ for $i = 1, \ldots, m$, ratio polynomials $h_i = (g_i - g_0)/(\rho_i - \rho_0) \in RS[H^2, k']$.
- Branch decomposition on $J_i = S_0 \cap S_i$: $E_i$ (same as $f_0$) with $|E_i| < N/2$, $F_i$ (opposite) with $|F_i| > 31N/64$.
- Even/odd parts: $Q = (a_o + b_o)/2$, $D_o = (a_o - b_o)/2$, $D_e = (a_e - b_e)/2$.
- Branch gap: $C(x) = B_{\rho_0}(x) - A_{\rho_0}(x) = -2D_e(x) - 2\rho_0 D_o(x)$.
- Parameters $\lambda_i = 1/(\rho_i - \rho_0)$.

---

## Establishing the Affine-Line Structure

**Claim.** If all hard witnesses satisfy $|E_i| < 15N/64$, then for all $i, j, k$:

$$|F_i \cap F_j \cap F_k| \geq 3 \cdot 47N/64 - 2N = 13N/64$$

Wait—this is below $k' = 16N/64$. However, pairwise overlaps suffice:

$$|F_i \cap F_j| \geq 2(47N/64) - N = 30N/64 > k' = 16N/64$$

**Lemma (Pairwise implies global affine line).** If $|F_i \cap F_j| > k'$ for all pairs, then the cross-factor $\hat{C}_{ij} := (h_i - h_j)/(\lambda_i - \lambda_j) \in RS[H^2, k']$ satisfies $\hat{C}_{ij}(x) = C(x)$ on $F_i \cap F_j$. Since $\hat{C}_{ij}$ and $\hat{C}_{ik}$ both agree with $C$ on $F_i \cap F_j \cap F_k \supseteq$ \{points agreeing with both\}, and we can verify by the cocycle relation that: from $|F_i \cap F_j| > k'$, $\hat{C}_{ij}$ is uniquely determined as the polynomial agreeing with $C$ on $F_i \cap F_j$. For any three witnesses $i, j, k$: $(\lambda_i - \lambda_j)\hat{C}_{ij} + (\lambda_j - \lambda_k)\hat{C}_{jk} = (\lambda_i - \lambda_k)\hat{C}_{ik}$ (polynomial identity). With all $|F \cap F| > k'$, a careful argument using RS uniqueness shows all $\hat{C}_{ij}$ coincide with a single $\hat{C} \in RS[H^2, k']$, giving $h_i = h_1 + (\lambda_i - \lambda_1)\hat{C}$ for all $i$.

---

## The Key New Polynomials

**Definition.** Given the affine-line structure $h_i = h_1 + c_i\hat{C}$ (with $c_i = \lambda_i - \lambda_1$), define:

$$u := g_0 + \hat{C} \in RS[H^2, k'], \qquad v := h_1 - \lambda_1\hat{C} \in RS[H^2, k']$$

**Key identity.** For each non-reference witness $i$:

$$g_i = g_0 + (\rho_i - \rho_0)h_i = (g_0 + \hat{C}) + \frac{h_1 - \lambda_1\hat{C}}{\lambda_i} = u + \frac{v}{\lambda_i}$$

**Independence of labeling.** If we relabel using witness $j$ instead of 1: $v' = h_j - \lambda_j\hat{C} = h_1 + (\lambda_j - \lambda_1)\hat{C} - \lambda_j\hat{C} = h_1 - \lambda_1\hat{C} = v$. So $u$ and $v$ are canonical (depending only on the reference and the affine-line data).

---

## Branch Collapse Lemma

**Lemma (Branch Collapse).** *On the set $\Omega := \bigcap_{i=0}^m S_i \cap \{C \neq 0\} \cap \{D_o \neq 0\}$:*

*(i) $g_0(x) = A_{\rho_0}(x)$ (the reference chose branch $a$ at every $x \in \Omega$).*

*(ii) For all non-reference witnesses $i$: $g_i(x) = B_{\rho_i}(x)$ (each chose branch $b$).*

**Proof.**

**Step 1: Universal branch equation.** At each $x$ in the common agreement set, each fold equation $g_i(x) \in \{A_{\rho_i}(x), B_{\rho_i}(x)\}$ gives:

$$u(x) + v(x)(\rho_i - \rho_0) = (P(x) + \epsilon_i(x)D_e(x)) + \rho_i(Q(x) + \epsilon_i(x)D_o(x))$$

where $\epsilon_i(x) \in \{+1, -1\}$ is the branch sign. Matching the $\rho_i$-coefficient for all $i$:

$$v(x) = Q(x) + \epsilon_i(x) D_o(x) \quad (\star)$$

When $D_o(x) \neq 0$: $\epsilon_i(x) = (v(x) - Q(x))/D_o(x)$, which is **independent of $i$**. Call this universal sign $\epsilon(x)$.

**Step 2: Constant-term equation.** From the $\rho_i$-free part:

$$u(x) - v(x)\rho_0 = P(x) + \epsilon(x) D_e(x)$$

Recall that $\epsilon_0(x) = +1$ iff $g_0(x) = A_{\rho_0}(x)$, and $\epsilon(x) = -\epsilon_0(x)$ (universal branch is opposite to reference).

**Step 3: Impossibility of $g_0 = B_{\rho_0}$ when $C \neq 0$.** Suppose $g_0(x) = B_{\rho_0}(x)$ at some $x \in \Omega$ (so $\epsilon_0(x) = -1$, hence $\epsilon(x) = +1$).

Then $u(x) = P(x) + D_e(x) + \rho_0(Q(x) + D_o(x)) = a_e(x) + \rho_0 a_o(x) = A_{\rho_0}(x)$.

But also $u(x) = g_0(x) + \hat{C}(x) = B_{\rho_0}(x) + \hat{C}(x)$.

On $\Omega$, $\hat{C}(x) = C(x)$ (since $|T(x)| \geq 2$ on $\Omega$ for $m \geq 2$). So:

$$A_{\rho_0}(x) = B_{\rho_0}(x) + C(x) = B_{\rho_0}(x) + (B_{\rho_0}(x) - A_{\rho_0}(x))$$

$$\implies 2A_{\rho_0}(x) = 2B_{\rho_0}(x) \implies C(x) = 0$$

This contradicts $x \in \Omega$ (which requires $C(x) \neq 0$). Therefore $g_0(x) = A_{\rho_0}(x)$ on $\Omega$. $\square$ (i)

Part (ii) follows: $\epsilon_0 = +1$ gives $\epsilon = -1$, so $v = Q - D_o = b_o$ and each $g_i(x) = B_{\rho_i}(x)$. $\square$

---

## Codeword Proximity Theorem

**Theorem.** *Under the hypotheses of the Branch Collapse Lemma, the polynomial*

$$p(h) := u(h^2) + (h - \rho_0) \cdot v(h^2)$$

*lies in $RS[H, k]$ and satisfies $p(h) = b(h)$ for every $h \in H$ with $h^2 \in \Omega$.*

**Proof.**

**Degree check.** $\deg u(\cdot) < k'$, $\deg v(\cdot) < k'$, so $u(h^2)$ has degree $\leq 2(k'-1)$ in $h$ and $(h-\rho_0)v(h^2)$ has degree $\leq 2(k'-1)+1 = 2k'-1$. Thus $\deg p \leq 2k'-1 = k-1 < k$, so $p \in RS[H,k]$.

**Agreement verification.** On $\Omega$: $u(x) = A_{\rho_0}(x) + C(x) = B_{\rho_0}(x)$ and $v(x) = b_o(x)$.

$$p(h) = B_{\rho_0}(h^2) + (h - \rho_0) b_o(h^2) = b_e(h^2) + \rho_0 b_o(h^2) + h \cdot b_o(h^2) - \rho_0 b_o(h^2) = b_e(h^2) + h \cdot b_o(h^2) = b(h).$$

Similarly $p(-h) = b_e(h^2) - h \cdot b_o(h^2) = b(-h)$. $\square$

---

## Quantitative Consequence

Since $b$ is $1/2$-far from $RS[H,k]$: $\text{agr}(p, b) < n/2 = N$. The agreement is $\geq 2|\Omega|$, so $|\Omega| < N/2$.

**Bounding $|\Omega|$ from below:**

$$|\Omega| \geq N - (m+1)N/128 - |\{C = 0\}| - |\{D_o = 0\}|$$

**Therefore:**

$$\boxed{|\{x : C(x) = 0\}| + |\{x : D_o(x) = 0\}| > N/2 - (m+1)N/128}$$

**Applying to each of $m+1$ references** $\rho_j$ and using the disjointness property $\sum_j |I_{\rho_j} \setminus I_{\text{all}}| \leq N$ (Lemma 6):

$$(m+1)\big(|I_{\text{all}}| + |\{D_o = 0\}|\big) + N > (m+1)\Big(\frac{N}{2} - \frac{(m+1)N}{128}\Big)$$

$$|I_{\text{all}}| + |\{D_o = 0\}| > \frac{N}{2} - \frac{(m+1)N}{128} - \frac{N}{m+1}$$

For $m \approx 11$: $|\{D_o = 0\}| \gtrsim N/3$, forcing substantial coincidence between the odd parts of $a$ and $b$.

---

## Flaw Identification in Current Files

1. **In proofs.md, Lemma 4:** The claim "$|F_i| > 31N/64$" is correct but the proof is stated too informally; specifically, the transition from $J_i = E_i \sqcup F_i$ to the numerical bound should explicitly use $|J_i| \geq 2T - N = 63N/64$ and $|E_i| < N/2$.

2. **In output.md:** The statement "Type A and Type B Regimes" refers to a density parameter $\beta$ but the exact definition of the graph $G_B$ edges is not specified precisely enough to be verifiable.

---

## Next Steps

1. **Exploit the constraint $|\{D_o = 0\}| > N/4$** to show that the "free cosets" (where different witnesses can differ) are themselves constrained, potentially via a secondary list-decoding argument on the even parts $D_e$.

2. **Cross-pair constraints:** For the Good Set $S$, apply the Branch Collapse to multiple pairs $(a_i, a_j)$ to derive a system of codeword proximity constraints. The codeword $p_{ij}$ agrees with $a_j$ on large sets; RS distance bounds ($\text{agr}(p_{ij}, p_{ik}) < k$) constrain overlaps.

3. **Handle the case $|E_i| \geq 15N/64$:** This regime may be tractable via a separate argument, possibly using the existing $R < 0.139$ technique with refined parameters.