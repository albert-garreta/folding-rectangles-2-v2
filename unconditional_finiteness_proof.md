# Finiteness of the Good Set for $R < 0.13939$: A Self-Contained Proof

## Setup and Definitions

Let $\mathbb{F}$ be a finite field and $H$ a multiplicative subgroup of $\mathbb{F}$ closed under additive inversion, with $|H| = n$. For $f : H \to \mathbb{F}$ and $\rho \in \mathbb{F}$, define the **fold**:
$$
\mathrm{Fold}[f, \rho](x) = \frac{f(h) + f(-h)}{2} + \rho \cdot \frac{f(h) - f(-h)}{2h}, \quad x = h^2 \in H^2.
$$

Equivalently, writing $f_e(x) = \frac{f(h)+f(-h)}{2}$ and $f_o(x) = \frac{f(h)-f(-h)}{2h}$, we have $\mathrm{Fold}[f,\rho](x) = f_e(x) + \rho \cdot f_o(x)$.

**Notation.**
- $N = |H^2| = n/2$.
- $k' = k/2$, $r = k'/N = k/n = R$ (the code rate).
- $V = \mathrm{RS}[H, k]$, the Reed–Solomon code on $H$ with dimension $k$.
- $\delta = 1/2$, $\delta_0 = 1/128$, $T = (1-\delta_0)N = 127N/128$.
- $A = 2T/N - 1 = 63/64$ (the fundamental agreement ratio).

**Rectangle.** A rectangle $R(a,b)$ is determined by maps $a, b : H \to \mathbb{F}$. For each $x = h^2 \in H^2$, define $A_\rho(x) = \mathrm{Fold}[a,\rho](x)$ and $B_\rho(x) = \mathrm{Fold}[b,\rho](x)$.

**Good set.** $X_R$ is the set of $\rho \in \mathbb{F}$ such that there exists $f \in \mathcal{F}(R(a,b))$ with $f$ being $\delta$-far from $V$ and $\mathrm{Fold}[f, \rho]$ is $\delta_0$-close to $\mathrm{RS}[H^2, k']$.

---

## Statement of the Main Theorem

**Theorem.** For any rectangle $R(a,b)$, if $R < \left(\dfrac{95 - 8\sqrt{79}}{64}\right)^2 \approx 0.13939$, then $|X_R| = O_R(1)$.

---

## Preliminary Lemmas

### Lemma 1 (Fold Structure)
*For any $\rho$ and rectangle $R(a,b)$, the set $\{\mathrm{Fold}[f,\rho] : f \in \mathcal{F}(R)\}$ is exactly the set of functions obtained by choosing pointwise between $A_\rho(x)$ and $B_\rho(x)$ at each $x \in H^2$.*

**Proof.** At each $x = h^2$, any $f \in \mathcal{F}(R)$ evaluates to either $(a(h), a(-h))$ or $(b(h), b(-h))$ on $\{h, -h\}$. The fold value $\mathrm{Fold}[f,\rho](x)$ depends only on this choice, yielding either $A_\rho(x)$ or $B_\rho(x)$. Since different points $x \in H^2$ correspond to disjoint pairs $\{h, -h\}$, the choices at different $x$ are independent. $\blacksquare$

### Lemma 2 (Correlated Agreement: $|CA(f)| \le 1$)
*If $f : H \to \mathbb{F}$ is $\delta$-far from $V$, there is at most one $\rho$ such that $\mathrm{Fold}[f,\rho]$ is $\delta_0$-close to $\mathrm{RS}[H^2, k']$.*

**Proof.** Suppose $\rho_1, \rho_2$ are two such parameters with matching codewords $g_1, g_2$. Let $A_i = \{x : f_e(x) + \rho_i f_o(x) = g_i(x)\}$ with $|A_i| \ge T$. Then $|A_1 \cap A_2| \ge 2T - N = 63N/64$. On $A_1 \cap A_2$, the system
$$f_e(x) + \rho_1 f_o(x) = g_1(x), \quad f_e(x) + \rho_2 f_o(x) = g_2(x)$$
uniquely determines $f_e(x)$ and $f_o(x)$ as evaluations of polynomials $p_e, p_o \in \mathrm{RS}[H^2, k']$. Constructing $p(h) = p_e(h^2) + h \cdot p_o(h^2) \in \mathrm{RS}[H, k]$, we find $f$ agrees with $p$ on $\ge 2 \cdot 63N/64 = 63n/64 > n/2$, contradicting $f$ being $1/2$-far from $V$. $\blacksquare$

### Lemma 3 (Constant List Size)
*For any $\rho$ and rectangle $R(a,b)$, the number of codewords $g \in \mathrm{RS}[H^2, k']$ such that some $f \in \mathcal{F}(R)$ with $f$ being $\delta$-far has $\mathrm{Fold}[f,\rho]$ matching $g$ on $\ge T$ positions is at most $7$.*

**Proof.** By Lemma 1, any such $g$ must agree with $\{A_\rho(x), B_\rho(x)\}$ on $\ge T$ positions. This is a list-recovery problem with input list size $\ell = 2$ and code dimension $k'$ over a domain of size $N$. By the Guruswami–Sudan theorem, the number of codewords is bounded when $T > \sqrt{\ell k' N}$. Since $r \le 1/4$, we have $\sqrt{\ell k' N} = \sqrt{2rN^2} \le \sqrt{N^2/2} \approx 0.707N$, and $T = 127N/128 \approx 0.992N$ exceeds this threshold. The explicit list-recovery bound gives at most $\lfloor \ell N / (T - \sqrt{\ell k'N}) \rfloor \le 7$ codewords. $\blacksquare$

### Lemma 4 (Affine-Line Parameter Multiplicity)
*Fix a rectangle $R(a,b)$ and polynomials $u, \phi \in \mathrm{RS}[H^2, k']$. There are at most $4$ parameters $\rho$ such that some $\delta$-far $f \in \mathcal{F}(R)$ has $\mathrm{Fold}[f,\rho]$ matching $u + \rho \phi$ on $\ge T$ positions.*

**Proof.** Consider the family of codewords $g_\rho = u + \rho\phi$ parameterized by $\rho$. Define the **lifted codeword** $\hat{g}(h) = u(h^2) + h \cdot \phi(h^2)$. Since $\deg u, \deg \phi < k'$, we have $\hat{g} \in \mathrm{RS}[H, k]$.

At each $x = h^2 \in H^2$, classify how each branch interacts with the affine line:
- **Branch $a$ is universal at $x$** if $a_e(x) = u(x)$ and $a_o(x) = \phi(x)$, i.e., $A_\rho(x) = g_\rho(x)$ for all $\rho$.
- **Branch $a$ is $\rho$-specific at $x$** if $a_o(x) \ne \phi(x)$: then $A_\rho(x) = g_\rho(x)$ for exactly one value $\rho = (u(x) - a_e(x))/(a_o(x) - \phi(x))$.
- **Branch $a$ is dead at $x$** if $a_o(x) = \phi(x)$ but $a_e(x) \ne u(x)$: then $A_\rho(x) \ne g_\rho(x)$ for all $\rho$.

The same trichotomy applies to branch $b$. Write $U_a$ (resp. $U_b$) for the set of positions where branch $a$ (resp. $b$) is universal.

**Key observation.** At $x \in U_a$: $a(h) = a_e(x) + h\, a_o(x) = u(x) + h\,\phi(x) = \hat{g}(h)$, and likewise $a(-h) = \hat{g}(-h)$. So $a$ agrees with $\hat{g} \in V$ at both fiber points $\{h, -h\}$. The identical statement holds for branch $b$ at positions in $U_b$.

**Bounding universal usage via $\delta$-farness.** Fix a valid parameter $\rho$ with $\delta$-far witness $f$ and success set $S_\rho$, $|S_\rho| \ge T$. Let $W_\rho = (S_\rho^a \cap U_a) \cup (S_\rho^b \cap U_b)$, where $S_\rho^a$ (resp. $S_\rho^b$) are the positions in $S_\rho$ where $f$ chooses branch $a$ (resp. $b$). At every $x \in W_\rho$, $f$ agrees with $\hat{g}$ on both fiber points, contributing $2|W_\rho|$ to $\mathrm{agr}(f, \hat{g})$. Since $f$ is $\delta$-far from $V$ with $\delta = 1/2$, we have $\mathrm{agr}(f, \hat{g}) < n/2 = N$, so $|W_\rho| < N/2$.

**Incidence count.** At each $\rho$-specific position $x$ (for a given branch), the matching $\rho$ is uniquely determined. So the total count of $(\rho, x)$ incidences from non-universal matches is bounded: branch $a$ contributes at most $|\{x : a_o(x) \ne \phi(x)\}| \le N$ incidences (each pinning a unique $\rho$), and branch $b$ contributes at most $N$. Hence the total number of non-universal incidences across all $\rho$ is at most $2N$.

**Combining.** Each valid $\rho$ contributes at least $|S_\rho| - |W_\rho|$ non-universal matches. Since $|S_\rho| \ge T$ and $|W_\rho| < N/2$ (strict), this is $> T - N/2 = 63N/128$. Since the total number of non-universal incidences is at most $2N$, we get $m \cdot 63N/128 < 2N$, hence $m < 256/63 \approx 4.063$, so $m \le 4$. $\blacksquare$

### Lemma 5 (Fractional Johnson Bound)
*Let $U$ be a set of size $N$, and let $A_1, \dots, A_m \subseteq U$ with $|A_i| \ge \alpha N$ and $|A_i \cap A_j| \le \beta N$ for all $i \ne j$. If $\alpha^2 > \beta$, then*
$$m \le \frac{\alpha - \beta}{\alpha^2 - \beta}.$$

**Proof.** Let $r_x = |\{i : x \in A_i\}|$. Then $\sum_x r_x \ge m\alpha N$. By Cauchy–Schwarz:
$$\sum_x r_x^2 \ge \frac{(\sum_x r_x)^2}{N} \ge m^2 \alpha^2 N.$$
The pairwise overlaps give $\sum_{i < j} |A_i \cap A_j| = \frac{1}{2}(\sum r_x^2 - \sum r_x) \ge \frac{1}{2}(m^2\alpha^2 - m\alpha)N$. Since each pairwise overlap is $\le \beta N$, we get $\frac{1}{2}\beta m(m-1)N \ge \frac{1}{2}(m^2\alpha^2 - m\alpha)N$, yielding $m(\alpha^2 - \beta) \le \alpha - \beta$. $\blacksquare$

### Lemma 6 (RS List Decoding Bound)
*Let $w : H^2 \to \mathbb{F}$ be an arbitrary function. If $q_1, \dots, q_m \in \mathrm{RS}[H^2, k']$ each agree with $w$ on $\ge \beta N$ positions and $\beta^2 > r$, then*
$$m \le L_r(\beta) := \frac{\beta - r}{\beta^2 - r}.$$

**Proof.** Two distinct RS codewords of dimension $k'$ over $H^2$ can agree on at most $k' - 1$ positions, so $|\{x: q_i(x) = q_j(x)\}| \le k' - 1 < k' = rN$ for $q_i \ne q_j$. In particular, $|\{x: q_i(x) = q_j(x)\}|/N < r$. Apply Lemma 5 with $\alpha = \beta$ and pairwise overlap bound $\beta' = r$ (valid since $k'-1 < rN$). Since $\beta^2 > r = \beta'$, the bound gives $m \le \frac{\beta - r}{\beta^2 - r}$. $\blacksquare$

### Lemma 7 (Reference Decomposition)
*Fix a valid reference witness $(f_0, \rho_0, g_0)$ with success set $S_0 = \{x \in H^2 : \mathrm{Fold}[f_0, \rho_0](x) = g_0(x)\}$, $|S_0| \ge T$. For any other valid witness $(f_i, \rho_i, g_i)$ with $\rho_i \ne \rho_0$ and success set $S_i$ with $|S_i| \ge T$, define:*
- *$h_i = (g_i - g_0)/(\rho_i - \rho_0) \in \mathrm{RS}[H^2, k']$,*
- *$\lambda_i = (\rho_i - \rho_0)^{-1}$,*
- *$J_i = S_0 \cap S_i$.*

*Let $\sigma_0(x)$ denote the branch chosen by $f_0$ at $x \in S_0$. For $x \in S_0$, write $o(x)$ for the odd part of $f_0$'s chosen branch and $o'(x)$, $L(x)$ for the derived functions from the opposite branch. Then $J_i$ partitions as $J_i = E_i \sqcup F_i$ where:*
- *$E_i = \{x \in J_i : f_i \text{ takes the same branch as } f_0\}$, on which $h_i(x) = o(x)$;*
- *$F_i = \{x \in J_i : f_i \text{ takes the opposite branch}\}$, on which $h_i(x) = o'(x) + \lambda_i L(x)$.*

*Moreover, $|J_i| \ge AN$, $|E_i| < N/2$, and $|F_i| > 31N/64$.*

**Proof.**

**Partition.** On $J_i = S_0 \cap S_i$, both folds succeed. At each $x \in J_i$, $f_i$ either takes the same branch as $f_0$ or the opposite. If the same branch:
$$g_i(x) = e(x) + \rho_i o(x), \quad g_0(x) = e(x) + \rho_0 o(x),$$
so $h_i(x) = \frac{g_i(x) - g_0(x)}{\rho_i - \rho_0} = o(x)$. This defines $E_i$.

If the opposite branch, writing $e'(x), o'(x)$ for the even/odd parts of the other branch:
$$g_i(x) = e'(x) + \rho_i o'(x), \quad g_0(x) = e(x) + \rho_0 o(x).$$
Computing:
$$h_i(x) = \frac{e'(x) - e(x) + \rho_i o'(x) - \rho_0 o(x)}{\rho_i - \rho_0} = o(x) + \frac{(e'(x) - e(x)) + \rho_i(o'(x) - o(x))}{\rho_i - \rho_0}.$$
Simplifying with $C(x) = o'(x) - o(x)$ and $D(x) = e'(x) - e(x)$:
$$h_i(x) = o(x) + C(x) + \lambda_i(D(x) + \rho_0 C(x)) = o'(x) + \lambda_i L(x),$$
where $L(x) = D(x) + \rho_0 C(x)$. This defines $F_i$.

**Size of $J_i$.** $|J_i| \ge |S_0| + |S_i| - N \ge 2T - N = 2(127N/128) - N = 63N/64 = AN$.

**Bound on $|E_i|$.** Construct $p_i(h) = (g_0(h^2) - \rho_0 h_i(h^2)) + h \cdot h_i(h^2) \in \mathrm{RS}[H, k]$. On $E_i$, $h_i(x) = o(x)$, so $p_i(h) = e(h^2) + h \cdot o(h^2) = f_0(h)$ and $p_i(-h) = f_0(-h)$. Thus $f_0$ agrees with $p_i \in V$ on $\ge 2|E_i|$ positions. Since $f_0$ is $1/2$-far from $V$, we need $2|E_i| < n = 2N$, giving $|E_i| < N/2$.

**Bound on $|F_i|$.** $|F_i| = |J_i| - |E_i| > AN - N/2 = (63/64 - 1/2)N = 31N/64$. $\blacksquare$

---

## Proof of the Main Theorem

Fix a rectangle $R(a,b)$ and assume $r = R < \left(\frac{95-8\sqrt{79}}{64}\right)^2$. We shall show $|X_R| = O_R(1)$.

If $X_R = \emptyset$, there is nothing to prove. Otherwise, fix any $\rho_0 \in X_R$ with valid witness $(f_0, \rho_0, g_0)$. By Lemma 2, $f_0$ determines $\rho_0$ uniquely. By Lemma 3, $g_0$ is one of at most $7$ codewords for this $\rho_0$.

For each other $\rho_i \in X_R \setminus \{\rho_0\}$, fix a valid witness $(f_i, \rho_i, g_i)$ and apply Lemma 7 to obtain the decomposition $J_i = E_i \sqcup F_i$, the polynomial $h_i = (g_i - g_0)/(\rho_i - \rho_0) \in \mathrm{RS}[H^2, k']$, and the constant $\lambda_i = (\rho_i - \rho_0)^{-1}$.

### Choice of threshold

Since $r < \left(\frac{95-8\sqrt{79}}{64}\right)^2$, we can choose $\beta$ with $\sqrt{r} < \beta$ such that $(A - \beta)^2 > \beta$. Concretely, the quadratic $(A - \beta)^2 = \beta$ has positive root
$$\beta_* = \frac{2A + 1 - \sqrt{4A + 1}}{2} = \frac{95 - 8\sqrt{79}}{64} \approx 0.3734,$$
and $(A - \beta)^2 > \beta$ holds for $\beta < \beta_*$. The hypothesis $r < \beta_*^2$ ensures $\sqrt{r} < \beta_*$, so we may choose any $\beta \in (\sqrt{r}, \beta_*)$.

### Partition into Type A and Type B

Partition the non-reference witnesses into:
- **Type A:** those with $|E_i| > \beta N$;
- **Type B:** those with $|E_i| \le \beta N$.

### Bounding Type A

For a Type A witness, $h_i \in \mathrm{RS}[H^2, k']$ agrees with the function $o$ on $|E_i| > \beta N$ positions. Since $\beta^2 > r$, by Lemma 6, the number of distinct such polynomials $h_i$ is at most $L_r(\beta) = \frac{\beta - r}{\beta^2 - r}$.

For each fixed value of $h$, the codewords $g_i = g_0 + (\rho_i - \rho_0)h$ all lie on a single affine line in $\mathrm{RS}[H^2, k']$. By Lemma 4, each affine line supports at most $4$ valid parameters. Hence:

$$|\text{Type A}| \le 4\, L_r(\beta) = O_R(1).$$

### Bounding Type B via a graph coloring argument

For a Type B witness, $|E_i| \le \beta N$ and therefore $|F_i| = |J_i| - |E_i| \ge AN - \beta N = (A - \beta)N$. Write $\alpha = A - \beta$.

**Define the overlap graph $G_B$.** The vertex set is the set of all Type B witnesses. Place an edge between $i$ and $j$ whenever $|F_i \cap F_j| > \beta N$.

**Step 1: Bounding the degree of $G_B$.**

Fix a Type B witness $i$ and consider a neighbor $j$ (so $|F_i \cap F_j| > \beta N$). On $F_i \cap F_j$:
$$h_i(x) - h_j(x) = (\lambda_i - \lambda_j) L(x).$$
Define the **cross-slope** polynomial $C_{ij} = \frac{h_i - h_j}{\lambda_i - \lambda_j} \in \mathrm{RS}[H^2, k']$. Then $C_{ij}$ agrees with the function $L$ on $F_i \cap F_j$, which has size $> \beta N$.

Since $\beta^2 > r$, Lemma 6 implies there are at most $L_r(\beta)$ distinct polynomials in $\mathrm{RS}[H^2, k']$ agreeing with $L$ on $> \beta N$ positions. So the cross-slopes $\{C_{ij}\}$ take at most $L_r(\beta)$ distinct values as $j$ ranges over the neighbors of $i$.

For each fixed cross-slope value $w$, all neighbors $j$ with $C_{ij} = w$ satisfy $h_j = h_i + (\lambda_j - \lambda_i)w$. Define $\tilde{h} = h_i - \lambda_i w \in \mathrm{RS}[H^2, k']$ (independent of $j$). Then $h_j = \tilde{h} + \lambda_j w$, and:
$$g_j = g_0 + (\rho_j - \rho_0)h_j = g_0 + (\rho_j - \rho_0)\tilde{h} + (\rho_j - \rho_0)\lambda_j w = g_0 + (\rho_j - \rho_0)\tilde{h} + w,$$
using $(\rho_j - \rho_0)\lambda_j = 1$. Therefore:
$$g_j = \underbrace{(g_0 + w - \rho_0\tilde{h})}_{\text{constant}} + \rho_j\,\tilde{h}.$$
This is an affine line in $\mathrm{RS}[H^2, k']$ parameterized by $\rho_j$. By Lemma 4, at most $4$ valid parameters $\rho$ lie on this line (including $\rho_i$ itself). Hence at most $3$ neighbors of $i$ share each cross-slope value.

Therefore: $\deg(i) \le 3\, L_r(\beta)$.

**Step 2: Bounding the independence number of $G_B$.**

Let $I \subseteq V(G_B)$ be an independent set. For distinct $i, j \in I$, $|F_i \cap F_j| \le \beta N$ (no edge). Each $|F_i| \ge \alpha N = (A - \beta)N$. By Lemma 5 (Fractional Johnson Bound) with parameters $\alpha = A - \beta$ and pairwise overlap bound $\beta$, and using $(A - \beta)^2 > \beta$ (guaranteed by $\beta < \beta_*$):
$$|I| \le \frac{\alpha - \beta}{\alpha^2 - \beta} = \frac{A - 2\beta}{(A - \beta)^2 - \beta}.$$

**Step 3: Combining via chromatic number.**

By the greedy coloring bound, $\chi(G_B) \le \Delta(G_B) + 1 \le 3L_r(\beta) + 1$. Each color class is an independent set of size at most $\frac{A - 2\beta}{(A-\beta)^2 - \beta}$. Therefore:
$$|\text{Type B}| \le \chi(G_B) \cdot \frac{A - 2\beta}{(A-\beta)^2 - \beta} \le (3L_r(\beta) + 1) \cdot \frac{A - 2\beta}{(A-\beta)^2 - \beta} = O_R(1).$$

### Conclusion

The total size of the good set is:
$$|X_R| \le 1 + |\text{Type A}| + |\text{Type B}| \le 1 + 4L_r(\beta) + (3L_r(\beta) + 1) \cdot \frac{A - 2\beta}{(A-\beta)^2 - \beta} = O_R(1),$$
completing the proof. $\blacksquare$

---

## Explicit Computation of the Rate Threshold

The proof requires the existence of $\beta$ with $\sqrt{r} < \beta$ and $(A - \beta)^2 > \beta$. The maximum $\beta$ satisfying the second condition solves $(A - \beta)^2 = \beta$:
$$\beta^2 - (2A+1)\beta + A^2 = 0 \implies \beta_* = \frac{2A + 1 - \sqrt{4A + 1}}{2}.$$

With $A = 63/64$:
$$\beta_* = \frac{2 \cdot \frac{63}{64} + 1 - \sqrt{4 \cdot \frac{63}{64} + 1}}{2} = \frac{\frac{95}{32} - \sqrt{\frac{79}{16}}}{2} = \frac{95 - 8\sqrt{79}}{64} \approx 0.3734.$$

The constraint $\sqrt{r} < \beta_*$ gives:
$$r < \beta_*^2 = \left(\frac{95 - 8\sqrt{79}}{64}\right)^2.$$

Numerically, $\sqrt{79} \approx 8.8882$, so $\beta_* \approx 0.37335$ and $r < 0.13939$.
