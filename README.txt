Physics-Informed Neural Networks (PINN) for Granular Segregation Modeling
==========================================================================

DESCRIPTION
-----------
This package implements Physics-Informed Neural Networks (PINNs) to solve and 
invert the granular segregation partial differential equation (PDE) from Fan et al. 
(2014). The project includes:

1. Forward Model: Solves the segregation PDE to predict concentration profiles
2. Inverse Models: Estimates unknown parameters (A, B, Lambda, or neural network-based)
   from experimental data
3. Visualization: Tools to plot and analyze results

The governing equation models size segregation of granular materials in a 
chute flow, incorporating advection, diffusion, and segregation mechanisms.

INSTALLATION
------------
1. Ensure Python 3.7+ is installed on your system

2. Install required packages:
   pip install torch numpy matplotlib jupyter pandas openpyxl

3. For GPU acceleration (optional but recommended):
   - Install CUDA-compatible PyTorch from https://pytorch.org/
   - The code will automatically use GPU if available

USAGE
-----
All code is organized in subdirectories within the SRC directory:

1. Forward Model (SRC/forwardModel/PINN_forward.ipynb):
   - Solves the forward problem with known parameters
   - Trains a PINN to predict concentration profiles
   - Saves trained model to visualization/pinn_forward.pth

2. Inverse Models (SRC/inverseModel/):
   - PINN_AB.ipynb: Learns parameters A and B from data
   - PINN_Lambda.ipynb: Learns parameter Lambda from data
   - PINN_NN.ipynb: Uses a neural network to learn parameter relationships
   - Each saves its trained model to visualization/pinn_inverse_*.pth

3. Visualization (SRC/visualization/Plots.ipynb):
   - Loads trained models and generates plots
   - Compares predictions with experimental data
   - Requires experimental_data.csv, Forward_data.xlsx, and Inverse_data.xlsx

To run a notebook:
   jupyter notebook SRC/[subdirectory]/[notebook_name].ipynb

Or use JupyterLab:
   jupyter lab SRC/[subdirectory]/[notebook_name].ipynb

DEMO
----
Quick start demo using pre-trained models:

1. Navigate to SRC/visualization/
2. Open Plots.ipynb in Jupyter
3. Run all cells to visualize results from pre-trained models
4. The notebook will load saved models (*.pth files) and generate plots

To train new models:
1. Run SRC/forwardModel/PINN_forward.ipynb to train the forward model (takes ~10-30 minutes)
2. Run any inverse model notebook in SRC/inverseModel/ (PINN_AB.ipynb, PINN_Lambda.ipynb, or PINN_NN.ipynb)
3. Use SRC/visualization/Plots.ipynb to visualize the results

FILES
-----
SRC/forwardModel/ contains:
  - PINN_forward.ipynb: Forward model implementation

SRC/inverseModel/ contains:
  - PINN_AB.ipynb: Inverse model for A and B parameters
  - PINN_Lambda.ipynb: Inverse model for Lambda parameter
  - PINN_NN.ipynb: Neural network-based inverse model

SRC/visualization/ contains:
  - Plots.ipynb: Visualization and analysis
  - experimental_data.csv: Experimental data for validation
  - Forward_data.xlsx: Ground truth data for forward model
  - Inverse_data.xlsx: Ground truth data for inverse models
  - *.pth: Pre-trained model weights (all models)

DOC/ contains:
  - CSE598_FinalReport.pdf: Complete project report
  - CSE598_Presentation.pdf: Presentation slides

NOTES
-----
- Training times vary based on hardware (GPU recommended)
- Models are saved automatically during training
- All notebooks include detailed comments explaining the implementation
- The code uses random seeds for reproducibility

IMPORTANT: File Paths
---------------------
The notebooks use relative paths for data files and model saving:
- Inverse models (PINN_AB, PINN_Lambda, PINN_NN) expect experimental_data.csv 
  in the same directory or need path adjustment to '../visualization/experimental_data.csv'
- Models are saved to './models/' directory - you may need to create this 
  directory or adjust paths to '../visualization/' to match the repository structure
- Visualization notebook (Plots.ipynb) expects all data files and model files 
  in the same directory (visualization/)

REFERENCE
---------
Fan, Y., et al. (2014). "Modelling size segregation of granular materials: 
the roles of segregation, advection and diffusion." Journal of Fluid Mechanics, 
741, 252-279.

