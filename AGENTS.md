# AGENTS.md

This repository is being audited only as a reference for building a MATLAB research-code implementation of the Material Point Method for geotechnical liquefaction modelling.

Do not modify source code unless explicitly requested.

The audit should focus on:

1. MPM time-integration pipeline;
2. P2G and G2P mapping;
3. velocity gradient, strain-rate tensor D, spin tensor W, and objective stress-rate treatment;
4. stress update and material model interface;
5. storage of particle-level history variables;
6. effective stress, total stress, pore pressure, and u-p coupling if available;
7. whether the architecture can support a Liao-type cyclic liquefaction constitutive model with internal variables delta, z, ell, Se, void ratio e, and effective stress;
8. which design ideas should be transferred to a MATLAB research-code implementation.

Do not translate the whole repository into MATLAB.

Avoid broad software-engineering comments unless they directly affect MPM, constitutive modelling, u-p coupling, history variables, or MATLAB reimplementation.

The expected output is an audit report with file paths, function/class names, data flow, and recommendations.
