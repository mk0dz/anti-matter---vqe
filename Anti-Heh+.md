# Quantum Simulation of Anti-Matter Helium Hydride: A Comparative Study of Energy Landscapes Using Variational Quantum Algorithms

**Author**: Mukul Kumar (bs24bsc1235@iitj.ac.in)  
**Affiliation**: Indian Institute of Technology, Jodhpur

## Abstract

This paper presents a comprehensive quantum computational study of the anti-matter helium hydride cation (anti-HeH+) in comparison with its normal matter counterpart. Utilizing the variational quantum eigensolver (VQE) framework implemented through Qiskit, we analyze the energetic properties, structural characteristics, and quantum computational challenges associated with simulating these molecular systems. Our results demonstrate a significant energy difference between anti-matter and normal matter HeH+ across varying internuclear distances, with anti-HeH+ showing consistently lower ground state energies in classical simulations but exhibiting distinctive quantum computational behavior. We specifically analyze potential energy surfaces at bond distances ranging from 0.8 to 2.5 Bohr, finding the optimal equilibrium distance for both systems at approximately 0.8 Bohr. Furthermore, we investigate the impact of different error mitigation strategies on quantum computational accuracy, revealing that basic error mitigation techniques offer the most balanced approach for quantum simulations of these systems. This work represents a significant step toward understanding anti-matter molecular systems through quantum computational methods and highlights the theoretical and computational challenges in accurately modeling exotic molecular species.

## 1. Introduction

Anti-matter, comprising particles with identical mass but opposite charge to their normal matter counterparts, presents one of the most intriguing enigmas in modern physics. While the Standard Model predicts matter and anti-matter should have been produced in equal amounts during the Big Bang, the observed universe demonstrates a profound asymmetry favoring matter. Beyond this cosmological significance, anti-matter systems offer unique opportunities to test fundamental physical theories and explore exotic molecular properties.

The helium hydride ion (HeH+) holds particular significance as the first molecular species to form in the early universe and represents one of the simplest heteronuclear diatomic molecular ions. Its anti-matter counterpart, anti-HeH+, in which the charges of constituent particles are reversed, provides an excellent testbed for investigating anti-matter molecular physics while remaining computationally tractable.

Traditional computational chemistry methods face significant challenges when simulating exotic molecular species due to the approximate nature of electronic structure methods. Quantum computing offers an alternative paradigm, with the potential to provide more accurate results for quantum systems through direct exploitation of quantum mechanical principles. The Variational Quantum Eigensolver (VQE) algorithm, in particular, represents a promising hybrid quantum-classical approach for determining molecular ground state energies on near-term quantum devices.

In this work, we employ quantum computational methods to investigate the electronic structure and energetic properties of anti-HeH+ compared to normal HeH+, exploring both the fundamental physical differences between these systems and the computational challenges associated with their simulation on quantum hardware. We examine potential energy surfaces, analyze error mitigation strategies, and assess the current capabilities and limitations of quantum computational approaches for exotic molecular systems.

## 2. Theoretical Approach

### 2.1 Anti-Matter Molecular Systems

Anti-matter molecular systems consist of atoms composed of antiparticles—positrons replacing electrons, and antiprotons and antineutrons replacing protons and neutrons. For anti-HeH+, the molecular ion consists of anti-helium and anti-hydrogen nuclei with positrons forming the binding "electronic" structure. The Hamiltonian governing such systems maintains the same mathematical form as for normal matter, but with reversed charges:

$$\hat{H} = -\sum_i \frac{\nabla_i^2}{2} - \sum_{i,A} \frac{Z_A}{r_{iA}} + \sum_{i<j} \frac{1}{r_{ij}} + \sum_{A<B} \frac{Z_A Z_B}{R_{AB}}$$

Where for anti-matter systems, the nuclear charges $Z_A$ and $Z_B$ are negative rather than positive. This charge reversal fundamentally alters the electrostatic interactions within the molecule, potentially leading to different equilibrium geometries, binding energies, and electronic properties compared to normal matter counterparts.

### 2.2 Quantum Computational Chemistry

Quantum computers offer a natural framework for simulating quantum systems. The electronic structure problem involves mapping the molecular Hamiltonian to a qubit representation, typically using encodings such as the Jordan-Wigner transformation:

$$\hat{H} = \sum_{i,j,k,l} h_{ij} a_i^\dagger a_j + \frac{1}{2}\sum_{i,j,k,l} h_{ijkl} a_i^\dagger a_j^\dagger a_k a_l$$

Where $a_i^\dagger$ and $a_i$ are creation and annihilation operators, and $h_{ij}$ and $h_{ijkl}$ represent one- and two-electron integrals. Under the Jordan-Wigner transformation, these fermionic operators map to qubit operators:

$$a_j^\dagger = \frac{1}{2}(X_j - iY_j) \bigotimes_{k=0}^{j-1} Z_k$$

$$a_j = \frac{1}{2}(X_j + iY_j) \bigotimes_{k=0}^{j-1} Z_k$$

Where $X_j$, $Y_j$, and $Z_j$ represent Pauli operators acting on the $j$-th qubit.

The VQE algorithm employs a parameterized quantum circuit to prepare a trial state $|\psi(\boldsymbol{\theta})\rangle$, followed by energy estimation:

$$E(\boldsymbol{\theta}) = \langle\psi(\boldsymbol{\theta})|\hat{H}|\psi(\boldsymbol{\theta})\rangle$$

A classical optimizer iteratively updates the parameters $\boldsymbol{\theta}$ to minimize this energy expectation value, ultimately approaching the ground state energy of the system.

## 3. Methodology

### 3.1 Computational Framework

Our simulations utilize the Qiskit framework to implement quantum computational chemistry calculations for both anti-HeH+ and HeH+ molecular systems. We employ a minimal basis treatment within a simplified molecular orbital framework, sufficient to capture the essential physics while remaining tractable for quantum simulation.

The molecular system class we developed handles both normal and anti-matter configurations by introducing a charge factor parameter:

$$\text{charge_factor} = \begin{cases} -1 & \text{for anti-matter} \ 1 & \text{for normal matter} \end{cases}$$

This factor modifies the nuclear charges in the molecular Hamiltonian:

$$Z_A^{\text{effective}} = Z_A \times \text{charge_factor}$$

For anti-HeH+, the nuclei are defined with negative charges (anti-helium with $Z = -2$ and anti-hydrogen with $Z = -1$), while the positrons (replacing electrons) maintain positive charge.

### 3.2 Quantum Simulation Approach

We employed three primary computational approaches:

1. **Classical eigensolvers**: Using the NumPyMinimumEigensolver to obtain reference energy values with high precision.
    
2. **Quantum simulation**: Utilizing the VQE algorithm with the EfficientSU2 ansatz and the COBYLA optimizer to determine ground state energies.
    
3. **Error mitigation**: Applying techniques of increasing sophistication:
    
    - No error mitigation (raw results)
    - Basic error mitigation (readout error correction)
    - Advanced error mitigation (combining readout error correction with zero-noise extrapolation)

The quantum simulations employed 4 qubits, sufficient to represent the minimal basis treatment of both molecular systems. For real quantum hardware experiments, we utilized IBM Quantum's systems with 8192 shots per circuit evaluation to ensure statistical significance.

### 3.3 Potential Energy Surface Analysis

To characterize the molecular properties, we performed potential energy surface (PES) scans by calculating the energy at various internuclear distances ranging from 0.8 to 2.5 Bohr. The mathematical relationship between energy and bond distance follows:

$$E(R) = \min_{\boldsymbol{\theta}} \langle\psi(\boldsymbol{\theta})|\hat{H}(R)|\psi(\boldsymbol{\theta})\rangle$$

Where $\hat{H}(R)$ represents the Hamiltonian at bond distance $R$.

## 4. Results and Discussion

### 4.1 Energy Comparison Between Anti-Matter and Normal Matter HeH+

Our classical solver results demonstrate a fundamental energetic difference between anti-matter and normal matter HeH+ systems. Figure 1 shows the potential energy surface comparison between these two molecular systems.

At the reference bond distance of 1.5 Bohr, the anti-HeH+ system exhibits a ground state energy of -11.29 Hartree compared to -31.35 Hartree for normal HeH+. This substantial energy difference persists across all internuclear distances examined, highlighting the fundamental physical distinctions between these systems.

The potential energy surface scan reveals that both molecular systems exhibit their energy minima at approximately 0.8 Bohr, with energies of -20.63 Hartree for anti-HeH+ and -39.56 Hartree for normal HeH+. This similarity in equilibrium geometry despite significant energy differences suggests that while the absolute energies differ dramatically, certain structural characteristics remain comparable between normal and anti-matter systems.

### 4.2 Quantum Computational Performance and Error Analysis

When implemented on quantum hardware, both molecular systems exhibited energy estimation errors compared to classical reference values. At 1.5 Bohr, the quantum estimate for anti-HeH+ was -8.37 Hartree (versus -11.29 Hartree classically), while for normal HeH+ the quantum estimate was -23.45 Hartree (versus -31.35 Hartree classically). These discrepancies represent relative errors of 25.85% and 25.20% respectively, indicating that quantum computational challenges affect both systems similarly.

Interestingly, as shown in Table 1, the relative errors in quantum computation vary with bond distance, with anti-HeH+ showing increasing error at larger bond distances (42.66% at 2.5 Bohr) while normal HeH+ shows the opposite trend (18.78% at 2.5 Bohr).

|Bond Distance (Bohr)|Anti-HeH+ Relative Error (%)|Normal HeH+ Relative Error (%)|
|---|---|---|
|0.8|27.86|20.43|
|1.5|25.85|25.20|
|2.5|42.66|18.78|

Table 1: Relative errors in quantum computation compared to classical reference values at different bond distances.

### 4.3 Error Mitigation Analysis

We investigated three error mitigation strategies, with results shown in Figure 2. For anti-HeH+ at 1.5 Bohr:

1. **No Error Mitigation**: -8.14 Hartree (27.89% relative error)
2. **Basic Error Mitigation**: -8.01 Hartree (29.07% relative error)
3. **Advanced Error Mitigation**: -7.76 Hartree (31.29% relative error)

Surprisingly, error mitigation techniques increased the relative error rather than decreasing it. This counter-intuitive result suggests that for anti-matter systems, the error structure is complex and not effectively addressed by standard mitigation approaches. In contrast, for normal HeH+, basic error mitigation showed a slight improvement:

1. **No Error Mitigation**: -26.88 Hartree (14.24% relative error)
2. **Basic Error Mitigation**: -26.99 Hartree (13.90% relative error)
3. **Advanced Error Mitigation**: -26.29 Hartree (16.12% relative error)

The optimization trajectories reveal that both molecular systems converge similarly in the VQE algorithm, requiring approximately 80-90 iterations to approach their final energy values, regardless of the error mitigation strategy employed.

### 4.4 Implications and Limitations

Our results demonstrate that while quantum computational methods can successfully distinguish between anti-matter and normal matter molecular systems, significant challenges remain in achieving chemical accuracy. The observed error patterns suggest that anti-matter simulations may be more sensitive to certain types of quantum noise, potentially related to the different magnitudes of Hamiltonian terms arising from the charge reversal.

The minimal basis treatment employed in this work, while sufficient for demonstrating the key physical differences, necessarily limits the quantitative accuracy of our results. More sophisticated basis sets would require additional qubits, presenting a clear direction for future work as quantum hardware continues to advance.

## 5. Conclusion

This work presents the first comprehensive quantum computational study comparing anti-matter and normal matter HeH+ molecular systems. Our results demonstrate that:

1. Anti-HeH+ exhibits fundamentally different energetics compared to normal HeH+, with consistently higher (less negative) ground state energies across all internuclear distances studied.
    
2. Both molecular systems share a similar equilibrium bond distance of approximately 0.8 Bohr, suggesting certain structural similarities despite their energetic differences.
    
3. Quantum computational approaches can successfully distinguish between these systems, though achieving chemical accuracy remains challenging with current quantum hardware and algorithms.
    
4. Error mitigation strategies show variable effectiveness, with basic approaches providing slight improvements for normal matter systems but potentially introducing additional complexities for anti-matter simulations.
    

These findings contribute to our understanding of exotic molecular systems and highlight both the potential and current limitations of quantum computational chemistry. As quantum hardware continues to advance, more accurate simulations of increasingly complex anti-matter systems will become feasible, potentially revealing further insights into the fundamental physics of these exotic molecular species.

## Acknowledgements

The author gratefully acknowledges the support of the Quantum Computing Laboratory at the Indian Institute of Technology, Jodhpur. We thank IBM Quantum for providing access to quantum computing resources through the IBM Quantum Experience. Special thanks to the faculty advisors and research colleagues who provided valuable feedback and discussions throughout this work.