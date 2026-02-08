# MATH5030 HW1 – Implied Yield via Root-Finding

This project studies numerical methods for computing the implied yield (YTM) of a stream of cashflows. The problem is formulated as a nonlinear root-finding problem and solved using several Newton-type methods, with Brent’s method used as a benchmark.

Author: Nigel Li (nl2992)

---

## Background

Given cashflows `c_k` paid at times `t_k`, the present value at yield `r` is

P(r) = sum_k c_k / (1 + r)^(t_k)

Given a market price `p`, the implied yield satisfies

P(r) = p

or equivalently

f(r) = P(r) - p = 0

Finding the implied yield is therefore a numerical root-finding problem.

---

## Methods Implemented

### Benchmark
- Brent’s method (`scipy.optimize.brentq`) with bracket `[0, 20]`

### SciPy Methods
- Secant method (`optimize.newton` with `x0`, `x1`)
- Newton’s method with derivative (`optimize.newton` with `fprime`)

### Optimized Newton Methods
- Fused Newton  
  Computes `f` and `f'` together in one loop to avoid repeated discount calculations.

- Hybrid Bracketed Newton  
  Uses Newton steps when safe and falls back to bisection when needed.

- Secant with Improved Starting Values  
  Uses multiple scale-aware initial guesses to improve convergence.

---

## Overview of Results

All methods were tested on the same 1000 randomly generated cashflow cases.

- Brent’s method is robust and reliable.
- Standard SciPy Newton and secant methods are slower due to repeated function evaluations.
- The fused Newton method is the fastest in most cases.
- The hybrid Newton method is more robust but slightly slower.
- Improved-start secant is reliable but the slowest overall.

Overall, computing `f` and `f'` together provides the largest performance improvement.

---

## Project Structure

MATH5030_HW1/
│
├── environment.yml
├── HW1_Root_Finding.ipynb
└── README.md

---

## Setup Instructions

### 1. Create the Conda Environment

conda env create -f environment.yml

### 2. Activate the Environment

conda activate math5030

### 3. Launch Jupyter

jupyter notebook

or

jupyter lab

Open: HW1_Root_Finding.ipynb

---

## Reproducibility

- All experiments use a fixed random seed.
- Run the notebook from top to bottom.
- Accuracy tolerance is set to 1e-8.

---