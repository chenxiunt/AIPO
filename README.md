# README 

Paper title: **Interpolation-Based Optimization for Enforcing ℓp-Norm Metric Differential Privacy in Continuous and Fine-Grained Domains**

Artifacts HotCRP Id: **92**

Requested Badge: **Artifacts Available**, **Artifacts Evaluated**, and **Results Reproduced**

## Description
This repository contains the source code related to the methodologies and experiments presented in the paper titled **"Interpolation-Based Optimization for Enforcing ℓp-Norm Metric Differential Privacy in Continuous and Fine-Grained Domains"**. 

The file **`main_2norm.m`** implements the **AIPO** algorithm (*Anchor-Interpolated Privacy Optimization*) proposed in the paper. 
### Directory Structure
PAnDA artifact/
* README.md 

* paper.pdf 

* main.m 

* main_appendix.m 

* parameters.m 

* functions/ 

* datasets/ 

* intermediate/ 

* results/ 

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
### Main Results and Claims
#### Main Result 1: Computation time (displayed in Table 2 and Table 3)
*PAnDA-e*, *PAnDA-p*, and *PAnDA-l* have higher computational time compared to *Exponential Mechanism (EM)* and *Bayesian Remapping (EM+BR)*, it outperforms optimization-based methods including *Linear Programming (LP)*, *Coarse Approximation of LP (LP+CA)*, *Benders Decomposition (LP+BD)*, and *ConstOPTMech (LP+EM)* in terms of *computation efficiency* (described in Section **4.3.1**). 

#### Main Result 2: Utility loss (displayed in Table 4 and Table 5)
*PAnDA-e*, *PAnDA-p*, and *PAnDA-l* achieve lower *utility loss* compared to *EM*, *LP+CA*, and *EM+BR* (described in the first paragraph of **Section 4.3.2**). 

### Experiments 

The file **`main.m`** provides entry points for running experiments on different datasets.  
To select a dataset, **uncomment the corresponding line**:

```matlab
% run_artifact_rome;               % Rome dataset (uniform vehicle distribution)
% run_artifact_nyc;                % New York City dataset (uniform vehicle distribution)
% run_artifact_london;             % London dataset (uniform vehicle distribution)
% run_artifact_real_distribution;  % Rome dataset (real vehicle distribution)
```
The estimated running time for each **`run_artifact_rome.m`**, **`run_artifact_nyc.m`**, **`run_artifact_london.m`**, and **`run_artifact_real_distribution.m`** is approximated one hour. 

**Configuring Repeats**: You can specify the number of experiment repetitions by setting the corresponding repeat parameter in **`main.m`**: 

```matlab
NR_REPEAT = 1; 
```

**Program Workflow**: When executed, the program will (1) load the dataset from the *dataset/* directory, (2) use functions routines from the *functions/* directory, and (3) apply parameters defined in *parameters.m*.

After completion, the program will display the experimental results (e.g., console outputs and/or generated figures/tables, depending on the selected experiment).

Note that, when running **`run_artifact_rome.m`**, **`run_artifact_nyc.m`**, **`run_artifact_london.m`**, or **`run_artifact_real_distribution.m`**, the methods *PAnDA-e*, *PAnDA-p*, *PAnDA-l*, *EM*, *EM+BR*, *LP+CA*, and *LP* are executed automatically. Because LP+EM and LP+BD incur much higher computation time and fail to return results when the number of records is ≥ 1,000, they must be run separately using **`run_LPEM.m`** and **`run_LPBD.m`** or **uncomment the corresponding lines** in **`main.m`**: 

```matlab
% run_LPEM
* run_LPBD
```
To adjust the number of  records for LP+EM or LP+BD, modify the parameter *env_parameters.NR_NODE_IN_TARGET* defined on line~8 in  **`run_LPEM.m`** and **`run_LPBD.m`**

```matlab
env_parameters.NR_NODE_IN_TARGET = 500;    % The number records is 500
```

#### 1. Utility loss of different algorithms 
an example table: 

**rome road map**

| Method                          | \(\epsilon=\)0.2       | $\epsilon=$0.4       | $\epsilon=$0.6       | $\epsilon=$0.8       | $\epsilon=$1.0       | $\epsilon=$1.2       | $\epsilon=$1.4       | $\epsilon=$1.6       |
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


This result support **Main result 2 (displayed in Table 4 and Table 5 in the paper)**: *PAnDA-e, PAnDA-p, and PAnDA-l achieve lower utility loss compared to EM, LP+CA, and EM+BR*. 

The exact utility loss values are **hard to reproduce**, since both location set and users are randomly distributed, leading to variation across runs. However, the overall trend remains consistent: *PAnDA-e, PAnDA-p, and PAnDA-l achieve lower utility loss compared to EM, LP+CA, and EM+BR*, as reported in the paper.


#### 2. Computation time of different algorithms 
An example table: 

| Method                          | $\epsilon=$0.2       | $\epsilon=$0.4       | $\epsilon=$0.6       | $\epsilon=$0.8       | $\epsilon=$1.0       | $\epsilon=$1.2       | $\epsilon=$1.4       | $\epsilon=$1.6       |
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


This result support **Main result 1 (displayed in Table 2 and Table 3 in the paper)**: *"PAnDA-e, PAnDA-p, and PAnDA-l have higher computational time compared to EM and EM+BR, it outperforms optimization-based methods including LP, LP+CA, LP+BD, and LP+EM in terms of computation efficiency"*. 

We would like to clarify that the exact computation times are **hard to reproduce** because they depend on factors beyond our control, such as hardware configuration, concurrent system load, operating system scheduling, library implementations, and randomness in the algorithm. As a result, while the relative trends (e.g., scalability across datasets and methods) are consistent and reproducible, the absolute runtime values may vary across environments. 

For instance, relative to EM+BR, our PAnDA variants (PAnDA-e/p/I) are competitive and, for larger k, can be faster; the crossover depends on problem size, environment, and random seed. While PAnDA runtimes are generally <1 s, given certain random seeds we occasionally see slow LP convergence that produces ~12 s outliers, which can raise the average in some runs.


