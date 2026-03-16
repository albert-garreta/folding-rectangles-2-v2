## Audit of the current draft

I found three concrete points where the current writeup can be tightened or corrected.

1. **Lemma 3 is true, but its current proof is not safe.**  
   The proof assumes that for distinct codewords $a,b \in RS[H,k]$, the folds $A_\rho=\mathrm{Fold}[a,\rho]$ and $B_\rho=\mathrm{Fold}[b,\rho]$ are distinct codewords of $RS[H^2,k/2]$. This can fail.

   A concrete example is:
   - take any $\rho_* \in \mathbb F$,
   - take any nonzero polynomial $Q(X)$ of degree $< k/2$,
   - define $a(h)=0$ and $b(h)=(h-\rho_*)Q(h^2)$ on $H$.

   Then $a,b$ are distinct codewords in $RS[H,k]$, but
   $b_e(x)=-\rho_* Q(x)$ and $b_o(x)=Q(x)$, so
   $B_{\rho_*}(x)=b_e(x)+\rho_* b_o(x)=0=A_{\rho_*}(x)$ for every $x \in H^2$.
   Thus $A_{\rho_*}=B_{\rho_*}$ identically.

   So the argument “distinct codewords in $RS[H^2,k/2]$ agree in at most $k'-1$ places” cannot be applied blindly.

   **However the statement of Lemma 3 is still correct, for a much simpler reason:** every selector in the rectangle agrees with one of the two endpoint maps on at least half of the pairs, hence on at least $n/2$ field points. I give a rigorous proof below.

2. **Lemma 12 has the right idea, but it misses a multiplicity issue.**  
   It bounds the number of possible slopes $h$ in the moderate regime using list recovery, but it does **not** by itself bound how many different $\rho$ can correspond to the same $h$.  
   I give a clean replacement below: an **affine-line counting lemma** showing that for any fixed slope $h$, there are at most $4$ such parameters $\rho$.

3. **Lemma 13 tries to bound the number of $\rho$ for fixed $g$, but the proof depends on an unproved global bound on $|Z(g)|$.**  
   This dependency can be avoided entirely. I give a direct argument yielding the unconditional bound $|W(g)| \le 4$.

---

## Setup and notation

Let

- $n = |H|$,
- $n' = |H^2| = n/2$,
- $k' = k/2 = n'/4$,
- $T = (1-\delta_0)n' = 127n'/128$,
- $z = n'-T = n'/128$.

For a map $c : H \to \mathbb F$, write its even/odd parts on $H^2$ as

- $c_e(x) = \frac{c(h)+c(-h)}{2}$,
- $c_o(x) = \frac{c(h)-c(-h)}{2h}$,

where $h^2=x$. These are well-defined on $H^2$.

Then

- $\mathrm{Fold}[c,\rho](x) = c_e(x) + \rho c_o(x)$.

For a rectangle $R(a,b)$, write

- $A_\rho(x)=a_e(x)+\rho a_o(x)$,
- $B_\rho(x)=b_e(x)+\rho b_o(x)$.

---

## Lemma A: if both endpoints are codewords, then $X_R=\varnothing$

**Claim.** If $a,b \in RS[H,k]$, then every $f \in \mathcal F(R(a,b))$ is $1/2$-close to one of $a,b$. Hence $X_{R(a,b)}=\varnothing$.

### Proof

Fix $f \in \mathcal F(R(a,b))$.

For each $x \in H^2$, the rectangle definition says that on the pair $\{h,-h\}$ with $h^2=x$, the function $f$ uses either the pair from $a$ or the pair from $b$.

Let $S_a \subseteq H^2$ be the set of $x$ where $f$ chooses the $a$-pair, and let $S_b=H^2\setminus S_a$.

- On each $x \in S_a$, the function $f$ agrees with $a$ on both points $h$ and $-h$.
  Therefore $\operatorname{agr}(f,a) \ge 2|S_a|$.
- On each $x \in S_b$, the function $f$ agrees with $b$ on both points $h$ and $-h$.
  Therefore $\operatorname{agr}(f,b) \ge 2|S_b|$.

Since $|S_a|+|S_b|=n'$, one of $|S_a|,|S_b|$ is at least $n'/2$. Hence one of the agreements is at least $2 \cdot (n'/2)=n'=n/2$.

So $f$ agrees with one of the codewords $a,b \in RS[H,k]$ on at least $n/2$ positions. By definition, $f$ is $1/2$-close to $RS[H,k]$.

Therefore there is no $f \in \mathcal F(R(a,b))$ that is $1/2$-far from $V$, so $X_{R(a,b)}=\varnothing$.

$\square$

### Comment

This gives a short, robust proof of the conclusion of the current Lemma 3, and it avoids the fold-degeneracy issue described above.

---

## Lemma B: correlated agreement is injective, i.e. $|CA(f)| \le 1$

This is the rigorous version of the “witness injectivity geometry” in the notes.

**Claim.** Let $f : H \to \mathbb F$ be $1/2$-far from $V=RS[H,k]$. Then there is at most one $\rho \in \mathbb F$ such that $\mathrm{Fold}[f,\rho]$ is $1/128$-close to $RS[H^2,k/2]$.

### Proof

Assume for contradiction that there are two distinct parameters $\rho_1 \ne \rho_2$ in $CA(f)$.

Then there exist codewords $g_1,g_2 \in RS[H^2,k']$ such that

- $\mathrm{Fold}[f,\rho_1]$ agrees with $g_1$ on a set $S_1 \subseteq H^2$ of size at least $T$,
- $\mathrm{Fold}[f,\rho_2]$ agrees with $g_2$ on a set $S_2 \subseteq H^2$ of size at least $T$.

By inclusion-exclusion,

$|S_1 \cap S_2| \ge |S_1|+|S_2|-n' \ge 2T-n' = 126n'/128 = 63n'/64$.

Now write

- $f_e(x)=\frac{f(h)+f(-h)}{2}$,
- $f_o(x)=\frac{f(h)-f(-h)}{2h}$,

so that $\mathrm{Fold}[f,\rho](x)=f_e(x)+\rho f_o(x)$.

For every $x \in S_1 \cap S_2$ we have

- $f_e(x)+\rho_1 f_o(x)=g_1(x)$,
- $f_e(x)+\rho_2 f_o(x)=g_2(x)$.

Subtracting gives

$f_o(x)=\frac{g_1(x)-g_2(x)}{\rho_1-\rho_2}$.

Define the codeword $p_o \in RS[H^2,k']$ by

$p_o = \frac{g_1-g_2}{\rho_1-\rho_2}$.

Then on $S_1 \cap S_2$ we have $f_o=p_o$.

Now define

$p_e = g_1 - \rho_1 p_o$.

Since $g_1,p_o \in RS[H^2,k']$, also $p_e \in RS[H^2,k']$. On $S_1 \cap S_2$ we have $f_e=p_e$.

Let $P(X),Q(X)$ be the degree $<k'$ polynomials whose evaluations on $H^2$ are $p_e,p_o$ respectively. Define the univariate polynomial

$r(T)=P(T^2)+TQ(T^2)$.

Its degree is $<k$, so its evaluation on $H$ is a codeword of $V=RS[H,k]$.

Now fix $x \in S_1 \cap S_2$, and choose $h \in H$ with $h^2=x$. Since on this $x$ we have $f_e=p_e$ and $f_o=p_o$,

- $f(h)=f_e(x)+h f_o(x)=p_e(x)+h p_o(x)=r(h)$,
- $f(-h)=f_e(x)-h f_o(x)=p_e(x)-h p_o(x)=r(-h)$.

So for each $x \in S_1 \cap S_2$, the function $f$ agrees with $r$ on both points $h$ and $-h$.

Therefore

$\operatorname{agr}(f,r) \ge 2|S_1 \cap S_2| \ge 2 \cdot 63n'/64 = 63n'/32 = 63n/64$.

Since $63n/64 > n/2$, this says $f$ is $1/2$-close to the codeword $r \in V$, contradicting the assumption that $f$ is $1/2$-far from $V$.

Hence $|CA(f)| \le 1$.

$\square$

---

## Lemma C: affine-line counting, at most $4$ parameters $\rho$ per slope

This is the cleanest replacement for the current Lemma 13, and it is stronger because it works not only for fixed $g$, but for any affine family $u+\rho \phi$ of candidate folded codewords.

**Claim.** Fix a rectangle $R(a,b)$, and fix $u,\phi \in RS[H^2,k']$. Define

$W_R(u,\phi)=\{\rho \in \mathbb F : \exists f \in \mathcal F(R(a,b)) \text{ with } f \text{ $1/2$-far from } V,$  
$\operatorname{agr}(\mathrm{Fold}[f,\rho],\, u+\rho \phi) \ge T\}$.

Then $|W_R(u,\phi)| \le 4$.

### Proof

Fix $\rho \in W_R(u,\phi)$. Choose a witness $f_\rho \in \mathcal F(R(a,b))$ such that

$\operatorname{agr}(\mathrm{Fold}[f_\rho,\rho],\,u+\rho\phi) \ge T$.

Let $S_\rho \subseteq H^2$ be the corresponding agreement set, so $|S_\rho| \ge T$.

For each $x \in S_\rho$, the selector defining $f_\rho$ chooses one branch, either $a$ or $b$. Let us call that chosen branch $c_x$.

Then for every $x \in S_\rho$,

$u(x)+\rho \phi(x)=c_{x,e}(x)+\rho c_{x,o}(x)$.

Now define the exceptional subset $E_\rho \subseteq S_\rho$ by declaring that $x \in E_\rho$ if the chosen branch satisfies

- $c_{x,e}(x)=u(x)$,
- $c_{x,o}(x)=\phi(x)$.

In other words, on $x \in E_\rho$, the chosen branch matches the pair $(u,\phi)$ exactly, so the above equation holds for every $\rho$.

Let $U(X),\Phi(X)$ be the degree $<k'$ polynomials evaluating to $u,\phi$ on $H^2$, and define

$P(T)=U(T^2)+T\Phi(T^2)$.

Then $\deg P<k$, so $P|_H \in V$.

If $x \in E_\rho$ and $h^2=x$, then the chosen branch on the pair $\{h,-h\}$ has even part $u(x)$ and odd part $\phi(x)$, hence its values are

- $u(x)+h\phi(x)=P(h)$,
- $u(x)-h\phi(x)=P(-h)$.

So on every $x \in E_\rho$, the function $f_\rho$ agrees with the codeword $P$ on both points $h,-h$.

Therefore

$\operatorname{agr}(f_\rho,P) \ge 2|E_\rho|$.

Since $f_\rho$ is $1/2$-far from $V$, it agrees with every codeword of $V$ on fewer than $n/2=n'$ positions. Hence

$2|E_\rho| < n'$,

so

$|E_\rho| < n'/2$.

It follows that the non-exceptional success set satisfies

$|S_\rho \setminus E_\rho| > T - n'/2 = 127n'/128 - 64n'/128 = 63n'/128$.

Now fix $x \in S_\rho \setminus E_\rho$, and let $c_x$ again denote the chosen branch. The equation

$u(x)+\rho \phi(x)=c_{x,e}(x)+\rho c_{x,o}(x)$

can be rewritten as

$\rho(\phi(x)-c_{x,o}(x)) = c_{x,e}(x)-u(x)$.

Because $x \notin E_\rho$, it is impossible that simultaneously $\phi(x)=c_{x,o}(x)$ and $u(x)=c_{x,e}(x)$. If $\phi(x)=c_{x,o}(x)$ but $u(x)\ne c_{x,e}(x)$, then the above equation has no solution, contradicting $x \in S_\rho$. Therefore for $x \in S_\rho \setminus E_\rho$ we must have $\phi(x)\ne c_{x,o}(x)$, and then $\rho$ is uniquely determined by the chosen branch:

$\rho = \frac{c_{x,e}(x)-u(x)}{\phi(x)-c_{x,o}(x)}$.

Thus for each fixed $x \in H^2$, there are at most two possible values of $\rho$ that can occur in the set $S_\rho \setminus E_\rho$: one coming from branch $a$, and one coming from branch $b$.

Now double-count the set of incidences

$\{(\rho,x) : \rho \in W_R(u,\phi),\ x \in S_\rho \setminus E_\rho\}$.

- For each $\rho \in W_R(u,\phi)$, we have just proved that $|S_\rho \setminus E_\rho| > 63n'/128$.
  So the number of incidences is strictly greater than $|W_R(u,\phi)| \cdot 63n'/128$.
- For each $x \in H^2$, there are at most $2$ incidences.
  So the total number of incidences is at most $2n'$.

Therefore

$|W_R(u,\phi)| \cdot 63n'/128 < 2n'$.

Hence

$|W_R(u,\phi)| < 256/63 < 5$.

Since this is an integer, $|W_R(u,\phi)| \le 4$.

$\square$

### Important special case

Taking $\phi=0$ gives:

- for any fixed codeword $g \in RS[H^2,k']$, there are at most $4$ values of $\rho$ for which some far witness has $\mathrm{Fold}[f,\rho]$ $1/128$-close to $g$.

So this gives a rigorous, unconditional replacement for the draft’s current Lemma 13.

### Why the far condition matters

This proof uses the far condition in exactly one place: it shows that the exceptional set $E_\rho$ has size $<n'/2$. Without that, the conclusion is false: if one branch is literally the codeword $P$, then the same affine family $u+\rho\phi$ can work for all $\rho$.

This is one place where the actual task is stronger than the earlier notes that omitted the requirement that witnesses be far from $V$.

---

## Lemma D: reference-witness geometry

Now fix one reference witness:

- choose $\rho_0 \in X_R$,
- choose a far witness $f_0 \in \mathcal F(R)$,
- choose $g_0 \in RS[H^2,k']$,

such that $\mathrm{Fold}[f_0,\rho_0]$ agrees with $g_0$ on a set $S_0 \subseteq H^2$ of size at least $T$.

For each $x \in S_0$, let the branch chosen by $f_0$ be the “reference branch” at $x$. Define:

- $e(x),o(x)$ = even/odd parts of the reference branch at $x$,
- $e'(x),o'(x)$ = even/odd parts of the opposite branch at $x$.

Since $f_0$ succeeds on $S_0$, we have for every $x \in S_0$:

$g_0(x)=e(x)+\rho_0 o(x)$.

For a codeword $\phi \in RS[H^2,k']$, define

- $P(\phi)=\{x \in S_0 : \phi(x)=o(x)\}$,
- $R(\phi)=\{x \in S_0 : \phi(x)\notin\{o(x),o'(x)\}\}$.

### Lemma D1: same-branch matches are sparse

**Claim.** For every $\phi \in RS[H^2,k']$, we have $|P(\phi)| < n'/2$.

### Proof

Let $\phi \in RS[H^2,k']$. Define the codeword $u=g_0-\rho_0 \phi \in RS[H^2,k']$ and consider the degree $<k$ polynomial

$Q(T)=U(T^2)+T\Phi(T^2)$,

where $U,\Phi$ are the degree $<k'$ polynomials evaluating to $u,\phi$ on $H^2$.

Fix $x \in P(\phi)$, and let $h^2=x$. Since $x \in P(\phi)$, we have $\phi(x)=o(x)$, and because $g_0(x)=e(x)+\rho_0 o(x)$ we get

$u(x)=g_0(x)-\rho_0 \phi(x)=e(x)$.

So at $x$, the reference branch has even part $u(x)$ and odd part $\phi(x)$. Therefore its values on $\{h,-h\}$ are exactly $Q(h),Q(-h)$.

Hence $f_0$ agrees with the codeword $Q|_H \in V$ on both points corresponding to each $x \in P(\phi)$, so

$\operatorname{agr}(f_0,Q|_H) \ge 2|P(\phi)|$.

Because $f_0$ is $1/2$-far from $V$, the agreement is $<n/2=n'$, so $2|P(\phi)|<n'$, i.e. $|P(\phi)|<n'/2$.

$\square$

---

### Lemma D2: any second witness must switch branches on many coordinates

**Claim.** Let $\rho \ne \rho_0$, and let $(f,\rho,g)$ be another witness with $g \in RS[H^2,k']$. Put

$\phi = \frac{g-g_0}{\rho-\rho_0} \in RS[H^2,k']$.

Let $S$ be the agreement set where $\mathrm{Fold}[f,\rho]=g$, so $|S| \ge T$, and let $J=S_0 \cap S$. Then $|J| \ge 63n'/64$.

Let $D \subseteq J$ be the set of coordinates where $f$ chooses the branch opposite to the reference branch of $f_0$. Then

$|D| > 31n'/64$.

### Proof

First, by inclusion-exclusion,

$|J| \ge |S_0|+|S|-n' \ge 2T-n' = 63n'/64$.

Now take $x \in J \setminus D$. By definition, both witnesses choose the same branch at $x$; call its even/odd parts $(e(x),o(x))$.

Since $x \in S_0$, we have

$g_0(x)=e(x)+\rho_0 o(x)$.

Since $x \in S$, and the same branch is used by $f$, we also have

$g(x)=e(x)+\rho o(x)$.

Subtracting,

$g(x)-g_0(x) = (\rho-\rho_0)o(x)$,

so

$\phi(x)=o(x)$.

Thus $J \setminus D \subseteq P(\phi)$.

By Lemma D1, $|P(\phi)|<n'/2$. Hence

$|D| = |J|-|J\setminus D| > 63n'/64 - n'/2 = 31n'/64$.

$\square$

This is a rigorous version of the “same-branch set is $<n'/2$” phenomenon in the notes.

---

### Lemma D3: trichotomy on the opposite-branch set

**Claim.** In the situation of Lemma D2, fix $x \in D$. Then

$(\rho-\rho_0)\phi(x) = e'(x)-e(x) + \rho o'(x) - \rho_0 o(x)$.

Moreover:

1. If $\phi(x)=o(x)$, then $A_\rho(x)=B_\rho(x)$.
2. If $\phi(x)=o'(x)$, then $A_{\rho_0}(x)=B_{\rho_0}(x)$.
3. If $\phi(x)\notin\{o(x),o'(x)\}$, then $\rho$ is uniquely determined by $x$ and $\phi$ via

   $\rho = \frac{e(x)-e'(x)+\rho_0(o(x)-\phi(x))}{o'(x)-\phi(x)}$.

### Proof

Since $x \in D$, the two witnesses choose opposite branches at $x$.

Because $x \in S_0$, the reference witness contributes

$g_0(x)=e(x)+\rho_0 o(x)$.

Because $x \in S$, the second witness contributes

$g(x)=e'(x)+\rho o'(x)$.

Subtracting gives

$g(x)-g_0(x)=e'(x)-e(x)+\rho o'(x)-\rho_0 o(x)$.

Since $g-g_0=(\rho-\rho_0)\phi$, we obtain

$(\rho-\rho_0)\phi(x)=e'(x)-e(x)+\rho o'(x)-\rho_0 o(x)$.

This proves the displayed identity.

Now:

- If $\phi(x)=o(x)$, then the identity becomes

  $(\rho-\rho_0)o(x)=e'(x)-e(x)+\rho o'(x)-\rho_0 o(x)$,

  which simplifies to

  $e(x)+\rho o(x)=e'(x)+\rho o'(x)$.

  That is exactly $A_\rho(x)=B_\rho(x)$.

- If $\phi(x)=o'(x)$, then the identity becomes

  $(\rho-\rho_0)o'(x)=e'(x)-e(x)+\rho o'(x)-\rho_0 o(x)$,

  which simplifies to

  $e(x)+\rho_0 o(x)=e'(x)+\rho_0 o'(x)$.

  That is exactly $A_{\rho_0}(x)=B_{\rho_0}(x)$.

- If $\phi(x)\notin\{o(x),o'(x)\}$, then in particular $o'(x)-\phi(x)\ne 0$, so we can solve uniquely for $\rho$ and obtain the displayed formula.

$\square$

A useful reformulation is:

- on the opposite-branch set $D$, every coordinate lies either in $I_{\rho_0}$, or in $I_\rho$, or in the residual set $R(\phi)$ where $\rho$ is pointwise forced.

---

### Lemma D4: if the same slope $\phi$ works twice, then its residual set is tiny

**Claim.** Suppose the same $\phi \in RS[H^2,k']$ occurs for two distinct parameters $\rho_1 \ne \rho_2$, both relative to the same reference witness $(f_0,\rho_0,g_0)$. Then

$|R(\phi)| \le n'/64$.

More generally, if the same $\phi$ works for $m \ge 2$ distinct parameters, then

$|R(\phi)| \le \frac{m}{m-1}\cdot \frac{n'}{128}$.

### Proof

For each $i \in \{1,2\}$, let $(f_i,\rho_i,g_i)$ be a witness with

$\phi = \frac{g_i-g_0}{\rho_i-\rho_0}$.

Let $S_i$ be the agreement set of $(f_i,\rho_i,g_i)$, so $|S_i|\ge T$.

Since $R(\phi)\subseteq S_0$ and $|S_0\setminus S_i| \le n'-T=z$, we get

$|R(\phi)\cap S_i| \ge |R(\phi)|-z$.

Now fix $x \in R(\phi)\cap S_i$.

Because $x \in R(\phi)$, we have $\phi(x)\notin\{o(x),o'(x)\}$.

Also $x \in S_0 \cap S_i$, so the branch at $x$ cannot be the same as the reference branch: by Lemma D2, same-branch would force $\phi(x)=o(x)$, impossible. Hence $x$ lies in the opposite-branch set for witness $i$.

Therefore Lemma D3 applies, and on such an $x$ the value $\rho_i$ is uniquely equal to the pointwise expression

$\lambda_\phi(x)=\frac{e(x)-e'(x)+\rho_0(o(x)-\phi(x))}{o'(x)-\phi(x)}$.

In particular, if $x$ lies in both $R(\phi)\cap S_1$ and $R(\phi)\cap S_2$, then $\rho_1=\lambda_\phi(x)=\rho_2$, contradicting $\rho_1\ne \rho_2$.

So the sets $R(\phi)\cap S_1$ and $R(\phi)\cap S_2$ are disjoint.

Each has size at least $|R(\phi)|-z$, so

$2(|R(\phi)|-z) \le |R(\phi)|$.

Hence $|R(\phi)| \le 2z = n'/64$.

The general $m$-parameter version is identical: the $m$ sets $R(\phi)\cap S_i$ are pairwise disjoint, each has size at least $|R(\phi)|-z$, so

$m(|R(\phi)|-z) \le |R(\phi)|$,

which rearranges to

$|R(\phi)| \le \frac{m}{m-1}z = \frac{m}{m-1}\cdot \frac{n'}{128}$.

$\square$

### Consequence

If $|R(\phi)| > n'/64$, then that slope $\phi$ can correspond to **at most one** parameter $\rho$.

This will be especially useful for the hard regime, because the hard threshold $9n'/32$ is much larger than $n'/64$.

---

## Corollary E: the moderate regime contributes only $O(1)$ values of $\rho$

This is, in my view, the cleanest rigorous progress toward bounding $|X_R|$.

Fix the reference witness $(f_0,\rho_0,g_0)$ as above, and define lists on $S_0$ by

$L_x = \{o(x),o'(x)\}$.

Extend these arbitrarily to size-$2$ lists on all of $H^2$.

Let $\mathcal H_{\mathrm{mod}}$ be the set of codewords $\phi \in RS[H^2,k']$ such that

$|\{x \in H^2 : \phi(x) \in L_x\}| \ge 91n'/128$.

Because $91/128 > \sqrt{2 \cdot (1/4)} = 1/\sqrt 2$, the Guruswami-Sudan list-recovery theorem for Reed-Solomon codes with list size $2$ implies that

$|\mathcal H_{\mathrm{mod}}| \le L_{\mathrm{mod}}$,

where $L_{\mathrm{mod}}$ is an absolute constant depending only on the gap
$91/128 - 1/\sqrt 2 > 0$.

Now define $X_{\mathrm{mod}}$ to be the set of those $\rho \in X_R \setminus \{\rho_0\}$ for which there exists some witness $(f,\rho,g)$ with slope

$\phi=\frac{g-g_0}{\rho-\rho_0}$

satisfying

$|R(\phi)| \le 9n'/32$.

Then for such a $\phi$ we have

$|\{x \in S_0 : \phi(x)\in\{o(x),o'(x)\}\}| = |S_0|-|R(\phi)| \ge 127n'/128 - 9n'/32 = 91n'/128$,

so $\phi \in \mathcal H_{\mathrm{mod}}$.

For each fixed $\phi \in \mathcal H_{\mathrm{mod}}$, the corresponding candidate folded codewords are exactly the affine line

$g_\rho = g_0 + (\rho-\rho_0)\phi = (g_0-\rho_0\phi)+\rho\phi$.

By Lemma C, for each fixed $\phi$ there are at most $4$ values of $\rho$ admitting a far witness.

Therefore

$|X_{\mathrm{mod}}| \le 4L_{\mathrm{mod}}$.

So we have the rigorous decomposition

$|X_R| \le 1 + 4L_{\mathrm{mod}} + |\mathcal H_{\mathrm{hard}}|$,

where $\mathcal H_{\mathrm{hard}}$ is the set of slopes $\phi$ arising from witnesses with

$|R(\phi)| > 9n'/32$.

By Lemma D4, the map $\rho \mapsto \phi$ is injective on the hard regime, because $9n'/32 > n'/64$.

### What this achieves

This proves:

- all the “moderate” witnesses contribute only $O(1)$ values of $\rho$,
- every remaining $\rho$ can be indexed injectively by a distinct **hard slope** $\phi$.

So any pair $(a,b)$ with very large $|X_R|$ must produce many distinct hard slopes.

That is a precise, auditable reduction of the original problem.

---

## A useful negative check: why simple Johnson/Cauchy arguments do not replace GS here

I checked a tempting shortcut: reduce the list-recovery condition $\phi(x)\in\{o(x),o'(x)\}$ to ordinary agreement on the duplicated codeword $(\phi,\phi)$ against the target word $(o,o')$ on two copies of $H^2$.

This does **not** suffice.

- The guaranteed agreement fraction on the duplicated domain would only be $91/256 \approx 0.355$.
- The repeated RS code still has pairwise agreement parameter about $1/4$.
- Since $(91/256)^2 < 1/4$, the standard Cauchy/Johnson second-moment argument does not give a constant list-size bound.

So here one genuinely needs a list-recovery input, not just ordinary list decoding or a pairwise-agreement argument.

This matches the spirit of your notes: the moderate regime is exactly the place where Guruswami-Sudan-type structure matters.

---

## Concrete flaws now fixed / clarified

Here is how the new lemmas interact with the draft:

- **Current Lemma 3:** statement correct, proof unsafe.  
  Replace the proof by Lemma A.

- **Current Lemma 9:** essentially correct.  
  Lemma B gives a clean full proof.

- **Current Lemma 12:** conceptually right, but incomplete.  
  It bounds the number of candidate slopes $h$, not the number of parameters $\rho$.  
  Lemma C supplies the missing multiplicity control.

- **Current Lemma 13:** can be replaced entirely by Lemma C with $\phi=0$.  
  No unproved global estimate on $Z(g)$ is needed.

---

## Next steps

The remaining difficulty is now sharply isolated.

### What is already rigorous

For a fixed rectangle $R(a,b)$ and a fixed reference witness $(f_0,\rho_0,g_0)$:

1. Moderate slopes, namely those with $|R(\phi)| \le 9n'/32$, contribute only $O(1)$ values of $\rho$.
2. Any large $|X_R|$ therefore forces many distinct hard slopes $\phi$ with $|R(\phi)| > 9n'/32$.

### What remains open

One now needs an algebraic bound on the number of hard slopes.

The notes correctly identify why naive distance arguments are insufficient: once one gets down to pairwise overlap around $0.234n'$, this is already below the RS dimension threshold $k'=n'/4$, so ordinary MDS uniqueness no longer rules out many codewords.

### Two plausible next directions

1. **Exploit the pointwise rational formula on the hard residual set.**  
   On $R(\phi)$, the parameter $\rho$ is forced by
   $\rho=\lambda_\phi(x)$.
   For many hard slopes, one gets many low-degree codewords whose associated rational functions are constant on large structured sets. There may be an algebraic incidence statement hiding here.

2. **Exploit the equality sets $I_\rho=\{x : A_\rho(x)=B_\rho(x)\}$.**  
   Lemma D3 shows that when a hard witness switches branches, the only way to avoid pointwise forcing is to land in $I_{\rho_0}$ or $I_\rho$. Since the sets $I_\rho \setminus I_{\mathrm{all}}$ are pairwise disjoint, any argument that forces $I_\rho$ to be nontrivially large would immediately give an $O(1)$ bound.

---

## Bottom line

The main rigorous progress from this round is:

- a clean proof that $|CA(f)|\le 1$,
- a new affine-line counting lemma giving at most $4$ parameters $\rho$ per fixed slope,
- a rigorous reduction showing that all but $O(1)$ elements of $X_R$ must lie in the hard regime,
- and a precise identification of where the current proof sketch still needs a new algebraic idea.

If you want, in the next round I can try to push on the hard regime itself, starting from Lemma D3 and the injective map from hard $\rho$ to hard slopes $\phi$.