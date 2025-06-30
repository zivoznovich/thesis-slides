<!-- slide -->
# On Deterministically Finding an Element of High Order Modulo a Composite
**Ziv Oznovich** and **Ben Lee Volk**
Reichman University

---

## Motivation

- **Derandomization** is believed to be possible with *only* polynomial slowdown
- **Computational Number Theory** features problems where randomized algorithms significantly outperform deterministic ones

---

## Integer Factorization Derandomization

- Fundamental to the security of **RSA encryption**
    - Relies on the hardness of factoring $N = pq$ for large primes $p, q$
- Best known randomized algorithm:
  $\exp(\tilde{O}(\sqrt{\log N}))$
- Best known deterministic algorithms from the 70's:
  $N^{1/4+o(1)}$
  <span class="fragment">Strassen and Pollard</span>
- Recent breakthroughs (2021–22):
  $N^{1/5+o(1)}$
  <span class="fragment">Hittmeir and Harvey</span>

---

## The Role of Multiplicative Order in Factorization

- **Finding large-order elements** is a natural derandomization problem
  <span class="fragment">Most elements in $\mathbb{Z}_N^*$ have large order</span>
  <span class="fragment">But finding one **deterministically** is hard</span>

- Latest deterministic factorization algorithms rely on
  <span class="fragment">$a \in \mathbb{Z}_N^*$ with $\operatorname{ord}_N(a) \gtrsim N^{1/5}$</span>

---

## Definitions

**$\mathbb{Z}_N^*$**:
The multiplicative group of integers modulo $N$:
$\{ a \in \mathbb{Z} \mid 1 \le a < N,\ \gcd(a, N) = 1 \}$

**Order of $a$ modulo $N$**:
Smallest $k$ such that $a^k \equiv 1 \mod N$
$\operatorname{ord}_N(a)$

---

## Hittmeir's Algorithm (2018)

- Given composite $N$ and $D \ge N^{2/5}$
- Runs in time $D^{1/2+o(1)}$
- Outputs:
    - $a \in \mathbb{Z}_N^*$ with $\operatorname{ord}_N(a) \ge D$, or
    - Nontrivial factor of $N$
- <span class="fragment">A "win-win" subroutine for factorization</span>
- <span class="fragment">With $D = N^{2/5}$, runtime = $N^{1/5+o(1)}$</span>

---

## Our Result

- A **deterministic algorithm**, based on Hittmeir’s idea
- Same runtime: $D^{1/2+o(1)}$
- Works for **wider range**: $D \ge N^{1/6}$
- <span class="fragment">Allows finding $a$ with $\operatorname{ord}_N(a) \approx N^{1/5}$</span>
- <span class="fragment">Now possible in $N^{1/10+o(1)}$ time</span>

---

## Main Algorithm – Simplified

For increasing $a = 2, 3, \dots$:

1. If $a^M \equiv 1 \pmod{N}$ → skip
2. Compute $m = \operatorname{ord}_N(a)$
3. If $m > D$ → **return $a$**
4. Else → update $M = \operatorname{lcm}(M, m)$

When $M \ge D$, use
<span class="fragment">$p \equiv 1 \mod M$</span>
<span class="fragment">→ Factor $N$</span>

---

## Shanks' Order Algorithm

- Given $a \in \mathbb{Z}_N^*$, goal is:
    - Find $\operatorname{ord}_N(a)$ if $\le D$, or prove it's $> D$
- **Baby-Step Giant-Step** method:
    - Precompute $a^j$ for $0 \le j < \sqrt{D}$ (baby steps)
    - Precompute $a^{-i\sqrt{D}}$ for $0 \le i < \sqrt{D}$ (giant steps)
    - Search for collision

Runtime: $\tilde{O}(\sqrt{D})$

---

## Improving Consecutive Roots Bound

- Hittmeir bounded:
  $\#\{a \mid a^M \equiv 1 \mod N\} \le M$
- We improve to $O(\sqrt{M})$
  <span class="fragment">Using a result by Forbes, Kayal, Mittal & Saha (2011)</span>
- <span class="fragment">Faster progress through candidate $a$ values</span>

---

## Factoring with Residue Classes

- Based on Harvey–Hittmeir (2022)
- Goal: Find $r$-th power divisors of $N$
  <span class="fragment">Given that $p \equiv 1 \mod s$</span>

Steps:
1. Construct polynomials $f_i(x)$ vanishing at roots tied to $p$
2. Build lattice from their coefficients
3. Use **LLL** basis reduction
4. Find small-norm polynomial $h(x)$
5. Solve $h(x) = 0$ over integers → find $p$

---

## Conclusion

- We present a deterministic algorithm to find elements of large multiplicative order
- Works for $D \ge N^{1/6}$ (vs $N^{2/5}$ in prior work)
- <span class="fragment">Enables faster subroutine in deterministic integer factorization</span>

---

# Thank you 🙏
## Special thanks to **Ben Lee Volk**
**Questions?**