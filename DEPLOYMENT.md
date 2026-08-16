# Deployment Guide

This project is a Python research and batch-analysis repository. It does not expose a web server or API, so deployment consists of preparing the runtime environment, supplying the datasets, configuring paths, and running the analysis scripts.

## 1. Windows

Install Python 3.10+ and Git, then clone the repository:

```powershell
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd <YOUR_REPOSITORY_NAME>
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install --upgrade pip
pip install -r requirements.txt
```

Create `Dataset\` and place the required CSV inputs there. Before running a script, change its `DATA_DIR`, `DATASET_DIR`, `BASE_PATH`, or related settings. Prefer a repository-relative pattern such as:

```python
from pathlib import Path
BASE_DIR = Path(__file__).resolve().parent
DATA_DIR = BASE_DIR / "Dataset"
```

Run a workflow with, for example:

```powershell
python connectedness_analysis.py
```

## 2. Linux server

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd <YOUR_REPOSITORY_NAME>
python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
```

Copy the research dataset into `Dataset/`. Keep private or licensed data outside GitHub. Update the selected script to use repository-relative paths, then run:

```bash
python connectedness_analysis.py
```

For long-running jobs, use cron, systemd timers, or a cloud batch/compute service.

## 3. GPU training

The ML scripts use PyTorch and select CUDA automatically when available. On a GPU server, install the PyTorch build appropriate for the server and verify it:

```bash
python -c "import torch; print(torch.__version__); print('CUDA:', torch.cuda.is_available())"
```

## 4. Required inputs

The uploaded archive did not contain the project dataset. The code references input files including:

```text
Returns_Data.csv
GARCH11_Volatility_Data.csv
RollingDY_Results.csv
Gold_Oil_USD.csv
AIQ ETF Stock Price History.csv
```

The complete required set depends on the workflow. Inspect the selected script before execution.

## 5. Outputs

The scripts generate CSV tables and figures such as connectedness matrices, rolling spillover results, forecasts, model comparisons, SHAP importance, and diagnostic plots. Generated datasets/results are ignored by `.gitignore` by default.


