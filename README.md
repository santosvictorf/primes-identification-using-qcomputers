# Prime Identification via Entanglement Dynamics on IBM Quantum Processors

This repository contains the code and data associated with the manuscript:

**Prime Number Identification Demonstrated with Quantum Processors Using a New Rescaling-Based Noise Mitigation Technique**

The work implements the PIED algorithm (Prime Identification via Entanglement Dynamics) on IBM Quantum processors and analyzes the extraction of number-theoretic information from the Fourier spectrum of the reduced purity of a bipartite quantum system. The repository also contains the data-analysis routines used to apply and test the CFE (Correction Factor Extrapolation) noise-mitigation method.

## Overview

PIED associates the prime or composite nature of integers with signatures in the Fourier modes of the reduced purity. In the hardware implementation, the reduced purity is sampled as a function of time, the corresponding Fourier modes are extracted, and the resulting amplitudes are used to distinguish prime and composite integers.

The repository includes:

- Jupyter notebooks used for the IBM Quantum implementations;
- experimental and processed data used in the manuscript;
- routines for computing reduced purities and Fourier modes;
- scripts/notebooks related to the CFE mitigation procedure;
- complementary zero-noise extrapolation (ZNE) analysis.

## Repository structure

The main hardware-implementation files are located in:

```text
implementations-ibmq/
