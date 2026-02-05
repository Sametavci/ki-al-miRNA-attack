# miRNA-Based Patient Re-Identification Attack with Siamese Network

## Project Overview

This project implements a Siamese Network for patient re-identification using miRNA gene expression profiles from the GSE68951 dataset. The goal is to simulate an attack scenario where leaked miRNA profiles are used to identify unknown profiles from the same patients, based on multiple timepoints.

- **Key Features**:
  - Data preprocessing (standardization, label encoding).
  - Siamese Network with Triplet Loss for embedding learning.
  - Evaluation protocols: Timepoint-based Leave-One-Out Cross-Validation (LOO CV) for re-identification.
  - Rank-1 and Rank-5 accuracy metrics using Nearest Neighbors (cosine similarity).
  - Handles longitudinal data (multiple timepoints per patient).

- **Dataset**: GSE68951 (plasma miRNA profiles from lung cancer patients, downloaded via GEOparse).
  - Total samples: ~215
  - Unique patients: ~26 (with controls)
  - miRNA features: 1205

- **Attack Scenario** (as per assignment):
  - Assume one timepoint per patient is "unknown" (test).
  - All other timepoints are "leaked" with known identities (train).
  - Iterate over test timepoints using cross-validation.

- **Results Example** (from Timepoint-based LOO CV):
  - Rank-1 Accuracy: ~0.42 (depends on runs, due to randomness in training).
  - Rank-5 Accuracy: ~0.65
  - Note: High values indicate potential privacy risks in miRNA data; low values show variability over time.

This project demonstrates the "advanced" part of the assignment by using a Siamese Network for similarity learning and comparing performance.

## Installation &  How to Run
1. Clone the repository  
    ```bash
   git clone https://github.com/Sametavci/ki-al-miRNA-attack.git
   cd ki-al-miRNA-attack
    ```
2. Create and activate a virtual environment (optional but recommended):
    Windows(Powershell/CMD)
    ```bash
    python -m venv venv
    venv\Scripts\activate
   ```
    macOS / Linux:
    ```bash
    python3 -m venv venv
    source venv/bin/activate
   ```
3. Install dependencies:
    ```bash
    pip install -r requirements.txt
   ```
4. To open in your browser with jupyter lab: 
    ```bash
    jupyter lab
    ```
5. In Jupyter Lab choose the kernel As: 
    ```bash
    mirna-gpu(TF 2.13 + GPU)
    ```

## Download the dataset (automatically handled via GEOparse in the code).

1. Run the main notebook or script (`baseline_methods.ipynb` for other methods or `siamese_NN.ipynb` for siamese network):
- Loads GSE68951 dataset.
- Preprocesses data.
- Trains Siamese Network in LOO loop.
- Computes and prints Rank-1/5 accuracies.

2. Key Files:
- `baseline_methods.ipynb` & `siamese_NN.ipynb`: Full code with data loading, model definitions, and timepoint-based LOO CV.
- `requirements.txt`: Dependencies.
- `data/`: Dataset storage (GSE68951 downloaded here).

3. Customization:
- Change epochs in `siamese_NN.ipynb` for longer training (e.g., 20-40).
- Adjust margin in TripletLoss (0.5 default, try 0.3-0.7).
- For faster runs, reduce epochs or use a subset of patients.


## Model Architecture

- **SiameseDataset**: Generates triplets (anchor, positive, negative) for training.
- **EmbeddingNet**: MLP with dropout and batch norm (input: 1205 miRNAs, output: 128-dim embedding).
- **TripletLoss**: Standard triplet loss with margin.
- **Evaluation**: NearestNeighbors with cosine metric for Rank-1/5.

## Results and Interpretation

- **Timepoint-based LOO CV**: Iterates over each timepoint as test, trains on remaining data. Measures re-identification risk.
- Typical Output:
    ```md
    Timepoint-based Leave-one-out CV
    Total test samples: 215
    Rank-1 Accuracy: 0.4186  (90/215)
    Rank-5 Accuracy: 0.6512  (140/215)
    ```
- Interpretation: ~42% Rank-1 means miRNA profiles can partially identify patients across timepoints, indicating privacy concerns. Variability due to treatment/time changes.

## Limitations

- Small dataset: Overfitting risk; results may vary with random seeds.
- No explicit timepoint column: Assumes samples per patient are timepoints (as per GSE68951).
- “Computationally expensive: Timepoint-based LOO requires retraining the Siamese model for each held-out timepoint (≈215 training runs) Reduce epochs or subsample patients for faster experimentation.”

## License

MIT License. See LICENSE file for details.

## Author
**Cihan Can**, **Bekir Mortas**, **Samet Avci**  
- Dataset: GSE68951 from GEO.
- Inspired by assignment on miRNA re-identification attacks.


