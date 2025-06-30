<!-- slide -->
# On Deterministically Finding an Element of High Order Modulo a Composite
**Ziv Oznovich** and **Ben Lee Volk**
Reichman University

---

## Motivation

- **Derandomization** is believed to be possible with *only* polynomial slow down
<span class="fragment">
- **Computational Number Theory** features problems where randomized algorithms significantly outperform deterministic ones
</span>

---

## Integer Factorization Derandomization
- Fundamental to the security of **RSA encryption**, which relies on the hardness of factoring $N = pq$ for large primes $p, q$
<span class="fragment">
- Best known randomized algorithm runs in time $\exp(\tilde{O}(\sqrt{\log N}))$
</span>
<span class="fragment">
- Best known deterministic algorithms from the 70's were $N^{1/4+o(1)}$
</span>
> By Strassen and Pollard
- Recent (2021-22) deterministic breakthroughs achieved $N^{1/5+o(1)}$
> By Hittmeir and Harvey

---

## The Role of Multiplicative Order in Factorization

- **Finding large-order elements** is a natural derandomization problem
> Most elements in $\mathbb{Z}_N^*$ have large order, but it is unclear how to **find one deterministically**
- The latest deterministic factorization algorithm relies on finding an element $a \in \mathbb{Z}_N^*$ with a **large multiplicative order**
> They specifically require finding an element whose order is at least roughly $N^{1/5}$

---

## Definitions

### $\mathbb{Z}_N^*$ - Multiplicative Group of Integers Modulo $N$

- Consists of all integers $a$ such that $1 \le a < N$ and $\gcd(a, N) = 1$

### $\text{ord}_N(a)$ -  Order of an Element $a$ Modulo $N$

- The smallest positive integer $k$ such that $a^k \equiv 1 \pmod{N}$

---

## Previous Results - Hittmeir's Algorithm (2018)

- Given composite $N$ and $D \ge N^{2/5}$
- Runs in time $D^{1/2+o(1)}$
- Outputs
    - an element $a \in \mathbb{Z}_N^*$ of multiplicative order at least $D$
    - or a nontrivial factor of $N$
> As a subroutine in a factorization algorithm this is a "win-win" result
- When applied with $D=N^{2/5}$, it runs in $N^{1/5+o(1)}$ time, matching other algorithm steps

---

## Our Result

- We give a deterministic algorithm based on Hittmeir's algorithm
- Runs in time $D^{1/2+o(1)}$
> Same as previous result
- It works for a **wider range of parameters** namely $D \ge N^{1/6}$
> Compared to $D \ge N^{2/5}$
- This enables finding an element of order $N^{1/5}$ in $N^{1/10+o(1)}$ time for the factorization algorithm
> Compared to finding an element of order $N^{2/5}$ in $N^{1/5+o(1)}$ time

---

## Main Algorithm Simplified Overview

- Try $a = 2, 3, \dots$
    - **While** $a^M\equiv 1 \pmod N$: $a\gets a+1$
    - Let $m = \mathrm{ord}_N(a)$
    - **If** $m > D$: **return** $a$
    - **Else**:
        - $M \gets \mathrm{lcm}(M, m)$
- When $M \ge D$
    - Learn $p\equiv 1 \pmod M$ for divisors of $N$
    - Use this to factor $N$

---

## Shanks' Method for Order Computation

- **Goal**: Given $a \in \mathbb{Z}_N^*$
    - if $\operatorname{ord}_N(a) < D$ calculate it
    - else, state $\operatorname{ord}_N(a) > D$
- **Shanks' Baby-Step Giant-Step** algorithm:
    - Precompute $a^j$ for $0 \le j < \lceil \sqrt{D} \rceil$ (baby steps)
    - Compute $a^{-i\lceil \sqrt{D} \rceil}$ for $0 \le i < \lceil \sqrt{D} \rceil$ (giant steps)
    - Search for collision: $a^{i\lceil \sqrt{D} \rceil + j} \equiv 1 \mod N$
- **Time Complexity**: $\tilde{O}(\sqrt{D})$

---

## Consecutive Roots Bound Improvement

- Hittmeir upper bounds the number of consecutive elements $a$ satisfying $a^M\equiv 1 \pmod N$ by $M$
- Forbes, Kayal, Mittal and Saha (2011) give a bound on the number of common roots of a set of polynomials $S=\{(x+a_i)^\ell-\theta_i\}_{1\leq i\leq k}$
- We use their lemma to bound $a^M\equiv 1 \pmod N$ by $O(\sqrt{M})$ consecutive roots

---

## Factoring Given the Residue Class of Divisors

- Based on Harvey–Hittmeir’s algorithm (2022) for finding all $r$'th power divisors
- Utilizing the $p \equiv 1 \pmod s$ information to reduce the runtime by a factor of $s$
- Define polynomials $f_i(x)$ that vanishe on a small root related to the divisor
- Build lattice from $f_i(x)$
- Apply "Lenstra–Lenstra–Lovász" lattice base reduction
- Get small-norm polynomial $h(x)$
- Find small roots over the integers

---

## Conclusion

- We provide a deterministic algorithm for finding elements of large multiplicative order, with improved parameter range
- This contributes to improving the efficiency of part of the current fastest deterministic integer factorization algorithm

---

# Thanks **Ben Lee Volk** 🙏
# Questions?