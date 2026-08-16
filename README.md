# AI, Robotics, Clean Energy & Macroeconomic Spillover Analysis

A research codebase for studying connectedness, spillovers, forecasting, and model comparison across artificial intelligence, robotics, clean-energy, and macroeconomic market variables. The repository combines traditional econometric connectedness methods with machine-learning forecasting models, including LSTM, GRU, and KAN-based hybrids.

## Project scope

The supplied scripts cover:

- Descriptive statistics and correlation analysis
- Diebold-Yilmaz (DY) connectedness and spillover measures
- Rolling connectedness
- TVP-VAR analysis
- Quantile VAR (QVAR) analysis
- Wavelet and quantile-based dependence analysis
- Machine-learning forecasts of connectedness and net spillovers
- LSTM-KAN hybrid forecasting
- Model comparison, Diebold-Mariano tests, SHAP analysis, and ablation studies

## Variables

The supplied `Data_Description.txt` groups the study variables into four clusters:

| Cluster | Variables |
| --- | --- |
| AI & technology | THNQ, ROBT, SRVR |
| Critical minerals & infrastructure | REMX, NCLR |
| Clean energy & sustainability | ICLN, GRNB, SUSA, CRBN, DSI |
| Macroeconomic controls | WTI, GLD, USD |

The forecasting scripts also use AIQ and derived targets such as `TCI`, `Net_AIQ`, `Net_ROBT`, and `Net_ICLN`, depending on the workflow.

## Repository structure

```text
.
├── connectedness_analysis.py
├── new05062026.py
├── paper_analysis25062026.py
├── spillover_ml_paper.py
├── lstm_kan_hybrid.py
├── lstm_kan_pipeline.py
├── Data_Description.txt
├── model/
├── requirements.txt
├── DEPLOYMENT.md
└── .gitignore
```

### Main scripts

| File | Purpose |
| --- | --- |
| `connectedness_analysis.py` | End-to-end econometric connectedness analysis with descriptive statistics, DY, rolling DY, TVP-VAR, QVAR, QQ, and wavelet outputs. |
| `new05062026.py` | Focused connectedness/spillover workflow for robotics, clean energy, gold, oil, and USD. |
| `paper_analysis25062026.py` | Paper-oriented analysis and table/figure generation. |
| `spillover_ml_paper.py` | Machine-learning forecasting of connectedness and spillover targets, including GRU/KAN-related comparisons and SHAP outputs. |
| `lstm_kan_hybrid.py` | LSTM-KAN hybrid forecasting workflow. |
| `lstm_kan_pipeline.py` | Utility code for forecast-error and Diebold-Mariano evaluation. |

## Data requirements

The uploaded archive does **not** contain the input dataset files referenced by the Python scripts. The scripts reference CSV files including:

```text
Dataset/
├── Returns_Data.csv
├── GARCH11_Volatility_Data.csv
├── RollingDY_Results.csv
├── Gold_Oil_USD.csv
├── AIQ ETF Stock Price History.csv
└── ...
```

The exact file set varies by script. Put the required CSV files in `Dataset/` and update the data/output path variables in the selected script before running it.

The original code uses Windows-specific paths such as `D:\Thesis\Imtiaz\Saeed shb\Dataset`. Change these to paths on your machine or refactor them to repository-relative paths/environment variables.

## Installation

Python 3.10+ is recommended. Create a virtual environment and install the dependencies:

```bash
python -m venv .venv

# Windows PowerShell
.venv\Scripts\Activate.ps1

# Linux/macOS
source .venv/bin/activate

pip install --upgrade pip
pip install -r requirements.txt
```

For GPU training, install the PyTorch build appropriate for your CUDA environment. The ML scripts automatically select CUDA when PyTorch reports a compatible GPU.

## Running

For the main econometric workflow:

```bash
python connectedness_analysis.py
```

Other workflows include:

```bash
python paper_analysis25062026.py
python spillover_ml_paper.py
python lstm_kan_hybrid.py
```

Check the configuration section near the top of the selected script and update input/output paths first.

## Model artifacts

The supplied `model/` directory contains serialized model state/configuration artifacts from the original project and is included in this repository package. If the model directory grows substantially, consider Git LFS for future model versions.

## Reproducibility

Complete reproducibility depends on Python and dependency versions, the PyTorch build, CUDA/cuDNN when using a GPU, the exact input data, random seeds, and model configuration.

## Deployment

This is a research/batch-analysis project rather than a web application. Deployment means preparing a reproducible Python environment, supplying the required dataset, configuring paths, and executing the relevant workflow. See [`DEPLOYMENT.md`](DEPLOYMENT.md).

## License

No license was included in the supplied archive. Add a suitable `LICENSE` file before making the repository public if you want to define reuse and redistribution terms.
