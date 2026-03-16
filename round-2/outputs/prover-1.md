I see two clean, auditable moves that directly answer the verifier’s prompt.

- First, the equality sets really do force $|R(\phi_i)|$ upward unless witness $i$ consumes a disjoint chunk of equality mass.
- Second, there are explicit pairwise interpolation polynomials on $D_i \cap D_j$ and on the harder core $F_i \cap F_j$, and any large common intersection immediately collapses the whole cluster onto one affine line, after which Lemma 3 gives the desired constant bound.

I will use the notation already established in `proofs.md`:

- $n' = |H^2|$ and $k' = n'/4$.
- Fix a reference witness $(f_0,\rho_0,g_0)$ with agreement set $S_0$.
- For another valid witness $(f_i,\rho_i,g_i)$ with $\rho_i \neq \rho_0$, write
  $J_i = S_0 \cap S_i$,
  $\phi_i = (g_i-g_0)/(\rho_i-\rho_0)$,
  $R_i = R(\phi_i)$,
  and let $D_i \subseteq J_i$ be the set where $f_i$ chooses the opposite branch relative to $f_0$.
- From the current proof state we may use:
  1. $|D_i| > 31n'/64$.
  2. $D_i \subseteq R_i \cup I_{\rho_0} \cup I_{\rho_i}$.
  3. The sets $I_\rho \setminus I_{\mathrm{all}}$ are pairwise disjoint.

I will also write $e,o$ for the branch chosen by $f_0$ on $S_0$, and $e',o'$ for the opposite branch, as in `proofs.md`.

---

## 1. Equality sets force $|R_i|$ upward

This is the cleanest rigorous way I found to use the equality sets.

### Lemma A: equality-budget lower bound

For every valid non-reference witness $i$,
$|I_{\rho_i} \setminus I_{\rho_0}| > \frac{31}{64}n' - |R_i| - |I_{\rho_0}|$.

In particular, for any subfamily $T$ of such witnesses satisfying $|R_i| \le \tau$ for all $i \in T$, we have
$|T| < \frac{n'}{\frac{31}{64}n' - \tau - |I_{\rho_0}|}$,
whenever the denominator is positive.

### Proof

Fix $i$.

By the already-proved trichotomy on $D_i$, every $x \in D_i$ lies in at least one of the sets $R_i$, $I_{\rho_0}$, $I_{\rho_i}$. Therefore
$D_i \subseteq R_i \cup I_{\rho_0} \cup I_{\rho_i}$.

Since $I_{\rho_i} = (I_{\rho_i}\setminus I_{\rho_0}) \cup (I_{\rho_i}\cap I_{\rho_0})$ and $I_{\rho_i}\cap I_{\rho_0} \subseteq I_{\rho_0}$, we get
$D_i \subseteq R_i \cup I_{\rho_0} \cup (I_{\rho_i}\setminus I_{\rho_0})$.

Taking cardinalities,
$|D_i| \le |R_i| + |I_{\rho_0}| + |I_{\rho_i}\setminus I_{\rho_0}|$.

Rearranging and using $|D_i| > 31n'/64$,
$|I_{\rho_i}\setminus I_{\rho_0}| \ge |D_i| - |R_i| - |I_{\rho_0}| > \frac{31}{64}n' - |R_i| - |I_{\rho_0}|$.

This proves the first statement.

Now let $T$ be a family with $|R_i|\le \tau$ for all $i\in T$. Then for each $i\in T$,
$|I_{\rho_i}\setminus I_{\rho_0}| > \frac{31}{64}n' - \tau - |I_{\rho_0}|$.

I claim the sets $I_{\rho_i}\setminus I_{\rho_0}$, for $i\in T$, are pairwise disjoint.

Indeed, suppose $x$ belonged to both $I_{\rho_i}\setminus I_{\rho_0}$ and $I_{\rho_j}\setminus I_{\rho_0}$ with $i\neq j$. Then $x\in I_{\rho_i}\cap I_{\rho_j}$ and $x\notin I_{\rho_0}$. By the already-proved equality-set lemma, the sets $I_\rho\setminus I_{\mathrm{all}}$ are pairwise disjoint; hence any point lying in both $I_{\rho_i}$ and $I_{\rho_j}$ must lie in $I_{\mathrm{all}}$. But $I_{\mathrm{all}} \subseteq I_{\rho_0}$, contradiction.

Therefore
$\sum_{i\in T} |I_{\rho_i}\setminus I_{\rho_0}| \le n'$.

Combining this with the lower bound for each $i$ gives
$|T|\left(\frac{31}{64}n' - \tau - |I_{\rho_0}|\right) < n'$.

This is the claimed bound on $|T|$. ∎

---

### Immediate consequence

This already gives a useful refinement of the moderate regime.

- Previously, all witnesses with $|R_i|\le 9n'/32$ were bounded by Guruswami–Sudan.
- Now, for a fixed reference $\rho_0$, all witnesses with
  $|R_i| \le \frac{31}{64}n' - |I_{\rho_0}| - \eta n'$
  are at most $1/\eta$ up to constants.

So if one can choose a reference witness with small $|I_{\rho_0}|$, then the “moderate” window extends much farther upward, potentially all the way close to $31n'/64$.

This is exactly the kind of forcing effect the verifier suggested.

---

## 2. Pairwise interpolation on $D_i \cap D_j$

This is the clean “pairwise intersection polynomial” on the opposite-branch sets.

### Lemma B: reconstructing the opposite branch from two witnesses

Let $i\neq j$ be two valid non-reference witnesses. Define
$v_{ij} = \frac{g_i-g_j}{\rho_i-\rho_j} \in \mathrm{RS}[H^2,k']$
and
$u_{ij} = \frac{\rho_i g_j-\rho_j g_i}{\rho_i-\rho_j} \in \mathrm{RS}[H^2,k']$.

Then for every $x \in D_i \cap D_j$,
$v_{ij}(x) = o'(x)$
and
$u_{ij}(x) = e'(x)$.

Equivalently, on $D_i \cap D_j$ we have
$g_t(x) = u_{ij}(x) + \rho_t v_{ij}(x)$
for every witness $t$ such that $x\in D_t$.

### Proof

Fix $x\in D_i\cap D_j$.

By definition of $D_i$ and $D_j$, both witnesses $i$ and $j$ choose the opposite branch relative to the reference witness at $x$, and both agree with their target codewords there. Therefore
$g_i(x) = e'(x) + \rho_i o'(x)$
and
$g_j(x) = e'(x) + \rho_j o'(x)$.

Subtracting the two equalities and dividing by $\rho_i-\rho_j \neq 0$ gives
$o'(x) = \frac{g_i(x)-g_j(x)}{\rho_i-\rho_j} = v_{ij}(x)$.

Next,
$\rho_i g_j(x) - \rho_j g_i(x)
= \rho_i(e'(x)+\rho_j o'(x)) - \rho_j(e'(x)+\rho_i o'(x))
= (\rho_i-\rho_j)e'(x)$.

Dividing by $\rho_i-\rho_j$ gives
$e'(x) = \frac{\rho_i g_j(x)-\rho_j g_i(x)}{\rho_i-\rho_j} = u_{ij}(x)$.

Since $g_i,g_j \in \mathrm{RS}[H^2,k']$, both $u_{ij}$ and $v_{ij}$ are also in $\mathrm{RS}[H^2,k']$.

Finally, if $x \in D_t$ as well, then by the same “opposite branch” description,
$g_t(x) = e'(x)+\rho_t o'(x) = u_{ij}(x)+\rho_t v_{ij}(x)$.

This proves the lemma. ∎

---

### Corollary C: a large common $D$-intersection collapses to one affine line

Let $T$ be a set of valid non-reference witnesses. Suppose there exists a set
$U \subseteq \bigcap_{i\in T} D_i$
with $|U| > k'$.

Then there exist codewords $u,v \in \mathrm{RS}[H^2,k']$ such that
$g_i = u + \rho_i v$
for every $i\in T$.

Consequently, by the affine-line multiplicity lemma already in `proofs.md`, we have
$|T| \le 4$.

### Proof

If $|T|\le 1$, there is nothing to prove, so assume $|T|\ge 2$ and pick distinct $i,j\in T$.

Set
$u = u_{ij}$ and $v = v_{ij}$,
as in Lemma B.

Fix any $t\in T$. For every $x\in U$, since $U\subseteq D_i\cap D_j\cap D_t$, Lemma B gives
$g_t(x) = u(x) + \rho_t v(x)$.

Now both $g_t$ and $u+\rho_t v$ belong to $\mathrm{RS}[H^2,k']$. They agree on the set $U$, whose size is greater than $k'$. Two distinct Reed–Solomon codewords of degree $<k'$ can agree on at most $k'-1$ evaluation points, so they must be identical:
$g_t = u + \rho_t v$.

This holds for every $t\in T$.

Therefore all witnesses in $T$ lie on one common affine line $u+\rho v$ in codeword space. The affine-line multiplicity lemma from `proofs.md` says that at most $4$ parameters $\rho$ can occur on such a line while still admitting valid far witnesses. Hence $|T|\le 4$. ∎

---

## 3. Pairwise interpolation on the truly hard core $F_i \cap F_j$

This is the version that isolates the $\phi_i = o' + \alpha_i C$ structure.

Define
$F_i = D_i \setminus (I_{\rho_0}\cup I_{\rho_i})$.

Then by the already-proved hard-regime geometry, for every $x\in F_i$,
$\phi_i(x) = o'(x) + \alpha_i C(x)$,
where
$\alpha_i = \frac{1}{\rho_i-\rho_0}$.

Also $F_i \subseteq R_i$.

### Lemma D: reconstructing $C$ and $o'$ from two hard witnesses

Let $i\neq j$ be two valid non-reference witnesses, and define
$\alpha_i = (\rho_i-\rho_0)^{-1}$,
$\alpha_j = (\rho_j-\rho_0)^{-1}$.

Set
$\chi_{ij} = \frac{\phi_i-\phi_j}{\alpha_i-\alpha_j} \in \mathrm{RS}[H^2,k']$
and
$\beta_{ij} = \phi_i - \alpha_i \chi_{ij} = \frac{\alpha_i \phi_j - \alpha_j \phi_i}{\alpha_i-\alpha_j} \in \mathrm{RS}[H^2,k']$.

Then for every $x \in F_i \cap F_j$,
$\chi_{ij}(x) = C(x)$
and
$\beta_{ij}(x) = o'(x)$.

In particular,
$|F_i\cap F_j| \le \max_{\chi\in \mathrm{RS}[H^2,k']} \operatorname{agr}(C,\chi)$.

### Proof

Fix $x \in F_i\cap F_j$.

By definition of $F_i$ and $F_j$, we have
$\phi_i(x) = o'(x) + \alpha_i C(x)$
and
$\phi_j(x) = o'(x) + \alpha_j C(x)$.

Subtracting,
$\phi_i(x)-\phi_j(x) = (\alpha_i-\alpha_j) C(x)$,
so
$C(x) = \frac{\phi_i(x)-\phi_j(x)}{\alpha_i-\alpha_j} = \chi_{ij}(x)$.

Then
$\beta_{ij}(x) = \phi_i(x) - \alpha_i \chi_{ij}(x)
= o'(x)+\alpha_i C(x)-\alpha_i C(x)
= o'(x)$.

Because $\phi_i,\phi_j \in \mathrm{RS}[H^2,k']$, both $\chi_{ij}$ and $\beta_{ij}$ also lie in $\mathrm{RS}[H^2,k']$.

The final inequality is immediate: on $F_i\cap F_j$, the arbitrary word $C$ agrees with the codeword $\chi_{ij}$. Hence
$|F_i\cap F_j| \le \max_{\chi\in \mathrm{RS}[H^2,k']} \operatorname{agr}(C,\chi)$.
∎

---

### Corollary E: a large common hard core also collapses to one affine line

Let $T$ be a set of valid non-reference witnesses, and suppose there exists
$U \subseteq \bigcap_{i\in T} F_i$
with $|U| > k'$.

Then there exist codewords $\beta,\chi \in \mathrm{RS}[H^2,k']$ such that
$\phi_i = \beta + \alpha_i \chi$
for every $i\in T$, where $\alpha_i = (\rho_i-\rho_0)^{-1}$.

Equivalently, there exist codewords $u,\beta \in \mathrm{RS}[H^2,k']$ such that
$g_i = u + \rho_i \beta$
for every $i\in T$.

Consequently $|T|\le 4$.

### Proof

Again assume $|T|\ge 2$ and choose distinct $i,j\in T$.

Define $\chi=\chi_{ij}$ and $\beta=\beta_{ij}$ as in Lemma D.

For every $x\in U$, Lemma D gives
$\chi(x)=C(x)$
and
$\beta(x)=o'(x)$.

Now fix any $t\in T$. Since $U\subseteq F_t$, on $U$ we have
$\phi_t(x) = o'(x) + \alpha_t C(x) = \beta(x) + \alpha_t \chi(x)$.

Both $\phi_t$ and $\beta+\alpha_t\chi$ lie in $\mathrm{RS}[H^2,k']$, and they agree on more than $k'$ points. Therefore
$\phi_t = \beta + \alpha_t \chi$.

Now convert back to $g_t$:
$g_t = g_0 + (\rho_t-\rho_0)\phi_t
= g_0 + (\rho_t-\rho_0)(\beta+\alpha_t\chi)
= g_0 + (\rho_t-\rho_0)\beta + \chi$,
since $(\rho_t-\rho_0)\alpha_t=1$.

Thus
$g_t = (g_0 - \rho_0 \beta + \chi) + \rho_t \beta$.

If we set $u = g_0 - \rho_0 \beta + \chi$, then
$g_t = u + \rho_t \beta$
for every $t\in T$.

So all witnesses in $T$ again lie on one common affine line, and Lemma 3 from `proofs.md` gives $|T|\le 4$. ∎

---

## 4. A precise flaw in the current informal notes

I think one informal claim should *not* be imported into `proofs.md` in its current form.

The notes currently suggest, informally, that on the hard sets $F_i$ the witnesses are “mutually exclusive” and that pairwise intersections should be controlled near the dimension threshold.

That is too strong as stated.

### Why it is too strong

At a fixed coordinate $x \notin I_{\rho_0}$, the values
$\phi_i(x) = o'(x) + \alpha_i C(x)$
for distinct $\alpha_i$ are indeed pointwise distinct whenever $C(x)\neq 0$.

But pointwise distinctness of the *values* does **not** imply small overlap of the *domains* $F_i$.

The correct rigorous statement is Lemma D above:

- on $F_i\cap F_j$, the fixed arbitrary words $C$ and $o'$ agree with explicit Reed–Solomon codewords $\chi_{ij}$ and $\beta_{ij}$;
- if a whole cluster shares a common intersection of size $>k'$, then the cluster collapses onto one affine line, and Lemma 3 bounds it by $4$.

So the right conclusion from large overlap is not “impossible”, but rather “affine-line collapse”.

This also explains why the hard regime is subtle: pairwise overlaps of sets of density about $31/64$ have average size
$(31/64)^2 n' = 961n'/4096 \approx 0.2346 n'$,
which is still below
$k' = n'/4 = 1024n'/4096$.
So raw second-moment counting on the $D_i$ or $F_i$ sets cannot, by itself, force a $>k'$ common intersection.

---

## 5. Another correction: the old heuristic $|E_i\cap E_j|\le k'$ is not currently justified

I also think the old informal bound of the form
$|E_i\cap E_j| \le k'$
should not be used without an extra argument.

Here is the issue.

On $E_i\cap E_j$, one can reconstruct the reference branch from $(g_i,g_j)$, exactly as in Lemma B but with the reference branch instead of the opposite branch. This gives a codeword on $H$ that matches the far witness $f_i$ on both roots corresponding to each $x\in E_i\cap E_j$.

However, this only gives agreement on $2|E_i\cap E_j|$ points of $H$. Since “far” means agreement is strictly less than $n/2 = n'$, this only implies
$|E_i\cap E_j| < n'/2$,
not $|E_i\cap E_j|\le k' = n'/4$.

So the old $k'$-level intersection claim for $E_i\cap E_j$ is not presently rigorous.

---

## 6. What these lemmas buy us immediately

The hard regime now splits more sharply into two sub-obstructions.

### 6.1. Equality-budget obstruction

By Lemma A, any witness with only moderately large $R_i$ must consume a large disjoint equality set $I_{\rho_i}\setminus I_{\rho_0}$. Therefore there can only be $O(1)$ of them.

So if a large hard family exists, then after choosing a good reference $\rho_0$, most witnesses must satisfy
$|R_i| \approx 31n'/64 - |I_{\rho_0}|$,
i.e. the hard set is forced much closer to the maximal possible opposite-branch size.

This is a genuine strengthening over the previous $9n'/32$ cutoff.

### 6.2. Common-core collapse obstruction

By Corollaries C and E, any cluster of witnesses sharing a common subset of $D_i$ or of $F_i$ of size $>k'$ collapses to one affine line, and then Lemma 3 bounds the cluster by $4$.

So the unresolved case is now very specific:

- many witnesses,
- each with very large $R_i$,
- but with no common $D$-core or $F$-core above the $k'$ threshold.

That is a much cleaner residual configuration than before.

---

## 7. Next steps I would suggest

I think the next promising steps are now very concrete.

### Step 1: choose the reference to minimize equality budget

Because the non-universal equality sets are disjoint, among many parameters one should be able to choose $\rho_0$ with very small $|I_{\rho_0}\setminus I_{\mathrm{all}}|$.

If we can formalize a clean “puncturing away $I_{\mathrm{all}}$” reduction, then Lemma A becomes much stronger numerically.

### Step 2: combine Lemma A with Corollary E

Once $|I_{\rho_0}|$ is small, Lemma A forces $|R_i|$ very close to $31n'/64$ for almost all remaining witnesses. Then the $F_i$ are also large, and Corollary E says that any common $>k'$ core gives immediate collapse to at most $4$ witnesses.

So the remaining combinatorics becomes:

- a family of dense subsets $F_i \subseteq H^2$,
- each coming from a hard witness,
- with no common intersection above $k'$.

That is the exact point where an extremal set-system or dependent-random-choice style argument might become relevant, but now it would be applied to a much narrower family.

### Step 3: if possible, exploit both $C$ and $o'$ jointly

Lemma D says that on $F_i\cap F_j$ we simultaneously interpolate both $C$ and $o'$ by codewords.

A future argument might use the *pair* $(C,o')$ rather than either one alone. Right now pairwise agreement sizes are below the naive uniqueness threshold, but the two-word structure could still carry extra rigidity if combined with the witness geometry.

---

In short, I think the strongest rigorous progress this round is:

1. a new equality-budget lemma showing how bounded equality sets force $|R(\phi_i)|$ upward, and  
2. explicit pairwise intersection polynomials on $D_i\cap D_j$ and $F_i\cap F_j$, with a clean corollary that any common intersection of size $>k'$ collapses the entire cluster to a single affine line, hence to at most $4$ witnesses.

These are both directly testable against the current `proofs.md` framework.