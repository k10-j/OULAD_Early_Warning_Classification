# Early Warning Classification with OULAD

This project investigates whether student outcomes in online courses can be
predicted early enough to support timely intervention. It uses the Open
University Learning Analytics Dataset (OULAD) to compare traditional machine
learning models with neural-network approaches.

## Project at a glance

- **Prediction task:** classify each student as **Pass**, **Fail**, or
  **Withdrawn**. Distinction is grouped with Pass.
- **Prediction window:** use information available during the first eight
  weeks of a module presentation (day 56).
- **Approach:** assess data quality, engineer early engagement and assessment
  features, compare models, and evaluate performance on a held-out test set.
- **Leakage controls:** split data by student, preserve the temporal cutoff,
  and fit preprocessing using training data.

## Repository contents

| Path | Description |
| --- | --- |
| [`Notebook/OULAD_Early_Warning_Classification_101.ipynb`](Notebook/OULAD_Early_Warning_Classification_101.ipynb) | Complete analysis and modeling workflow |
| [`report/OULAD_Early_Warning_Report.pdf`](report/OULAD_Early_Warning_Report.pdf) | Project report |
| [`results/figures/`](results/figures/) | Saved analysis, evaluation, and model-diagnostic figures |
| [`requirement.txt`](requirement.txt) | Python package versions used by the notebook |

The raw dataset and trained model files are **not** included in this repository.

## Dataset

Download the OULAD archive (`anonymisedData.csv` zip package) from the
[Open University Learning Analytics Dataset page](https://analyse.kmi.open.ac.uk/open_dataset).
The notebook expects the archive to contain the seven OULAD tables:

- `courses.csv`
- `assessments.csv`
- `vle.csv`
- `studentInfo.csv`
- `studentRegistration.csv`
- `studentAssessment.csv`
- `studentVle.csv`

OULAD is described by Kuzilek, Hlosta, and Zdrahal in
[*Open University Learning Analytics dataset*](https://doi.org/10.1038/sdata.2017.171),
*Scientific Data* (2017), and is released under the
[Creative Commons Attribution 4.0 International license](https://creativecommons.org/licenses/by/4.0/).
Please follow the dataset's terms and cite the original work when using it.

## Getting started

Use Python with Jupyter Notebook or JupyterLab. From the repository root,
install the pinned dependencies:

```bash
python -m pip install -r requirement.txt
```

If Jupyter is not already installed in your environment, install it separately:

```bash
python -m pip install jupyter
```

In a local run, the notebook uses a project folder named
`ML_Final_Project_OULAD_Early_Warning` relative to the notebook kernel's
current working directory. Create its `data` directory and place the downloaded
OULAD zip archive there:

```text
ML_Final_Project_OULAD_Early_Warning/
└── data/
    └── anonymisedData.zip
```

Then launch Jupyter and open the notebook:

```bash
python -m jupyter notebook
```

Run the cells from top to bottom. The notebook extracts the archive, loads the
tables, and creates the remaining working directories. It also contains
Google Colab setup; when running there, place the archive in the configured
project's `data` directory in Google Drive.

The notebook's project directory is configured in its environment-setup cell.
If you prefer to keep generated files in a different location, update
`PROJECT_DIR` there before running the analysis.

## Analysis workflow

The notebook proceeds through:

1. Dataset loading, target creation, and early-withdrawal handling.
2. Data-quality checks and exploratory analysis.
3. Group-aware train, validation, and test splitting.
4. Early-window behavioral features, preprocessing, and sequence preparation.
5. Traditional machine-learning and deep-learning experiments.
6. Model selection, held-out test evaluation, bootstrap uncertainty, learning
   curves, error analysis, and feature importance.
7. Saving selected models and preprocessing artifacts.

Generated models, logs, and additional results are written under the configured
project directory (`models/`, `logs/`, and `results/`). The figures already in
this repository are example saved outputs; rerunning the notebook may produce
different values depending on the dataset, environment, and experiment
configuration.

## Reported results

The notebook reports a best gradient-boosting result of approximately **0.685
macro-F1** and **0.814 macro ROC-AUC** on its evaluation. These values are
specific to the notebook's data split and experiment setup; consult the
[project report](report/OULAD_Early_Warning_Report.pdf) and rerun the notebook
to inspect the full evaluation and trade-offs, particularly for the smaller
Withdrawn class.
