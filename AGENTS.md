# AGENTS.md

This repository is being audited only as a reference for rebuilding a clean MATLAB minimal production MPM host for geotechnical liquefaction modelling.

Do not modify source code unless explicitly requested.

Do not implement the Liao model at this stage.

Do not translate this repository line by line into MATLAB.

## Current project context

The previous self-developed MATLAB MPM framework did not fail primarily because of the Liao constitutive kernel. It failed when the Liao kernel was placed into a slope driver, where geostatic equilibrium, force balance, internal-force assembly, low-mass node handling, and boundary/runout treatment were not sufficiently reliable.

Therefore, the immediate audit priority is the MPM "vehicle", not the liquefaction "engine".

## Audit focus

The audit should focus on:

1. main MPM time-integration pipeline;
2. P2G and G2P mapping;
3. particle and grid/node data structures;
4. velocity gradient, strain-rate tensor D, spin tensor W, and objective stress-rate treatment;
5. stress update sequence and whether stress is updated before/after grid solve;
6. internal force assembly and sign convention;
7. body force and gravity treatment;
8. geostatic stress initialisation and gravity equilibrium strategy;
9. manufactured stress equilibrium or equivalent force-balance tests;
10. low-mass node filtering or stabilisation;
11. boundary conditions, base shaking, free surface, contact, and runout treatment;
12. material model interface;
13. storage of particle-level scalar and tensor history variables;
14. effective stress, total stress, pore pressure, and u-p coupling if available;
15. which design ideas should be transferred to a MATLAB minimal production MPM host.

## Native material pressure-test focus

In addition to auditing the MPM vehicle, also audit existing native constitutive models that can be used to de-risk the MATLAB clean-host rebuild before the Liao model is migrated.

Focus on existing materials only. Do not implement new materials.

Prioritise:

1. Elastic material:
   - for P2G/G2P, internal-force, body-force, gravity and geostatic validation.

2. Mohr-Coulomb or Drucker-Prager if available:
   - for dry slope smoke, simple plastic slope, shear localisation, boundary and runout checks.

3. Modified Cam Clay or other stateful geomechanics material if available:
   - for material-state persistence, hardening-variable storage, effective-stress logic and history-variable management.

4. Existing two-phase, u-p, pore-pressure or undrained examples if available:
   - for u → sigma' → internal-force handoff checks.

The audit should identify which existing native models are useful for MATLAB validation Gates B-E before migrating the Liao kernel.

The goal is to use native materials as chassis and interface pressure tests, not as replacements for the Liao model.

Do not over-expand into a full constitutive-model survey. Only extract the models that help de-risk:
- force balance;
- geostatic equilibrium;
- boundary/runout;
- material update sequence;
- state-variable persistence;
- effective-stress handoff.

## Liao model context for later stages

The future MATLAB host should eventually support a Liao-type cyclic liquefaction constitutive model with particle-level variables:

- delta: intergranular strain tensor;
- z: fabric or loading-history tensor;
- ell: semifluidized-state scalar variable;
- Se: degradation / semifluidisation factor;
- void ratio e;
- pore pressure u if available;
- effective stress tensor.

However, do not implement this model during the audit. Only evaluate whether the architecture can support such variables later.

## Expected output

The expected output is an audit report with:

- file paths;
- function/class names;
- minimal call graph;
- data-flow description;
- stress/sign/unit convention notes;
- force-balance and geostatic-equilibrium design notes;
- boundary/runout design notes;
- material-interface design notes;
- recommendations for a MATLAB reimplementation;
- explicit warnings about what should NOT be copied into MATLAB.

Avoid broad software-engineering comments unless they directly affect MPM, constitutive modelling, force balance, geostatic initialisation, boundary/runout treatment, u-p coupling, or MATLAB reimplementation.
