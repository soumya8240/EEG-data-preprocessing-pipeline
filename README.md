# EEG Preprocessing Tutorial with EEGLAB in MATLAB 🧠

**A step-by-step video tutorial for preprocessing resting-state EEG recordings using EEGLAB in MATLAB.**

This tutorial demonstrates a practical preprocessing workflow using **32-channel resting-state EEG data from patients with Parkinson's disease**. The goal is to prepare raw EEG recordings for downstream analyses by reducing artifacts and improving signal quality.

## What you'll learn

- How to set up and open EEGLAB in MATLAB
- How to inspect and prepare EEG channels and electrode locations
- How to filter and resample resting-state EEG recordings
- How to use Independent Component Analysis (ICA) to help identify artifacts
- How to inspect and reject artifact-related components and re-reference the cleaned data

## Tools and data

| Item | Description |
| --- | --- |
| Software | MATLAB and the EEGLAB toolbox |
| Recording type | Resting-state EEG |
| Example dataset | Parkinson's disease EEG recordings |
| EEG channels | 32 |
| Original sampling rate | 512 Hz |
| Resampled rate | 250 Hz |
| Band-pass filter | 0.5–70 Hz |
| Power-line filtering | 60 Hz notch filter (US recording setting) |
| Artifact handling | ICA with visual component inspection |

> **Data privacy:** Patient recordings are not included in this repository unless explicitly permitted by the dataset's access and sharing terms.

## Preprocessing workflow

| Step | Procedure | Purpose |
| --- | --- | --- |
| 1 | Add **EEGLAB** to the MATLAB path and launch it | Set up the EEG processing environment |
| 2 | Remove slow baseline drift | Reduce slow fluctuations in the recordings |
| 3 | Exclude auxiliary **EXG channels** from the EEG-channel analysis | Focus on the EEG channels used in this workflow |
| 4 | Import the **32-channel 10–20 electrode location file** | Associate EEG channels with scalp electrode positions |
| 5 | Apply a **0.5–70 Hz band-pass filter** | Attenuate frequencies outside the selected analysis range |
| 6 | Apply a **60 Hz notch filter** | Reduce mains electrical interference |
| 7 | Resample from **512 Hz to 250 Hz** | Reduce data size and computational cost |
| 8 | Run **Independent Component Analysis (ICA)** | Decompose the recordings into statistically independent components |
| 9 | Inspect **scalp topographies, power spectra, and component activity heatmaps**, then reject artifact-related components | Identify and remove likely non-neural contamination |
| 10 | **Re-reference** the cleaned EEG | Apply the selected reference montage for downstream analysis |

### Workflow at a glance

```text
Raw resting-state EEG (512 Hz)
           │
           ▼
Set up EEGLAB and inspect recordings
           │
           ▼
Drift handling and channel selection
           │
           ▼
Load 32-channel electrode locations
           │
           ▼
Band-pass (0.5–70 Hz) + 60 Hz notch
           │
           ▼
Resample to 250 Hz
           │
           ▼
ICA decomposition
           │
           ▼
Inspect and reject artifact components
           │
           ▼
Re-reference cleaned EEG
           │
           ▼
EEG ready for subsequent analysis
```

## Getting started

1. Install **MATLAB** and download **[EEGLAB](https://sccn.ucsd.edu/eeglab/)**.
2. Add the EEGLAB directory to your MATLAB path and launch EEGLAB. For example:

   ```matlab
   addpath('PATH_TO_EEGLAB'); % Replace with your local EEGLAB folder
   eeglab;
   ```

3. Load your EEG recording in EEGLAB, then follow the and the workflow above.
4. Adjust preprocessing parameters for your recording conditions, analysis goals, and dataset requirements.

## Important processing notes

- **Filtering and drift:** A 0.5 Hz high-pass cutoff already attenuates slow drift; an additional baseline-drift removal operation should be justified and documented to avoid unnecessary duplicate filtering.
- **EXG channels:** EOG/ECG or other auxiliary channels can be valuable for identifying eye, cardiac, and motion-related artifacts. Consider retaining them for artifact detection even if they are later excluded from EEG-only analyses.
- **ICA interpretation:** ICA separates components statistically; it does **not** by itself provide anatomical source localization. Reject components based on multiple lines of evidence rather than a scalp map alone.
- **Sampling:** Resampling from 512 Hz to 250 Hz should use appropriate anti-alias filtering (EEGLAB's resampling tools handle this). A 250 Hz rate has a Nyquist frequency of 125 Hz, above the 70 Hz selected upper cutoff.
- **Line noise:** A 60 Hz notch filter is relevant when the recording contains 60 Hz interference. Filter settings should be adapted to the local mains frequency and analysis needs.
- **Referencing:** The reference montage influences EEG signals. Record which re-reference method was used, and ensure the final data remain appropriate for your intended analyses.
- **Order and quality control:** The exact sequence of filtering, bad-channel handling, ICA, rejection, and re-referencing may vary across validated pipelines. Review signal quality before and after artifact removal.

## Potential next steps

After preprocessing, the cleaned EEG may be used for analyses such as:

- Power spectral density and frequency-band analysis
- Functional connectivity
- Time-frequency analysis
- Quantitative characterization of resting-state brain activity

These analyses are **not** covered by this preprocessing tutorial.

## Resources

- [EEGLAB official website](https://sccn.ucsd.edu/eeglab/)
- [EEGLAB documentation and tutorials](https://eeglab.org/tutorials/)

## Feedback and contributions

Suggestions for improving the workflow or explanations are welcome. Feel free to open a GitHub issue or discussion (if enabled) to share feedback.

## Acknowledgment

This tutorial is intended for **educational and research demonstration purposes**. Preprocessing settings are dataset-specific and should not be assumed to be optimal for every EEG study.
