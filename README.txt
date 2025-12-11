README: AIPO (Anchor-Interpolated Privacy Optimization) - MATLAB Implementation
-------------------------------------------------------------------------------

This supplementary material contains the MATLAB implementation of the AIPO framework
proposed in our NeurIPS 2025 submission. AIPO enforces ℓₚ-norm Metric Differential Privacy (mDP)
in continuous or fine-grained domains by optimizing perturbation distributions at a set of
anchor points, followed by dimension-wise log-convex interpolation to extend them across the domain.

-------------------------------------------------------------------------------
Directory Structure
-------------------------------------------------------------------------------

- main_1norm.m  
  Reproduces experiments under the ℓ₂ utility metric (Tables 8–10).  
  Estimated runtime: ~37 hours

- main_2norm.m  
  Reproduces experiments under the ℓ₁ utility metric (Tables 2–4， Figures 8–10).  
  Estimated runtime: ~36 hours

- main_granularity.m  
  Analyzes the impact of grid granularity (Figure 14).  
  Estimated runtime: ~15 hours

- main_ablation_privacybudget.m  
  Studies privacy budget allocation strategies (Table 7, Figures 11–13).  
  Estimated runtime: ~7.5 hours

-------------------------------------------------------------------------------
Requirements
-------------------------------------------------------------------------------

- MATLAB R2022a or later
- Optimization Toolbox

-------------------------------------------------------------------------------
How to Run
-------------------------------------------------------------------------------

1. Open MATLAB and set the working directory to the project root.

2. Run any of the provided scripts. For example:
       >> main_1norm
       >> main_2norm
       >> main_granularity
       >> main_ablation_privacybudget

3. Output files will be saved to the "./results/" directory. Results include:
   - Utility loss
   - mDP violation
   - Perturbation probability ratio (PPR)
   - Runtime metrics

   Output is provided for three datasets: Rome, London, and New York City.

   Example output structure:
   - main_1norm.m:
     ./results/1norm/cost/  
     ./results/1norm/violation/  
     ./results/1norm/time/  
     ./results/1norm/ppr/  

   - main_2norm.m:
     ./results/2norm/cost/  
     ./results/2norm/violation/  
     ./results/2norm/time/  
     ./results/2norm/ppr/  

   - main_granularity.m:
     ./results/granularity/cost/  
     ./results/granularity/violation/  
     ./results/granularity/time/  
     ./results/granularity/ppr/  

   - main_ablation_privacybudget.m:
     ./results/ablation_privacybudget/cost/  
     ./results/ablation_privacybudget/violation/  
     ./results/ablation_privacybudget/time/  
     ./results/ablation_privacybudget/ppr/  

-------------------------------------------------------------------------------
File Naming Convention
-------------------------------------------------------------------------------

Each output file is named as:

    xxxx_yyyy

Where:
- `xxxx` is the performance metric:
    - `loss`: Utility loss
    - `violation`: mDP violation ratio (%)
    - `time`: Running time (seconds)
    - `ppr`: Perturbation probability ratio

- `yyyy` is the algorithm identifier:
    - `em`: Exponential mechanism
    - `laplace`: Laplacian noise
    - `tem`: Truncated exponential mechanism
    - `copt`: COPT
    - `lp`: Linear programming
    - `aipo`: AIPO
    - `aipor`: AIPO (relaxed version)
    - `aipoe`: AIPO with equal privacy budgets across dimensions
    - `bound`: Lower bound

-------------------------------------------------------------------------------
Summary of Reproducible Results
-------------------------------------------------------------------------------

| Tables / Figures         | Script                          | Estimated Runtime |
|--------------------------|---------------------------------|-------------------|
| Tables 8–10		   | main_1norm.m                    | ~37 hours         |
| Tables 2–4, Figures 8–10 | main_2norm.m                    | ~36 hours         |
| Figure 14                | main_granularity.m              | ~15 hours         |
| Table 7, Figures 11–13   | main_ablation_privacybudget.m   | ~7.5 hours        |

Each script performs the following steps:
- Solves the Approx-APO optimization problem via linear programming
- Applies dimension-wise log-convex interpolation
- Computes utility loss, mDP violation, runtime, and PPR

-------------------------------------------------------------------------------
Additional Directories
-------------------------------------------------------------------------------

- ./datasets/  
  Contains the road network data (nodes and edges) for Rome, London, and New York City.

- ./functions/  
  Includes utility, optimization, and support functions used in all experiments.

- ./intermediate/  
  Stores cached intermediate results to avoid redundant computations and improve efficiency.


