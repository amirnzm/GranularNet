# Physics-Informed Neural Networks for Granular Segregation Modeling

## Project Overview

This project implements Physics-Informed Neural Networks (PINNs) to (1) solve the granular segregation partial differential equation (PDE) and (2) predict segregation velocity given limited data from experiment/simulation. The work addresses the challenge of modeling size segregation in granular materials heap flow, where particles of different sizes separate due to the combined effects of advection, diffusion, and segregation mechanisms.

### Problem Statement

Granular segregation is a critical phenomenon in industrial processes involving particle mixtures. When granular materials flow, smaller particles tend to percolate downward while larger particles rise to the top, leading to non-uniform concentration distributions. Accurately predicting and understanding this behavior is essential for optimizing processes in industries such as pharmaceuticals, food processing, and mining.

### Methodology

The project employs Physics-Informed Neural Networks (PINNs), which integrate physical laws directly into the neural network training process. Unlike traditional neural networks that learn purely from data, PINNs enforce the governing PDE as a constraint during training, allowing them to learn solutions that satisfy both the physics and available experimental data.

**Governing Equation:**

The non-dimensionalized segregation PDE is:

$$\frac{\partial c}{\partial \tilde{t}} + \tilde{u} \frac{\partial c}{\partial \tilde{x}} + \tilde{w} \frac{\partial c}{\partial \tilde{z}} + \Lambda(1 - \tilde{x}) \frac{\partial}{\partial \tilde{z}} \left[ g(\tilde{z}) c(1-c) \right] = \frac{\partial}{\partial \tilde{z}} \left[ \frac{1}{Pe} \frac{\partial c}{\partial \tilde{z}} \right]$$

where:
- $c$ is the concentration (volume fraction of small particles)
- $\tilde{x} \in [0, 1]$, $\tilde{z} \in [-1, 0]$, $\tilde{t} \in [0, t_{end}]$ are dimensionless coordinates
- $\Lambda$ is the segregation parameter
- $Pe$ is the Péclet number
- $\tilde{u}$ and $\tilde{w}$ are dimensionless velocity profiles
- $g(\tilde{z})$ is a shear-rate-like profile

### Project Components

The project consists of three main components:

1. **Forward Model** (`SRC/forwardModel/`): Solves the forward problem with known parameters to predict concentration profiles throughout the domain. This serves as a baseline and validation of the PINN approach.

2. **Inverse Models** (`SRC/inverseModel/`): Three different approaches to parameter estimation:
   - **PINN_Lambda**: Learns the segregation parameter $\Lambda$ from experimental data
   - **PINN_AB**: Learns parameters $A$ and $B$ from an extended segregation model
   - **PINN_NN**: Uses a neural network to learn complex parameter relationships, replacing the functional form of segregation velocity with a trainable network

3. **Visualization** (`SRC/visualization/`): Tools for analyzing results, comparing predictions with experimental data, and visualizing training progress.

### Key Contributions

- Implementation of PINNs for solving the granular segregation PDE with proper boundary conditions
- Development of multiple inverse modeling approaches for parameter estimation
- Integration of experimental data with physics-informed constraints
- Comprehensive validation against ground truth solutions

### Results

The PINN models successfully:
- Solve the forward problem with high accuracy
- Estimate unknown parameters from sparse experimental data
- Capture the complex dynamics of granular segregation including advection, diffusion, and segregation effects

## Quick Start Guide

### Installation

1. **Install Python dependencies:**
   ```bash
   pip install torch numpy matplotlib jupyter pandas openpyxl
   ```

2. **For GPU acceleration (recommended):**
   - Install CUDA-compatible PyTorch from [pytorch.org](https://pytorch.org/)
   - The code automatically detects and uses GPU if available

### Running the Code

#### Option 1: Quick Demo with Pre-trained Models

1. Navigate to the visualization directory:
   ```bash
   cd SRC/visualization
   ```

2. Launch Jupyter:
   ```bash
   jupyter notebook Plots.ipynb
   ```

3. Run all cells to visualize results from pre-trained models

#### Option 2: Train New Models

**Forward Model:**
1. Navigate to `SRC/forwardModel/`
2. Open `PINN_forward.ipynb` in Jupyter
3. Run all cells (training takes ~10-30 minutes depending on hardware)

**Inverse Models:**
1. Navigate to `SRC/inverseModel/`
2. Choose one of the inverse model notebooks:
   - `PINN_Lambda.ipynb` - Learn segregation parameter
   - `PINN_AB.ipynb` - Learn A and B parameters
   - `PINN_NN.ipynb` - Neural network-based approach
3. Run all cells to train the model
4. Trained models are automatically saved to `SRC/visualization/`

**Visualization:**
1. Navigate to `SRC/visualization/`
2. Open `Plots.ipynb` in Jupyter
3. Run all cells to generate plots comparing predictions with experimental data

### Directory Structure

```
Github/
├── README.txt          # Detailed user manual
├── OVERVIEW.md         # This file - project overview and quick start
├── DOC/                # Documentation
│   ├── CSE598_FinalReport.pdf
│   └── CSE598_Presentation.pdf
└── SRC/                # Source code
    ├── forwardModel/
    │   └── PINN_forward.ipynb
    ├── inverseModel/
    │   ├── PINN_AB.ipynb
    │   ├── PINN_Lambda.ipynb
    │   └── PINN_NN.ipynb
    └── visualization/
        ├── Plots.ipynb
        ├── experimental_data.csv
        ├── Forward_data.xlsx
        ├── Inverse_data.xlsx
        └── *.pth (trained model files)
```

### Important Notes

- **Training Time**: Model training times vary significantly based on hardware. GPU acceleration is highly recommended.
- **Data Requirements**: The visualization notebook requires `experimental_data.csv`, `Forward_data.xlsx`, and `Inverse_data.xlsx` to be in the `visualization/` directory.
- **Reproducibility**: All notebooks use fixed random seeds for reproducibility.
- **Model Saving**: Trained models are automatically saved during training. Ensure sufficient disk space.
- **File Paths**: Some notebooks may need path adjustments:
  - Inverse models reference `experimental_data.csv` - adjust to `../visualization/experimental_data.csv` if needed
  - Model saving paths may need adjustment to save to `../visualization/` directory
  - Run notebooks from their respective directories (forwardModel/, inverseModel/, or visualization/)

### For More Details

For comprehensive installation instructions, detailed usage guidelines, and complete file descriptions, please refer to **README.txt**.

### Reference

Fan, Y., et al. (2014). "Modelling size segregation of granular materials: the roles of segregation, advection and diffusion." *Journal of Fluid Mechanics*, 741, 252-279.

