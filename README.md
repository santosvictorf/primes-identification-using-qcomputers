# Prime Number Identification Demonstrated with Quantum Processors Using a New Rescaling-Based Noise Mitigation Technique

This repository contains the code and data associated with the manuscript:

**Prime Number Identification Demonstrated with Quantum Processors Using a New Rescaling-Based Noise Mitigation Technique**

The work implements the PIED algorithm (Prime Identification via Entanglement Dynamics) on IBM Quantum processors and analyzes the extraction of number-theoretic information from the Fourier spectrum of the reduced purity of a bipartite quantum system. The repository also contains the data-analysis routines used to apply and test the CFE (Correction Factor Extrapolation) noise-mitigation method.

# Overview

PIED associates the prime or composite nature of integers with signatures in the Fourier modes of the reduced purity. In the hardware implementation, the reduced purity is sampled as a function of time, the corresponding Fourier modes are extracted, and the resulting amplitudes are used to distinguish prime and composite integers.

The repository includes:

- Jupyter notebooks used for the IBM Quantum implementations;
- experimental and processed data used in the manuscript;
- routines for computing reduced purities and Fourier modes;
- scripts/notebooks related to the CFE mitigation procedure;
- complementary zero-noise extrapolation (ZNE) analysis.

# Repository structure

The main hardware-implementation files are located in:

```text
implementations-ibmq/
```

# Software requirements

The notebooks were developed using the following main software versions:
- Python 3.9.19
- Qiskit 2.1.0
- SciPy 1.13.1

The main Python packages required are:

- numpy
- scipy
- matplotlib
- qiskit
- qiskit-ibm-runtime

A minimal environment can be prepared with:

**pip install numpy scipy matplotlib qiskit qiskit-ibm-runtime**

# Main parameters in the notebooks

The main parameters are defined near the beginning of each notebook. For example, in the d = 4 implementation one finds parameters of the form:

- batches = 3
- d = 4
- w = 0.1
- p = 30
- nshots = 8192
- q = 2 * int(np.ceil(np.log(d) / np.log(2)))
- num_qubits = 2*q + 1

Their meaning is:

- d: subsystem dimension;
- w: frequency parameter ω used in the time evolution;
- p: number of sampled time points;
- nshots: number of measurement shots per circuit;
- batches: number of independent repetitions of the experiment;
- q: number of qubits used to encode the bipartite system before adding the ancilla;
- num_qubits: total number of qubits in the SWAP-test circuit, including the ancilla.

The sampled time values are generated as:

t_values = np.linspace(0, np.pi / w, p)

# Adjustable parameters

The notebooks are written so that several parameters can be modified for further analysis.

## Dimension

The subsystem dimension is set by:

d = 4

The manuscript reports hardware demonstrations for d=4, d=8, and d=16. Changing d changes the number of qubits, the circuit structure, and the range of Fourier modes analyzed. In the present implementation, d is chosen as a power of two.

## Number of time points

The number of sampled time points is set by:

p = 30

Increasing p improves the numerical Fourier extraction but also increases the number of circuits that must be executed on hardware.

The values used in the manuscript are:

- d = 4   -> p = 30
- d = 8   -> p = 120
- d = 16  -> p = 480

## Number of shots

The number of shots is set by:

nshots = 8192

Increasing nshots reduces statistical fluctuations but increases hardware usage.

## Number of batches

The number of independent repetitions is set by:

batches = 3

Multiple batches are used to estimate averages and error bars. The manuscript uses three batches for d = 4 and d = 8, and one batch for d = 16.

## Frequency parameter

The frequency parameter is set by:

w = 0.1

Changing w changes the time interval because the sampled interval is [0,π/ω].

## IBM Quantum backend

The backend is selected through Qiskit Runtime. The manuscript results were obtained using IBM Aachen.

To run the notebooks on a currently available IBM Quantum backend, the backend name can be replaced by the desired backend available to the user account, for example:

backend_name = "backend_name_here"
backend = service.backend(backend_name)

Exact numerical reproduction on hardware is not expected, since IBM Quantum devices, calibration data, connectivity, noise levels, and availability change over time.

# Reproducing the analysis from the provided data

The repository includes processed experimental data used to generate the figures and Fourier-mode analysis in the manuscript. Therefore, the analysis and plots can be reproduced without resubmitting jobs to IBM Quantum hardware.

The general workflow implemented in the notebooks is:

experimental data -> reduced purity -> Fourier-mode extraction -> CFE correction -> plots

The data files contain the sampled time values, measured reduced purities, and corresponding errors. In the CSV files, the main columns are:

t, Tr, err

where:

- t is the sampled time value;
- Tr is the measured reduced purity γ_A(t);
- err is the corresponding statistical error.

The notebooks load these data, extract the Fourier modes α_n, apply the CFE correction when appropriate, and generate the plots used in the manuscript.

## Re-running the hardware experiments

The notebooks also contain the code used to construct and submit the circuits to IBM Quantum hardware.

Re-running the hardware experiments requires:

- an IBM Quantum account;
- local Qiskit Runtime credentials;
- access to the selected backend;
- sufficient runtime or usage quota.

The total number of circuits increases with the number of sampled time points p and the number of batches. Therefore, changing these parameters may substantially increase the required hardware resources.

Because the original experiments were performed on IBM Aachen, which is no longer available through the current IBM Quantum platform interface, exact reruns under the same hardware conditions are not possible. However, the notebooks can be adapted to currently available IBM Quantum backends by changing the backend name and, if necessary, adjusting the transpilation or execution settings.

# CFE correction

The CFE correction is applied at the data-analysis stage. The notebooks compare the experimentally extracted Fourier modes with the expected analytical structure and use this information to construct the correction factor described in the manuscript.

The corrected Fourier-mode amplitudes are then used to improve the identification of prime and composite integers from the experimental data.

# Zero-noise extrapolation

The folder

```text
implementations-ibmq/zne/
```

contains the complementary zero-noise extrapolation analysis discussed in the manuscript appendix. These results are provided for comparison with the CFE mitigation procedure.

# JSON data files

When available, JSON files are provided as structured versions of the processed experimental data originally stored in CSV format. These files are intended to make the data easier to load and verify programmatically.

The JSON files are not the original IBM Quantum job-result JSON files. They contain processed data used in the analysis, such as time values, measured purities, and errors.

## Notes on IBM Quantum job data

The repository focuses on providing the processed data required to reproduce the analysis and figures reported in the manuscript.

IBM Quantum job IDs are not sufficient for public reproducibility, since jobs generated from one IBM Quantum account are generally not retrievable by other users. In addition, backend availability and platform interfaces change over time.

For this reason, the repository provides the processed experimental data rather than relying on job IDs for reproducibility.

# Citation

If this repository is used, please cite the associated manuscript:
Prime Number Identification Demonstrated with Quantum Processors Using a New Rescaling-Based Noise Mitigation Technique
