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
- Lab book p. 10
- Commit: same as 09-10-2026

## 09-10-2026 - SESSION: Data test
- downloaded mat73 Python library to upload MATLAB data into Python
- Added code to upload and print data keys and values
- test successful 
- Commit: code [cf1b48c]

## 11-10-2026 - Session: Data understanding
- loaded the data from MAP00 into a notebook 
- compared the pump range/increments and delay values with the Suresh paper - values are consistent
- printed the meta data to understand the layout of the values: for the nPump x nDelay grid, each cell has two graphs for both OSA measurements and Photodiode measurements
- data stucture is now understood, next step is to visualise and observe behaviours 
- Commit: code []