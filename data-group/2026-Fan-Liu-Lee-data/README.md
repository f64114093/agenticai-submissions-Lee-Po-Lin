# Data: ECG Pan-Tompkins Processing Dataset

**Group:** 2026-Fan-Liu-Lee
**Members:** Cheng-Yu Fan, Wu-Jun Liu, Po-Lin Lee
**License:** CC-BY-4.0 

---

## Source

This dataset is derived from the **Heartbeat Sounds / ECG dataset** available on Kaggle, which is originally based on the MIT-BIH Arrhythmia Database.

**Original Dataset:**  
* **Dataset Name:** Heartbeat Sounds / ECG dataset
* **Author:** Shayan Fazeli
* **URL:** https://www.kaggle.com/datasets/shayanfazeli/heartbeat
* **Original License:** [Please Check Kaggle and insert here, e.g., MIT License / CC0]

---

## Statistics

| Property | Value |
|----------|-------|
| **Subjects** | Pooled subjects (derived from MIT-BIH) |
| **Demographics** | Anonymized / Mixed |
| **Data Length** | ~600 heartbeats (concatenated) |
| **Sampling Rate** | 125 Hz |
| **Conditions** | Arrhythmia / Normal (Mixed) |
| **Total Duration** | [Insert total seconds here, e.g., 480 seconds] |

---

## Data Description

This submission contains ECG signals **before and after signal processing** using the **Pan-Tompkins R-peak detection algorithm**.

The purpose of this dataset is to demonstrate ECG preprocessing, noise filtering, and R-wave peak detection for AI agent system development and signal analysis experiments.

---

## Folder Structure

2026-Fan-Liu-Lee/
├── README.md
├── raw/
│ └── mitbih_test.csv
├── processed/
│ └── pan_tompkins_output.csv
└── metadata.json (optional)

### Format & Files

#### 1. `mitbih_test.csv` (Raw)
* **Description:** Raw ECG beat segments loaded from the Kaggle source.
* **Format:** CSV, no header in original file (processed as arrays).

#### 2. `pan_tompkins_output.csv` (Processed)
This file is generated after applying signal filtering and R-peak detection.

| Column | Type | Unit | Description |
|--------|------|------|-------------|
| `Time_Seconds` | float | s | Time axis generated at 125Hz |
| `ECG_Raw` | float | mV | Raw ECG signal (concatenated) |
| `ECG_Filtered` | float | mV | Signal after Bandpass filter |
| `R_Peak_Marker` | int | Binary | 1 = Detected R-peak, 0 = Non-peak |

---

## Preprocessing

The following preprocessing steps were applied using Python and NeuroKit2:

1.  **Data Loading:** Loaded raw ECG beats from `mitbih_test.csv`.
2.  **Concatenation:** The first **600 ECG segments** were concatenated to simulate a continuous signal.
3.  **Resampling:** A time axis was generated assuming a sampling rate of **125 Hz**.
4.  **Cleaning:** Applied `nk.ecg_clean` (Biosppy method) using a Bandpass filter (0.5-40 Hz) to remove baseline wander and high-frequency noise.
5.  **Peak Detection:** R-peaks were identified using the **Pan-Tompkins algorithm**.
6.  **Labeling:** Generated a binary marker column aligned with the time axis.

---

## Privacy Statement

**CRITICAL: No Personally Identifiable Information (PII)**

* This dataset contains no personally identifiable information.
* All ECG signals are derived from a public, anonymized Kaggle dataset.
* No subject names, IDs, or sensitive personal data are included.
* Data is used strictly for academic and educational purposes.

---

## Usage

### Load the processed ECG data

```python
import pandas as pd

df = pd.read_csv("processed/pan_tompkins_output.csv")

time = df["Time_Seconds"]
ecg_filtered = df["ECG_Filtered"]
r_peaks = df["R_Peak_Marker"]

print(f"Loaded {len(df)} samples.")
```

---

## Visualization (Excel)

To quickly inspect the ECG waveform using Microsoft Excel: 
1. Download pan_tompkins_output.csv 
2. Open the file with Excel 
3. Select column ECG_Filtered 
4. Click Insert → Line Chart 
5. The filtered ECG waveform will be displayed 
This provides a simple visual validation of the ECG preprocessing results.

---

## Tools & Environment

Google Colab 
Python 3 
NeuroKit2 
Pandas 
NumPy

---

## License

Dual Licensing Model:

1. Original Data (mitbih_test.csv): Subject to the original license provided by Shayan Fazeli on Kaggle (MIT License/Public Domain). We do not claim ownership of the raw data.
2. Processed Data & Documentation (pan_tompkins_output.csv, README.md): Released by the authors (Group 2026-Fan-Lee-Liu) under CC-BY-4.0.