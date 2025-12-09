# README 

Paper title: **Interpolation-Based Optimization for Enforcing ℓp-Norm Metric Differential Privacy in Continuous and Fine-Grained Domains**


## Description
This repository contains the source code related to the methodologies and experiments presented in the paper titled **"Interpolation-Based Optimization for Enforcing ℓp-Norm Metric Differential Privacy in Continuous and Fine-Grained Domains"**. 

The file **`main_2norm.m`** implements the **AIPO** algorithm (*Anchor-Interpolated Privacy Optimization*) proposed in the paper. 
### Directory Structure
AIPO artifact/
* `README.md`: Describes the artifact and explains how to reproduce the main experimental results.  
* `paper.pdf`: PDF of the paper *“Interpolation-Based Optimization for Enforcing ℓp-Norm Metric Differential Privacy in Continuous and Fine-Grained Domains”*.  
* `main_2norm.m`: Reproduces experiments under the ℓ₂ utility metric, including Tables 2–4 and Figures 8–10.  
* `main_1norm_appendix.m`: Reproduces experiments under the ℓ₁ utility metric, including Tables 8–10.  
* `main_granularity_appendix.m`: Evaluates the effect of grid granularity (Figure 14).  
* `main_ablation_budget_appendix.m`: Studies the impact of privacy-budget allocation strategies, reproducing Table 7 and Figures 11–13.  
* `parameters.m`: Specifies the parameter settings used in the experiments.  
* `functions/`: Folder containing helper and core function implementations.  
* `datasets/`: Folder containing the road-map datasets.  
* `intermediate/`: Folder containing intermediate results (utility loss matrices) that are expensive to recompute.
* `results/`:  Forder containing the experimental results. 


### Security/Privacy Issues and Ethical Concerns
There are no security or ethical concerns.

## Basic Requirements
### **Recommended Hardware Requirements**
- **Processor**: Dual-core CPU or higher
- **Memory**: 64 GB RAM (16 GB recommended for larger datasets)
- **Disk Space**: 2 GB of free space for MATLAB installation and artifact files

### **Supported Operating Systems**
- **Windows 10/11**
- **macOS Monterey/Ventura**
- **Ubuntu Linux 20.04/22.04**

## Environment 

### Set up the environment
The code was developed and tested using **MATLAB R2024b** with the **Optimization Toolbox**, **Symbolic Math Toolbox**, and **Statistics and Machine Learning Toolbox** installed. The toolboxes include the [**`linprog`**](https://www.mathworks.com/help/optim/ug/linprog.html) function for linear programming and the [**`randsample`**](https://www.mathworks.com/help/stats/randsample.html) function for random sample.


## Artifact Evaluation

### Experiments 

* First, set the working directory in MATLAB to the root folder containing the provided scripts.
* Run the desired script (e.g., `main_2norm.m`, `main_1norm_appendix.m`, `main_granularity_appendix.m`, or `main_ablation_budget_appendix.m`) to generate the corresponding tables and figures.
* Output files (e.g., mDP violation ratio, utiliy loss, and runtime of different methods) will be saved in the following directories:
   * `./results/1norm_appendix/`: Output of `main_1norm.m`, including utility loss, mDP violation ratio, PPR, and runtime of all compared methods across the three datasets.
   * `./results/2norm/`: Output of `main_2norm.m`, including utility loss, mDP violation ratio, PPR, and runtime of all compared methods across the three datasets.
   * `./results/granularity_appendix/`: Output of `main_granularity.m`, including utility loss, runtime, and the number of anchors used in AIPO.
   * `./results/ablation_budget_appendix/`: Output of `main_ablation_budget_appendix.m`, including the utility loss of AIPO with and without privacy budget optimization.

**Configuring Repeats**: You can specify the number of experiment repetitions by setting the corresponding repeat parameter in **`parameters.m`**: 

```matlab
NR_TEST = 1; 
```

**Program Workflow**: When executed, the program (1) loads datasets from the `datasets/` directory, (2) calls function routines in the `functions/` directory, and (3) applies the parameters defined in `parameters.m`.

After completion, the program saves the experimental results to the appropriate subfolders in `results/`. For the main script `main_2norm.m`, the corresponding results are also displayed on screen.


### Main Results and Claims
#### Main Result 1: metric differential privacy violation ratio (displayed in Table 2)
***Key observations***: *AIPO* and *Pre-defined Noise Distribution mechanisms (e.g., Laplace, EM, TEM)* attain **0% violations** across all datasets and budgets. In contrast, LP and COPT exhibit nonzero violation ratios. The relaxed variant, AIPO-R, exhibits higher violation ratios. 

An example table produced by running **`main_2norm.m`** is shown below, which supports **Main result 1 (displayed in Table 2)**. 

**Rome Road Map - mDP Violation Ratio**

| Method                          |ε=0.2       |ε=0.4       |ε=0.6       |ε=0.8       |ε=1.0       |ε=1.2       |ε=1.4       |ε=1.6       |
|---------------------------------|---------------|---------------|---------------|---------------|---------------|---------------|---------------|---------------|
| **Pre-defined Noise Distribution:** |               |               |               |               |               |               |               |               |
| EM                              | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   |
| Laplace                         | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   |
| TEM                             | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   |
| **Hybrid Method:**              |               |               |               |               |               |               |               |               |
| RMP                             | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   |
| COPT                            | 3.505±0.000   | 9.040±0.000   | 3.569±0.000   | 3.343±0.000   | 3.159±0.000   | 2.985±0.000   | 2.756±0.000   | 2.594±0.000   |
| LP                              | 2.169±0.000   | 2.276±0.000   | 2.048±0.000   | 1.860±0.000   | 1.726±0.000   | 1.220±0.000   | 1.124±0.000   | 0.861±0.000   |
| AIPO-R                          | 8.928±0.000   | 7.399±0.000   | 4.982±0.000   | 3.352±0.000   | 2.138±0.000   | 1.288±0.000   | 0.924±0.000   | 0.597±0.000   |
| AIPO*                           | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   | 0.000±0.000   |





#### Main Result 2: Utility loss (displayed in Table 3)
Across all three datasets, AIPO consistently achieves lower utility loss than all baselines. Compared to pre-defined noise distributions (EM, Laplace, TEM), AIPO reduces utility loss by roughly 60% on average, replacing global/isotropic perturbations—which ignore geometry and direction-dependent sensitivity and thus tend to over-perturb dense regions and under-protect sparse ones—with anchor-based optimization and log-convex interpolation that align smoothly with the metric structure. Relative to hybrid methods, AIPO attains around 60% lower average utility loss than COPT, whose rigid LP formulation scales poorly in high-resolution domains, and around 10% lower loss than RMP, whose posterior reshaping remains fundamentally limited by the quality of its initial pre-defined noise. In contrast, AIPO directly optimizes perturbation probabilities under \((\epsilon, d_p)\)-mDP constraints without relying on a fixed base mechanism. Compared to LP, AIPO sacrifices some utility—LP can achieve lower loss by optimizing directly over distance-based constraints—but LP only enforces mDP on a discrete grid and can violate \((\epsilon, d_p)\)-mDP off-grid in the continuous domain. Relative to the universal lower bound (LB) from Proposition 5, AIPO’s empirical utility is typically within a


An example table produced by running **`main_2norm.m`** is shown below, which supports **Main result 2 (displayed in Table 3)**. 

**Rome Road Map - Utility Loss**

| Method                          | ε=0.2       |ε=0.4       |ε=0.6       |ε=0.8       |ε=1.0       |ε=1.2       |ε=1.4       |ε=1.6       |
|---------------------------------|-------------|-------------|-------------|-------------|-------------|-------------|-------------|-------------|
| **Pre-defined Noise Distribution:** |             |             |             |             |             |             |             |             |
| EM                              | 8.62±0.00   | 8.52±0.00   | 8.50±0.00   | 8.55±0.00   | 8.64±0.00   | 8.74±0.00   | 8.84±0.00   | 8.93±0.00   |
| Laplace                         | 8.62±0.00   | 8.52±0.00   | 8.50±0.00   | 8.55±0.00   | 8.64±0.00   | 8.74±0.00   | 8.84±0.00   | 8.93±0.00   |
| TEM                             | 8.59±0.00   | 8.59±0.00   | 8.59±0.00   | 8.59±0.00   | 8.59±0.00   | 8.59±0.00   | 8.59±0.00   | 8.59±0.00   |
| **Hybrid Method:**              |             |             |             |             |             |             |             |             |
| RMP                             | 6.02±0.00   | 5.07±0.00   | 4.35±0.00   | 3.88±0.00   | 3.57±0.00   | 3.37±0.00   | 3.23±0.00   | 3.14±0.00   |
| COPT                            | 7.67±0.00   | 11.79±0.00  | 8.71±0.00   | 8.87±0.00   | 8.98±0.00   | 9.06±0.00   | 9.11±0.00   | 9.14±0.00   |
| LP                              | 4.89±0.00   | 3.18±0.00   | 2.56±0.00   | 2.27±0.00   | 2.12±0.00   | 2.03±0.00   | 1.98±0.00   | 1.96±0.00   |
| AIPO-R                          | 3.93±0.00   | 2.99±0.00   | 2.62±0.00   | 2.46±0.00   | 2.36±0.00   | 2.32±0.00   | 2.29±0.00   | 2.27±0.00   |
| LB                              | 0.00±0.00   |             |             |             |             |             |             |             |
| AIPO*                           | 5.64±0.00   | 4.56±0.00   | 3.90±0.00   | 3.47±0.00   | 3.18±0.00   | 2.96±0.00   | 2.82±0.00   | 2.71±0.00   |




#### Main Result 3: Computation time (displayed in Table 4)

We would like to clarify that the exact computation times are **difficult to reproduce**, as they depend on factors beyond our control, including hardware configuration, concurrent system load, operating system scheduling, library implementations, and algorithmic randomness. As a result, while the relative ordering of runtimes for LP, COPT, and AIPO (on average LP > COPT > AIPO) is consistent and reproducible, the absolute runtime values may vary across environments.

An example table produced by running **`main_2norm.m`** is shown below, which supports **Main result 3 (displayed in Table 4)**. 


**Rome Road Map - Computation Time (sec)**

| Method | ε = 0.2      | ε = 0.4      | ε = 0.6      | ε = 0.8      | ε = 1.0      | ε = 1.2      | ε = 1.4      | ε = 1.6      |
|--------|--------------|--------------|--------------|--------------|--------------|--------------|--------------|--------------|
| COPT   | 157.373±0.000 | 157.770±0.000 | 170.102±0.000 | 157.598±0.000 | 159.141±0.000 | 164.475±0.000 | 158.304±0.000 | 178.042±0.000 |
| LP     | 266.852±0.000 | 53.865±0.000  | 889.372±0.000 | 266.866±0.000 | 253.014±0.000 | 176.692±0.000 | 185.082±0.000 | 154.150±0.000 |
| AIPO*  | 18.083±0.000  | 18.153±0.000  | 18.337±0.000  | 15.869±0.000  | 15.817±0.000  | 15.718±0.000  | 14.780±0.000  | 16.750±0.000  |






















