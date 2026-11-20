# liquid-rocket-combustion-kerosene-h2o2
# OpenFOAM Combustion Simulation: Initial Startup Configuration (`fvSchemes`)

This repository documents the numerical discretization schemes (`fvSchemes`) optimized for the startup phase of a reactive flow and liquid rocket combustion case using **OpenFOAM (v2312)**.

## Numerical Strategy & Design Choices
* **Solver Stability:** Employs bounded first-order convection schemes (`upwind`) during the initial startup phase. This prevents non-physical negative species mass fractions or enthalpy spikes caused by cold-flow mixing and ignition transients.
* **Temporal Discretization:** Uses a robust first-order implicit Euler scheme (`default Euler`) for temporal terms.
* **Gradient & Laplacian Schemes:** Second-order `Gauss linear` for gradients and limited corrected schemes (`limited corrected 0.5`) for Laplacian and surface normal gradients to maintain accuracy and boundedness on complex meshes.

## File Overview (`system/fvSchemes`)
* `ddtSchemes`: First-order implicit Euler integration.
* `gradSchemes`: Standard `Gauss linear` for velocity, pressure, temperature, and turbulence kinetic energy.
* `divSchemes`: Bounded `Gauss upwind` applied to convective terms, momentum ($\phi, U$), energy ($\phi, h$), turbulence ($k$), and key chemical species ($\text{O}_2, \text{H}_2\text{O}, \text{C}_{12}\text{H}_{26}, \text{CO}_2$) to ensure numerical stability during initial ignition.
* `laplacianSchemes`: Bounded second-order diffusion terms with non-orthogonal correctors.

## Requirements
* **OpenFOAM v2312** (or compatible modern version)
<img width="892" height="525" alt="Screenshot 2026-06-05 114031" src="https://github.com/user-attachments/assets/fc8c1163-af4b-45db-8618-ba5a3cff2c4d" />
<img width="1145" height="677" alt="Screenshot 2026-05-27 172927" src="https://github.com/user-attachments/assets/32ae57e9-afa9-4a5e-8c51-4cbb5c52202d" />
<img width="1087" height="412" alt="Screenshot 2026-06-06 102743" src="https://github.com/user-attachments/assets/87348706-6c1a-42a6-93fe-05d7cf6c67d2" />

