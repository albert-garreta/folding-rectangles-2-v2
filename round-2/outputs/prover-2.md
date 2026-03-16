# Analysis of the Hard Regime and Strengthened Per-Codeword Bound

## Overview

I carefully analyze the hard regime identified in previous rounds and prove a **strengthened per-codeword bound** $|W(g)| \le 2$, improving on the previously claimed $|W(g)| \le 4$. I also identify the precise remaining gap and clarify the collinear/non-collinear case structure.

---

## 1. Strengthened Per-Codeword Bound

### Lemma (Per-Codeword Bound): $|W(g)| \le 2$

**Statement.** Fix a rectangle $R(a,b)$ and any codeword $g \in RS[H^2, k']$. Let
$$W(g) = \{\rho \in \mathbb{F} : \exists f \in \mathcal{F}(R),\; f \text{ is } \tfrac{1}{2}\text{-far from } RS[H,k],\; \operatorname{agr}(\mathrm{Fold}[f,\rho],g) \ge T\}$$
where $T = (1 - 1/128)n' = 127n'/128$. Then $|W(g)| \le 2$.

**Proof.** Define $\hat{g}(h) = g(h^2) \in RS[H,k]$ (this has degree $< 2k' = k$).

**Step 1: Define the "free" set and bound its components.**

Define:
- $Z_a = \{x \in H^2 : a_o(x) = 0 \text{ and } g(x) = a_e(x)\}$
- $Z_b = \{x \in H^2 : b_o(x) = 0 \text{ and } g(x) = b_e(x)\}$
- $Z = Z_a \cup Z_b$, $U = H^2 \setminus Z$

**Claim 1:** $|Z_a| < n'/2$ and $|Z_b| < n'/2$.

*Proof.* Consider $a$, which is $\frac{1}{2}$-far from $RS[H,k]$, so $\operatorname{agr}(a, p) < n/2 = n'$ for all $p \in RS[H,k]$. At each $x \in Z_a$: $a_o(x) = 0$ implies $a(h) = a(-h) = a_e(x)$, and $g(x) = a_e(x)$ implies $\hat{g}(h) = \hat{g}(-h) = g(x) = a_e(x)$. So $a(\pm h) = \hat{g}(\pm h)$, yielding $\operatorname{agr}(a, \hat{g}) \ge 2|Z_a|$. Since $a$ is $\frac{1}{2}$-far: $2|Z_a| < n'$, i.e., $|Z_a| < n'/2$. Identically for $b$ and $Z_b$. $\square$

**Step 2: Incidence bound (valid for $|Z| < T$).**

For $x \in U$: the equation $g(x) \in \{A_\rho(x), B_\rho(x)\}$ is equivalent to:
$$(g(x) - a_e(x) - \rho a_o(x))(g(x) - b_e(x) - \rho b_o(x)) = 0$$
which is quadratic in $\rho$, giving **at most 2** solutions per $x$.

For each $\rho \in W(g)$: the agreement set $S_\rho = \{x : g(x) \in \{A_\rho(x), B_\rho(x)\}\}$ satisfies $|S_\rho| \ge T$. Since $S_\rho \cap Z \subseteq Z$: $|S_\rho \cap U| \ge T - |Z|$.

Total incidences $\sum_{\rho \in W(g)} |S_\rho \cap U| \le 2|U| = 2(n' - |Z|)$.

Therefore:
$$|W(g)| \cdot (T - |Z|) \le 2(n' - |Z|) \quad \implies \quad |W(g)| \le \frac{2(n' - |Z|)}{T - |Z|}. \tag{$\star$}$$

**Step 3: Exception bound (valid for $|Z| > n'/2$).**

Fix $\rho \in W(g)$ with far witness $f_\rho$. We lower-bound $\operatorname{agr}(f_\rho, \hat{g})$.

*Key structure:* $I_{\text{all}} = \{x : a_e(x)=b_e(x), a_o(x)=b_o(x)\}$. At $x \in I_{\text{all}} \cap Z_a$: $a_o=b_o=0$ and $a_e=b_e=g(x)$, so $x \in Z_b$. Hence $I_{\text{all}} \cap (Z \setminus (Z_a \cap Z_b)) = \emptyset$.

At $x \in Z_a \setminus Z_b$ with $x \notin I_\rho$: $A_\rho(x) = a_e(x) = g(x)$ but $B_\rho(x) \neq A_\rho(x)$, so $f_\rho$ is **forced** to choose branch $a$. Then $f_\rho(\pm h) = a_e(x) = \hat{g}(\pm h)$ (contributing 2 to agreement). Similarly for $x \in Z_b \setminus Z_a$ with $x \notin I_\rho$.

At $x \in Z_a \cap Z_b$: $a(\pm h) = b(\pm h) = g(x) = \hat{g}(\pm h)$, so agreement is 2 regardless of branch.

Define $c(\rho) = |(Z \setminus (Z_a \cap Z_b)) \cap I_\rho|$. These are "exception" positions where the adversary can choose the non-matching branch. In the worst case, agreement at exceptions is 0.

Therefore:
$$\operatorname{agr}(f_\rho, \hat{g}) \ge 2(|Z| - c(\rho)).$$

Since $f_\rho$ is $\frac{1}{2}$-far: $2(|Z| - c(\rho)) < n'$, giving $c(\rho) > |Z| - n'/2$.

**Claim 2:** $\sum_{\rho \in W(g)} c(\rho) \le n'$.

*Proof.* Since $I_{\text{all}} \cap (Z \setminus (Z_a \cap Z_b)) = \emptyset$, we have $c(\rho) \le |I_\rho \setminus I_{\text{all}}|$. By Lemma 6 (from proofs.md), the sets $\{I_\rho \setminus I_{\text{all}}\}_\rho$ are pairwise disjoint (each $x \notin I_{\text{all}}$ belongs to at most one $I_\rho$). Therefore $\sum_\rho c(\rho) \le \sum_\rho |I_\rho \setminus I_{\text{all}}| \le n'$. $\square$

Combining: $|W(g)| \cdot (|Z| - n'/2) < n'$, so:
$$|W(g)| < \frac{n'}{|Z| - n'/2}. \tag{$\star\star$}$$

**Step 4: Case analysis combining both bounds.**

| Range of $|Z|$ | Binding bound | Value | Result |
|---|---|---|---|
| $|Z| \le n'/2$ | $(\star)$ | $\le 2n'/T = 256/127 \approx 2.016$ | $|W(g)| \le 2$ |
| $n'/2 < |Z| < T$ | $\min(\star, \star\star)$ | $\le 16/7 \approx 2.29$ (at crossover $|Z|=15n'/16$) | $|W(g)| \le 2$ |
| $|Z| \ge T$ | $(\star\star)$ | $< n'/(T - n'/2) = 128/63 \approx 2.03$ | $|W(g)| \le 2$ |

*Detail for the middle case:* $(\star)$ is increasing in $|Z|$ and $(\star\star)$ is decreasing. They equal at $|Z| = z_c$ satisfying $2(n'-z_c)(z_c - n'/2) = n'(T-z_c)$, which gives $z_c = n' - \sqrt{2n'(n'-T)}/2 = n' - n'/16 = 15n'/16$. At $z_c$: both bounds yield $16/7 < 3$. Since $|W(g)|$ is a non-negative integer, $|W(g)| \le 2$.

**In all cases, $|W(g)| \le 2$.** $\blacksquare$

---

## 2. Collinearity Structure in the Hard Regime

### Definition (Collinear hard slopes)

Fix a reference witness $(f_0, \rho_0, g_0)$. For each hard slope $\phi_i$ with parameter $\rho_i$ and $\lambda_i = 1/(\rho_i - \rho_0)$, define the "direction polynomial":
$$\hat{C}_{ij} = \frac{\phi_i - \phi_j}{\lambda_i - \lambda_j} \in RS[H^2, k']$$

**Lemma (Case 1 Closure):** If all hard slopes $\phi_1, \ldots, \phi_M$ satisfy $\phi_i = \hat{o}' + \lambda_i \hat{C}$ for fixed polynomials $\hat{o}', \hat{C} \in RS[H^2, k']$, then $M \le 4$.

**Proof.** In this case:
$$g_i = g_0 + (\rho_i - \rho_0)\phi_i = g_0 + (\rho_i - \rho_0)\hat{o}' + \hat{C} = (g_0 + \hat{C}) + (\rho_i - \rho_0)\hat{o}'.$$

Setting $u^* = g_0 + \hat{C} - \rho_0\hat{o}'$ and $\tilde{\phi} = \hat{o}'$: all $g_i = u^* + \rho_i \tilde{\phi}$ lie on a single affine line in $RS[H^2, k']$. By Lemma 3 (proofs.md), at most 4 values of $\rho$ admit far witnesses along any affine line. $\blacksquare$

### Non-Collinear Triple Intersection Bound

**Lemma:** If hard slopes $\phi_i, \phi_j, \phi_k$ are not affinely collinear (i.e., $\hat{C}_{ij} \neq \hat{C}_{ik}$), then $|F_i \cap F_j \cap F_k| < k' = n'/4$.

**Proof.** On $F_i \cap F_j$: $\hat{C}_{ij}(x) = C(x)$ (the actual function $C$). On $F_i \cap F_k$: $\hat{C}_{ik}(x) = C(x)$. So on $F_i \cap F_j \cap F_k$: $\hat{C}_{ij}(x) = \hat{C}_{ik}(x)$. Since $\hat{C}_{ij} - \hat{C}_{ik}$ is a nonzero polynomial of degree $< k'$, it has $< k'$ zeros on $H^2$. $\blacksquare$

---

## 3. Identification of the Remaining Gap

### The geometric barrier

In the hard regime, each opposite-branch set satisfies $|F_i| > 31n'/64 \approx 0.484n'$. This is **strictly below** the Johnson bound $n'/2 = 0.5n'$ for $RS[H^2, k']$.

Consequence: Standard list-decoding arguments cannot bound the number of hard slopes $M$ in the non-collinear case (Case 2), because:
- The approximation $\phi_i \approx o' + \lambda_i C$ holds on $|F_i| > 31n'/64$ points, but this agreement level is below the Johnson radius.
- Pairwise intersections $|F_i \cap F_j|$ cannot be bounded below $k' = n'/4$ from size constraints alone (since $2 \times 31n'/64 - n' < 0$).

### What is settled vs. open

| Component | Status | Bound |
|---|---|---|  
| Correlated agreement per $f$ | ✅ Proved | $|CA(f)| \le 1$ |
| Affine-line multiplicity | ✅ Proved | $\le 4$ per line |
| Per-codeword $\rho$-count | ✅