# bioTS-ML-Biomedical-Time-Series-ML

# ECG Recurrence Plot Analysis with the MIT-BIH Arrhythmia Database

This repository demonstrates how to download, preprocess, and analyze ECG signals from the widely used **MIT-BIH Arrhythmia Database**, culminating in the creation of **recurrence plots** to reveal hidden dynamics in cardiac time series.

---

## 🚀 Project Overview

Electrocardiogram (ECG) signals often contain nonlinear patterns and subtle dynamics that standard time-domain plots can miss. This project:

1. **Downloads** raw ECG records from the MIT-BIH Arrhythmia Database using the `wfdb` Python package.  
2. **Loads & normalizes** the multi-lead ECG time series.  
3. **Extracts** a segment of interest from the signal.  
4. **Generates** a Recurrence Plot (RP) using `pyts` to visualize recurrences in phase space.  

Recurrence plots can help detect arrhythmias, noise, and other dynamical behaviors in cardiac data, making them a valuable tool for research and clinical decision support.


