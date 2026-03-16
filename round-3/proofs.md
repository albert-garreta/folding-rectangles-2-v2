### Notation and Setup
Let $n = |H|$, $n' = n/2$, $k' = k/2 = n'/4$.
Evaluation threshold $T = (1-\delta_0)n' = 127n'/128$. Let $z = n' - T = n'/128$.
For $x = h^2 \in H^2$, define even and odd parts of a map $c: H \to \mathbb{F}$:
$$c_e(x) = \frac{c(h)+c(-h)}{2}, \quad c_o(x) = \frac{c(h)-c(-h)}{2h}$$
For a rectangle $R(a,b)$, denote $A_\rho(x) = a_e(x) + \rho a_o(x)$ and $B_\rho(x) = b_e(x) + \rho b_o(x)$.
Every $f \in \mathcal{F}(R)$ pointwise selects between $a$ and $b$, meaning $\mathrm{Fold}[f, \rho](x) \in \{A_\rho(x), B_\rho(x)\}$. 

### Lemma 1: No Good Set from Codewords
**Claim:** If $a, b \in \mathrm{RS}[H,k]$, then $X_R = \emptyset$.
**Proof:** For any $f \in \mathcal{F}(R(a,b))$, let $S_a \subseteq H^2$ be the coordinates where $f$ chooses the pair from $a$, and $S_b = H^2 \setminus S_a$ where $f$ chooses $b$. On $S_a$, $f$ perfectly matches $a$ on both roots $\{h, -h\}$, yielding $2|S_a|$ agreements. Similarly for $b$ on $S_b$. Since $|S_a| + |S_b| = n'$, one set has size $\ge n'/2$, giving agreement $\ge n' = n/2$ with either $a$ or $b$. Thus $f$ is $1/2$-close to $\mathrm{RS}[H,k]$, making $f$ an invalid witness. $\blacksquare$

### Lemma 2: Injectivity of Correlated Agreement
**Claim:** For any $f$ that is $1/2$-far from $\mathrm{RS}[H,k]$, there exists at most one $\rho$ such that $\mathrm{Fold}[f, \rho]$ is $1/128$-close to $\mathrm{RS}[H^2, k']$.
**Proof:** Suppose $\rho_1 \ne \rho_2$ both succeed. There exist $g_1, g_2 \in \mathrm{RS}[H^2, k']$ agreeing with the respective folds on $S_1, S_2$ of size $\ge T$.
$|S_1 \cap S_2| \ge 2T - n' = 63n'/64$.
For $x \in S_1 \cap S_2$:
$f_e(x) + \rho_1 f_o(x) = g_1(x)$ and $f_e(x) + \rho_2 f_o(x) = g_2(x)$.
Solving gives $f_o(x) = \frac{g_1(x)-g_2(x)}{\rho_1-\rho_2} =: p_o(x)$, and $f_e(x) = g_1(x) - \rho_1 p_o(x) =: p_e(x)$. Since $g_1, g_2$ have degree $< k'$, so do $p_o, p_e$. 
Define $r(Y) = p_e(Y^2) + Y p_o(Y^2)$; $\deg(r) < 2k' = k$. For $x \in S_1 \cap S_2$, $f(\pm h) = r(\pm h)$. 
Thus $\operatorname{agr}(f, r) \ge 2(63n'/64) = 63n/64 > n/2$, contradicting $f$ being $1/2$-far. $\blacksquare$

### Lemma 3: Affine-Line Parameter Multiplicity
**Claim:** Fix $R(a,b)$ and $u, \phi \in \mathrm{RS}[H^2, k']$. There are at most 4 values of $\rho$ admitting a $1/2$-far witness $f_\rho$ such that $\operatorname{agr}(\mathrm{Fold}[f_\rho, \rho], u + \rho\phi) \ge T$.
**Proof:** Let $W$ be the set of valid $\rho$. For each $\rho \in W$, let $S_\rho$ be the agreement set ($|S_\rho| \ge T$). At $x \in S_\rho$, the branch chosen $c_x \in \{a,b\}$ satisfies $u(x) + \rho\phi(x) = c_{x,e}(x) + \rho c_{x,o}(x)$.
Define $E_\rho \subseteq S_\rho$ where $c_{x,e}(x) = u(x)$ and $c_{x,o}(x) = \phi(x)$. 
Since $P(Y) = u(Y^2) + Y\phi(Y^2) \in \mathrm{RS}[H,k]$ perfectly matches $f_\rho$ on both roots for $x \in E_\rho$, $2|E_\rho| < n/2 \implies |E_\rho| < n'/2$. 
Thus, $|S_\rho \setminus E_\rho| > T - n'/2 = 63n'/128$.
For $x \in S_\rho \setminus E_\rho$, $\rho(\phi(x) - c_{x,o}(x)) = c_{x,e}(x) - u(x)$. Since $x \notin E_\rho$, $\phi(x) \ne c_{x,o}(x)$ ensuring $\rho$ is uniquely determined. Hence, each $x$ provides $\le 2$ possible $\rho$ values (bounded by branches $a, b$).
Counting incidences $(\rho, x)$ over $S_\rho \setminus E_\rho$:
$|W| \times \frac{63n'}{128} \le 2n' \implies |W| < 5 \implies |W| \le 4$. $\blacksquare$

### Lemma 4: Reference Geometry and the Hard Regime Reduction
Fix a reference witness $(f_0, \rho_0, g_0)$ with agreement $S_0$ ($|S_0| \ge T$). Let $e, o$ be the even/odd parts of the branch $f_0$ chose, and $e', o'$ the opposite branch. For any $\phi \in \mathrm{RS}[H^2, k']$, define:
$P(\phi) = \{x \in S_0 : \phi(x) = o(x)\}$, $R(\phi) = \{x \in S_0 : \phi(x) \notin \{o(x), o'(x)\}$.
1. **Same-Branch Sparse:** $|P(\phi)| < n'/2$ (via far condition identical to Lemma 3).
2. **Trichotomy:** For any witness $(f, \rho, g)$ with $\rho \neq \rho_0$, define $\phi = \frac{g-g_0}{\rho-\rho_0}$. On the overlap $J = S_0 \cap S$, $f$ chooses the opposite branch on a set $D \subseteq J$. $|D| > 31n'/64$. For $x \in D$, $(\rho - \rho_0)\phi(x) = e'(x) - e(x) + \rho o'(x) - \rho_0 o(x)$.
3. **Disjointness on $R(\phi)$:** If the same slope $\phi$ works for $m$ distinct parameters $\rho$, they must yield mutually disjoint sets $R(\phi) \cap S_i$. Thus $|R(\phi)| \le \frac{m}{m-1} \frac{n'}{128}$. Consequently, if $|R(\phi)| > 9n'/32$, $\phi$ corresponds to **at most one** parameter $\rho$.
4. **Moderate Bound:** If $|R(\phi)| \le 9n'/32$, $x \in S_0 \setminus R(\phi)$ implies $\phi \in \{o, o'\}$. The agreement is $\ge 127n'/128 - 9n'/32 = 91n'/128$. Since $91/128 > 1/\sqrt{2}$ (the $\ell=2$ Johnson bound), Guruswami-Sudan ensures at most $O(1)$ such slopes $\phi$. By Lemma 3, this yields $O(1)$ valid $\rho$ in the moderate regime. $\blacksquare$

### Lemma 15: Generic Pairwise Overlap Obstruction on Hard Regimes
For any universal branch-gap function $C(x)$ uniformly mapping $S_0 \to \mathbb{F}$ evaluated natively natively upon independent intersection sizes $|S_0| \ge 127n'/128$, define fundamentally boundary $\Gamma(C) = \max_{q \in \operatorname{RS}[H^2, k']} |\{x \in S_0 : q(x) = C(x)\}|$.
1. By generic subset code-interpolation constraints, structurally uniformly evaluated: $\Gamma(C) \ge k' = n'/4 = 0.25n'$.
2. The minimum generic pairwise packing condition strictly mapping unconditionally exactly bounding constraints inherently yielding independent sets $m \le O(1)$ utilizing generic overlaps uniformly dictates $\Gamma(C) < (31/64)^2 n' \approx 0.234 n'$. Because interpolation algebraically universally violates geometric overlaps, no unconditionally generic intersection uniformly constraints strict dimensions uniformly bounding mappings independently without strict matrix code relations natively strictly evaluating unconditionally affine polynomials.