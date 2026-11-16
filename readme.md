TSP Solvers Comparison Framework

This repository provides a unified benchmarking framework to compare the performance (latency, throughput, and optimality gap) of various end-to-end neural combinatorial optimization solvers for the Traveling Salesman Problem (TSP).

Based on the required working base, this project compares:

NAR4TSP (Xiao et al.)

Attention Learn to Route (Kool et al.)

TSP Transformer (Bresson and Laurent)

Graph ConvNet TSP (Joshi et al.)

tspFormer (Jung et al.)

Prerequisites

Python 3.8+

PyTorch (with CUDA support recommended for GPU batching)

Git

1. Clone the Base Repository

First, clone this main repository to your local machine and navigate into it:

git clone <your_repository_url>
cd <your_repository_name>


2. Setting Up the Working Base Folders

Your working directory must contain the source code for each of the models being compared. If these were not included as submodules in the main repository, you need to clone or extract each model's source code into its respective folder.

Ensure your root directory structure looks exactly like this:

working_base/
├── .git/
├── NAR4TSP/                  # Place the official NAR4TSP code here
├── TSP_Transformer/          # Place Bresson & Laurent's code here
├── attention-learn-to-route/ # Place Kool et al.'s code here
├── graph-convnet-tsp/        # Place Joshi et al.'s code here
├── shared/                   # Shared utilities, datasets, or distance matrix generators
├── tspFormer/                # Place Jung et al.'s code here
├── .gitignore
├── all_comparison.png        # Generated output graph
├── beam_comparison.png       # Generated output graph
└── beam_results.csv          # Generated output data


Adding Missing Model Folders

If any folders are missing, you can typically add them by cloning their official repositories directly into your working base. For example:

# Example for adding Kool et al.'s model
git clone https://github.com/wouterkool/attention-learn-to-route.git


(Repeat this process or extract the provided source code for NAR4TSP, TSP_Transformer, graph-convnet-tsp, and tspFormer into their exact folder names shown above).

3. Environment Setup

It is highly recommended to use a virtual environment to avoid dependency conflicts, as these models may require specific library versions.

python -m venv tsp_env
source tsp_env/bin/activate  # On Windows use: tsp_env\Scripts\activate

# Install core dependencies (adjust based on your specific requirements file)
pip install torch numpy pandas numba matplotlib


Note: You may need to run pip install -r requirements.txt inside the specific model folders (e.g., attention-learn-to-route) if they have unique dependencies.

4. Running the Benchmarks

Depending on your setup, the benchmarking is executed either via a central Python script or a Jupyter/Colab notebook.

Option A: Running via Python Script

If you have a central execution script (e.g., run_benchmarks.py) that imports from the shared folder and the model folders:

python run_benchmarks.py


Option B: Running via Jupyter Notebook / Colab

If you are using a notebook to run the baseline cells and GPU tensor calculations:

Launch Jupyter:

jupyter notebook


Open your benchmark notebook.

Ensure the BASE path in your code points to this root directory (e.g., /content/drive/MyDrive/Colab Notebooks/TSP if using Colab, or ./ if running locally).

Run all cells. The scripts will generate the beam_results.csv and export the comparison charts (all_comparison.png, etc.) directly into the root folder.