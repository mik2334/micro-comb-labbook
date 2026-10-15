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
- Commit: code []