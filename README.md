# EDA1 — Steam Games Exploratory Data Analysis

> A first-ever Exploratory Data Analysis (EDA) project, examining the Steam gaming platform catalogue using a large real-world dataset sourced from Kaggle.

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Dataset](#dataset)
3. [Goals & Research Questions](#goals--research-questions)
4. [Repository Structure](#repository-structure)
5. [Technologies & Dependencies](#technologies--dependencies)
6. [Setup & Installation](#setup--installation)
7. [Running the Notebook](#running-the-notebook)
8. [Analysis Summary](#analysis-summary)
9. [Key Findings (so far)](#key-findings-so-far)
10. [Limitations & Known Issues](#limitations--known-issues)
11. [Future Work](#future-work)
12. [Acknowledgements](#acknowledgements)

---

## Project Overview

This repository contains a Jupyter Notebook-based Exploratory Data Analysis of the Steam digital game store catalogue.  
It is the author's **first data analysis project**, written in Python using standard data-science libraries.

The aim is to practise and demonstrate the full EDA workflow:
- loading and inspecting raw data,
- cleaning and transforming columns into usable types,
- selecting a meaningful subset of features,
- producing visualisations to answer concrete questions about the Steam library.

The project is intentionally kept beginner-friendly and self-contained inside a single notebook (`EDA0.ipynb`).

---

## Dataset

| Property | Detail |
|---|---|
| **Source** | [Kaggle — Steam Games Dataset](https://www.kaggle.com/datasets/fronkongames/steam-games-dataset/data) by *fronkongames* |
| **File** | `games.csv` (not committed to the repository — download separately, see [Setup](#setup--installation)) |
| **Rows** | ~122 611 Steam game entries |
| **Format** | CSV with a comma separator |

### Columns used in the analysis

| Column | Type | Description |
|---|---|---|
| `AppID` | int | Unique Steam application identifier |
| `Name` | string | Game title |
| `Release date` | datetime | Date the game was published on Steam |
| `Estimated owners` | string | Bracketed owner count estimate (e.g. `"20000 - 50000"`) |
| `Price` | float | Current price in USD |
| `Supported languages` | string | List of languages the game supports |
| `Windows` | bool | Whether the game runs on Windows |
| `Mac` | bool | Whether the game runs on macOS |
| `Linux` | bool | Whether the game runs on Linux |
| `Metacritic score` | int | Metacritic review score (0 if not rated) |
| `User score` | int | Steam user review score (0 if not rated) |
| `Achievements` | int | Number of Steam achievements |
| `Average playtime forever` | int | Average total playtime across all owners (minutes) |
| `Categories` | string | Steam store categories (e.g. "Single-player", "Multi-player") |
| `Genres` | string | Steam store genres (e.g. "Action", "Indie") |

> **Note:** The original CSV contains a missing comma in the header row. This is a known data-quality issue that required extra attention during the initial loading step.

---

## Goals & Research Questions

The analysis targets five concrete questions:

1. **Platform distribution** — Which operating system (Windows, macOS, Linux) has the most supported games on Steam? (Spoiler: Windows dominates by a large margin.)
2. **Price vs. review scores** — Is there a measurable correlation between a game's price and the scores it receives from critics (Metacritic) or users?
3. **Releases & scores over time** — How has the number of new game releases evolved year by year, and has average review quality improved or declined?
4. **Estimated owners vs. average playtime** — Do games with more owners also tend to have higher average playtimes, or is ownership count a poor predictor of engagement?
5. **Release date vs. price** — Have games released more recently become more expensive, suggesting price inflation in the digital games market?

---

## Repository Structure

```
EDA1_Steam_Games/
├── EDA0.ipynb          # Main Jupyter Notebook containing all analysis
├── requirements.txt    # Python dependency list
└── README.md           # This file
```

> The `games.csv` data file is **not** included in the repository. It must be downloaded separately (see [Setup](#setup--installation)).

---

## Technologies & Dependencies

| Library | Purpose |
|---|---|
| [Python 3](https://www.python.org/) | Core language (developed with Python 3.12) |
| [pandas](https://pandas.pydata.org/) | Data loading, cleaning, and transformation |
| [NumPy](https://numpy.org/) | Numerical operations and array manipulation |
| [Matplotlib](https://matplotlib.org/) | Low-level plotting |
| [Seaborn](https://seaborn.pydata.org/) | High-level statistical visualisations |
| [Jupyter Notebook](https://jupyter.org/) | Interactive notebook environment |

Versions confirmed working during development:
- pandas **2.2.3**
- NumPy **2.3.1**
- Seaborn **0.13.2**

---

## Setup & Installation

### 1. Clone the repository

```bash
git clone https://github.com/Drag0neUsz/EDA1_Steam_Games.git
cd EDA1_Steam_Games
```

### 2. Create and activate a virtual environment (recommended)

```bash
python -m venv .venv
# Linux / macOS
source .venv/bin/activate
# Windows
.venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install pandas numpy matplotlib seaborn jupyter
```

> If a populated `requirements.txt` is provided in the future, use:
> ```bash
> pip install -r requirements.txt
> ```

### 4. Download the dataset

1. Visit the Kaggle dataset page: <https://www.kaggle.com/datasets/fronkongames/steam-games-dataset/data>
2. Download `games.csv`.
3. Place the file in the **root directory** of the cloned repository (next to `EDA0.ipynb`).

---

## Running the Notebook

Launch Jupyter and open the notebook:

```bash
jupyter notebook EDA0.ipynb
```

Then execute cells sequentially from top to bottom using **Shift + Enter**, or use **Run All** from the *Cell* menu.

Alternatively, if you prefer JupyterLab:

```bash
jupyter lab EDA0.ipynb
```

---

## Analysis Summary

The notebook (`EDA0.ipynb`) is organised into the following sections:

### 1. Imports & version check
Imports all required libraries and prints their versions for reproducibility.

### 2. Data loading & selection
Reads `games.csv` using `pandas.read_csv`, selecting only the 15 relevant columns listed above. Prints a `DataFrame.info()` summary showing 122 611 rows and column types.

### 3. Data cleaning
- Converts the `Release date` column from a raw string to a proper `datetime64` type using `pd.to_datetime` with `errors="coerce"` (invalid dates become `NaT`).
- Drops rows where `Name` or `Release date` are missing (1 row dropped, leaving 122 610 clean entries).

### 4. Platform comparison
Counts how many games support each operating system by summing the boolean `Windows`, `Mac`, and `Linux` columns. Renders a bar chart (Seaborn) comparing OS support counts.

**Upcoming sections (in progress):**
- Price vs. review score scatter/correlation plots
- Yearly release counts and average scores over time
- Estimated owners vs. average playtime analysis
- Release year vs. price analysis

---

## Key Findings (so far)

| Metric | Value |
|---|---|
| Total games analysed | 122 610 |
| Windows-supported games | 122 566 (~100 %) |
| macOS-supported games | 21 292 (~17 %) |
| Linux-supported games | 15 706 (~13 %) |

Windows is the overwhelmingly dominant platform on Steam, with macOS and Linux titles representing only a fraction of the catalogue — a result consistent with broader PC gaming market-share data.

---

## Limitations & Known Issues

- **Missing comma in CSV header** — The original `games.csv` contains a missing comma in its header row. This was discovered during initial exploration and must be kept in mind when loading with `pd.read_csv`.
- **`Estimated owners` as a string range** — Values such as `"20000 - 50000"` require additional parsing before numeric analysis can be performed.
- **Zero-valued scores** — Many games have a `Metacritic score` or `User score` of 0, which typically means *not rated*, not an actual score of zero. These entries should be filtered out before any score-based analysis.
- **Dataset snapshot** — The Kaggle dataset is a point-in-time snapshot of the Steam catalogue and may not reflect the current state of the store.

---

## Future Work

- Complete the remaining four research questions with corresponding visualisations.
- Parse `Estimated owners` into numeric midpoints or ranges for quantitative analysis.
- Filter out unscored games (score = 0) before computing correlations.
- Add a dedicated data-cleaning section that documents all transformations.
- Export final charts as PNG/SVG for use in reports or presentations.
- Potentially extend the analysis to genre-level breakdowns (e.g. which genres command higher prices?).

---

## Acknowledgements

- Dataset by **fronkongames** on Kaggle: [Steam Games Dataset](https://www.kaggle.com/datasets/fronkongames/steam-games-dataset/data)
- Steam store data is property of [Valve Corporation](https://www.valvesoftware.com/).
- Built with [PyCharm](https://www.jetbrains.com/pycharm/) and the Jupyter Notebook integration it provides.
