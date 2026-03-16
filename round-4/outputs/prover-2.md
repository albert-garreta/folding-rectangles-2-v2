# Analysis of Hard-Regime Witnesses: New Structural Lemmas

## Preamble

I have carefully reviewed the existing notes, proofs, and output. The moderate regime is handled (Lemma 4/12 in proofs.md). The hard regime—witnesses with $|R(h)| > 9n'/32$—remains open. The second-moment obstruction (Lemma 15) shows generic packing arguments fail. I will now exploit the **polynomial structure** of the witness slopes to establish new, concrete constraints.

---

## Setup Recap

Fix a reference witness $(f_0, \rho_0, g_0)$ with agreement set $S_0$, $|S_0| \geq T = 127n'/128$. For each hard witness $(f_j, \rho_j, g_j)$ with $\rho_j \neq \rho_0$, define:
- $\lambda_j = 1/(\rho_j - \rho_0)$
- $h_j = (g_j - g_0)/(\rho_j - \rho_0) \in RS[H^2, k']$
- $J_j = S_0 \cap S_j$ (joint agreement set), $|J_j| \geq 63n'/64$
- $E_j = \{x \in J_j : f_j \text{ chose same branch as } f_0\}$ (same-branch set)
- $F_j = \{x \in J_j : f_j \text{ chose opposite branch to } f_0\}$ (opposite-branch set)

Established in Lemma 4: $h_j(x) = o(x)$ on $E_j$ and $h_j(x) = o'(x) + \lambda_j C(x)$ on $F_j$, where $o, o'$ are the odd parts of the reference and opposite branches, and $C(x) = e'(x) - e(x) + \rho_0(o'(x) - o(x))$. Also $|E_j| < n'/2$ and $|F_j| > 31n'/64$.

---

## Lemma A (Same-Branch Overlap Bound)

**Claim.** For any two distinct hard witnesses $i \neq j$ (with $h_i \neq h_j$), $|E_i \cap E_j| \leq k' - 1 < k' = n'/4$.

**Proof.** On $E_i \cap E_j$, both $h_i(x) = o(x)$ and $h_j(x) = o(x)$, so $(h_i - h_j)(x) = 0$.

The polynomial $h_i - h_j$ is a nonzero element of $RS[H^2, k']$ (nonzero because $h_i \neq h_j$ as codewords). A nonzero polynomial of degree $< k'$ has at most $k' - 1$ zeros among the $n' = |H^2|$ evaluation points.

Therefore $|E_i \cap E_j| \leq k' - 1$. $\blacksquare$

**Remark.** Hard witnesses have distinct slopes: if $h_i = h_j$ then $g_j - g_0 = (\rho_j - \rho_0)h_j = (\rho_j - \rho_0)h_i$, meaning $g_j = g_0 + (\rho_j - \rho_0)h_i$ lies on the affine line through $g_i$ with slope $h_i$. In the hard regime ($|R(h_i)| > 9n'/32$), Lemma 4 claim 3 associates at most one $\rho$ per slope, so $h_i = h_j$ would force $\rho_i = \rho_j$, contradicting distinctness. Hence $h_i \neq h_j$.

---

## Lemma B (Slope-Polynomial Agreement with $C$)

**Claim.** For distinct hard witnesses $i, j$, define $C_{ij} = (h_i - h_j)/(\lambda_i - \lambda_j) \in RS[H^2, k']$. Then:

(i) $C_{ij}$ is a **nonzero** polynomial of degree $< k'$.

(ii) $C_{ij}(x) = 0$ for all $x \in E_i \cap E_j$.

(iii) $C_{ij}(x) = C(x)$ for all $x \in F_i \cap F_j$.

**Proof.**

(i) $C_{ij} = (h_i - h_j)/(\lambda_i - \lambda_j)$. Since $h_i \neq h_j$ (by the remark above) and $\lambda_i \neq \lambda_j$ (since $\rho_i \neq \rho_j$), $C_{ij}$ is a nonzero scalar multiple of $h_i - h_j$, hence nonzero.

(ii) On $E_i \cap E_j$: $h_i(x) = h_j(x) = o(x)$, so $C_{ij}(x) = 0$.

(iii) On $F_i \cap F_j$: $h_i(x) = o'(x) + \lambda_i C(x)$ and $h_j(x) = o'(x) + \lambda_j C(x)$. Thus:
$$C_{ij}(x) = \frac{(o'(x) + \lambda_i C(x)) - (o'(x) + \lambda_j C(x))}{\lambda_i - \lambda_j} = C(x). \quad \blacksquare$$

---

## Lemma C (Group Structure and Affine-Line Reduction)

**Claim.** Fix a reference hard witness $i$. Group the remaining hard witnesses by their slope polynomial: $j \sim j'$ iff $C_{ij} = C_{ij'}$. Let the groups be $\Gamma_1, \ldots, \Gamma_L$ with common slope polynomials $\mathcal{C}_1, \ldots, \mathcal{C}_L$. Then:

(a) For each group $\Gamma_\ell$, the set $\{h_j : j \in \Gamma_\ell\} \cup \{h_i\}$ lies on a single affine line $h_i + t \cdot \mathcal{C}_\ell$ in $RS[H^2, k']$.

(b) $|\Gamma_\ell| \leq 3$ for each $\ell$.

(c) The total number of hard witnesses satisfies $m \leq 3L + 1$.

**Proof.**

**(a)** For $j \in \Gamma_\ell$: $h_j = h_i + (\lambda_j - \lambda_i) \mathcal{C}_\ell$, which is a point on the affine line $\{h_i + t \cdot \mathcal{C}_\ell : t \in \mathbb{F}\}$.

**(b)** We show all witnesses in $\Gamma_\ell \cup \{i\}$ lie on a common affine line in the $(g, \rho)$-parameterization of Lemma 3.

For $j \in \Gamma_\ell$, we have $h_j = h_i + (\lambda_j - \lambda_i)\mathcal{C}_\ell$. Define $\phi = h_i - \lambda_i \mathcal{C}_\ell \in RS[H^2, k']$. Then $h_j = \phi + \lambda_j \mathcal{C}_\ell$, giving:

$$g_j = g_0 + (\rho_j - \rho_0)h_j = g_0 + (\rho_j - \rho_0)(\phi + \lambda_j \mathcal{C}_\ell)$$
$$= g_0 + (\rho_j - \rho_0)\phi + \mathcal{C}_\ell \quad (\text{since } (\rho_j - \rho_0)\lambda_j = 1)$$
$$= (g_0 + \mathcal{C}_\ell - \rho_0 \phi) + \rho_j \phi$$

Setting $u^* = g_0 + \mathcal{C}_\ell - \rho_0 \phi$, we get $g_j = u^* + \rho_j \phi$ for all $j \in \Gamma_\ell \cup \{i\}$.

By Lemma 3 (affine-line parameter multiplicity), at most $4$ values of $\rho$ on the line $g = u^* + \rho \phi$ admit far witnesses. Since witness $i$ is one of them, $|\Gamma_\ell| + 1 \leq 4$, so $|\Gamma_\ell| \leq 3$.

**(c)** The total number of witnesses other than $i$ is $\sum_\ell |\Gamma_\ell| \leq 3L$, giving $m \leq 3L + 1$. $\blacksquare$

---

## Lemma D (Cross-Group Disjointness)

**Claim.** For two distinct groups $\ell \neq \ell'$ (with representatives $j \in \Gamma_\ell, j' \in \Gamma_{\ell'}$), define the polynomial $P^{(\ell)} = h_i - \lambda_i \mathcal{C}_\ell$. Then:

(i) $P^{(\ell)}(x) = o'(x)$ on $F_i \cap (\bigcup_{j \in \Gamma_\ell} F_j)$.

(ii) $P^{(\ell)} - P^{(\ell')} = \lambda_i(\mathcal{C}_{\ell'} - \mathcal{C}_\ell)$ is a nonzero polynomial of degree $< k'$.

(iii) $\big|(\text{agreement of } P^{(\ell)} \text{ with } o') \cap (\text{agreement of } P^{(\ell')} \text{ with } o')\big| < k'$.

In particular, the agreement sets $G_\ell = \{x \in H^2 : P^{(\ell)}(x) = o'(x)\} \supseteq F_i \cap (\bigcup_{\Gamma_\ell} F_j)$ satisfy $|G_\ell \cap G_{\ell'}| < k'$ for $\ell \neq \ell'$.

**Proof.**

**(i)** On $F_i$, $h_i(x) = o'(x) + \lambda_i C(x)$. So $P^{(\ell)}(x) = o'(x) + \lambda_i C(x) - \lambda_i \mathcal{C}_\ell(x)$. For $j \in \Gamma_\ell$ and $x \in F_i \cap F_j$: $\mathcal{C}_\ell(x) = C_{ij}(x) = C(x)$ by Lemma B(iii). Hence $P^{(\ell)}(x) = o'(x)$.

**(ii)** $P^{(\ell)} - P^{(\ell')} = \lambda_i(\mathcal{C}_{\ell'} - \mathcal{C}_\ell)$, which is nonzero since $\mathcal{C}_\ell \neq \mathcal{C}_{\ell'}$ and $\lambda_i \neq 0$.

**(iii)** On $G_\ell \cap G_{\ell'}$: $P^{(\ell)}(x) = P^{(\ell')}(x) = o'(x)$, so $(P^{(\ell)} - P^{(\ell')})(x) = 0$. By (ii), this polynomial has $< k'$ zeros, giving $|G_\ell \cap G_{\ell'}| < k'$. $\blacksquare$

---

## Reduction: Bounding $m$ via Bounding $L$

By Lemma C, $m \leq 3L + 1$. By Lemma D, the question reduces to:

> **How many distinct polynomials $P^{(\ell)} \in RS[H^2, k']$ can agree with the function $o' : H^2 \to \mathbb{F}$ on pairwise-disjoint (up to $k'$) subsets?**

This is essentially a **list-decoding question** for the function $o'$. By the Guruswami–Sudan list-decoding bound:

- If each $|G_\ell| > \sqrt{k' \cdot n'} = n'/2$, then $L \leq O(n'/k') = O(4)$, giving $m \leq 13$.

**Current gap:** We cannot guarantee $|G_\ell| > n'/2$ for every group, because $|F_i \cap F_j|$ can be as small as $O(1)$ when $|E_i|, |E_j|$ are close to their maximum $n'/2$.

---

## Identified Obstruction and Proposed Path Forward

The numerical obstruction is sharp: each $|F_i| > 31n'/64 \approx 0.484n'$, and the Johnson threshold is $n'/2 = 0.5n'$. The gap $0.484 < 0.5$ prevents direct application of list-decoding to each group's agreement set.

**To close this gap, one needs to exploit:**

1. **The cocycle identity:** For any triple $(i, j, k)$, the polynomial
$$Q_k = h_k - \frac{\lambda_k - \lambda_2}{\lambda_1 - \lambda_2} h_1 - \frac{\lambda_1 - \lambda_k}{\lambda_1 - \lambda_2} h_2$$
vanishes on $(E_1 \cap E_2 \cap E_k) \cup (F_1 \cap F_2 \cap F_k)$. If this set has size $\geq k'$, then $Q_k \equiv 0$ and $h_k$ is collinear with $h_1, h_2$, forcing $L = 1$ and $m \leq 4$.

2. **Global list-recovery with shared structure:** All $P^{(\ell)}$ approximate the *same* function $o'$, with pairwise overlap $< k'$. Their *total* coverage of $F_i$ is substantial ($\sum_\ell |G_\ell \cap F_i| \approx |F_i|$). An interleaved or multiplicity list-decoding argument exploiting this collective coverage should bound $L$.

3. **The tensor/column constraint:** The $m \times n'$ matrix of evaluations has columns lying (approximately) in the 2D affine subspace $\{a \cdot \mathbf{1} + b \cdot \boldsymbol{\lambda}\}$. Rows are RS codewords. This interleaved structure should force low rank, hence $L = O(1)$.

---

## Flaw Check on Existing Documents

- **notes.md**: The discussion of "0.234N vs 0.25N" obstruction is correct in spirit but the notation is inconsistent (uses $N$ in some places and $n'$ in others). The phrasing "structurally," "identically," "natively" is redundant and obscures the logic.

- **proofs.md, Lemma 14**: The statement about $|E_i \cap E_j| \leq K$ (claim 3) is correct but was not fully proven in the document. My Lemma A above provides the complete proof.

- **proofs.md, Lemma 15**: The claim $\Gamma(C) \geq k'$ lacks a rigorous proof. It relies on the assertion that for any function on $\geq 127n'/128$ points, some RS codeword agrees on $\geq k'$ points. This follows from the Singleton bound: a polynomial of degree $< k'$ can be interpolated through $k'$ points, so by choosing the "best-fitting" polynomial to $C$, one gets agreement $\geq k'$. This should be made explicit.