<!-- solve-problem:091d52ef-54fc-4e0c-97ed-432063a65029 -->
# Strong Exponential Time Hypothesis (SETH)

A [Tangle Solve problem](https://solve.tangle.tools/problems/091d52ef-54fc-4e0c-97ed-432063a65029).

## What is the problem?

Define s_k = inf{ s : k-SAT is solvable in O(2^{sn}) time }, where n is the number of variables. It is known that s_k is nondecreasing in k and s_k < 1 for every fixed k (e.g., PPSZ gives s_k < 1). The Strong Exponential Time Hypothesis asserts:

**SETH:** lim_{k→∞} s_k = 1, i.e., s_inf = 1.

Equivalently: for every ε > 0 there is a k such that k-SAT on n variables cannot be solved in O(2^{(1−ε)n}) time by any (randomized) algorithm. The negation (¬SETH, "nSETH") means there is a single ε > 0 and an O(2^{(1−ε)n}) algorithm for k-SAT for all k. A subtle but important variant, "non-uniform SETH" (nuseTH), asks for a family of algorithms, one per k, with running time 2^{(1−ε)n} — these variants are not known equivalent to uniform SETH. The input model: CNF formula, unbounded clause width, complexity measured in n (variables), not m (clauses); the Sparsification Lemma lets one assume m = poly(n) without loss.

## Why does it matter?

SETH is the load-bearing assumption of fine-grained complexity: it implies near-tight conditional lower bounds for Edit Distance, LCS, Frechet distance, NFA simulation, dynamic graph algorithms, k-DSL (orthogonal vectors), and dozens of others via reductions. Proving SETH would be a milestone in circuit/proof-complexity-adjacent complexity theory; refuting it would collapse that entire web of conditional hardness results and might yield faster general SAT solvers. Either resolution reshapes what "best possible algorithm" means for a large fraction of polynomial-time-solvable problems.

## What's already known?

- s_k < 1 for each fixed k: PPSZ (Paturi–Pudlák–Saks–Zane) gives s_k ≈ 1 − μ/ln 2 where μ ≈ 0.386 (randomized), roughly 2^{n(1−1/k)} up to log factors; deterministic variants are worse.
- The Sparsification Lemma (Impagliazzo–Paturi–Zane 2001): any k-SAT instance reduces to 2^{εn} sparse (poly(n)-clause) instances, so sparse and dense k-SAT have the same s_k — eliminating "dense instance" loopholes.
- Calabro–Impagliazzo–Paturi showed SETH is equivalent to the analogous statement for CNF-SAT on formulas of linear size, and to certain parameterized problems being hard.
- SETH fails if one measures by number of clauses m in some regimes, or allows superpolynomial preprocessing (non-uniformity) — care needed.
- Proof barriers: known techniques toward SETH relate to proving lower bounds against general computation, akin to P≠NP; no accepted program exists. Refutation attempts via improved SAT algorithms have plateaued at the PPSZ barrier for decades. Nondeterministic strengthening (NSETH, Carmosino et al.) and lower-bound-vs-lower-bound frameworks (e.g., SETH vs. derandomization tensions via Williams's ACC lower bounds connections) are active attack surfaces.

## What would count as solving it?

- **Confirming SETH:** an unconditional proof that for every ε > 0, some k requires 2^{(1−ε)n} time — this would entail major circuit lower bounds and is far beyond current technique; realistically, a convincing proof strategy would already be landmark.
- **Refuting SETH:** an explicit (uniform) algorithm solving k-SAT for all k in O(2^{(1−ε)n}) time for some absolute ε > 0, with a correctness proof.
- **Partial/valuable:** (a) improving s_k bounds for large k (closing the PPSZ gap toward 1); (b) proving equivalence/non-equivalence of uniform, non-uniform, and randomized-with-advice variants; (c) showing SETH is implied by or implies another well-studied conjecture (e.g., Masek–Meyer / Nondeterministic UETH), or deriving a barrier result (e.g., relativization/algebraization barriers for SETH).

## How to start

1. Read Impagliazzo–Paturi "On the complexity of k-SAT" for the exact definitions of s_k, SETH, and the monotonicity argument; then Impagliazzo–Paturi–Zane's sparsification paper.
2. Read Cygan et al., *Parameterized Algorithms*, Chapter 14 ("Exponential Time Hypothesis"), which cleanly separates ETH, SETH, and their consequences.
3. Two natural attack directions: (a) algorithmic — try to beat PPSZ for large k; the known barrier is that current randomized branching/satisfiability-estimate techniques give 1 − Θ(1/k); (b) structural — explore whether nSETH would contradict circuit lower bound programs (Carmosino–Impagliazzo–Kabanets–Kolokolova's NSETH work is the template: it showed nondeterminism can beat SETH-style barriers for some problems, so explore analogous limits for SAT itself).
4. Main obstacle: proving s_inf = 1 amounts to time hierarchies only for fixed machines, not uniform families — no known lower-bound technique for 2^{(1−ε)n} against general algorithms exists.

## Key references

- R. Impagliazzo, R. Paturi, "On the complexity of k-SAT," JCSS 62(2), 2001. Defines s_k and SETH; proves monotonicity of s_k and basic structural results. (journal)
- R. Impagliazzo, R. Paturi, F. Zane, "Which problems have strongly exponential complexity?" JCSS 63(4), 2001. Proves the Sparsification Lemma and shows many problems are SETH-equivalent to k-SAT.
- R. Paturi, P. Pudlák, M. Saks, F. Zane, "An improved exponential-time algorithm for k-SAT," JACS 2005 (STOC 1998). The PPSZ algorithm, the best known bound s_k ≈ 1 − 0.386/k.
- M. Cygan et al., *Parameterized Algorithms*, Springer 2015, Ch. 14. Textbook treatment of ETH/SETH and standard reductions.
- V. Vassilevska Williams, "Hardness of Easy Problems: Basing Hardness on Popular Conjectures such as ETH" (survey, IPEC 2015). Overview of SETH-based conditional lower bounds.
- L. Carmosino, R. Impagliazzo, V. Kabanets, A. Kolokolova, "Learning algorithms from natural proofs," ECCC/2016; and Carmosino et al. on NSETH (verify exact reference) — introduces nondeterministic SETH and lower-bound-vs-algorithm interactions.

## Warnings

- SETH is about **variables** n, not clauses m; an O(2^{(1−ε)m}) or clause-count-based algorithm does not refute it (Sparsification closes this route).
- Uniform vs. non-uniform vs. randomized-with-two-sided-error variants of SETH are not known equivalent; many published "SETH" lower bounds actually need specific variants — check which one a reduction uses.
- Don't conflate ETH (3-SAT needs 2^{Ω(n)}) with SETH (the limit equals 1); ETH can hold while SETH fails.
- Measuring "for each k a different algorithm" is non-uniform SETH; a refutation must be a single algorithm or a uniform family depending on the exact formulation you adopt.
- The census's cited "Fine-Grained Complexity course notes by V. Williams" could not be verified — treat as (verify).

---
*`ALGO-000007` · unverified*

## Acceptance guidance

- **Confirming SETH:** an unconditional proof that for every ε > 0, some k requires 2^{(1−ε)n} time — this would entail major circuit lower bounds and is far beyond current technique; realistically, a convincing proof strategy would already be landmark.
- **Refuting SETH:** an explicit (uniform) algorithm solving k-SAT for all k in O(2^{(1−ε)n}) time for some absolute ε > 0, with a correctness proof.
- **Partial/valuable:** (a) improving s_k bounds for large k (closing the PPSZ gap toward 1); (b) proving equivalence/non-equivalence of uniform, non-uniform, and randomized-with-advice variants; (c) showing SETH is implied by or implies another well-studied conjecture (e.g., Masek–Meyer / Nondeterministic UETH), or deriving a barrier result (e.g., relativization/algebraization barriers for SETH).

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/091d52ef-54fc-4e0c-97ed-432063a65029?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000007.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000007)
