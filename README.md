<!-- solve-problem:a09334cd-bba4-4ef7-9fc5-ca85fadf533e -->
# 3SUM conjecture

A [Tangle Solve problem](https://solve.tangle.tools/problems/a09334cd-bba4-4ef7-9fc5-ca85fadf533e).

## What is the problem?

Given a set S of n integers, decide whether there exist a, b, c ∈ S with a + b + c = 0. The trivial algorithm runs in O(n²) time (via sorting and a linear scan, or hashing). The 3SUM conjecture asserts that no algorithm achieves O(n^{2−ε}) time for any constant ε > 0.

Formal setting: word-RAM model with O(log n)-bit words (the model matters — see Warnings). Input integers may be assumed bounded in magnitude, since the problem is fixed-parameter tractable in the bit length: distinct sums span O(n² · U) values, so with U = poly(n) the input "fits" in O(log n) bits, and the conjecture is about this regime. Variants include 3SUM on three separate sets A, B, C (deciding ∃a∈A, b∈B, c∈C: a+b+c=0), which are subquadratic-equivalent to the set version up to log factors. A related distinct notion: output-sensitive or approximate versions, and the conjecture is standardly stated for randomized algorithms with two-sided error allowed to fail.

The conjecture is a conditional hardness assumption in fine-grained complexity: it is the quantitative analog for n² of what ETH (ALGO-000008) is for 2ⁿ. It is a conjecture, not a theorem — "solving" means either refuting it (finding a truly subquadratic algorithm) or proving a matching lower bound (conditioned on, or unconditionally in a restricted model).

## Why does it matter?

3SUM-hardness reductions establish essentially quadratic lower bounds for dozens of problems: collinearity detection, polygon containment, planar motion planning queries (Gajentaan–Overmars), and string problems like jumbled indexing — but these all inherit the conditional status. A truly subquadratic algorithm would collapse all these lower bounds at once and force a rewrite of the fine-grained complexity landscape (which has since shifted toward the stronger 3SUM+ / APSP-hardness framework). A proof of hardness (even in restricted models) would give the first unconditional quadratic lower bound for a natural algebraic problem. Practically, 3SUM-style kernels appear in computational geometry pipelines and database join processing.

## What's already known?

- **Slightly subquadratic algorithms:** Baran–Demaine–Pătraşcu (2008) achieved n²/polylog n viaFredman's trick and hashing/sorting networks on word-RAM; Chan (SODA 2018) improved this to n²(log log n)^{O(1)} / log^Ω(1) n using (median,+)-convolution machinery. These show the conjecture, if true, is tight up to log factors — but the techniques seem incapable of n^{2−ε}.
- **Integer magnitude matters:** Grønlund–Pettie (2014, not in census; verify) gave slightly subquadratic 3SUM in the decision-tree / comparison model, disproving the conjecture's comparison-model form. The conjecture survives only on the full word-RAM with unrestricted memory.
- **Quantum:** Ambainis (2007) gave Õ(n) quantum algorithms (quantum walks / element distinctness).
- **Hardness side:** No unconditional superlinear lower bound exists on any general model. Even proving an Ω(n log n) lower bound for 3SUM in general is open. Conditional reductions connect 3SUM to convolution-3SUM, algebraic-3SUM, and geometric problems (Pătraşcu 2010 reductions to triangles in graphs, etc.).
- Self-reducibility tricks (e.g., hashing input into buckets so a+b+c=0 must have elements in nearby buckets, as in BDP08) reduce to convolutions — the main known lever.

## What would count as solving it?

1. **Refutation:** An explicit randomized (or deterministic) algorithm deciding 3SUM on O(log n)-bit integers in O(n^{2−ε}) expected time for some constant ε > 0 on the word-RAM.
2. **Confirmation (conditional):** A proof that no such algorithm exists under a standard stronger assumption (e.g., via tight reduction from a hardness assumption believed stronger) — though this partially begs the question.
3. **Confirmation (restricted models):** An unconditional Ω(n²) (or even n^{2−o(1)}) lower bound in a meaningful nontrivial model (e.g., generalizing comparison trees beyond Grønlund–Pettie, or bounded communication/sampling models).
4. **Weaker accepted milestones:** improved polylog exponent; an n^{1.99} algorithm; unconditional lower bounds above Ω(n log n) for the word-RAM.

## How to start

1. Read Chan (arXiv:1708.03063) Sections 1–3 to understand the current log-factor barrier, then Baran–Demaine–Pătraşcu's bucketing/Fredman-trick framework.
2. Study the convolution connection: reduce 3SUM to (min,+)-type convolution structure and check whether any known algebraic technique (matrix multiplication, FFT on structured subsets) breaks the barrier.
3. For lower bounds: read Grønlund–Pettie's decision-tree lower bound (verify) and consider whether the Ω(n²) comparison bound can be lifted to computation models with cell-probe analogues.
4. Main obstacle on the algorithmic side: bucketing/randomization reduces 3SUM to problems (convolution, dominance) that are themselves 3SUM-hard-equivalent — you bounce between equivalent forms without gaining ε. Identify a genuinely inequivalent intermediate problem.

## Key references

- A. Gajentaan, M. Overmars, "On a class of O(n²) problems in computational geometry," Computational Geometry: Theory and Applications 5, 1995. Defines 3SUM-hardness via linear-time reductions from 3SUM to dozens of geometry problems. (No stable link; standard journal.)
- T. Chan, "More logarithmic-factor speedups for 3SUM, (median,+)-convolution, and some geometric 3SUM-hard problems," SODA 2018, arXiv:1708.30763-corrected → arXiv:1708.03063 (verify exact number), https://arxiv.org/abs/1708.03063. Current best classical bound n²(log log n)^{O(1)}/log^Ω(1) n via self-reduction to convolutions.
- I. Baran, E. Demaine, M. Pătraşcu, "Subquadratic algorithms for 3SUM," Algorithmica 50, 2008. First n²/polylog speedup using input bucketing and Fredman's trick.
- A. Ambainis, "Quantum walk algorithm for element distinctness," SIAM J. Comput. 37(1), 2007, arXiv:quant-ph/0311001. Quantum walk machinery yielding near-linear quantum 3SUM.
- A. Grønlund, S. Pettie, "Threesomes, degenerates, and love triangles," FOCS 2014 (verify). Subquadratic 3SUM in the comparison/decision-tree model, refuting that variant of the conjecture.
- M. Pătraşcu, "Towards polynomial lower bounds for dynamic problems," STOC 2010 (verify relevance). Reductions from 3SUM to reporting triangles, connecting it to broader fine-grained hardness.

## Warnings

- **Model sensitivity:** The conjecture is false in the comparison model (Grønlund–Pettie) and false quantumly (Ambainis). It is only credible on the word-RAM with randomization. State your model before claiming anything.
- **Integer size:** 3SUM is solvable in near-linear time via FFT if the universe is small enough (n^{2−ε} range, roughly); the conjecture concerns inputs with poly(n)-bounded or arbitrary integers. An "algorithm" exploiting tiny universes doesn't count.
- **Duplicate handling:** the standard version requires x + y + z = 0 with elements as set members; allowing reuse of the same element three times (x+x+x) vs. distinct indices changes nothing asymptotically but fix a convention.
- Common dead end: reducing 3SUM to itself-equivalent forms (convolution-3SUM, 3SUMX) and mistaking reformulation for progress — the equivalence class is large and closed under known techniques.

---
*`ALGO-000009` · flagged for review*

## Acceptance guidance

1. **Refutation:** An explicit randomized (or deterministic) algorithm deciding 3SUM on O(log n)-bit integers in O(n^{2−ε}) expected time for some constant ε > 0 on the word-RAM.
2. **Confirmation (conditional):** A proof that no such algorithm exists under a standard stronger assumption (e.g., via tight reduction from a hardness assumption believed stronger) — though this partially begs the question.
3. **Confirmation (restricted models):** An unconditional Ω(n²) (or even n^{2−o(1)}) lower bound in a meaningful nontrivial model (e.g., generalizing comparison trees beyond Grønlund–Pettie, or bounded communication/sampling models).
4. **Weaker accepted milestones:** improved polylog exponent; an n^{1.99} algorithm; unconditional lower bounds above Ω(n log n) for the word-RAM.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/a09334cd-bba4-4ef7-9fc5-ca85fadf533e?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000009.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000009)
