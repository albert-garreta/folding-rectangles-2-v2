# Analysis of the Hard Regime: Fiber Uniqueness and Disjoint Johnson Balls

## Overview

I will prove a new structural lemma that clarifies the geometry of hard-regime witnesses and identifies a concrete obstruction. The key results are:

1. **Quantitative fiber uniqueness** for hard polynomials (sharpening Lemma 10).
2. **Disjoint Johnson balls** when $|I_{\rho_0}|$ is small: different hard witness parameters correspond to non-overlapping list-decoding regions.
3. An explicit characterization of the bottleneck: the equality set $|I_{\rho_0}|$ controls the number of hard witnesses.

---

## Setup and Refined Notation

Fix a reference witness $(f_0, \rho_0, g_0)$ with agreement set $|S_0| \ge T = 127n'/128$. At each $x \in S_0$, the reference $f_0$ chooses branch $c_0(x) \in \{a, b\}$, defining:

- $o(x) = c_{0,o}(x)$, $e(x) = c_{0,e}(x)$ (chosen branch even/odd parts)
- $o'(x) = c'_{0,o}(x)$, $e'(x) = c'_{0,e}(x)$ (opposite branch)
- $C(x) = e'(x) - e(x) + \rho_0(o'(x) - o(x))$, $D(x) = o'(x) - o(x)$

**Key identity:** $C(x) = \pm \eta(x)$ where $\eta(x) = A_{\rho_0}(x) - B_{\rho_0}(x)$, so $C(x) = 0 \iff x \in I_{\rho_0}$.

For any hard witness $(f_j, \rho_j, g_j)$: $\lambda_j = 1/(\rho_j - \rho_0)$, $h_j = (g_j - g_0)/(\rho_j - \rho_0)$.

---

## Lemma A (Quantitative Fiber Uniqueness)

**Statement:** Let $h \in RS[H^2, k']$ be a hard-regime polynomial with $|R(h)| > 9n'/32$, where $R(h) = \{x \in S_0 : h(x) \notin \{o(x), o'(x)\}\}$. Define:

- $E_h = \{x \in S_0 : h(x) = o(x)\}$
- $Z_h = \{x \in S_0 : h(x) = o'(x), C(x) = 0\}$

Then $h$ admits at most $\left\lfloor \frac{n' - |E_h| - |Z_h|}{63n'/64 - |E_h| - |Z_h|} \right\rfloor$ valid parameters $\lambda$. In particular, when $|E_h| + |Z_h| < 23n'/32$, this count is **at most 1**.

**Proof:**

*Step 1: Partition of the domain.* For any valid $\lambda \neq 0$ and associated witness:

The overlap $J = S_0 \cap S_j$ has $|J| \ge 63n'/64$. On $J$, $h(x) \in \{o(x), o'(x) + \lambda C(x)\}$ at every point. The agreement set decomposes as $J = (E_h \cap J) \sqcup (F_h(\lambda) \cap J)$ where:

$$F_h(\lambda) = \{x : h(x) = o'(x) + \lambda C(x)\}$$

*Step 2: Fiber structure.* For $x$ with $C(x) \neq 0$ and $h(x) \neq o(x)$: the equation $h(x) = o'(x) + \lambda C(x)$ uniquely determines $\lambda = \Lambda_h(x) := (h(x) - o'(x))/C(x)$. Define $V_h = \{x : C(x) \neq 0, h(x) \neq o(x), h(x) \neq o'(x)\}$.

Since $R(h) \cap E_h = \emptyset$ and $R(h) \cap Z_h = \emptyset$ (by definition), we have $R(h) \subseteq V_h \cup (H^2 \setminus S_0)$.

For a valid $\lambda$: the set $\{x \in V_h : \Lambda_h(x) = \lambda\}$ constitutes the "non-trivial" part of $F_h(\lambda)$. Counting:

$$|F_h(\lambda) \cap J| = |Z_h \cap J| + |\{x \in V_h \cap J : \Lambda_h(x) = \lambda\}|$$

The condition $|J| = |E_h \cap J| + |F_h(\lambda) \cap J| \ge 63n'/64$ gives:

$$|\{x \in V_h \cap J : \Lambda_h(x) = \lambda\}| \ge 63n'/64 - |E_h| - |Z_h| := \tau_h$$

*Step 3: Counting valid $\lambda$'s.* On $V_h$, the function $\Lambda_h$ maps each point to a unique field element. The total:

$$\sum_{\lambda \in \mathbb{F}} |\{x \in V_h : \Lambda_h(x) = \lambda\}| = |V_h| \le n' - |E_h| - |Z_h|$$

The number of $\lambda$'s with fiber size $\ge \tau_h$ is at most:

$$\frac{n' - |E_h| - |Z_h|}{\tau_h} = \frac{n' - |E_h| - |Z_h|}{63n'/64 - |E_h| - |Z_h|} = 1 + \frac{n'/64}{63n'/64 - |E_h| - |Z_h|}$$

*Step 4: Hard-regime constraint.* Since $|R(h)| > 9n'/32$ and $R(h) \subseteq S_0 \setminus (E_h \cup Z_h)$:

$$|E_h| + |Z_h| \le |S_0| - |R(h)| < n' - 9n'/32 = 23n'/32$$

Therefore:

$$1 + \frac{n'/64}{63n'/64 - 23n'/32} = 1 + \frac{n'/64}{(126n' - 92n')/128} = 1 + \frac{n'/64}{34n'/128} = 1 + \frac{128}{64 \cdot 34} = 1 + \frac{1}{17} < 2$$

Since the count is an integer, it is $\le 1$. $\blacksquare$

---

## Lemma B (Disjoint Johnson Balls)

**Statement:** Assume $|I_{\rho_0}| = 0$ (equivalently, $C(x) \neq 0$ for all $x \in H^2$). For two distinct hard witnesses with parameters $\lambda_1 \neq \lambda_2$ and associated polynomials $h_1, h_2 \in RS[H^2, k']$, define:

$$A_i = \{x \in H^2 : h_i(x) = o'(x) + \lambda_i C(x)\}$$

Then $A_1 \cap A_2 = \emptyset$.

**Consequence:** The Johnson balls $\mathcal{B}(\lambda) = \{h \in RS[H^2, k'] : |\{x : h(x) = o'(x) + \lambda C(x)\}| > n'/2\}$ are **pairwise disjoint** across distinct $\lambda$'s.

**Proof:**

Suppose $x \in A_1 \cap A_2$. Then:

$$h_1(x) = o'(x) + \lambda_1 C(x) \quad \text{and} \quad h_2(x) = o'(x) + \lambda_2 C(x)$$

Wait — $A_1$ and $A_2$ refer to different polynomials $h_1, h_2$. The statement should be about a SINGLE polynomial being in two balls. Let me restate:

**Corrected Statement:** If a single polynomial $h \in RS[H^2, k']$ satisfies $|\{x : h(x) = o'(x) + \lambda_1 C(x)\}| > n'/2$ and $|\{x : h(x) = o'(x) + \lambda_2 C(x)\}| > n'/2$ simultaneously, then $\lambda_1 = \lambda_2$.

**Proof of corrected statement:**

Let $A_i = \{x : h(x) = o'(x) + \lambda_i C(x)\}$ for $i = 1, 2$. At any $x \in A_1 \cap A_2$:

$$o'(x) + \lambda_1 C(x) = h(x) = o'(x) + \lambda_2 C(x)$$

$$\implies (\lambda_1 - \lambda_2) C(x) = 0$$

Since $|I_{\rho_0}| = 0$ means $C(x) \neq 0$ for all $x$: this forces $\lambda_1 = \lambda_2$, contradicting distinctness. Hence $A_1 \cap A_2 = \emptyset$.

By inclusion: $|A_1| + |A_2| \le n'$. But both are $> n'/2$, giving $|A_1| + |A_2| > n'$, a contradiction.

Therefore no polynomial $h$ can lie in two distinct balls $\mathcal{B}(\lambda_1)$ and $\mathcal{B}(\lambda_2)$. $\blacksquare$

---

## Lemma C (Hard Witness Agreement Exceeds Johnson Radius)

**Statement:** For a hard witness polynomial $h$ with $|R(h)| > 9n'/32$, $|E_h| < n'/2$, and valid parameter $\lambda$ (with $|I_{\rho_0}| = 0$):

$$|\{x : h(x) = o'(x) + \lambda C(x)\}| > \frac{67n'}{128} > \frac{n'}{2} = \sqrt{k' \cdot n'}$$

so $h \in \mathcal{B}(\lambda)$ and the Johnson bound applies.

**Proof:**

From the witness structure: $|J| \ge 63n'/64$ and $J = E_h \sqcup F_h(\lambda)$.

$|F_h(\lambda)| = |J| - |E_h| \ge 63n'/64 - |E_h|$.

From the hard-regime + far condition: $|E_h| + |R(h)| \le |S_0| \le n'$ and $|R(h)| > 9n'/32 = 36n'/128$. Also (from Lemma 3 proof), the far condition gives $|E_h| < n'/2 = 64n'/128$.

But more precisely, in the hard regime when $|I_{\rho_0}| = 0$: $Z_h = \emptyset$, and $|E_h| = |S_0| - |F_h(\lambda)| - |R(h) \cap S_0 \setminus F_h(\lambda)|$...

Actually, let me directly use: $|E_h| \le |S_0| - |R(h)| - |Z_h| \le n' - 9n'/32 - 0 = 23n'/32$.

Wait, I need $|E_h| < 59n'/128$ (tighter). Let me re-derive:

$S_0 \cap J = J$ (since $J \subseteq S_0$). On $J$: $h(x) = o(x)$ on $E_h \cap J$ and $h(x) = o'(x) + \lambda C(x)$ on $F_h(\lambda) \cap J$. Points in $S_0 \setminus J$ have $|S_0 \setminus J| \le n' - 63n'/64 = n'/64$.

$R(h) \cap J$: on $J$, $h(x) \in \{o(x), o'(x) + \lambda C(x)\}$. So $h(x) \notin \{o(x), o'(x)\}$ only when $h(x) = o'(x) + \lambda C(x) \neq o'(x)$ (i.e., $\lambda C(x) \neq 0$, guaranteed since $|I_{\rho_0}| = 0$ and $\lambda \neq 0$) AND $h(x) \neq o(x)$. So $R(h) \cap J \subseteq F_h(\lambda) \cap J \setminus \{x : o'(x) + \lambda C(x) = o(x)\}$.

Actually, every $x \in F_h(\lambda) \cap J$ with $\lambda C(x) \neq 0$ gives $h(x) = o'(x) + \lambda C(x) \neq o'(x)$. And $h(x) = o(x)$ would require $o'(x) + \lambda C(x) = o(x)$, i.e., $D(x) + \lambda C(x) = 0$. The set of such $x$ is bounded.

Let $B_\lambda = \{x : D(x) + \lambda C(x) = 0\}$. Then $R(h) \cap J = (F_h(\lambda) \cap J) \setminus B_\lambda$.

From $|R(h)| \ge |R(h) \cap J| = |F_h(\lambda) \cap J| - |B_\lambda \cap F_h(\lambda)|$ and $|R(h)| > 9n'/32$:

$|F_h(\lambda) \cap J| > 9n'/32 + |B_\lambda \cap F_h(\lambda)| \ge 9n'/32$

More directly: $|F_h(\lambda)| \ge |J| - |E_h| = 63n'/64 - |E_h|$. And $|E_h| < n'/2$ (far condition). So:

$$|F_h(\lambda)| > 63n'/64 - n'/2 = \frac{126n' - 64n'}{128} = \frac{62n'}{128} = \frac{31n'}{64}$$

Actually, let me sharpen using $|R(h)| > 9n'/32$ more directly. We have $R(h) \subseteq S_0 \setminus E_h$ (since $h = o$ on $E_h$ implies $h \in \{o, o'\}$). And similarly $W_h = \{x \in S_0 : h(x) = o'(x)\} \subseteq S_0 \setminus E_h \setminus R(h)$.

$|E_h| + |W_h| + |R(h)| \le |S_0| \le n'$.

$|W_h| = |B_\lambda \cap F_h(\lambda) \cap S_0|$ (points where the opposite-branch evaluation coincidentally equals $o'$; since $|I_{\rho_0}| = 0$, this means $D(x) + \lambda C(x) = 0$).

Now $|E_h| \le n' - |R(h)| - |W_h| \le n' - 9n'/32 - 0 = 23n'/32$.

And $|F_h(\lambda)| = |J| - |E_h \cap J| \ge 63n'/64 - 23n'/32 = (126 - 92)n'/128 = 34n'/128 = 17n'/64$.

But that's just $> 17n'/64$, not $> n'/2$. Hmm, we need a better bound.

Actually: $|F_h(\lambda)| = |J| - |E_h \cap J|$ and $|E_h \cap J| \le |E_h| < n'/2$. So $|F_h(\lambda)| > 63n'/64 - n'/2 = 31n'/64 > n'/4 = k'$.

We need $> n'/2$. Since $31n'/64 < n'/2$, this doesn't hold in general!

Hmm, so the agreement of $h$ with $q_\lambda$ on $F_h(\lambda)$ is only $> 31n'/64 \approx 0.484 n'$, which is BELOW the Johnson radius $n'/2$. This is the known obstruction.

So **Lemma C as stated is FALSE** for the tightest parameters. The agreement $|A| = |F_h(\lambda)| > 31n'/64$ is below $n'/2$.

I apologize for the error. Let me reconsider.

The fiber uniqueness argument requires $|F_h(\lambda)| \ge \tau_h = 63n'/64 - |E_h| - |Z_h|$, which for the hard regime gives $\tau_h > 67n'/128$ (as I computed earlier using $|E_h| + |Z_h| < 23n'/32$). But wait:

$\tau_h = 63n'/64 - |E_h| - |Z_h|$ and $|E_h| + |Z_h| < 23n'/32 = 92n'/128$.

$\tau_h > 63n'/64 - 92n'/128 = 126n'/128 - 92n'/128 = 34n'/128 = 17n'/64$. 

So $\tau_h > 17n'/64$, not $67n'/128$. Let me recheck my earlier computation.

Earlier I wrote: "$|E_h| < 59n'/128$". Let me reverify. 

$W_h = \{x \in S_0 : h(x) = o'(x)\}$: the polynomial $h - o'$ (as a function) vanishes on $W_h$. But $o'$ is NOT a polynomial, so $h(x) = o'(x)$ doesn't mean $h - o'$ is a polynomial with zeros. Still, $|W_h|$ could be up to $k' - 1$ if we use the polynomial $h$ to approximate $o'$.

Wait: $W_h \subseteq \{x : h(x) = o'(x)\}$, and $h$ is a polynomial of degree $< k'$. For ANY function $q$: $|\{x : h(x) = q(x)\}|$ could be anything from 0 to $n'$; there's no upper bound from the polynomial structure alone (because $q$ is not a polynomial).

So $|W_h|$ is unbounded from above by polynomial arguments.

Hmm, I think the issue is that $|W_h|$ could be large. If $h$ agrees with $o'$ on many points: $|W_h|$ is large, $|R(h)|$ is small (since $R(h)$ excludes $W_h$).

For a hard witness: $|R(h)| > 9n'/32$, so $|W_h| \le |S_0| - |E_h| - |R(h)| < n' - |E_h| - 9n'/32$.

$|E_h| + |W_h| < 23n'/32$, so the combined "uninteresting" sets are bounded. The "interesting" fiber $F_h(\lambda) \setminus W_h \supseteq R(h)$ has size $> 9n'/32$.

But $|F_h(\lambda)|$ includes $W_h$ (since $o'(x) + \lambda C(x) = o'(x)$ when $C(x) = 0$; but we assumed $|I_{\rho_0}| = 0$ so $C(x) \neq 0$). Wait: with $|I_{\rho_0}| = 0$, $o'(x) + \lambda C(x) = o'(x)$ iff $\lambda C(x) = 0$ iff $C(x) = 0$ (nope, since $\lambda \neq 0$) iff it's in $I_{\rho_0}$ (empty). So $o'(x) + \lambda C(x) \neq o'(x)$ for all $x$.

Therefore $W_h \cap F_h(\lambda) = \{x : h(x) = o'(x) = o'(x) + \lambda C(x)\} = \emptyset$ (since $\lambda C(x) \neq 0$ everywhere). So $W_h \cap F_h(\lambda) = \emptyset$.

This means: $F_h(\lambda)$ does NOT include $W_h$. The partition of $J$ is: $J = (E_h \cap J) \sqcup (W_h \cap J) \sqcup (R(h) \cap J) \sqcup (\text{rest of } F_h(\lambda) \cap J)$.

Wait, more carefully: on $J$, $h(x) \in \{o(x), o'(x) + \lambda C(x)\}$. If $h(x) = o(x)$: $x \in E_h$. If $h(x) = o'(x) + \lambda C(x) \neq o(x)$ AND $\neq o'(x)$ (since $\lambda C \neq 0$): $x \in R(h) \cap F_h(\lambda)$. If $h(x) = o'(x) + \lambda C(x) = o(x)$: then $x \in B_\lambda$ (where $D(x) + \lambda C(x) = 0$), and $h(x) = o(x)$, so $x \in E_h$? No: $h(x) = o'(x) + \lambda C(x) = o(x)$, meaning the "opposite branch" evaluation happens to equal the "same branch" value. So on the fold, $f_j$ chose the opposite branch but the result equals $o(x)$. Does $x$ count as $E_h$ or $F_h(\lambda)$?

$E_h = \{x : h(x) = o(x)\}$. Since $h(x) = o(x)$ (from above): $x \in E_h$. Also, $h(x) = o'(x) + \lambda C(x)$: $x \in F_h(\lambda)$. So $x \in E_h \cap F_h(\lambda)$.

$E_h \cap F_h(\lambda) = B_\lambda \cap J$.

So on $J$: $J = (E_h \setminus F_h(\lambda)) \sqcup (E_h \cap F_h(\lambda)) \sqcup (F_h(\lambda) \setminus E_h)$.

$(E_h \setminus F_h(\lambda))$: $h = o$, $h \neq o' + \lambda C$. Size: $|E_h| - |B_\lambda|$.
$(E_h \cap F_h(\lambda)) = B_\lambda$: $h = o = o' + \lambda C$. Size: $|B_\lambda|$.
$(F_h(\lambda) \setminus E_h)$: $h = o' + \lambda C$, $h \neq o$. These are the points in $R(h)$ (since $h \neq o$ and $h \neq o'$ as $\lambda C \neq 0$). Size: $|F_h(\lambda)| - |B_\lambda|$.

$|J| = |E_h| + |F_h(\lambda)| - |B_\lambda|$.

$|F_h(\lambda)| = |J| - |E_h| + |B_\lambda| \ge 63n'/64 - n'/2 + |B_\lambda| = 31n'/64 + |B_\lambda|$.

For the fiber counting: $|F_h(\lambda) \setminus E_h| = |F_h(\lambda)| - |B_\lambda| = 31n'/64 + |B_\lambda| - |B_\lambda| = 31n'/64$.

These are the "genuine" opposite-branch points. On these: $\Lambda_h(x) = \lambda$ (uniquely determined since $C(x) \neq 0$ and $h(x) \neq o(x)$).

On $B_\lambda$: $h(x) = o(x) = o'(x) + \lambda C(x)$. Both branches give $o(x)$. $\Lambda_h(x)$ is not defined (since $h(x) = o(x)$, so $x \in E_h$, and the fiber function is only defined on $V_h = \{h \neq o, C \neq 0\}$).

So the "genuine fiber" of $\Lambda_h$ at $\lambda$ has size exactly $31n'/64$.

The total domain of $\Lambda_h$ is $V_h = \{x : C(x) \neq 0, h(x) \neq o(x)\} = \{x \in H^2 : h(x) \neq o(x)\}$ (since $C \neq 0$ everywhere). Size: $n' - |E_h|$.

The fibers sum: $\sum_{\mu} |\Lambda_h^{-1}(\mu)| = |V_h| = n' - |E_h| < n' - 0 = n'$.

Number of $\lambda$'s with fiber $\ge 31n'/64$: at most $\frac{n' - |E_h|}{31n'/64} \le \frac{n'}{31n'/64} = 64/31 \approx 2.06$, so $\le 2$.

Hmm, so the fiber counting gives at most 2, not 1. Let me sharpen.

For the HARD regime: $|R(h)| > 9n'/32$ and $R(h) = F_h(\lambda) \setminus E_h$ (in the case $W_h = \emptyset$, which holds when $|I_{\rho_0}| = 0$ since $o' + \lambda C \neq o'$). Wait, $R(h) = \{x \in S_0 : h(x) \notin \{o(x), o'(x)\}\}$. On $F_h(\lambda) \setminus E_h$: $h(x) = o'(x) + \lambda C(x) \neq o(x)$ and $\neq o'(x)$. So YES, $R(h) \supseteq F_h(\lambda) \setminus E_h \cap S_0 \supseteq F_h(\lambda) \setminus (E_h \cup (H^2 \setminus S_0))$.

$|R(h)| \ge |F_h(\lambda) \setminus E_h| - |H^2 \setminus S_0| \ge 31n'/64 - n'/128 = (62-1)n'/128 = 61n'/128 > 9n'/32 = 36n'/128$. ✓

So the fiber at $\lambda$ has size exactly $31n'/64$ (the "genuine opposite" set). 

And the number of $\lambda$'s with fiber $\ge 31n'/64$: $\le (n' - |E_h|) / (31n'/64)$.

For $|E_h| > n'/64$: $\le (n' - n'/64)/(31n'/64) = (63/64)/(31/64) = 63/31 \approx 2.03$, so $\le 2$.

For $|E_h| = 0$: $\le n'/(31n'/64) = 64/31 \approx 2.06$, so $\le 2$.

So each hard $h$ admits at most 2 valid $\lambda$'s. But I was