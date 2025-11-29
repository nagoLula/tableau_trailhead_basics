# tableau_trailhe# Tableau Public Assignment – GBBO + Healthcare Viz

## Repository Setup

- This repository has been created and made **public** on GitHub.
- It includes:
  - `README.md` (documentation and reflection)
  - `LICENSE` (Apache 2.0)
  - `/images` folder (screenshots of Trailhead badges and Tableau vizzes)
  - `/data` folder (Admissions.csv healthcare dataset)
- Repo structure and deliverables are being actively built and refined in **Visual Studio Code** for clarity, reproducibility, and alignment with rubric expectations.

## Trailhead Evidence

- Completed modules:
  - Data Storytelling with Tableau Public
  - The Tableau Data Model
- Screenshots:
  ![Trailhead Badge 1](https://github.com/user-attachments/assets/afc67cc1-4b31-411a-a1c3-aa1d4cf26cf2)

  ![Trailhead Badge 2](https://github.com/user-attachments/assets/cd16133a-adcd-428a-99df-b43560371d98)
  ![my first GBBO viz](https://github.com/user-attachments/assets/72f43fe6-3489-46ba-8d50-833ce2116a55)



## Tableau Public Visualizations

- GBBO Viz (Trailhead exercise): [View on Tableau Public](https://public.tableau.com/app/profile/naira.khergiani/viz/MyFirstVizonTableauPublic_17643790360270/Sheet1)
- Healthcare Viz (Admissions dataset): [View on Tableau Public](https://public.tableau.com/app/profile/naira.khergiani/viz/MonthlyHospitalAdmissionsbyDepartment/Sheet1)
- Screenshot of published viz:
  ![My First Healthcare Viz](https://github.com/user-attachments/assets/ee40734e-bb26-47d7-be49-ed54951e3ae1)

## Reflection

*learned*: 

-how Tableau relationships differ from joins, and how multiple clauses ensure accurate linking.  
-Publishing to Tableau Public showed me how to share interactive dashboards.  
-will be useful in healthcare: similar dashboards could track admissions trends, imaging turnaround times, readmission rates, etc.

## Running the Anonymization Script in VS Code

To ensure privacy, original GBBO CSVs (from Trailhead exercise) containing contestant names are excluded via `.gitignore`.  
An anonymized version (`*_anon.csv`) is generated using the helper script `anonymize_gbbo.py`.

### Steps

1. **Open the repo in VS Code**
   - Navigate to the project root (`tableau_trailhead_basics`).
   - Create annonimize_GBBO.py file
   - - Python script:
     - ## Running the Anonymization Script in VS Code

To ensure privacy, original GBBO CSVs containing contestant names are excluded via `.gitignore`.  
An anonymized version (`*_anon.csv`) is generated using the helper script `anonymize_gbbo.py`.

### Steps

1. **Open the repo in VS Code**
   - Navigate to the project root (`tableau_trailhead_basics`).
   - -Created anonymize_GBBO.py file and run the Python script below:

import pandas as pd
import os

# Path to the unzipped GBBO_dataset folder
folder = "data/GBBO_Dataset"

# Loop through all CSV files in the folder
---
for file in os.listdir(folder):
        # Only process CSV files (skip the script and any other non-csv files)
        if not file.lower().endswith('.csv'):
                continue

        # Skip files that are already anonymized to avoid creating _anon_anon.csv
        if file.lower().endswith('_anon.csv'):
                continue

        path = os.path.join(folder, file)
        try:
                # Skip malformed rows instead of erroring out
                df = pd.read_csv(path, on_bad_lines='skip')  # pyright: ignore[reportUnknownMemberType]
        except Exception as e:
                print(f"Skipping '{file}' — failed to read CSV: {e}")
                continue

        # If there's a column called 'Name' or 'Baker', anonymize it
        for col in df.columns:
                if "Name" in col or "Baker" in col:
                        df[col] = [f"Baker_{i+1:02d}" for i in range(len(df))]

        # Save anonymized version with _anon suffix
        new_path = os.path.join(folder, file.replace(".csv", "_anon.csv"))
        df.to_csv(new_path, index=False)
        
print("Anonymization complete. Check data/GBBO-Dataset for _anon files.")

---
---
