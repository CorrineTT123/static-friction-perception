# static-friction-perception
Code and analysis associated with the study "Static friction expands the dimensionality of friction perception to enable tactile reality on screens".

# Static friction expands the dimensionality of friction perception to enable tactile reality on screens

This repository contains raw friction measurements, scanning electron microscopy (SEM) files, and Python analysis scripts associated with the study **“Static friction expands the dimensionality of friction perception to enable tactile reality on screens.”**

The files are stored in a single directory. They can be identified by the material abbreviation, friction regime, and file extension, as described below.

## Repository contents

### 1. Static- and dynamic-friction measurements

The `.xls` and `.xlsx` files contain the raw friction measurements used to characterize the material library in Fig. 2a, Extended Data Fig. 1, Extended Data Fig. 3, and the corresponding Supplementary figures.

- Filenames containing `static friction` or `static` contain measurements of the maximum static-friction coefficient.
- Filenames containing `dynamic friction` or `dynamic` contain measurements obtained during steady sliding.
- The material name or abbreviation appears at the beginning of each filename.
- For AAO and F-AAO, files labelled `with 0 and 250V DC` contain measurements collected under both 0 V and 250 V DC conditions and support the electroadhesion characterization presented in Extended Data Fig. 3.

Material names and abbreviations are retained as used in the manuscript and Supplementary Information. The identifiers represented in the filenames include `AAO`, `F-AAO`, `Acrylic`, `Al`, `Alc`, `Cu`, `CP`, `Glass`, `GP`, `MSS`, `NP`, `PE`, and `PET`.

### 2. SEM files

The `.zip` archives contain the original SEM files for the corresponding materials. Each archive is identified by the material name or abbreviation in its filename, such as `AAO.zip`, `F-AAO.zip`, `CP.zip`, and `glass.zip`. These files support the surface-characterization results reported in the manuscript and Supplementary Information.

### 3. Material-recognition data

`Table_S1_raw_data_static_dynamic_friction_material_recognition.csv` contains the trial-level static- and dynamic-friction material-recognition records used to calculate Table S1 and the relative behavioral cue contributions in Fig. 2i. This CSV is the public, merged version of the original local workbook named `subject trail.xlsx`.

### 4. Video calibration

`pixel_to_cm_ratio.txt` contains the spatial calibration factor used to convert displacement measured in video pixels into physical distance in centimetres. It is an input to `finger speed.txt`.

### 5. Python analysis scripts

The following three `.txt` files contain Python source code, not experimental data. They may be opened in a Python editor or renamed from `.txt` to `.py` before execution.

#### `calculate_relative_behavioral_cue_contribution.txt`

This script calculates the relative behavioral contributions of dynamic- and static-friction information reported in Fig. 2i, Supplementary Note 1, and Table S1.

The script:

- reads the trial-level static- and dynamic-friction recognition results;
- recalculates trial correctness by requiring an exact match between the presented and reported sequences;
- uses a nominal chance level of 25%, corresponding to the four permitted responses: A-A, A-B, B-A, and B-B;
- extracts the dynamic-cue condition with approximately matched static friction (`Dcue` and `S_equal`) and the static-cue condition with approximately matched dynamic friction (`Scue` and `D_equal`);
- converts participant-level accuracies into chance-corrected information scores;
- normalizes the two scores within each participant to obtain the relative dynamic- and static-friction contributions; and
- exports participant-level results, group summaries, plotting data, rechecked raw data, and calculation definitions to `relative_behavioral_cue_contribution.xlsx`.

The participant-level mean contributions reported in the manuscript are 57.8% for dynamic-friction information and 42.2% for static-friction information.

**Input-format note:** the archived script retains the original local setting `INPUT_FILE = "subject trail.xlsx"` and imports one participant from each Excel worksheet. The publicly shared `Table_S1_raw_data_static_dynamic_friction_material_recognition.csv` contains the corresponding records in a merged CSV table. To run the script directly with the public file, replace the Excel worksheet-import section with `pandas.read_csv()` while retaining the subsequent participant-level calculations.

#### `finger motion.txt`

This script performs video-based finger tracking using OpenCV and MediaPipe Hands. It is part of the analysis supporting the free-exploration results in Extended Data Fig. 2 and Figs. S3–S5.

The user selects the fingertip or another hand landmark in the video, after which the script tracks that landmark frame by frame. It uses the video frame rate to calculate movement speed in pixels per second and identifies stationary periods using a speed threshold and a minimum duration of 0.15 s.

Default inputs and outputs in the script are:

- input video: `2.mp4`;
- tracked video: `tracking_output.mp4`; and
- time-resolved speed data: `finger_speed_data.csv`.

The video path and analysis parameters should be changed in the user-settings section of the script when analysing another recording.

#### `finger speed.txt`

This is a related video-analysis script used to quantify fingertip motion during free material exploration. It tracks the index fingertip with MediaPipe, reads the spatial calibration from `pixel_to_cm_ratio.txt`, converts inter-frame displacement into speed in centimetres per second, and labels stationary and moving periods. These measurements support the separation of static-contact and dynamic-sliding periods and the calculation of the fraction of exploration time spent in static contact, `T_static/T_total`, shown in Extended Data Fig. 2.

Default inputs and outputs in the script are:

- input video: `2.mp4`;
- spatial calibration: `pixel_to_cm_ratio.txt`, which records the conversion factor from image pixels to centimetres;
- tracked video: `output_with_tracking.mp4`; and
- speed and state data: `finger_speed_cm_with_stop.csv`.

The output CSV contains time, raw speed, smoothed speed, and a binary stationary-state label. Some variable names and console messages in the script use the earlier terms `dwelling` and `sliding`; these correspond to `static contact` and `dynamic sliding`, respectively, in the manuscript.

## Software requirements

The behavioral-contribution script requires:

```text
Python 3
numpy
pandas
xlsxwriter
openpyxl
```

The finger-tracking scripts require:

```text
Python 3
opencv-python
mediapipe
numpy
matplotlib
```

The scripts were designed for use in common Python environments such as Anaconda, Spyder, or Jupyter. File paths and input filenames should be checked in the user-settings section before execution.

## File-naming convention

Most friction datasets follow the pattern:

```text
<material>_<friction regime>.<extension>
```

For example, `NP_static friction.xlsx` and `NP_dynamic friction.xlsx` contain the static- and dynamic-friction measurements for NP, respectively. Minor differences in capitalization, spacing, and wording reflect the original filenames produced during data collection and do not indicate different processing levels.

## Anonymization

Participant information has been anonymized. The repository does not contain directly identifying personal information.

## License

This repository is distributed under the terms specified in the `LICENSE` file.

## Citation

If you use these data or scripts, please cite the associated article and this repository:

> Tang, Y. *et al.* Static friction expands the dimensionality of friction perception to enable tactile reality on screens. Manuscript submitted for publication.

Repository: https://github.com/CorrineTT123/static-friction-perception

The article citation will be updated after publication.

