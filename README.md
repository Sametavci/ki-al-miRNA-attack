# miRNA Re-Identification Project (GSE68951)

This project performs data extraction, preprocessing, and patient re-identification using miRNA expression profiles from the GEO dataset **GSE68951**.  
Group-based train/test splitting is applied to ensure that the same patient never appears in both training and test folds.

---

## 🚀 Environment Setup (One-Liner)

### macOS / Linux:

    python3 -m venv venv && source venv/bin/activate && pip install -r requirements.txt && python -m ipykernel install --user --name ml-project-env --display-name "ML Project"

### Windows PowerShell:

    python -m venv venv; venv\Scripts\Activate.ps1; pip install -r requirements.txt; python -m ipykernel install --user --name ml-project-env --display-name "ML Project"

This command installs all dependencies and registers the virtual environment as a Jupyter kernel.

---

## ️ Running the Notebook

1. Create & activate environment (one-liner above)  
2. Launch Jupyter:

       jupyter notebook

3. Select the kernel **"ML Project"**  
4. Open:  
   
       notebooks/mRNA.ipynb

---

##  Project Structure


