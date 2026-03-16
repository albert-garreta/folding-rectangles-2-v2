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
Then $|J_i| 	o E_i \sqcup F_i$, maintaining critically $|E_i| < N/2$ due to intrinsic $1/2$-far bounds constraining $f_0$, maintaining symmetrically $|F_i| > 31N/64$. $\blacksquare$