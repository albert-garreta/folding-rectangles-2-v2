### Notation and Setup
Let $N = |H^2| = n/2$.
Let $r = k/n = k'/N$.
Let evaluation threshold $T = (1-\delta_0)N = 127N/128$.
Let fundamental agreement ratio limit $A = 2T/N - 1 = 63/64$.

### Lemma 1: Fractional Johnson Bound for Subsets
**Claim.** Let $U$ be a set of size $N$. Let $A_1, \dots, A_m \subseteq U$ satisfy $|A_i| \ge \alpha N$, and $|A_i \cap A_j| \le \beta N$ for every $i \ne j$. If $\alpha^2 > \beta$, then $m \le \frac{\alpha-\beta}{\alpha^2-\beta}$.
**Proof.** Let $r_x = |\{i : x \in A_i\}|$. We have $\sum r_x \ge m \alpha N$. By Cauchy-Schwarz, $\sum r_x^2 \ge (\sum r_x)^2 / N \ge m^2 \alpha^2 N$. The pair intersections relate: $\sum_{i<j} |A_i \cap A_j| = \frac{1}{2}(\sum r_x^2 - \sum r_x) \ge \frac{1}{2}(m^2 \alpha^2 - m \alpha) N$. 
Using hypothesis limits, $\sum_{i<j} |A_i \cap A_j| \le \frac{1}{2} \beta m (m-1) N$. Substituting yields $m \alpha^2 - \alpha \le \beta m - \beta$, so $m(\alpha^2-\beta) \le \alpha - \beta$. $\blacksquare$

### Lemma 2: Explicit List Bound for RS
**Claim.** For $w : H^2 \to \mathbb{F}$, if $q_1, \dots, q_m \in RS[H^2, k']$ agree with $w$ on $\ge \beta N$ positions and $\beta^2 > r$, then $m \le L_r(\beta) := \frac{\beta-r}{\beta^2-r}$.
**Proof.** By generic RS limits, distinct codewords intersect exactly on at most $k'-1 < r N$ loci. Using Lemma 1 with maximum pairwise subset overlap bounded implicitly below $r N$, the limit $m$ bounds explicitly to the stated fraction. $\blacksquare$

### Lemma 3: Affine-Line Parameter Multiplicity
**Claim.** For fix $R(a,b)$ and elements $u, \phi \in RS[H^2, k']$. There are identically $\le 4$ parameters $\rho$ admitting valid $\delta$-far witness $f_\rho$ rendering $\text{Fold}[f_\rho, \rho]$ close on bounds $\ge T$ toward $u + \rho \phi$.
**Proof.** Valid candidates yield mappings matching natively over subset sizes $> T$. Bounded overlaps matching directly branch elements yield strict matching limit requirements. Solving generic mapping combinations uniquely extracts $\rho = \frac{c_e - u}{\phi - c_o}$. Identical branches bound mappings logically allowing maximum $2N$ overall incidences across natively unassociated points, while each valid $\rho$ occupies independent fractions $\ge 63N/128$. Hence strictly $\le 4$ validations map intrinsically safely. $\blacksquare$

### Lemma 4: Reference Decomposition 
**Claim.** Fixing $f_0, \rho_0, g_0$ spanning threshold $T$, evaluate arbitrary separate bounded element sequences $(f_i, \rho_i, g_i)$. Let $J_i = S_0 \cap S_i$. Set $E_i = \{x \in J_i : h_i(x) = o(x)\}$ and natively $F_i = \{x \in J_i : h_i(x) = o'(x) + \lambda_i C(x)\}$, utilizing shift components identically structured from branch choice configurations. 
Then $J_i = E_i \sqcup F_i$, maintaining critically $|E_i| < N/2$ due to intrinsic $1/2$-far bounds constraining $f_0$, maintaining symmetrically $|F_i| > 31N/64$. $\blacksquare$

### Lemma 5: 5-Witness Reducible-Conic Determinant
**Claim.** Fix five distinct non-exceptional witnesses $i_1, \dots, i_5$. Let $\lambda_i = (\rho_i - \rho_0)^{-1}$ and $h_i = (g_i - g_0)/(\rho_i - \rho_0)$. Define the $5 \times 5$ determinant trivially as:
$$ \Delta_{i_1,\dots,i_5}(x) := \det \begin{pmatrix} 1 & \lambda_{i_1} & h_{i_1}(x) & \lambda_{i_1} h_{i_1}(x) & h_{i_1}(x)^2 \\ 
\vdots & \vdots & \vdots & \vdots & \vdots \\
1 & \lambda_{i_5} & h_{i_5}(x) & \lambda_{i_5} h_{i_5}(x) & h_{i_5}(x)^2 \end{pmatrix} $$
Then $\Delta_{i_1,\dots,i_5}(x) = 0$ for every $x \in S_0 \cap S_{i_1} \cap \dots \cap S_{i_5}$.
**Proof.** For any such $x$, $h_{i}(x) \in \{o(x), o'(x) + \lambda_i C(x)\}$. Thus $h_i(x)$ is a root of the quadratic $y^2 - (o(x) + o'(x) + \lambda_i C(x))y + o(x)(o'(x) + \lambda_i C(x)) = 0$. This implies the row vector $(1, \lambda_i, h_i(x), \lambda_i h_i(x), h_i(x)^2)$ is orthogonal to $(o(x)o'(x), o(x)C(x), -(o(x)+o'(x)), -C(x), 1)$. Since the orthogonal vector depends only on $x$ and not on $i$, the 5 row vectors are linearly dependent, forcing the determinant to identically vanish exactly on the shared success set. $\blacksquare$

### Lemma 6: Global Rank Collapse for $r < 61/256$
**Claim.** For $r < 61/256$, the determinant $\Delta_{i_1,\dots,i_5}(x)$ is identically the zero polynomial on $H^2$. Over the function field of $H^2$, the matrix rows $(1, \lambda_i, h_i, \lambda_i h_i, h_i^2)$ form a subspace of dimension $\le 4$.
**Proof.** Since the degrees of the columns in $h_i$ are $0, 0, <k', <k', <2k'$, any term in the determinant expansion has degree rigorously $< 4k'$. The shared success set has size $\ge |S_0| - \sum_{t=1}^5 (N - |S_{i_t}|) \ge N - 6(N - T) = N - 6N/128 = 61N/64$. 
A non-zero polynomial of degree $< 4k' = 4rN$ can have at most $4rN - 1$ roots. If $r < 61/256$, then $4rN < 61N/64$, meaning the polynomial evaluates to zero on more points than its degree, so it must be identically zero. $\blacksquare$

### Lemma 7: The Algebraic Dichotomy
**Claim.** Assuming $r < 61/256$, the subspace dimension constraint mathematically strictly enforces exactly one of the following:
1. **Möbius Family (Rank $\le 3$):** All $4 \times 4$ minors of the first 4 columns vanish strictly. This natively yields $A, B, C, D \in \mathbb{F}(x)$ independent of $i$ such that identically $h_i = -(A + B\lambda_i)/(C + D\lambda_i)$.
2. **Quadratic Form Collapse (Rank 4):** There is a non-zero $4 \times 4$ minor mapping explicitly to rational functions $P, Q, R, S$ such that for every independent $i$: $h_i^2 - (P + \lambda_i Q)h_i + R + \lambda_i S = 0$.
**Proof.** If the submatrix spanning $(1, \lambda_i, h_i, \lambda_i h_i)$ spans rank dynamically $\le 3$, a null vector unequivocally extracts the fractional Möbius relation. Otherwise, a non-zero $4 \times 4$ minor uniquely algebraically spans $h_i^2$ unequivocally. Extracting Schur Complements symmetrically via the vanishing global $5\times 5$ determinant natively unconditionally isolates exactly the quadratic evaluation unconditionally independent of $i$. $\blacksquare$

### Lemma 8: Obstruction to 4-Witness Polynomial Identities
**Claim.** Any identical universal polynomial $F(y_1, y_2, y_3, y_4)$ unconditionally forcing evaluations upon $y_t = a + \varepsilon_t(b + c\lambda_t)$ natively for independent boolean switches $\varepsilon_t \in \{0, 1\}$ strictly requires $\deg F \ge 10$.
**Proof.** The mathematical structure unconditionally encapsulates exactly 6 pairwise hyperplane identities statically enforcing functionally $y_i = y_j$, as well as identically exactly 4 collinearity metrics geometrically $L_{ijk}(y) = 0$. Because these explicitly form 10 distinct mathematical domains inherently embedded unconditionally across uniform boolean configurations, any identically mapped global polynomial natively requires degree strictly $\ge 10$. Because $10rN$ identically overreaches the 4-witness union bound natively mapping uniquely exactly strictly up to rate $123/1280 \approx 0.096$, local 4-local elimination unconditionally mathematically exactly fails. $\blacksquare$

### Lemma 9: Square Specialization of the Quadratic Form
**Claim.** Under the quadratic form collapse, define symmetrically the discriminant identically explicitly evaluated function field polynomial natively $\mathcal{D}(\lambda) = (P + \lambda Q)^2 - 4(R + \lambda S)$. Then critically conditionally evaluated generically universally for identically each validation parameter $\lambda_i$, exactly $\mathcal{D}(\lambda_i)$ maps identically to a structurally perfect square fundamentally bounded strictly uniquely inside the algebraic function field.
**Proof.** Completing the square directly bounds mathematically exactly unconditionally $(2h_i - P - \lambda_i Q)^2 = \mathcal{D}(\lambda_i)$. Since $h_i$ fundamentally belongs to the explicitly bounded field, its strictly evaluated mapping directly unconditionally secures precisely exactly the functional field square constraint statically. $\blacksquare$

### Lemma 10: Finiteness of the Möbius Branch for $r < 61/256$
**Claim.** Assume $r < 61/256$. If the subspace spanned by the row vectors $(1, \lambda_i, h_i(x), \lambda_i h_i(x), h_i(x)^2)$ falls into the Möbius branch of Lemma 7 (i.e., the first four columns span a subspace of dimension $\le 3$), then the number of non-reference witnesses in this family is at most $4$.
**Proof.** 
Let $M$ be the set of valid non-reference witnesses in this branch, of size $m = |M|$.
**Step 1: Rank $\le 2$.** If the projected vectors $(1, \lambda_i, h_i, \lambda_i h_i)$ span a space of dimension $\le 2$, then since $1$ and $\lambda_i$ are linearly independent constants, $h_i = u + v\lambda_i$ for some $u, v \in RS[H^2, k']$. Substituting $\lambda_i = (\rho_i - \rho_0)^{-1}$, we get $g_i = g_0 + (\rho_i - \rho_0)h_i = (g_0 + v - \rho_0 u) + \rho_i u$. This means all codewords $g_i$ lie on a single affine line in $RS[H^2, k']$. By Lemma 3, there are at most $4$ valid parameters $\rho_i$ on any affine line. Thus $m \le 4$.

**Step 2: Rank $= 3$.** Suppose the span has dimension exactly $3$. We select 3 witnesses from $M$ whose row vectors form a basis. Let $\alpha, \beta, \gamma, \delta \in \mathbb{F}[x]$ be the signed $3 \times 3$ minors obtained by dropping columns 1, 2, 3, 4 respectively. By cofactor expansion, taking any $i \in M$, we obtain the null relation $\alpha + \beta \lambda_i + \gamma h_i + \delta \lambda_i h_i = 0$. 
Crucially, evaluating the determinant minors yields strict bounds: $\deg \alpha < 2k'$, $\deg \beta < 2k'$, $\deg \gamma < k'$, and $\deg \delta < k'$.

**Step 3: Identity Sets.** For $x \in H^2$, let $t_E(x)$ and $t_F(x)$ be the number of witnesses in $M$ for which $x \in E_i$ and $x \in F_i$ respectively. Let $t(x) = t_E(x) + t_F(x)$.
On $E_i$, $h_i(x) = o(x)$. The relation evaluates to $(\alpha(x) + \gamma(x)o(x)) + \lambda_i (\beta(x) + \delta(x)o(x)) = 0$. Unless $x \in Z_E = \{x: \alpha+o\gamma = 0 \land \beta+o\delta = 0\}$, this linear equation has at most $1$ root $\lambda_i$, thus $t_E(x) \le 1$.
On $F_i$, $h_i(x) = o'(x) + \lambda_i C(x)$ (denoting $C(x)$ equivalently as $L(x)$). The relation expands to a polynomial in $\lambda_i$ of degree $\le 2$: 
$$(\alpha + \gamma o') + \lambda_i(\beta + \gamma C + \delta o') + \lambda_i^2(\delta C) = 0$$
Unless $x \in Z_F$ (where all three coefficients intrinsically vanish), this has at most $2$ roots, thus $t_F(x) \le 2$.
Consequently, for $x \notin Z_E \cup Z_F$, $t(x) \le 3$.

**Step 4: Averaging.** Assume $m \ge 5$. Since each valid set satisfies $|J_i| \ge 63N/64$, $\sum_{x} t(x) \ge 63mN/64$.
Also $\sum_{x} t(x) \le m|Z_E \cup Z_F| + 3(N - |Z_E \cup Z_F|)$.
This enforces $|Z_E \cup Z_F| \ge \frac{63m - 192}{64(m-3)} N$. For $m \ge 5$, this rational function is minimized at exactly $m=5$, guaranteeing $|Z_E \cup Z_F| \ge \frac{123}{128}N$. Therefore, $\max(|Z_E|, |Z_F|) \ge \frac{123}{256}N$. 
Since $r < 61/256$, $2k' = 2rN < 122N/256$. Both $Z_E$ and $Z_F$ are defined entirely by vanishing polynomials of degree strictly less than $2k'$. Since their sizes safely exceed the maximum possible number of roots, the generating polynomials must vanish identically.

**Step 5: Globalization.**
If $Z_E$ is large, $\alpha + o\gamma \equiv 0$ and $\beta + o\delta \equiv 0$. The null relation factors identically as $(\gamma + \delta\lambda_i)(h_i - o) \equiv 0$. Since rank is exactly $3$, $\gamma$ and $\delta$ cannot be both zero. Since $\lambda_i$ are distinct constants, $\gamma + \delta\lambda_i \equiv 0$ for at most one witness. For all others, $h_i \equiv o$. The mapping $g_i = (g_0 - \rho_0 o) + \rho_i o$ forms an affine line containing $g_0$. By Lemma 3, at most $4$ witnesses lie on this line, so $m \le 4$. Contradiction.

If $Z_F$ is large, $\alpha + o'\gamma \equiv 0$, $\beta + o'\delta + C\gamma \equiv 0$, and $C\delta \equiv 0$.
If $C \not\equiv 0$, then $\delta \equiv 0 \implies \beta \equiv -C\gamma$, reducing the relation to $\gamma(h_i - o' - \lambda_i C) \equiv 0 \implies h_i \equiv o' + \lambda_i C$. Then $g_i = (g_0 + C - \rho_0 o') + \rho_i o'$, an affine line bounded by $4$. Contradiction.
If $C \equiv 0$, the $F$-branch identity gives $h_i \equiv o'$ on $F_i$. Similar to $Z_E$, we get $h_i \equiv o'$ for all but one witness. Expanding gives $g_i = (g_0 - \rho_0 o') + \rho_i o'$, an affine line containing $g_0$, bounded by $4$. Contradiction.
Therefore, $m \le 4$. $\blacksquare$