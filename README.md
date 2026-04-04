"This repository includes two MATLAB-based applications designed to accurately predict arbitrary-ratio power-splitter outputs using user-defined geometric parameters. Both applications are fully compatible with MATLAB 2024 and provide a practical interface for rapid performance estimation and design exploration."
LNOI Power Splitter — User Manual

Overview
This application is a DNN (Deep Neural Network)-based tool developed to predict the performance of and inversely design arbitrary-ratio power splitters on the LNOI (Lithium Niobate on Insulator) platform. The application provides two core functions:

Forward Prediction: Computes the output power splitting ratio from user-defined geometric parameters
Inverse Design: Determines the optimal geometric parameter set for a user-specified target power ratio


Requirements

MATLAB R2024b or later
Deep Learning Toolbox
Optimization Toolbox
Installation
Clone the repository: https://github.com/aksoy1993/power-splitter.git
Run run_app.m in MATLAB, or open PowerSplitterApp.mlapp directly
The application interface will load automatically
Input Parameters and Physical Bounds
The table below lists the six geometric parameters accepted by the application, their physical descriptions, and the feasible value ranges:
Parameter Description Feasible Range Width (µm)Rib top width — determines single-mode propagation 0.8 – 1.5
h₁ (µm) Slab height — affects vertical mode leakage 0.18 – 0.5

h₂ (µm) Rib height — provides vertical mode confinement 0.2 – 0.5 

L (µm)Total optical propagation length 26 – 110

W (µm)Multimode region width — governs higher-order mode excitation 5 – 14

L₁ (µm)Length of the removed rectangular section — directly controls power ratio 0 – 16

⚠️ Warning: Entering parameter values outside the specified ranges may cause the model predictions to lose reliability. The application will display an automatic warning in such cases.

Forward Prediction Module — 
Step-by-Step Guide
Purpose: You have a specific device geometry and want to find out what power splitting ratio it produces.

Step 1: Open the application and navigate to the "Forward Prediction" tab.

Step 2: Enter the six geometric parameters into the corresponding fields. For example, for a 50:50 distribution:

Width = 1.25 µm

h₁    = 0.20 µm

h₂    = 0.50 µm

L     = 26.4 µm

W     = 7.60 µm

L₁    = 0.00 µm

Step 3: Click the "Predict" button.

Step 4: The result screen displays the P₁ and P₂ values, representing the percentage of optical power delivered to the primary and secondary output ports, respectively (P₁ + P₂ = 100%).

Inverse Design Module — Step-by-Step Guide

Purpose: You know the target power ratio you need and want to find the geometric parameters that achieve it.

Step 1: Navigate to the "Inverse Design" tab.

Step 2: Enter the target power ratio in P1:P2 format. For example: 70:30

Step 3: Click the "Run Optimization" button. The system uses the pre-trained DNN model jointly with a gradient-based 

optimization algorithm to compute the optimal geometric 
parameter set.

Step 4: The recommended parameters are displayed on the screen. To verify the result, click "Verify with Forward Prediction" to automatically transfer the computed parameters to the forward prediction module.

Step 5 (optional): Each parameter is perturbed by ±0.05 µm and the resulting variation in the output power ratio is computed; the most fabrication-robust solution is highlighted.


Achievable Visual Outputs
The following section describes the representative output field patterns obtained from Lumerical MODE/EME simulations, corresponding to the power distributions predicted by the application. These figures illustrate the output distributions achievable with different geometric parameter sets.

a) 50:50 Power Distribution
Equal optical power exits from both output ports. The field intensities at both ports are similar and symmetric. This configuration is achieved with L₁ = 0 µm, meaning no material is removed from the asymmetry region. The symmetric self-imaging condition in the multimode region is fully satisfied, resulting in an even power split. This distribution is typically used in balanced interferometer arms, optical networks, and reference measurement systems.

In the application: Enter L₁ = 0 and a value of W between 7–10 µm in the forward prediction module to obtain this result. Expected output: P₁ ≈ 50%, P₂ ≈ 50%.

(b) 60:40 Power Distribution
The field intensity at the primary output port is noticeably higher than at the secondary port, though the secondary port still carries a significant fraction of the total power. This asymmetry is achieved by setting L₁ to a small non-zero value; the slight increase in coupling length introduces a moderate phase imbalance between the propagating modes, leading to a mild power asymmetry. Such distributions are preferred in power balancing circuits, optical test systems, and signal amplification applications.

In the application: Enter 60:40 in the Inverse Design tab to obtain the suggested L₁ and W values. A typical value of L₁ ≈ 3 µm is expected.

(c) 70:30 Power Distribution
The primary port clearly exhibits higher field intensity while the contribution of the secondary port has noticeably diminished. As L₁ increases, the modal interference pattern in the multimode region shifts, progressively directing more power toward the primary port. According to coupled-mode theory, the accumulated phase difference grows with increasing coupling length, causing a stronger power imbalance. This configuration is commonly encountered in optical signal routing, asymmetric power budget circuits, and communication systems.

In the application: Enter 70:30 in the Inverse Design tab and run the optimization. Verify the result using the Forward Prediction module. A typical value of L₁ ≈ 5–6 µm is expected.
(d) 80:20 Power Distribution
The field intensity at the primary output port is dominant; the secondary port carries only a small fraction of the total optical power. Further increasing L₁ concentrates power transfer toward the primary port and decisively alters the modal coupling dynamics. At this level of asymmetry, the self-imaging condition of the multimode region is substantially disrupted, and the output power ratio is predominantly governed by the interaction length L₁. This asymmetric distribution is used in optical neural networks, programmable photonic circuits, and power monitoring systems.

Quick Reference — Which L₁ Value Produces Which Ratio?
Target Ratio Approximate, L₁ (µm),    Notes
50:50, 0, Full symmetry W-dependent; 60:40, ~3, Mild asymmetry; 70:30, ~5–6, Moderate asymmetry; 80:20, ~9–10, Pronounced asymmetry; 90:10, ~12–16, High asymmetry, tolerance analysis strongly recommended

Important Note: These values are provided as guidance only. The exact parameter set depends on the specific values of Width, h₁, h₂, L, and W. The Inverse Design module will always provide the most accurate result.

