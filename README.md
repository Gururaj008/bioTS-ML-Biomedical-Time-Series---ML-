# bioTS-ML
# Biomedical-Time-Series-ML

# ECG Recurrence Plot Analysis

This notebook implements end-to-end analysis of ECG signals from the MIT-BIH Arrhythmia Database, with a focus on generating and interpreting **recurrence plots** to uncover hidden temporal dynamics.

---

## 🗂️ Input

- **ECG Records**: Raw multi-lead ECG files (`.dat`, `.hea`) from the MIT-BIH Arrhythmia Database (e.g., record “100”).
- **Segment Parameters**: Start and end indices for the time window of interest (e.g., 100 000–101 000 samples) to focus on a specific cardiac cycle or arrhythmic event.
- **Recurrence Settings**:  
  - **Threshold type** (`point` or `distance`)  
  - **Percentage** of nearest neighbors to consider (e.g., 10 %).

---

## 🔄 Processing Steps

1. **Download & Load**  
   - Use the `wfdb` package to download selected records into `data/mitdb/`.  
   - Read the record with `wfdb.rdrecord()`, extract lead I signal (`record.p_signal[:, 0]`).

2. **Normalization**  
   - Compute mean and standard deviation of the chosen segment.  
   - Normalize:  
     ```python
     ecg_seg = ecg[start:end]
     ecg_norm = (ecg_seg - ecg_seg.mean()) / ecg_seg.std()
     ```

3. **Recurrence Plot Generation**  
   - Instantiate a `pyts.image.RecurrencePlot` transformer:  
     ```python
     from pyts.image import RecurrencePlot
     rp = RecurrencePlot(threshold='point', percentage=10)
     ```
   - Fit and transform the normalized signal into a 2D recurrence matrix:  
     ```python
     rp_matrix = rp.fit_transform(ecg_norm.reshape(1, -1))[0]
     ```

4. **Visualization**  
   - Display the binary recurrence matrix using Matplotlib:  
     ```python
     import matplotlib.pyplot as plt
     plt.imshow(rp_matrix, origin='lower')
     plt.title("Recurrence Plot (10% threshold)")
     plt.xlabel("Time index")
     plt.ylabel("Time index")
     plt.show()
     ```

---

## 📊 Output

- **Recurrence Plot**: A binary image of size _N×N_ (where _N_ = segment length), with black pixels indicating times at which the trajectory revisits a previous state within the defined threshold.
- **Quantitative Measures** (optional extensions):  
  - Recurrence rate, determinism, laminarity, etc., computed via pattern analysis on the recurrence matrix.

---

## 🔍 Interpretation & Inference

- **Diagonal Lines**: Long diagonals indicate periodic or repeating behavior—typical of healthy sinus rhythms.  
- **Interrupted/Scattered Patterns**: Gaps or fragmented diagonals suggest arrhythmias or ectopic beats.  
- **Vertical/Horizontal Structures**: Indicate laminar states or signal plateaus—helpful for detecting features like QT intervals.

By comparing recurrence plots across multiple segments or patients, researchers can:

1. **Detect Anomalies**: Spot abnormal heartbeats or transitions into arrhythmic regimes.  
2. **Quantify Complexity**: Use recurrence quantification analysis (RQA) metrics to measure signal regularity and complexity.  
3. **Assess Treatment Effects**: Visualize how interventions (e.g., medications, pacemakers) alter the heart’s dynamical patterns.

---

*This notebook provides a reproducible framework for exploring nonlinear dynamics in ECG data and can be extended to other biomedical or sensor-based time series.*  



