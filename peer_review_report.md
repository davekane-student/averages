# Peer Review Report

**Journal**: *Involve: A Journal of Mathematics* (or similar 3rd-tier discrete probability/undergraduate research journal)  
**Manuscript Title**: *Tie Probability in Repeated Random Averages: Diophantine and Asymptotic Analysis*  
**Reviewer**: Anonymous Referee  

---

## General Evaluation

This manuscript presents a thorough, detailed, and pedagogically oriented investigation of the "tie probability" $P_{\text{tie}}(R)$—the probability that two players achieve identical sample averages after $R$ repeated independent trials from discrete probability distributions. The authors successfully bridge elementary combinatorics, number theory (linear Diophantine equations and collision lattices), and classical analysis (Local Limit Theorems and Laplace's method for sums). 

The paper is exceptionally well-suited for an undergraduate-focused mathematics journal. It is highly verbose, self-contained, and includes interactive client-side HTML visualizations that greatly aid in illustrating the analytical regimes. The resolution of "Conjecture 8.2" (establishing that the $n$-sided symmetric case decays as $\Theta(R^{-1/2})$ for all $n$) is a strong contribution that corrects a common polynomial-decay misconception.

However, from the perspective of a rigorous academic mathematician, there are several key areas where the mathematical precision, definitions, and geometric explanations must be tightened before publication. Below, I outline these critiques and provide concrete suggestions for improvement.

---

## Rigorous Critiques & Recommendations

### 1. The Removable Singularity at Complementarity ($p_1 + p_2 = 1$)
* **Critique**: In Section 4.3, the authors derive a beautiful exact representation of the tie probability in terms of Legendre Polynomials:
  $$P_{\text{tie}}(R) = (p_1 + p_2 - 1)^R P_R\left( \frac{1 - p_1 - p_2 + 2 p_1 p_2}{p_1 + p_2 - 1} \right)$$
  While mathematically elegant, the authors fail to address the obvious singularity when $p_1 + p_2 = 1$ (which includes equal-but-fair probabilities $p_1=p_2=1/2$). If $p_1+p_2=1$, the denominator of the Legendre argument becomes zero, and the leading coefficient vanishes. Although the authors take the limit as $p \to 1/2$, a rigorous review requires resolving this singularity for *all* complementary pairs $p_1 + p_2 = 1$.
* **Recommendation**: Show explicitly that the singularity is **removable** for any pair satisfying $p_1 + p_2 = 1$. By using the leading term of the Legendre polynomial of degree $R$, $P_R(x) \sim \frac{1}{2^R} \binom{2R}{R} x^R$, prove that as $u = p_1+p_2-1 \to 0$:
  $$\lim_{u \to 0} u^R P_R\left( \frac{2p_1p_2 - u}{u} \right) = \binom{2R}{R} (p_1 p_2)^R$$
  Since $p_1+p_2=1 \implies p_2 = 1-p_1$, this recovers the Vandermonde-collapsed baseline $[p_1(1-p_1)]^R \binom{2R}{R}$ exactly. Incorporating this proof resolves a major potential source of confusion.

### 2. Precise Conditions on the Lattice Spacing (Span $d$)
* **Critique**: In Section 8 (Proof of Theorem 8.2), the authors define $V$ as consisting of $n$ "equally spaced values with lattice spacing $d$". In discrete probability and the Local Limit Theorem, we must be exceptionally precise about the **span** (maximal lattice spacing) of a distribution. A distribution on $\mathbb{Z}$ is *strongly $d$-lattice* if its support lies in a lattice $a + d\mathbb{Z}$ and $d$ is the largest integer for which this holds.
* **Recommendation**: Formally define the span $d$ of a discrete distribution $D$ supported on a set of integers $V = \{v_1, \dots, v_n\}$ as:
  $$d = \gcd(v_2 - v_1, v_3 - v_2, \dots, v_n - v_{n-1})$$
  Explain to the reader that the span of the sum of $R$ independent copies of $D$ is identical to the span of a single roll, which justifies why the lattice step size in the Riemann sum remains $d$ for all $R$.

### 3. Geometric Projection Interpretation of the Collision Lattice Rank
* **Critique**: While the rank of the collision lattice $L(V)$ is correctly identified as $n-2$ in Proposition 7.3, the authors do not fully connect *why* this $(n-2)$-dimensional kernel results in a 1D projection that decays as $\Theta(R^{-1/2})$ rather than $\Theta(R^{-(n-1)/2})$ (the original conjecture). The transition from the high-dimensional composition space to the 1D sum space is the core of the problem, and a geometric explanation would be highly illuminating.
* **Recommendation**: Introduce a geometric explanation of the projection:
  - The composition space lies on an $(n-1)$-dimensional simplex of size $R$, containing $\binom{R+n-1}{n-1} \approx O(R^{n-1})$ integer points.
  - The sum map $\sigma: \mathbb{R}^n \to \mathbb{R}$ acts as a 1D projection of this $(n-1)$-dimensional simplex.
  - Due to the Central Limit Theorem, the probability mass concentrates in an $(n-1)$-dimensional Gaussian ellipsoid of volume $O(R^{(n-1)/2})$.
  - Projecting this ellipsoid onto the 1D sum axis yields an interval of length $O(R^{1/2})$ containing $O(R^{1/2} / d)$ lattice sum classes.
  - Since the total probability inside the ellipsoid is close to 1, the average probability per active sum class is of order $\Theta(R^{-1/2})$, meaning the sum of squares (tie probability) must decay as $\Theta(R^{-1/2})$. This geometric "ellipsoid projection" argument makes the physics of the decay intuitive.

### 4. Generalization of the Convex Optimization Formulation
* **Critique**: In Section 5.3, the authors present a beautiful application of Large Deviations Theory and Lagrange multipliers to find the saddle-point head fractions $(x_1^*, x_2^*)$ in log-odds space for the binary case. However, a serious mathematician would ask: "Why limit this to the binary case? The same variational principle applies to any multi-valued distribution."
* **Recommendation**: Generalize the saddle-point formulation to $S$-valued distributions. Show that minimizing the joint KL divergence $\sum x_i \log(x_i / p_i)$ subject to the sum constraints yields the classical **Gibbs/Boltzmann-like distribution**:
  $$x_i^* = \frac{p_i e^{\lambda v_i}}{\sum_j p_j e^{\lambda v_j}}$$
  where $\lambda$ is the unique Lagrange multiplier that aligns the expected values of the two players. This elevates Section 5 from a specific binary trick to a powerful, general thermodynamic-probabilistic connection.

### 5. Rigorous Definition of Asymptotic Symbols
* **Critique**: The paper frequently uses $\Theta(\cdot)$, $\sim$, and $o(\cdot)$ without formally defining them. In an academic paper, even one designed for undergraduates, definitions of these symbols are necessary to maintain mathematical rigor.
* **Recommendation**: Add a brief, rigorous definition block in the **Notation Guide**:
  - $f(R) \sim g(R)$ means $\lim_{R \to \infty} \frac{f(R)}{g(R)} = 1$.
  - $f(R) = O(g(R))$ means there exist positive constants $M$ and $R_0$ such that $|f(R)| \le M |g(R)|$ for all $R \ge R_0$.
  - $f(R) = o(g(R))$ means $\lim_{R \to \infty} \frac{f(R)}{g(R)} = 0$.
  - $f(R) = \Theta(g(R))$ means $f(R) = O(g(R))$ and $g(R) = O(f(R))$.

---

## Conclusion

This is an excellent draft that is close to publication-ready. Implementing these 5 mathematical refinements will transform it from a "good undergraduate draft" into a highly polished, academically impeccable paper that any 3rd-tier or 2nd-tier mathematics journal would be proud to publish.
