# README
---
This vault stores a series of OpenFOAM cases with the release by [openfoam.org](openfoam.org) and 13+ version

## Backward Facing Step

- A typical cases to test for shock waves and expansion waves and other complex supersonic flow conditions
- Use rhoPimpleFoam, but the newest release has delete such solver.
- Instead, its equivalent configuration is to take the `fluid` solver such that the fluid is rho-based, and take the Pimple solver for turbulence flow
- There is an **error** case misused with incompressible fluid solver, the case works when the velocity flipped to z-direction, while the result has lost its true nature

> The coordinate is right-handed and standard, flipping is unneeded.
