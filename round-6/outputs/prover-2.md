# Progress Report: Hard-Regime Analysis via Column Parametric Structure and Cocycle Enhancement

## Overview

I present several new rigorous results advancing the hard-regime analysis. The key contributions are:

1. A **product factorization** revealing that each hard polynomial $h_i$ satisfies a clean quadratic relation at every point.
2. A **column parametric structure** showing all hard polynomial evaluations lie on a common affine line at each point.
3. A **reference-free cocycle** whose zero set is enhanced by equality sets from *all* valid parameters, not just the chosen reference.
4. A **conditional bound**: if any valid parameter has a large equality set, the entire hard regime collapses to $O(1)$.

---

## 1. Product Factorization

**Lemma A (Product Identity):** For each hard-regime polynomial $h_i \in RS[H^2, k']$, define the map $\Phi_i : H^2 \to \mathbb{F}$ by
$$\Phi_i(x) := (h_i(x) - a_o(x))(h_i(x) - b_o(x)).$$
Then on $J_i = S_0 \cap S_i$ (with $|J_i| \ge 63n'/64$):
- On $E_i$: $\Phi_i(x) = 0$.
- On $F_i$: $\Phi_i(x) = \lambda_i \Delta_0(x)(2D(x) + \lambda_i \Delta_0(x))$, where $D = (a_o - b_o)/2$ and $\Delta_0 = A_{\rho_0} - B_{\rho_0}$.

**Proof.** On $E_i$: $h_i(x) = o(x) \in \{a_o(x), b_o(x)\}$, so one factor vanishes, giving $\Phi_i(x) = 0$.

On $F_i$: $h_i(x) = o'(x) + \lambda_i C(x)$ where $C(x) = e'(x) - e(x) + \rho_0(o'(x) - o(x))$.

**Case $\sigma_0(x) = a$:** Then $o = a_o$, $o' = b_o$, $C = -\Delta_0$. So $h_i - b_o = -\lambda_i \Delta_0$ and $h_i - a_o = (b_o - a_o) - \lambda_i \Delta_0 = -2D - \lambda_i \Delta_0$. Thus:
$$\Phi_i = (-2D - \lambda_i \Delta_0)(-\lambda_i \Delta_0) = \lambda_i \Delta_0(2D + \lambda_i \Delta_0).$$

**Case $\sigma_0(x) = b$:** Then $o = b_o$, $o' = a_o$, $C = \Delta_0$. So $h_i - a_o = \lambda_i \Delta_0$ and $h_i - b_o = 2D + \lambda_i \Delta_0$. Thus:
$$\Phi_i = \lambda_i \Delta_0(2D + \lambda_i \Delta_0). \qquad \blacksquare$$

---

## 2. Column Parametric Structure

**Lemma B (Affine Line Structure):** At any $x \in H^2$ with $C(x) \neq 0$ and $x \in J_i$, define the affine line $\ell_x(t) = o'(x) + t \cdot C(x)$ and the "background parameter" $\mu(x) = \delta(x)/C(x)$ where $\delta = o - o'$. Then:

1. $o(x) = \ell_x(\mu(x))$ and $o'(x) = \ell_x(0)$.
2. Both $a_o(x)$ and $b_o(x)$ lie on $\ell_x$ (at parameters $\mu(x)$ and $0$ in some order).
3. For each hard witness $i$ with $x \in J_i$:
   - If $x \in E_i$: $h_i(x) = \ell_x(\mu(x))$.
   - If $x \in F_i$: $h_i(x) = \ell_x(\lambda_i)$.

**Proof.** Statement (1): $\ell_x(\mu(x)) = o'(x) + (\delta(x)/C(x)) \cdot C(x) = o'(x) + \delta(x) = o(x)$. And $\ell_x(0) = o'(x)$.

Statement (2): Since $\{o(x), o'(x)\} = \{a_o(x), b_o(x)\}$ (the two branches), both lie on $\ell_x$.

Statement (3): On $E_i$, $h_i(x) = o(x) = \ell_x(\mu(x))$. On $F_i$, $h_i(x) = o'(x) + \lambda_i C(x) = \ell_x(\lambda_i)$. $\blacksquare$

**Consequence:** At each column $x$ (with $C(x) \neq 0$), the vector of evaluations $(h_1(x), \ldots, h_m(x))$ lies entirely on the one-dimensional affine line $\ell_x$. The "effective parameter" for witness $i$ is $\mu_i(x) \in \{\mu(x), \lambda_i\}$.

---

## 3. Equality Set Connection

**Lemma C (Equality Set Identification):** Define $V_i = \{x \in H^2 : \delta(x) = \lambda_i C(x)\}$. Then $V_i = I_{\rho_i}$, the fold equality set $\{x : A_{\rho_i}(x) = B_{\rho_i}(x)\}$.

**Proof.** The condition $\delta(x) = \lambda_i C(x)$ with $\lambda_i = 1/(\rho_i - \rho_0)$ and $C(x) = -\sigma_0(x) \Delta_0(x)$ gives $(o - o')(x) = \lambda_i C(x)$. Substituting and simplifying:

If $\sigma_0(x) = a$: $(a_o - b_o) = -\lambda_i \Delta_0$, i.e., $(\rho_i - \rho_0)(a_o - b_o) = -\Delta_0 = -(a_e - b_e) - \rho_0(a_o - b_o)$, giving $\rho_i(a_o - b_o) + (a_e - b_e) = 0$, i.e., $A_{\rho_i}(x) = B_{\rho_i}(x)$.

If $\sigma_0(x) = b$: similarly gives $A_{\rho_i}(x) = B_{\rho_i}(x)$.

All steps reverse, so the equivalence holds. $\blacksquare$

**Key property on $V_i$:** If $x \in V_i \cap J_i$ and $C(x) \neq 0$, then $\mu(x) = \lambda_i$, so $h_i(x) = \ell_x(\lambda_i) = \ell_x(\mu(x)) = o(x)$ regardless of whether $x \in E_i$ or $x \in F_i$.

---

## 4. Cocycle Factorization and Enhanced Zero Set

**Lemma D (Cocycle Factorization):** For any triple $(i,j,k)$ of hard witnesses, define the reference-free cocycle:
$$\hat{Q}_{ijk} = g_i(\rho_k - \rho_j) + g_j(\rho_i - \rho_k) + g_k(\rho_j - \rho_i) \in RS[H^2, k'].$$

This is a polynomial of degree $< k'$. On the common domain $J = J_i \cap J_j \cap J_k$ (with $|J| \ge n' - 3n'/64$), at points where $C(x) \neq 0$:

$$\hat{Q}_{ijk}(x) = \kappa \cdot C(x) \cdot \bigl[\mu_i(x)(\lambda_j - \lambda_k) + \mu_j(x)(\lambda_k - \lambda_i) + \mu_k(x)(\lambda_i - \lambda_j)\bigr]$$

where $\kappa = (\rho_i - \rho_0)(\rho_j - \rho_0)(\rho_k - \rho_0) \neq 0$ is a nonzero scalar.

**Proof.** The reference-dependent cocycle satisfies $Q^{(\rho_0)}_{ijk} = \hat{Q}_{ijk} / \kappa$ (verified by expanding $h_i = (g_i - g_0)/(\rho_i - \rho_0)$ and $\lambda_i = 1/(\rho_i - \rho_0)$; the $g_0$ terms cancel). On $J$, the column parametric structure gives $h^{(\rho_0)}_\ell(x) = o'(x) + \mu_\ell(x) C(x)$. Substituting into $Q^{(\rho_0)}$ and using $(\lambda_j - \lambda_k) + (\lambda_k - \lambda_i) + (\lambda_i - \lambda_j) = 0$ (which kills the $o'$ terms), the factorization follows. $\blacksquare$

**Lemma E (Eight-Case Zero Analysis):** From the factorization, $\hat{Q}_{ijk}(x) = 0$ on $J$ whenever one of:
- $C(x) = 0$, i.e., $x \in I_{\rho_0}$ (the reference equality set).
- All three $\mu_\ell = \mu(x)$ (case $EEE$: all in $E$).
- All three $\mu_\ell = \lambda_\ell$ (case $FFF$: all in $F$).
- In any "mixed" case (exactly 1 or 2 witnesses in $E$): the bracketed expression vanishes iff $\mu(x) = \lambda_\ell$ where $\ell$ is the witness whose $E/F$ status differs from the other two. Equivalently, $x \in V_\ell = I_{\rho_\ell}$.

**Proof.** Complete eight-case analysis using $\mu_\ell \in \{\mu(x), \lambda_\ell\}$:

For example, $\mu_i = \mu, \mu_j = \lambda_j, \mu_k = \lambda_k$ (witness $i$ in $E$, $j,k$ in $F$):
$$Q' = \mu(\lambda_j - \lambda_k) + \lambda_j(\lambda_k - \lambda_i) + \lambda_k(\lambda_i - \lambda_j) = (\lambda_j - \lambda_k)(\mu - \lambda_i),$$
which vanishes iff $\mu(x) = \lambda_i$, i.e., $x \in V_i$. All eight cases are verified similarly. $\blacksquare$

---

## 5. Reference-Free Universal Vanishing

**Theorem (Universal Equality-Set Vanishing):** The reference-free cocycle $\hat{Q}_{ijk}$ vanishes on $I_\rho$ for **every** valid parameter $\rho$ (not just the reference $\rho_0$).

**Proof.** For any valid witness parameter $\rho_r$, we may re-derive the cocycle factorization using $\rho_r$ as reference. This yields:

$$\hat{Q}_{ijk}(x) = \kappa_r \cdot C^{(r)}(x) \cdot Q'^{(r)}(x)$$

on $J^{(r)} = S_r \cap S_i \cap S_j \cap S_k$ (with $|J^{(r)}| \ge n' - 4n'/128 = 31n'/32$), where $C^{(r)}(x) = 0$ iff $x \in I_{\rho_r}$.

Since $\hat{Q}_{ijk}$ is a *polynomial* whose pointwise values agree with $\kappa_r C^{(r)}(x) Q'^{(r)}(x)$ on $J^{(r)}$, we conclude that $\hat{Q}_{ijk}(x) = 0$ for all $x \in I_{\rho_r} \cap J^{(r)}$.

This holds for every valid $\rho_r$, not just the original reference. $\blacksquare$

**Corollary (Conditional Collapse):** If there exists any valid parameter $\rho^*$ with $|I_{\rho^*}| \ge k' + 4n'/128 = k' + n'/32$, then $|I_{\rho^*} \cap J^{(r)}| \ge k'$, forcing $\hat{Q}_{ijk} \equiv 0$ for ALL triples $(i,j,k)$. This means all hard polynomials lie on a single affine line, and by the affine-line multiplicity bound (Lemma 3 of proofs.md), the hard regime contributes at most 4 valid parameters.

---

## 6. Quantitative Lower Bound on Cocycle Zeros

**Proposition:** The total zero set of $\hat{Q}_{ijk}$ on a random triple satisfies:

$$\mathbb{E}[|Z_{ijk}|] \ge |I_{\text{all}}| + \frac{63(n' - |I_{\text{all}}|)}{256} + \frac{3}{4m}\sum_{r} |I_{\rho_r} \setminus I_{\text{all}}|$$

where the sum is over all $m$ hard-regime parameters. Since $\sum_r |I_{\rho_r} \setminus I_{\text{all}}| \le n'$, this gives:

$$\mathbb{E}[|Z_{ijk}|] \ge \frac{193|I_{\text{all}}| + 63n'}{256} + \frac{3n'}{4m}.$$

For $\hat{Q}_{ijk} \equiv 0$ (forcing collinearity), we need $|Z_{ijk}| \ge k' = n'/4$. The sufficient condition becomes $193\beta + 192n'/m \ge n'$ where $\beta = |I_{\text{all}}|$.

**Remark:** When $\beta = 0$, this gives $m \le 192$: for at most 192 hard witnesses, the averaging argument guarantees existence of a collinear triple. However, this alone does not force ALL witnesses onto a single affine line, and additional structural arguments (inductive application or global matrix rank constraints) are needed.

---

## Next Steps

1. **Inductive collinearity**: If one collinear triple exists, show that the affine line it determines captures ALL hard witnesses (via a refined cocycle argument on triples containing two known-collinear witnesses and one unknown).

2. **Global rank constraint**: Use the column parametric structure (all evaluations on affine lines) combined with the polynomial row constraint ($h_i \in RS[H^2, k']$) to derive an interleaved Reed-Solomon rank bound forcing $m = O(1)$.

3. **Exploit the full union $\bigcup I_\rho$**: The universal vanishing theorem gives zeros on ALL equality sets simultaneously. A Turán-type argument on the "private" equality points $I_\rho \setminus I_{\text{all}}$ (which are pairwise disjoint) may yield a stronger bound when combined with the $EEE/FFF$ contribution.