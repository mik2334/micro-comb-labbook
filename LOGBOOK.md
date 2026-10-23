# Electronic Project Log

Short, dated summaries of each coding session. Full reasoning, calculations and interpretations are in the physical lab book; page numbers are given for each entry. 

> Entries dated before 07/10/2026 were written up on 07/10/2026 when this
> log was moved to its own public repository. From 07/10/2026 onwards, entries
> are added at the end of each session.

===============================================================

## 02-10-2026 - SESSION: Project Setup
- Created repository and folder structure
- Set up Python environment (see environment.yml)
- Lab book p. 1-3: front matter and repo details.
- Code commit: [6c468fb]

## 05-10-2026 - READING: Pasquazi et al. 2018, micro-combs review
- Notes: 'reading/pasquazi2018_microcombs-review.md'
- Lab book p. 7-8

## 06-10-2026 - MEETING: Supervisor & Co-supervisor
- Discussed: keep data private, attempt to make electronic lab book public and code private; equations governing setup in lab contains more than LLE
- Agreed: electronic lab book to be public, code private
- Actions: load given data using MATLAB to Python libraries and observe behaviour; read provided "minimal observables" paper; research neural network methods. 
- Lab book p. 9 (signed)

## 07-10-2026 - SESSION: Split into public lab book + private code repositories 
- Created public "micro-comb-labbook" repo; moved 'LOGBOOK.md' from code repo and added 'reading/' to the lab book repo
- Confirmed code repo is private
- Updated both READMEs; set up VS Code workspace with both repos.
- Commits: code [c96a628]

## 08-10-2026 - READING: Suresh et al. 2026, Minimal observables for discriminating laser cavity solitons in a microresonator-filtered fibre laser
- Notes: 'reading/suresh2026_minimal-observables.md'
- Lab book p. 10-11
- Commit: same as 09-10-2026, [cf1b48c]

## 09-10-2026 - SESSION: Data test
- downloaded mat73 Python library to upload MATLAB data into Python
- Added code to upload and print data keys and values ("09-10-2026_data_load_test.ipynb")
- test successful 
- Commit: code [cf1b48c]

## 11-10-2026 - SESSION: Data understanding
- loaded the data from MAP00 into a notebook ("11-10-2026_data_check_test.ipynb")
- compared the pump range/increments and delay values with the Suresh paper - values are consistent
- printed the meta data to understand the layout of the values: for the nPump x nDelay grid, each cell has two graphs for both OSA measurements and Photodiode measurements
- data stucture is now understood, next step is to visualise and observe behaviours 
- Lab book p. 12
- Commit: code [4df4162]

## 14-10-2026 - SESSION: Visualising data to discriminate states
- data loaded from MAP00 ("14-10-2026_data_visualise.ipynb")
- 'osa_axis' used as x-axis for the OSA measurements, with 'OSAS' as the y-axis values
- 'PDtime' plotted as a function of index number (100,000 values)
- both plotted on the same subplots, 2 plots for each experimental configuration
- 5 cells chosen to span the grid, one row per cell, spectrum and trace side by side, (0,0), (0,100), (25, 50), (50, 0), (50, 100)
- loaded for future discrimination after the following reading, will repeat for different maps
- Next: read Bao et al. 2019, then label each cell by eye
- Lab book p. 13
- Commit: code [3c8c9f1]

## 14-10-2026 - READING: Bao et al. 2019, Laser cavity-soliton microcombs 
- Notes: 'reading/bao2019_laser_cavity_solitons.md'
- Lab book p. 15
- Commit: code [ab27142]

## 15-10-2026 - MEETING: Supervisor & Co-supervisor
- Discussed: what extent of physics knowledge is required for this project; what metrics are used within the project; what data to input and what features to use for the model
- Agreed: create a FT of the PD trace into an RF spectrum; understand physics of the experimental setup rather than fully understanding how states arise; understand states qualitatively
- Actions: required to provide model/feature analysis and comparison - why the implemented model is used, why the chosen features are used and how they affect performance; map the data using pump power and delay as shown in the "Minimal Observables" paper (Fig. 3); aim of the model is to create a map similar to this, based on discrete classifications rather than a continuous index.
- Next Steps: research neural network models; FT the PD data; map out data 
- Lab book p. 16 (signed)
- Commit: code [ff64517]

## 17-10-2026 - SESSION: Planning Project Structure
- Model input = measured spectra (OSA + RF); pump/delay only position predictions on the map
- Proposed three-part comparison (confirm with supervisors): Suresh metrics = thresholds (benchmark, labels) -> ML using the six metrics -> neural networks on the raw spectra
- Labels from metrics; split by delay columns; circularity handled with a hand-checked test set
- Lab book p. 17

## 17-10-2026 - SESSION: RF Spectra and Suresh metrics for all cells
**Metrics**
- Code: 'src/metrics.py' ('rf_spectrum', 'rf_metrics', 'spectral_moment', 'osa_metrics'), 'src/plotting.py' ('plot_spectra'); notebook '17-10-2026_RF_spectra_metrics.ipynb'
- RF spectrum: 'rfft' of each PD trace; 100,000 samples, 5KHz resolution, 0-250MHz
- Metrics per Suresh eqs 1-4: sigma, P_AC, p_AC (f_L = 20MHz); N (using 'find_peaks', prominence = 10dB, distance = 15); second-order moment, fourth-order moment (1520-1575nm)
- Bugs fixed: AC mask ('freq > 0'); peak-finding settings added
- Open: second- and fourth-order moments dominated by background, need to agree of noise floor method with supervisor 

**Results**
- Key results: all 5,151 cells computed -> 'data/MAP00_metrics.npz' (metrics (51, 101, 6); RF 0-20MHz (51,101,4001))
- Heatmaps + histograms of all six metrics ('pcolormesh', log_10 P_AC/p_AC, log counts)
- Started N vs sigma (Suresh Fig. 4) with 20kHz boundary

**Evaluation Plan**
- All three methods scored as classifiers on the same test set, with an independent reference (hand-checked cells; paper's Fig. 4 classification if available)
- Metrics: confusion matrix; per-class precision; will need to research more

- Next: finish any missing plots, choose appropriate thresholds based on the paper, label cells; week 4: research classification methods
Lab book p.17-25
- Commit: code [d6803e2]

## 20-10-2026 - SESSION: Recreating Suresh Fig. 4
**Code** 
- 'compute_metrics' in 'src/metrics.py': returns a dict of metrics, cropped RF spectra, axes, names and settings (taken from the argument)
- 'plot_spectra', 'plot_metric_maps', 'plot_N_vs_RF' in 'src/plotting.py': all return 'fig'

**Fig. 4 recreation (MAP00)**
- N on x, RF metric on y (sigma is linear); paper's layout: vertical CW line + diagonal soliton line, "other" inbetween; paper calls these provisional "pre-cluster labels"
- Physical basis: CW = few lines regardless of noise; soliton = many lines + low noise, tolerance rising with N
- Prominence 10 -> 8: max N ~90 -> ~105 (paper has ~115), cluster structure unchanged ; CW still N ~ 0-10 (paper has ~5)
- Draft separators (provisional): CW at N = 8; σ (35, 0)→(105, 350 kHz); log P_AC (25, −5.2)→(95, −0.4); log p_AC (20, −5.75)→(90, −0.3)

**MAP01 / MAP02 follow same settings**
- Higher RF floor suggests different acquisition settings ; no strongly incoherent states; sharp split at N ~ 50
- MAP00 separators don't transfer (consistent with the paper's proposed caveat that thresholds are device/condition specific)

**Evaluation Design** 
- Training labels from method 1; blind by-eye test labels; all three methods scored against them; settings and lines set before final evaluation 
- Multi-map options: (A) core on MAP00, others as generalisation test; (B) all maps with normalisation, leave one test map out

**QUESTIONS**
- What are MAP01/02 and why is their noise floor higher; paper's N counting and moment calculation settings; one map vs all three

Next Steps:
- Set settings for find_peaks and moments and leave untouched (ask supervisor); re-run settings for MAP00 and set lines; check MAP01/02 in metadata (if there is metadata); heatmaps + example spectra for MAP01/02
- Commit: code [4b6e47e]

## 22-10-2026 - MEETING: Supervisor and Co-supervisor
**Written on 23-10-2026 following the meeting notes**

**Framing of project**
- The project should be treated as an exploration of what makes a good machine-learning approach for classifying the comb states, carried out and discussed over the 18 weeks. Do not think of it as a single method to be proven
- The aim is to assess which method specifics (labelling, classes, preprocessing, model) produce a "good" classifier, and to justify those choices with evidence

**Points discussed**
1. Labelling
    - Test whether the Suresh et al. (2026) thresholds give good labels for method 1 (rule-based) and method 2 (ML on metrics)
    - If they do not, label the data by eye and train/test on those labels
    - Stated clearly that labelling must be consistent between training and testing data
2. Maps
    - MAP00, MAP01 and MAP02 are the same measurements at different frequency resolutions
3. Classes
    - Decide which classes and how many e.g. soliton/CW/other, or split "other" into more classes
4. Class-related mitigation strategies
    - Strategies for class imbalance (rare states being under-represented), e.g. class weighting, resampling, and choosing metrics that expose poor performance on rare classes
5. Normalisation/scaling
    - Some data "normalisation" so the model can handle data at different scales. This links to the different frequency resolutions and to intensity of scaling spectra

**Decisions**
- The three-method comparison (rules/ML metrics/NN on raw spectra) stays, but as one part of a wider exploration 
- The project is organised around research questions on the points discussed above

**Implications from meeting**
- Because all maps contain the same physical points, the maps are not independent test sets. Training on MAP00 and testing on MAP01 would test on the same states (data leakage). Splits must be by location on each respective map, with the same split used at every resolution.
- Labels describe the physical state, not the resolution, so one label set can be applied to all three maps

**Actions**
- Confirm the resolutions of MAP01/MAP02

- Lab book p. 26-29(signed)
- Commit: code []

