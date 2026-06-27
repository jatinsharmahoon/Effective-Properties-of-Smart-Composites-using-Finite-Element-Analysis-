# Effective Properties of Smart Composites Using Finite Element Analysis

This repository contains the numerical modeling, simulation data, and validation studies for evaluating the effective mechanical properties of **Piezoelectric Fiber-Reinforced Composites (PFRCs)**. The analysis was conducted using the micromechanics approach within **ANSYS Workbench** to predict composite stiffness constants and validate numerical solutions against theoretical Strength of Materials (SM) equations.

---

## Project Overview

* **Objective:** Determine the effective elastic properties ($C_{11}^c$) of a unidirectional smart composite subjected to transverse electromechanical constraints.
* **Methodology:** Micromechanical modeling leveraging a geometric quarter-cell symmetry approach to represent a periodic material matrix structure.
* **Key Highlight:** Includes a comprehensive **Mesh Convergence Study** verifying the mathematical validity and stability of the numerical solution.
* **Validation:** Finite Element Method (FEM) experimental calculations were benchmarked against established analytical formulas, characterizing the bounds of standard micromechanical assumptions.

---

## Engineering Framework & Simulation Setup

### 1. Geometric Modeling & Symmetry
Taking advantage of the symmetrical, periodic architecture of the unidirectional composite, a **quarter-cell representation** of the square matrix and circular fiber region was modeled. This heavily optimizes computational efficiency without limiting solution accuracy.
* **Matrix Domain:** $10 \times 10\text{ units}$ square boundary.
* **Fiber Fractions Analyzed:** 40%, 60%, and 80% Area Fractions.

### 2. Material Specifications
The constituent phases consist of an active piezoelectric ceramic fiber embedded in a flexible polymer (epoxy) matrix:

| Phase | Density ($\text{kg/m}^3$) | Core Stiffness Constant ($C_{11}$) | Poisson's Ratio ($\nu$) | Piezo Stress Coefficients ($e_{33}^p$) |
| :--- | :---: | :---: | :---: | :---: |
| **Fiber (Piezo)** | $7600$ | $111\text{ GPa}$ | — | $15\text{ C/m}^2$ |
| **Matrix (Epoxy)** | $2800$ | $6.59\text{ GPa}$ | $0.3$ | $0\text{ C/m}^2$ |

### 3. Boundary Conditions & Solving (ANSYS Workbench)
The system replicates a pure mechanical load test under electric ground constraints:
1. **Symmetry Constraints:** Fixed normal displacements on left and bottom symmetry planes ($U_x = 0$ on Left; $U_y = 0$ on Bottom).
2. **Electrical Constraints:** Voltage across the system grounded to zero ($V = 0\text{V}$) to isolate structural stiffness coefficients.
3. **Mechanical Loading:** Uniform unit forces ($F_x = 1\text{N}, F_y = 1\text{N}$) applied along the top and right boundaries to generate multi-axial stress fields.

---

## Solution Convergence Study

To verify that the finite element mesh did not artificially bias the results, a rigorous mesh refinement loop was executed at a 40% area fraction:

* **X-Stress Convergence:** As the element size was reduced down to $0.25\text{ units}$, the average normal stress stabilized securely at $\approx 1.05$, showing an ultimate variation of under 4%.
* **Displacement Convergence:** Peak displacement tracked at the critical top-right corner plateaued tightly at $6.7 \times 10^{-10}\text{ m}$ (with a marginal variation of only 0.6%), confirming complete mathematical convergence.

---

## Representative Mathematical Formula

The effective composite stiffness matrix ($C^{\text{comp}}$) was derived directly from the computed average nodal stress ($\sigma^{\text{av}}$) and strain ($\varepsilon^{\text{av}}$) fields using:

$$C^{\text{comp}} = [\sigma^{\text{av}}] [\varepsilon^{\text{av}}]^{-1}$$

Where the structural tensors are resolved from localized planar components:

$$[\sigma^{\text{av}}] = \begin{bmatrix} \sigma_x^{\text{av}} & \sigma_{xy}^{\text{av}} \\ \sigma_{xy}^{\text{av}} & \sigma_y^{\text{av}} \end{bmatrix}, \quad [\varepsilon^{\text{av}}] = \begin{bmatrix} \varepsilon_x^{\text{av}} & \varepsilon_{xy}^{\text{av}} \\ \varepsilon_{xy}^{\text{av}} & \varepsilon_{y}^{\text{av}} \end{bmatrix}$$

---

## Major Key Results

### 1. Nodal Field Profiles (40% Area Fraction)
* **Stress Distributions:** Normal stresses ($\sigma_x, \sigma_y$) decrease predictably moving away from the loaded boundaries toward the fixed symmetry edges. The load transfer is highly uniform inside the stiffer ceramic fiber region compared to the compliant epoxy matrix.
* **Shear Profile:** The shear stress distribution shows precise diagonal symmetry stretching from the bottom-left vertex to the top-right corner.

### 2. Analytical vs. Numerical Comparison
Evaluating the primary composite stiffness coefficient ($C_{11}^c$) at a 40% fiber fraction reveals a distinct variance between standard analytical approximations and full continuum FEA models:
* **Theoretical Model (Strength of Materials approach):** $38.72\text{ GPa}$
* **Numerical Model (ANSYS Workbench FEA):** $29.92\text{ GPa}$
* **Discrepancy Variance:** $\approx 29\%$

> **Engineering Takeaway:** The variation underlines the critical limitation of simplified 1D Strength of Materials assumptions when applied to complex multi-axial smart composites. This validates the absolute necessity of rigorous 3D continuum FEA modeling to capture localized geometric constraints and phase mismatch effects accurately.

---

## Proposed Future Work
1. **Active Voltage Application:** Introduce electric potential loops ($V \neq 0$) to model the inverse piezoelectric effect and map active sensor/actuator strain profiles.
2. **3D Microstructural Scaling:** Expand the current 2D planar analysis into true 3D Representative Volume Elements (RVEs) to extract transversal shear properties.
3. **Multifunctional Design Optimization:** Implement parameter optimization tracking to map fiber volume fraction curves relative to localized mechanical fatigue limits.

---

## References & Supervision
* **Supervised by:** Dr. Nilanjan Malik, Department of Mechanical Engineering, Indian Institute of Technology (BHU) Varanasi.
* Analytical methods based on foundational micromechanical frameworks established by *Mallik & Ray (2003)*.
