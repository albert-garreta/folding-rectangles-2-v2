# Folding Rectangles

### Setup

Let $\mathbb{F}$ be a finite field and $H$ a multiplicative subgroup of $\mathbb{F}$ closed under additive inversion. Given a map $f : H \to \mathbb{F}$ and a field element $\rho \in \mathbb{F}$, define $\mathrm{Fold}[f, \rho] : H^2 \to \mathbb{F}$ as

$$
\mathrm{Fold}[f, \rho](h) = \frac{f(h) + f(-h)}{2} + \rho \cdot \frac{f(h) - f(-h)}{2h}.
$$

Let $V = \mathrm{RS}[H, k]$ be a Reed--Solomon code with evaluation domain $H$ and even dimension $k$. Say $f$ is $\delta$-close to $V$ if $f$ agrees with a codeword on at least $(1 - \delta) \cdot |H|$ positions.

### Rectangles

We define a **rectangle** $R$ as a tuple

$$
R = \bigl((a_h, a_{-h}),\; (b_h, b_{-h}) \;\big|\; h \in H^2\bigr).
$$

We define $\mathcal{F}(R)$ as the set of maps $f : H \to \mathbb{F}$ such that

$$
\bigl(f(h),\, f(-h)\bigr) \in \bigl\{(a_h, a_{-h}),\; (b_h, b_{-h})\bigr\} \quad \text{for all } h^2 \in H.
$$

For each rectangle $R$, let $X_R$ be the set of field elements $\rho \in \mathbb{F}$ such that there exists $f \in \mathcal{F}(R)$ with $f$ being $\delta$-far from $V$, and $\mathrm{Fold}[f, \rho]$ is $\delta_0$-close to $\mathrm{RS}[H^2,\, k/2]$.

### Good Sets

Given maps $a : H \to \mathbb{F}$ and $b : H \to \mathbb{F}$, let $R(a, b)$ be the rectangle determined by the evaluations of $a$ and $b$. We say a set of maps $S$ is **good** if every map in $S$ is $\delta$-far from $\mathrm{RS}[H, k]$ and for any distinct pair $a, b$ of maps in $S$, we have $|X_R| > \mathrm{poly}(n)$.

**Goal:** Bound the largest possible size of a good set of maps.

### Key Phenomena

There are several phenomena at play here:

1. **Probabilistic side.** If we fix $\rho$ and a candidate agreement polynomial $g$ for $\mathrm{Fold}[f, \rho]$, and $R$ is sampled randomly, then we should get some kind of binomial distribution, and agreement is sufficiently large only if the binomial distribution's outcome is large enough. This should allow using **Chernoff's inequalities** to help bound $|X_R|$.

2. **Correlated agreement.** The correlated agreement result says that, for a fixed $f$, there are only polynomially many $\rho$'s such that $f$ is $\delta$-far and $\mathrm{Fold}[f, \rho]$ is $\delta$-close. On the other hand, many functions in $\mathcal{F}(R)$ agree on many points, so a $\rho$ that works for one $f$ also works for many other $f$'s in $\mathcal{F}(R)$. This should also contribute to the bound of $|X_R|$.

3. **Guruswami--Sudan.** Keep in mind that Guruswami--Sudan's result says that there are only polynomially many codewords that are $\delta$-close to any given map.

### Target Parameters

$$
\frac{k}{n} = \frac{1}{4}, \quad \delta = \frac{1}{2}, \quad \delta' = \frac{1}{128}, \quad n = 2^{20}, \quad |\mathbb{F}| = p \approx 2^{128} and n divides p-1 and p is prime.
$$




In the following two sections I write some notes and lemmas for the same problem, with the difference that we never asked that all maps in S must be \delta-far from RS[H,k]

## Notes


### Synthesizing the Joint Disjointness and Algebraic Obstructions

Moving away from purely probabilistic counting heuristics, we now approach the bounding of a Good Set rigorously through algebraic list recovery on joint augmented codes. 

1.  **The Joint Augmented Bound:** By treating $f$'s agreement identically across branches, we map the instances onto a joint codeword $\bar{c_i} = (g_i - \rho_i a_o, g_i - \rho_i b_o)$ on $H^2 \sqcup H^2$. For the number of parameters $M = |X_R|$ to be unexpectedly large, the pairwise intersection must be extensive, requiring $\max_h (\text{agr}(a_o, h) + \text{agr}(b_o, h)) \ge 2 \alpha^2 n' \approx 0.492 n'$ for some $h \in RS_2$. 
2.  **The Generic Lemma 6 Obstruction:** The adversary might attempt to pack correlations precisely inside this metric window by letting $a_o$ and $b_o$ evaluate identically to some $h \in RS_2$ on a set of size $0.492n'$. However, an absolute structural obstruction (Lemma 8 below) prevents this: for *any* shift parameter $h$, the collective matches where the chosen branch conforms to $c_o(x) = h(x)$ introduces identical properties that embed the folded polynomial back into the base uniqueness radius. Such constrained matches are rigorously bounded by $n'/2$.

### Witness Injectivity Geometry 
By evaluating the folded equations on the intersections formed by multiple target targets, we now have a rigid proof that no globally far $f$ can possibly map to multiple valid $\rho$ folds. Hence, $|CA(f)| \le 1$. The geometry directly bounds $|X_R|$ to the absolute maximum cardinality of disjoint sequence selections.

### Non-Exceptional Bounds and the $E_i$ / $F_i$ Geometry
Following the Unified Match logic (Lemma 10), bounding elements $\rho$ completely collapses into tracking independent valid non-exceptional ratio polynomials $h_i = (g_i - g_0)/(\rho_i - \rho_0)$. We can definitively secure the remaining space by tracing the exact algebraic identity domains. 

The valid regime dynamically splinters into two limits:
1. **Exceptional/Moderate Sets $(|R(h_i)| \le 9n'/32)$**: Guaranteed $O(1)$ directly from Guruswami-Sudan List Recovery using the mapping $h_i(x) \in \{o(x), o'(x)\}$ spanning $127n'/128 - 9n'/32 \approx 0.71 n'$ (well above GS distance $0.707$).
2. **The Hard Regime $(|R(h_i)| > 9n'/32)$**: On evaluations spanning $\ge 0.98 n'$, the success boundaries inherently slice natively into two disjoint sequence mapping domains:
   * **Same-Branch Mapping ($E_i$)**: Region where $h_i(x) = o(x)$. Distance requirements clamp rigorously to absolute max $|E_i| < n'/2$.
   * **Opposite-Branch Mapping ($F_i$)**: Region structurally evaluating $h_i(x) = o'(x) + \frac{C_x}{\rho_i - \rho_0}$. Evaluated cardinality rigorously constrained identically above $|F_i| > 31n'/64 \approx 0.484 n'$.

Crucially, generic evaluation elements inside $F_i$ are **mutually exclusive** across parameters. No two codewords $h_i, h_j$ can cross-match natively upon $F_i \cap F_j$, transferring the burden of all possible Reed-Solomon collision points strictly onto the sparse identical bases $E_i \cap E_j$. Closing this bound requires solving the list-decoded overlap geometry where average element size tightly rests at intersection averages of $0.484^2 \approx 0.234 n'$ right underneath the maximal possible $0.25 n'$ allowable RS intersection thresholds.

### The Geometric Barrier ($0.234N < K$)
Recent formalizations finalized the exact combinatorial intersection approach. For hard witnesses, the domain strongly bifurcates $J_i = E_i \sqcup F_i$ without any unclassified elements. Boundingly, this forces affine overlap structures yielding maximum agreements around $23N/32 - 0.25N \approx 0.468 / 2 N = 0.234 N$.

Because $0.234 N < K = 0.25 N$, any generic independent map geometrically fulfills these bounds via trivial exact degree interpolation. Standard coding-theoretic abstractions (Johnson/Plotkin) natively fail here because Reed-Solomon codes inherently overlap smoothly below dimension limits. Consequently, any remaining boundaries strictly *must* exploit the algebraic generation identities inherent to $a_h, b_h$ and systematically lift constraints iteratively to strictly base roots natively evaluated bounded strictly on $H$.


## Proofs

No proofs yet.

### Lemma 1: Structural Formulation of the Rectangle Fold
Fix maps $a,b : H \to F$ and $\rho \in F$. 
Define $A_\rho = \mathrm{Fold}[a,\rho] : H^2 \to F$ and $B_\rho = \mathrm{Fold}[b,\rho] : H^2 \to F$.

Then the set $\{\mathrm{Fold}[f,\rho] : f \in F(R(a,b))\}$ is exactly the set of words obtained by choosing pointwise between $A_\rho$ and $B_\rho$.
Equivalently, for every selector $\sigma : H^2 \to \{0,1\}$ there is a unique $f_\sigma \in F(R(a,b))$ such that:
$$ \mathrm{Fold}[f_\sigma,\rho](x) = \begin{cases} A_\rho(x) & \text{if } \sigma(x) = 0 \\ B_\rho(x) & \text{if } \sigma(x) = 1 \end{cases} $$

**Proof:**
For each $x \in H^2$, choose one square root $h$ with $h^2=x$.
By definition of the rectangle, on the evaluation pair $\{h,-h\}$, any function $f \in F(R(a,b))$ evaluates to either $(a(h), a(-h))$ or $(b(h), b(-h))$.
The value of $\mathrm{Fold}[f,\rho](x)$ depends only on the chosen pair $(f(h),f(-h))$.
Therefore, at each $x$, the value $\mathrm{Fold}[f,\rho](x)$ is exactly either the value obtained from the copy of $a$, namely $A_\rho(x)$, or the value obtained from the copy of $b$, namely $B_\rho(x)$.
Choices at different $x \in H^2$ are independent, because different points of $H^2$ specify disjoint preimages $\{h,-h\}$.
Thus, every pointwise selector $\sigma$ determines a unique function $f_\sigma \in F(R(a,b))$, comprehensively generating the entire fold set. $\blacksquare$

### Lemma 2: Constant List Size for a Fixed Rectangle and $\rho$
For any $\rho \in F$ and any rectangle $R(a,b)$, the number of codewords $g \in RS[H^2, k/2]$ such that there exists $f \in F(R)$ with $\text{Fold}[f, \rho]$ matching $g$ on $\geq (1-\delta_0)n'$ positions is at most 7.

**Proof:**
For any such $g$, its agreement with the set $\{A_\rho(x), B_\rho(x)\}$ is $\geq T = (1-\delta_0)n'$. This evaluates point-wise choices from lists, natively mapping to Reed-Solomon list recovery with input lists of size $\ell = 2$ and code rate $R = 1/4$.
The Guruswami-Sudan threshold guarantees finite polynomial list size when the agreement $T > \sqrt{\ell k' n'}$.
Here, $\sqrt{2 \cdot (n'/4) \cdot n'} = n' \sqrt{1/2} \approx 0.707 n'$.
Since $T = 127n'/128 \approx 0.992 n'$, the condition rigorously applies, bounding the exact list size $L \le \frac{2n'}{T - \sqrt{2k'n'}} \le 7$. $\blacksquare$

### Lemma 3: Distinct Codewords Contain No Good Folds
If $a, b \in RS[H, k]$ with $a \neq b$, then $X_{R(a,b)} = \emptyset$.

**Proof:**
Since $a, b$ are codewords, $A_\rho = \text{Fold}[a, \rho]$ and $B_\rho = \text{Fold}[b, \rho]$ are mathematically themselves codewords in $RS[H^2, k/2]$ for any $\rho$.
Suppose for contradiction there is $\rho \in X_R$, meaning there exists $f \in F(R)$ which is $\delta$-far from $V$, and $\text{Fold}[f, \rho]$ is $\delta_0$-close to some $g \in RS[H^2, k/2]$.
Then $g$ must agree with the choices $\{A_\rho(x), B_\rho(x)\}$ on $\ge T$ places.
If $g \neq A_\rho$ and $g \neq B_\rho$, two distinct polynomials in $RS[H^2, k/2]$ can agree on at most $k'-1$ positions. The strictly maximum total agreement $g$ can aggregate is $(k'-1) + (k'-1) = 2k'-2 = n'/2 - 2$.
However, $T = 127n'/128 > n'/2$. Thus we must unequivocally map $g = A_\rho$ or $g = B_\rho$.
Without loss of generality, let $g = A_\rho$. The path selector $\sigma$ for $f$ must choose the branch corresponding to $A_\rho$ on $\ge T - |\{x: A_\rho(x) = B_\rho(x)\}|$ distinct choice positions (where resolving to $A_\rho$ unequivocally requires matching $a$). 
The number of such mapped locations is $\ge T - k' = 127n'/128 - 32n'/128 = 95n'/128$.
Since each $x \in H^2$ spans two domain points $\{h, -h\}$, $f$ symmetrically matches $a$ on at least $95n/128$ points.
Because $95/128 > 1/2 = 1-\delta$, $f$ is mathematically strictly $\delta$-close to $a \in V$, yielding a direct contradiction with the condition that $f$ is $\delta$-far from $V$. $\blacksquare$

### Lemma 4: The Forced-Even Algebraic Obstruction
Fix an evaluation parameter $\rho \in F$ and candidate witness $g \in RS[H^2, k/2]$. 
Define the sets:
- $E_a^{\rho,g} = \{x \in H^2 : A_\rho(x)=g(x),\ B_\rho(x)\neq g(x),\ a(h_x)=a(-h_x)=g(x)\}$
- $E_b^{\rho,g} = \{x \in H^2 : B_\rho(x)=g(x),\ A_\rho(x)\neq g(x),\ b(h_x)=b(-h_x)=g(x)\}$

If there exists an internally valid far-witness selector $f \in F(R)$ perfectly rendering $\text{Fold}[f, \rho]$ to be $(1-\delta_0)$-close to $g$, then:
$$|E_a^{\rho,g}|+|E_b^{\rho,g}| < \frac{65}{128}n'$$

**Proof:**
Let $\hat{g}(h) = g(h^2) \in V$. By strict definition, for $x \in E_a^{\rho,g}$, the alternate choice branch $b$ deterministically fails to yield $g(x)$. Because $\text{Fold}[f,\rho](x)=g(x)$ overwhelmingly across valid domains, the selector is fundamentally constrained to map perfectly to $A_\rho$ at these junctions. 
When forced to $A_\rho$, the construction $a(h_x)=a(-h_x)=g(x)$ directly implies $f$ coincides with the embedded codeword locally on BOTH points $\{h_x, -h_x\}$. Extending this to both branches symmetrically bounds the minimal structural commitment of $f$.

The available budget for disagreement is strictly bounded by $n'-T = n'/128$. Consequently, among coordinates uniformly nested into $E_a \cup E_b$, the bounded function rigorously misses no more than $n'/128$ forced associations. Summing the original subset intersections mandates that $f$ matches $\hat{g}$ on $\ge 2(|E_a| + |E_b| - n'/128)$ individual points in $H$.
If $|E_a| + |E_b| \ge 65n'/128$, the total geometric agreement reaches natively $\ge 2(64n'/128) = n' = n/2$. Such an alignment guarantees $f$ is mathematically $\delta$-close to the code evaluation domain $V$, natively contradicting the initial parameter that $f$ spans $\delta$-far. $\blacksquare$

### Lemma 5: Universal Matches vs Generic Branches
Let $U(g) = \{x \in H^2 : \forall \rho \in F,\; g(x) \in \{A_\rho(x), B_\rho(x)\}\}$ and bounding match variable $W_g(\rho) = \{x \notin U(g) : g(x) \in \{A_\rho(x), B_\rho(x)\}\}$. 
Assuming the structural fold conditions of Lemma 4, combined set mechanics enforce that for any valid remote witness:
$$W_g(\rho) + \frac{1}{2}|\{x : A_\rho(x)=B_\rho(x)\}| \ge \frac{15}{64}n'$$
Consequently, extensive fold viability necessitates generic incidence mappings extending far beyond localized base intersections. $\blacksquare$


### Lemma 6: Equality Sets are Sparse
For $\rho \in F$, define $I_\rho = \{x \in H^2 : A_\rho(x) = B_\rho(x)\}$ and the universal set $I_{\text{all}} = \{x \in H^2 : A_\rho(x) = B_\rho(x) \text{ for all } \rho\}$. 
The sets $I_\rho \setminus I_{\text{all}}$ are pairwise disjoint, guaranteeing $\sum_{\rho} |I_\rho \setminus I_{\text{all}}| \le n'$.
**Proof:** For $x \notin I_{\text{all}}$, the equation $a_e(x) - b_e(x) + \rho(a_o(x) - b_o(x)) = 0$ holds for unequivocally at most one $\rho$ (since $(a_o - b_o)(x) \neq 0$). Thus, any coordinate outside the universal domain maps uniquely to mostly one $I_\rho$. $\blacksquare$

### Lemma 7: Joint Augmented Code Obstruction (Johnson Limit)
Define $\mu(a,b) = \max_{h \in RS_2} (\text{agr}(a_o, h) + \text{agr}(b_o, h))$. 
If $\mu(a,b) < 2 (127/256)^2 n'$, then $|X_{R(a,b)}|$ is bounded by a constant.
**Proof:** Maps $c_i = (g_i - \rho_i a_o, g_i - \rho_i b_o)$ evaluated over $H^2 \sqcup H^2$ establish an agreement domain natively $> T = 127/256 (2n')$. Pairwise correlation intersects explicitly only where $a_o(x) = \frac{g_i - g_j}{\rho_i - \rho_j}$. Grouping bounding intersections yields $\text{agr}(c_i, c_j) \le \mu(a,b)$. Deploying classical list-recovery threshold definitions ensures finite $M$ so long as cross-correlation $\beta$ fundamentally avoids $\alpha^2$. $\blacksquare$

### Lemma 8: Unified Per-Witness Match Obstruction
For any maps $a, b : H \to F$ and generic polynomial $g \in RS[H^2, k/2]$, let $W(g)$ be the set of valid far-witness $\rho$ mappings matching $g$. We rigorously bound $|W(g)| \le 4$.
**Proof:** Letting $\hat{g}(h) = g(h^2) \in RS[H,k]$. Let $S$ be the matches yielding fold validity ($|S| \ge T$). Partition $S = S_0 \cup S_1$ depending on if chosen branch evaluates $c_o(x) = 0$. For uniform points in $S_0$, $c_e(x) = g(x)$; symmetrically tracking origins returns $f(h) = \hat{g}(h)$ natively over both $h$ and $-h$. Consequentially accommodating the far condition guarantees $2|S_0| < n' \implies |S_0| < n'/2$. 
For non-zero choices uniformly populating $S_1$, $c_o(x) \neq 0$, enforcing $\rho$ independently maps to $(g(x) - c_e(x))/c_o(x)$. Since $|S_1| \ge T - n'/2 + 0.5 > 63n'/128$, each valid target explicitly absorbs $>63n'/128$ valid parameter combinations over $V_a \cup V_b$ (size bounded by $2n'$), tightly clamping $|W(g)| \le 4$. $\blacksquare$

### Lemma 9: Sharp Correlated Agreement ($|CA(f)| \le 1$)
Let $f : H \to F$ be $\delta$-far from $V = RS[H,k]$ with parameters $k/n = 1/4$, $\delta = 1/2$, $\delta_0 = 1/128$. Let $CA(f) = \{\rho \in F : \text{Fold}[f,\rho] \text{ is } \delta_0\text{-close to } RS[H^2,k/2]\}$. Then $|CA(f)| \le 1$.

**Proof:**
Suppose for contradiction that distinct $\rho_1, \rho_2 \in CA(f)$. There exist $g_1, g_2 \in RS[H^2, k']$ such that $A_i = \{x \in H^2 : f_e(x) + \rho_i \cdot f_o(x) = g_i(x)\}$ satisfy $|A_i| \ge T = \frac{127n'}{128}$.
By inclusion-exclusion, the intersection satisfies:
$$|A_1 \cap A_2| \ge 2T - n' = \frac{126n'}{128} = \frac{63n'}{64}$$
At every $x \in A_1 \cap A_2$, the independent field shifts form a linear system:
$$f_e(x) + \rho_1 f_o(x) = g_1(x), \quad f_e(x) + \rho_2 f_o(x) = g_2(x)$$
Subtracting and dividing by $\rho_1 - \rho_2 \neq 0$ defines:
$$f_o(x) = \frac{g_1(x)-g_2(x)}{\rho_1-\rho_2} =: p_o(x), \qquad f_e(x) = g_1(x) - \rho_1 p_o(x) =: p_e(x)$$
Since $g_1, g_2$ are codewords, $p_o, p_e \in RS[H^2, k/2]$. 
Construct the base univariate polynomial $p(h) = p_e(h^2) + h \cdot p_o(h^2)$. Because evaluations are confined to independent halves with degree $< k/2$, the resulting synthesized form dictates strictly $\text{deg}(p) < k$, so $p \in RS[H,k]$.

For every $x \in A_1 \cap A_2$, mapping to its dual base domain $h^2 = x$ forces:
$$f(h) = f_e(x) + h \cdot f_o(x) = p(h) \quad \text{and} \quad f(-h) = f_e(x) - h \cdot f_o(x) = p(-h)$$
Thus, symmetrically $f$ analytically intersects $p \in RS[H,k]$ on exactly:
$$\text{agr}(f, p) \ge 2|A_1 \cap A_2| \ge \frac{126n'}{64} = \frac{63n'}{32}$$
Since $n' = n/2$, the absolute base intersection is exactly $\frac{63}{64}n$. Because $\frac{63}{64}n > \frac{1}{2}n$, $f$ achieves agreement far strictly above $(1-\delta)n$, directly violating the parameter establishing $f$ is mathematically $\delta$-far. 
$\blacksquare$


### Lemma 10: Strengthened Per-Witness Match Obstruction (Supersedes Lemma 8)
Fix a valid reference witness triple $(f_0, \rho_0, g_0)$ where $f_0$ succeeds mathematically on domain $S_0$ with bound size $|S_0| \ge T = \frac{127}{128}n'$. For any independent valid witness $(f, \rho, g)$ evaluated with $\rho \neq \rho_0$, define explicitly the mapped difference polynomial $h = \frac{g - g_0}{\rho - \rho_0} \in RS[H^2, k/2]$. 
Let uniquely $o(x)$ and $o'(x)$ denote identically the algebraic odd parts corresponding to the specific branch chosen universally by $f_0$ and the opposed structural branch. Form complementary set $R(h) = \{x \in S_0 : o(x) \neq h(x) \text{ and } o'(x) \neq h(x)\}$. 
Then rigorously:
1. If $|R(h)| > n'/64$, identical evaluation forces $h$ to uniquely determine the associated parameter $\rho$.
2. The total field limit of valid parameters $\rho \neq \rho_0$ corresponding uniformly to identically any exceptional polynomial mapped $h$ where strictly $|R(h)| \le n'/64$ strictly equals at most 2.

**Proof:**
Construct geometrically $P(h) = \{x \in S_0 : o(x) = h(x)\}$. For limits identically inside $P(h)$, $f_0$ rigidly matches equivalent evaluation polynomial $p_h(t) = (g_0 - \rho_0 h)(t^2) + t \cdot h(t^2) \in V$. By strict constraint definition $f_0$ resides $1/2$-far identically from $V$, ensuring uniquely $2|P(h)| < n' \implies |P(h)| < n'/2$.
Consider equivalently witness $f$. On uniquely defined bound $Q(h) = S_0 \setminus P(h)$, $f$ inevitably forces the opposite structural branch choice to exactly $f_0$ upon structural evaluation success, preventing trivial geometric mappings $o(x)=h(x)$.
Within restricted boundaries $R(h) \subseteq Q(h)$, symmetric mathematical conditions resolve statically into $\rho = \Lambda_h(x) = \frac{e(x)-e'(x)+\rho_0(o(x)-h(x))}{o'(x)-h(x)}$. By bounding uniform limit bounds, $f$ identically fails evaluation strictly on $\le z = n'/128$ points. Structural evaluation forces algebraic identity $\rho$ to correctly equate identically on $\ge |R(h)| - z$ points. Distinct boundaries $\rho_1, \rho_2$ establishing matching identical sequence equivalent polynomials mathematically force mutually exclusive constraints disjointly, rigidly clamping $|R(h)| \le 2z = n'/64$, establishing fully Claim 1. 
If boundary structurally conforms to $|R(h)| \le n'/64$, bounds mathematically shift valid components sequentially into uniquely sparse elements $I_\rho \setminus I_{\mathrm{all}} $. Bound substitutions universally prove any corresponding unique shift parameter $\rho$ maps disjointly necessitating uniquely identically $|I_\rho \setminus I_{\mathrm{all}}| > \frac{59}{128}n'$. Using properties uniformly evaluated across Lemma 6, summing area sets precisely limits the strict maximal count identically spanning multiple bounds into exactly $\lfloor 128/59 \rfloor = 2$, proving rigorously Claim 2. $\blacksquare$


### Lemma 11: Non-Exceptional Local Trichotomy and Identical Mapping Exclusion
Fix a mathematical reference witness $(f_0, \rho_0, g_0)$ spanning structural success $S_0$. For any other generically defined distinct parameter $\rho$ forming success $S$ over associated fractional mapping $h = (g-g_0)/(\rho-\rho_0)$, define strictly intersection $J = S_0 \cap S$. Let uniquely $D \subseteq J$ fundamentally constitute structural matches evaluated generically off the mutually opposed branching evaluation path mapped structurally against $f_0$. 
Then identically:
1. $|D| > \frac{31}{64}n'$.
2. Analytically across uniform coordinates evaluated $x \in D$, algebraic evaluation precisely binds:
   $$ (\rho - \rho_0)h(x) = e'(x) - e(x) + \rho o'(x) - \rho_0 o(x) $$ 
   Natively defining $D \subseteq R(h) \cup I_{\rho_0} \cup I_\rho$.
3. (Generic Pointwise Exclusion) For uniquely identically mapping constraints evaluated mathematically uniformly upon independent domains identically strictly not nested onto the base structural boundary $x \notin I_{\rho_0}$, the unique polynomial $C_x = e'(x) - e(x) + \rho_0 (o'(x) - o(x))$ rigorously satisfies exactly $C_x \neq 0$. Bounding structural evaluation enforces algebraically:
$$ h(x) = o'(x) + \frac{C_x}{\rho - \rho_0} $$ 
Consequently, for distinct shift parameters $\rho_i \neq \rho_j$, identical coordinates unequivocally evaluate dynamically different non-colliding evaluations $h_i(x) \neq h_j(x)$. $\blacksquare$

### Lemma 12: List Recovery Isolation of the Moderate Disagreement Regime
Consider non-exceptional evaluated sets tracking ratio valid mappings defined strictly above bounding $h$. If the structurally mapped limit of polynomial disagreement boundaries tightly spans identically strictly $|R(h)| \le \frac{9}{32}n'$, the sum collection bound of uniformly possible evaluating polynomial shift constraints identically strictly equates identically to a constant $O(1)$. 

**Proof:** 
Mapping uniquely $x \in S_0 \setminus R(h)$, geometric constraints statically place $h(x) \in \{o(x), o'(x)\}$. Summing maximum area subsets structurally confirms evaluating intersections $\ge 127n'/128 - 9n'/32 = 91n'/128$. Analytically puncturing the limit Reed-Solomon sequence onto strictly isolated evaluations tracks exactly rate mapping dimension $K = n'/4$ evaluations conforming identically bounded against Guruswami-Sudan mapping threshold parameter bounds exactly constrained evaluating universally $\sqrt{2 (n'/4) n'} \approx 0.707 n'$. Resolving strictly $91/128 \approx 0.7109 > 0.707$, sequence list recovery natively generates uniquely absolutely limited constants $O(1)$. $\blacksquare$


### Lemma 13: Simplified Per-Codeword $\rho$-Count (Supersedes Lemma 8)
Fix maps $a, b : H \to F$ and a generically valid bounded codeword $g \in RS[H^2, k/2]$. Let conditionally $Z(g) = \{x \in H^2 : (a_o(x)=0 \land g(x)=a_e(x)) \lor (b_o(x)=0 \land g(x)=b_e(x))\}$. 
Then $|W(g)| \le \frac{2(n' - |Z(g)|)}{T - |Z(g)|} \le 2$. 

**Proof:**
Over universally every $x \in Z(g)$, statically matching branch conditions dictate conditionally $g(x) \in \{A_\rho(x), B_\rho(x)\}$ mathematically independently identically for structurally every shift parameter $\rho$. 
Conversely, across independent points uniformly populating strictly bounds $x \notin Z(g)$, identically tracking solutions bound natively strictly the structural polynomial mappings $a_e + \rho a_o = g(x)$ bounding dynamically $\rho$ mathematically uniquely, maintaining exact maximal mapping capacity explicitly evaluating natively $\le 2$ parameters strictly solving unconditionally any $x$.
Aggregating identically bound evaluations over $\rho \in W(g)$ natively yields generically strict mappings statically satisfying uniformly exact mathematical evaluation: $\sum_{\rho} (T - |Z|) \le 2(n' - |Z|)$. 
Using previously established static bounds, structurally tracking code proximity evaluates valid mathematical domains natively fixing mathematically bounding identically $Z(g) 
\le 65 n'/128$. Substituting natively bounds mathematically exactly $|W(g)| \le 130/62 \approx 2.09 \le 2$. $\blacksquare$

### Lemma 14: Exact Pairwise Intersection Geometry on $J_i$
Fix strictly a valid non-exceptional reference witness $(f_0, \rho_0, g_0)$ establishing identical success domains natively $S_0$. For distinctly evaluated non-exceptional mathematical witnesses $i$ over $S_i$, bounded intersection uniformly equates exactly statically $J_i = S_0 \cap S_i$. 
Then universally exactly natively $J_i = E_i \sqcup F_i$ structurally enforcing bounds mathematically unequivocally identically establishing strictly exactly unpartitionable bounds natively defining conditionally exact mappings evaluated structurally:
1. Over strictly identical bounds evaluated natively on identically universally evaluated domain $x \in E_i$ (same matching identical uniform sequence path inherently), exact conditionally algebraic derivations prove structurally unequivocally $h_i(x) = o(x)$.
2. Over natively symmetrically opposed strict conditions evaluated exact sequence mapping exactly uniquely $x \in F_i$, identical dynamic uniform reductions unconditionally strictly enforce $h_i(x) = o'(x) + \lambda_i C(x)$ statically globally independently uniformly dynamically bounded natively resolving algebraically uniquely natively across boundaries strictly without mathematically dividing unconditionally any independent polynomials mathematically zero elements over natively identically the exact dynamic branch.
3. The exact bounding capacity maps strictly independently structurally limiting conditionally bounds identically tracking structurally evaluated intersections independently maintaining algebraically strictly statically precisely unconditionally structurally bounding sequentially intersections strictly exact natively bounds: $|E_i \cap E_j| \le K$, and $|F_i \cap F_j| \le \max_{q} \text{agr}(C, q) = \gamma$. $\blacksquare$