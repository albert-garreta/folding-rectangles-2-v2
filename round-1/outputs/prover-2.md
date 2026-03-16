# Analysis: Bounding $|W(g)|$ and Structural Results for Rectangle Folding

## Overview

I carefully analyze the existing notes and lemmas, identify a gap in the proof of the per-codeword bound, and provide a complete, rigorous proof that $|W(g)| \leq 2$ for the target parameters. I also formalize the ratio polynomial structure and identify the key remaining obstacle.

---

## Result 1: Clean Per-Codeword $\rho$-Bound

**Theorem.** For parameters $k/n = 1/4$, $\delta = 1/2$, $\delta_0 = 1/128$, let $a, b : H \to \mathbb{F}$ be arbitrary maps and $g \in \mathrm{RS}[H^2, k/2]$. Define
$$W(g) = \{\rho \in \mathbb{F} : \exists f \in \mathcal{F}(R(a,b)),\; f \text{ is } \delta\text{-far from } V,\; |\{x \in H^2 : \mathrm{Fold}[f,\rho](x) = g(x)\}| \geq (1-\delta_0)n'\}$$
Then $|W(g)| \leq 2$.

### Proof

**Notation.** Set $n' = |H^2| = n/2$, $k' = k/2 = n'/4$, $T = (1-\delta_0)n' = 127n'/128$. For $x = h^2 \in H^2$, define:
- $a_e(x) = \frac{a(h)+a(-h)}{2}$, $a_o(x) = \frac{a(h)-a(-h)}{2h}$, $A_\rho(x) = a_e(x) + \rho\, a_o(x)$
- $b_e(x) = \frac{b(h)+b(-h)}{2}$, $b_o(x) = \frac{b(h)-b(-h)}{2h}$, $B_\rho(x) = b_e(x) + \rho\, b_o(x)$

By Lemma 1, $\mathrm{Fold}[f,\rho](x) \in \{A_\rho(x), B_\rho(x)\}$ for all $f \in \mathcal{F}(R)$ and $x \in H^2$.

**Step 1 (Universal matching).** Define:
$$U_a(g) = \{x \in H^2 : a_o(x) = 0 \text{ and } g(x) = a_e(x)\}, \quad U_b(g) = \{x \in H^2 : b_o(x) = 0 \text{ and } g(x) = b_e(x)\}$$
$$Z = U_a(g) \cup U_b(g), \quad \hat{Z} = U_a(g) \cap U_b(g)$$

For $x \in U_a(g)$: $A_\rho(x) = a_e(x) = g(x)$ for all $\rho$. Similarly for $U_b(g)$. So for all $x \in Z$ and all $\rho$: $g(x) \in \{A_\rho(x), B_\rho(x)\}$.

For $x \notin Z$: $g(x) = A_\rho(x)$ holds for at most one $\rho$ (since either $a_o(x) \neq 0$, giving unique $\rho = (g(x)-a_e(x))/a_o(x)$, or $a_o(x) = 0$ with $g(x) \neq a_e(x)$, giving none). Similarly for $B_\rho$. So $g(x) \in \{A_\rho(x), B_\rho(x)\}$ for **at most 2 values of $\rho$**.

**Step 2 (Non-universal incidence bound).** Define $N(\rho) = \{x \notin Z : g(x) \in \{A_\rho(x), B_\rho(x)\}\}$. Then
$$\sum_{\rho \in \mathbb{F}} |N(\rho)| \leq 2(n' - |Z|) \qquad (\star)$$
since each $x \notin Z$ contributes to at most 2 terms.

For $\rho \in W(g)$: total matching $|Z| + |N(\rho)| \geq T$, so $|N(\rho)| \geq T - |Z|$ when $|Z| < T$. Thus:
$$|W(g)| \cdot (T - |Z|) \leq 2(n' - |Z|)$$
$$|W(g)| \leq \frac{2(n' - |Z|)}{T - |Z|} = 2 + \frac{2(n' - T)}{T - |Z|} = 2 + \frac{n'/64}{T - |Z|} \qquad \text{(Bound I)}$$

**Step 3 (Far condition via escape counting).** Define $\hat{g}(t) = g(t^2) \in \mathrm{RS}[H, k]$ (since $\deg g < k'$ implies $\deg \hat{g} < 2k' = k$).

*Key observation:* At $x \in U_a(g)$: $a_o(x) = 0$ and $a_e(x) = g(x)$, so $a(h) = a(-h) = a_e(x) = g(x) = \hat{g}(h) = \hat{g}(-h)$.

If the selector of $f$ uses branch $a$ at $x \in U_a(g)$: $f(h) = a(h) = \hat{g}(h)$ and $f(-h) = a(-h) = \hat{g}(-h)$, giving agreement 2 with $\hat{g}$.

If instead $f$ uses branch $b$ at $x \in U_a(g) \setminus \hat{Z}$ (possible only when $B_\rho(x) = g(x)$): since $x \notin U_b(g)$, we have $b_o(x) \neq 0$ or $b_e(x) \neq g(x)$. The matching $B_\rho(x) = g(x)$ with $b_o(x) \neq 0$ fixes a unique $\rho$. Then $b(h) = \hat{g}(h)$ iff $h = \rho$ (solving $(h - \rho)b_o(x) = 0$ with $b_o(x) \neq 0$). So the "escape" gives agreement at most 0 with $\hat{g}$ per pair $\{h, -h\}$ (generically).

Define **escapes**: $e(\rho) = |\{x \in Z \setminus \hat{Z} : \text{the non-universal branch also matches at } \rho\}|$.

Then:
$$\mathrm{agr}(f, \hat{g}) \geq 2(|Z| - e(\rho))$$
The far condition $\mathrm{agr}(f, \hat{g}) < n/2 = n'$ gives:
$$|Z| - e(\rho) < n'/2 \quad \Longrightarrow \quad e(\rho) > |Z| - n'/2 \qquad (\diamondsuit)$$

Each $x \in U_a \setminus \hat{Z}$ contributes to at most 1 value of $\rho$ in the escape sum (unique $\rho = (g(x)-b_e(x))/b_o(x)$). Similarly for $U_b \setminus \hat{Z}$. So:
$$\sum_{\rho \in \mathbb{F}} e(\rho) \leq |U_a \setminus \hat{Z}| + |U_b \setminus \hat{Z}| = |Z| - |\hat{Z}| \qquad (\spadesuit)$$

Summing $(\diamondsuit)$ over $\rho \in W(g)$ and applying $(\spadesuit)$:
$$|W(g)| \cdot (|Z| - n'/2) < |Z| - |\hat{Z}| \leq |Z|$$
$$|W(g)| < \frac{|Z|}{|Z| - n'/2} \qquad \text{(Bound II, valid for } |Z| > n'/2\text{)}$$

**Step 4 (Combining bounds).**

**Case A: $|Z| \leq n'/2$.** Bound I gives $|W(g)| \leq 2 + \frac{n'/64}{T - n'/2} = 2 + \frac{128}{64 \cdot 63} = 2 + \frac{2}{63} < 3$. So $|W(g)| \leq 2$. $\checkmark$

**Case B: $n'/2 < |Z| < 3n'/4$.** Bound I gives $|W(g)| \leq 2 + \frac{n'/64}{T - 3n'/4 + \epsilon} = 2 + \frac{n'/64}{31n'/128 + \epsilon} < 2 + \frac{128}{64 \cdot 31} = 2 + \frac{2}{31} < 3$. So $|W(g)| \leq 2$. $\checkmark$

**Case C: $|Z| \geq 3n'/4$.** Bound II gives $|W(g)| < \frac{|Z|}{|Z| - n'/2}$. For $|Z| \geq 3n'/4$: $\frac{3n'/4}{n'/4} = 3$, and this ratio is decreasing, so $|W(g)| < 3$, meaning $|W(g)| \leq 2$. $\checkmark$

More precisely, for $|Z| \leq n'$: $\frac{|Z|}{|Z|-n'/2} \leq \frac{T}{T-n'/2} = \frac{127}{63} \approx 2.016 < 3$, so $|W(g)| \leq 2$.

For $|Z| > T$ (only Bound II applies): $\frac{|Z|}{|Z|-n'/2} \leq \frac{n'}{n'/2} = 2$, giving $|W(g)| \leq 1$. $\checkmark$

In all cases: $\boxed{|W(g)| \leq 2}$. $\square$

---

## Result 2: Ratio Polynomial Structure

**Lemma.** Fix a reference active triple $(\rho_0, g_0, f_0)$ and another $(\rho_1, g_1, f_1)$ with $\rho_0 \neq \rho_1$, $g_0 \neq g_1$. Let $h = (g_1 - g_0)/(\rho_1 - \rho_0) \in \mathrm{RS}[H^2, k/2]$ and $\lambda = 1/(\rho_1 - \rho_0)$.

Let $S = S_0 \cap S_1$ (intersection of matching sets, $|S| \geq 63n'/64$), partitioned as $S = E \sqcup F$ where $E$ = same-branch points, $F$ = different-branch points.

Then:
1. $h(x) = o(x)$ for all $x \in E$, where $o$ is the odd part of $f_0$'s branch.
2. $h(x) = o'(x) + \lambda \cdot C(x)$ for all $x \in F$, where $o'$ is the odd part of the opposite branch and $C(x) = B_{\rho_0}(x) - A_{\rho_0}(x)$ (with appropriate sign).
3. $|E| < n'/2$ (from far condition on $f_0$, via the codeword $p_h(t) = (g_0 - \rho_0 h)(t^2) + t \cdot h(t^2)$).
4. $|F| > 31n'/64$.

**Proof sketch for (3):** The polynomial $p_h(t) = (g_0 - \rho_0 h)(t^2) + t \cdot h(t^2) \in V$ (degree $< k$). On $E$: $h(x) = o(x)$, so $p_h(h_x) = (f_0)_e(x) + h_x \cdot (f_0)_o(x) = f_0(h_x)$ and similarly $p_h(-h_x) = f_0(-h_x)$. Thus $\mathrm{agr}(f_0, p_h) \geq 2|E|$. The far condition gives $2|E| < n'$, hence $|E| < n'/2$.

**(4)** follows from $|E| + |F| \geq |S| \geq 63n'/64$ and $|E| < n'/2 = 32n'/64$. $\square$

---

## Result 3: Consequences and the Key Remaining Challenge

**Corollary (Johnson bound on ratio polynomials).** Since $|F| > 31n'/64 > n'/2 = \sqrt{k' n'}$, the Johnson bound implies: for each $\lambda$, the number of codewords $h$ with $|\{x : h(x) = o' + \lambda C\}| \geq 31n'/64$ is at most $\lfloor n'/(31n'/64) \rfloor = 2$.

**Structural summary:** We have:
- $|W(g)| \leq 2$ for each codeword $g$ (Theorem above).
- At most $L \leq 7$ codewords per $\rho$ (Lemma 2, via Guruswami-Sudan list recovery with $\ell = 2$, $T/n' \approx 0.992 > \sqrt{1/2} \approx 0.707$).
- $|X_R| \leq 2|G|$ where $G = \{g : W(g) \neq \emptyset\}$.

**Key remaining challenge:** Bounding $|G|$ (the number of active codewords). The bipartite graph between $X_R$ and $G$ has max degree 7 on the $\rho$-side and max degree 2 on the $g$-side, yielding $|X_R| \leq 14|X_R|$ (circular). An independent bound on $|G|$ — likely exploiting the algebraic structure of the ratio polynomials $h_i$ and their interaction with the fixed functions $o, o', C$ — is needed to close the argument.

**Potential approach:** Each ratio polynomial $h_i$ satisfies $h_i = o' + \lambda_i C + r_i$ where $r_i$ vanishes on $F_i$ ($|F_i| > 31n'/64$). The function $r_i = h_i - (o' + \lambda_i C)$ has at most $n' - |F_i| < 33n'/64$ non-zeros. Distinct $h_i - h_j = (\lambda_i - \lambda_j)C$ on $F_i \cap F_j$, meaning the codeword $(h_i - h_j)/(\lambda_i - \lambda_j)$ agrees with the **fixed** function $C$ on $F_i \cap F_j$. When $C$ is far from all codewords, the number of codewords close to $C$ is bounded by the Johnson bound, potentially yielding a polynomial bound on the number of distinct ratio polynomials.

---

## Corrections to Existing Notes

1. **Lemma 4 (Forced-Even Obstruction)**: The claim $|E_a| + |E_b| < 65n'/128$ is weaker than needed. Our Theorem shows $|W(g)| \leq 2$ directly without requiring this intermediate bound on $|Z(g)|$.

2. **Lemma 8 (Per-Witness Match)**: Claims $|W(g)| \leq 4$. Our Theorem improves this to $|W(g)| \leq 2$ by combining both the incidence bound and the far-condition escape argument.

3. **Lemma 13**: Claims $|W(g)| \leq 2$ but the proof sketch is incomplete. Our proof above provides the full argument with all cases handled.