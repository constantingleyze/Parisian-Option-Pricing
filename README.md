# Parisian Option Pricing

This repository provides a theoretical and computational study of **Parisian options**, a class of path-dependent barrier options whose payoff depends not only on whether a barrier is breached, but **for how long** the asset remains beyond that barrier.

In particular, we focus on the implementation of a pricing method based on **Laplace transforms**, which enables fast and accurate valuation of these complex derivatives. This approach is rooted in a seminal paper using explicit Laplace expressions and controlled numerical inversion.

> **Reference paper:**  
> Labart, C., & Lelong, J. (2009). *Pricing Parisian options using Laplace transforms*. *Bankers, Markets & Investors*, 99, 24p.

## Content

The project follows a structured progression:

- **Introduction**: We start by defining Parisian options and placing them in the context of financial derivatives. We detail the eight standard types of Parisian options (e.g., PUIC, PDIC, PUOC, etc.) and introduce key pricing relationships, including **in–out parity** and **inversion identities**.

- **Laplace Transform Method**: The core of the project is the implementation of the pricing method developed by Labart and Lelong (2009), which leverages Laplace transforms to derive fast and accurate formulas. We explain the mathematical principles, derive closed-form expressions, and describe the numerical inversion process based on accelerated Euler summation.
  
- **Monte Carlo Methods**: We then present two simulation-based alternatives to the Laplace method:

  1. A **naive Monte Carlo** approach, which estimates option prices by discretely simulating asset paths and checking whether the barrier condition holds for the required duration.

  2. A **Brownian Bridge Monte Carlo** method, which corrects for the discretization bias of the naive approach by analytically modeling the behavior of the process between simulation points.


For each of these methods, we first explain the theoretical and mathematical foundations. We then describe their practical implementation, detailing the simulation procedures, path tracking mechanisms, and payoff evaluations.

To enhance the quality of the Monte Carlo estimates, we further incorporate an **adaptive antithetic variance reduction** technique. The method is first introduced from a theoretical standpoint, and we then detail its practical implementation on top of both the naive and Brownian Bridge Monte Carlo simulations.

- **Results Analysis**:  
We conclude the project with a structured evaluation of the pricing methods across three key dimensions:

  1. **Bias**: We begin by analyzing the intrinsic bias of each estimator. As expected, the naive Monte Carlo method exhibits a structural discretization bias of order O(sqrt(Δt)), which remains even as the number of paths increases. The Brownian Bridge estimator corrects this     bias significantly, and the Laplace transform method, being analytical, is unbiased by construction.

  2. **Variance**: We then compare the raw variance of each method. The naive Monte Carlo estimator exhibits high variance, especially for options with low activation probabilities. The Brownian Bridge method achieves lower variance by more accurately capturing barrier excursions. When combined with     adaptive antithetic variance reduction, both Monte Carlo methods experience dramatic reductions in variance — ranging from factors of 10⁴ to 10⁶—while the Laplace method, being deterministic, has no variance by construction.

  3. **Speed and Practical Efficiency**: Finally, we assess the computational cost of each method. The Laplace transform approach is nearly instantaneous (sub-second execution), whereas the naive and Brownian Bridge simulations require between 16 and 30 seconds to generate 1 million trajectories with    500 discretization steps, depending on the setup. The additional cost introduced by variance reduction remains modest and is well justified by the significant gains in estimator precision.

**Implementation Details**:  
All implementation decisions—including algorithmic design and optimization techniques—are documented in the **Appendix**. This includes justifications for performance-related choices made in our code.

**Visual Outputs**:  
We also provide **screenshots of selected results**, including pricing tables and graphical comparisons, to give a quick visual overview of each method’s behavior under different configurations.

**Interactive Notebook**:  
The full project is available as a **Python Jupyter notebook** within the repository. This allows readers to easily reproduce our simulations, explore parameter variations, and consult the implemented algorithms in a clear, executable format.

## Possible Extensions

We suggest several directions for future exploration:

- Parisian options under stochastic volatility or jump models  
- Early exercise via PDE or free-boundary approaches  
- Exact Brownian Bridge formulations with closed-form variance-reduced estimators  
- Machine learning-based pricing benchmarks

These extensions aim to enhance the practical relevance and generality of Parisian pricing frameworks.
