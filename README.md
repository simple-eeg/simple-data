# SIMPLE data

This repository accompanies **SIMPLE: a workflow for reviewable and traceable
analysis of single-trial EEG**. It provides a synthetic EEG example, the saved
Petal statistical analyses, and selected numerical data underlying the
manuscript figures.

## Choose a starting point

| Folder | Contents | Use it to |
| --- | --- | --- |
| [Synthetic EEG](synthetic-eeg/README.md) | 31 synthetic recordings and their dataset list | Try the SIMPLE workflow without clinical recordings. |
| [JASP](jasp/README.md) | The Petal input CSV and saved JASP analysis file | Inspect the statistical data, settings, results, and plots. |
| [Figure source data](figure-source-data/README.md) | Oxford and Strasbourg quality-control measurements and fitted EEG response magnitudes, with a guide to every manuscript figure | Find the measurements used in a figure and the relevant columns and selection rules. |

Each folder has a README and a `data/` directory. The data files retain their
original names and contents. The figure guide links to the JASP files and
software templates where they provide the relevant source, so these are not
duplicated in the figure folder.

## Download and open the files

On this repository's GitHub page, select **Code → Download ZIP**, then extract
the downloaded file. Open one of the three folders above and follow its README.

CSV files are tables that can be read in a spreadsheet application or a
programming language. Open the `.jasp` file in [JASP](https://jasp-stats.org/),
the statistical software used for these analyses, to inspect the saved results
and settings. Use MATLAB and EEGLAB with SIMPLE to work through the synthetic
example.

## Scope

The clinical tables contain derived measurements and screening indicators
from Petal (Oxford) and NOCI-Prem (Strasbourg). Clinical EEG recordings are not
included. The [figure guide](figure-source-data/README.md) identifies which
panels are covered and which waveform-derived data are not included, including
the numerical data behind the group-average plots in Figure 3's first three
rows.

## Related software

- [simple](https://github.com/simple-eeg/simple): the shared workflow and
  synthetic tutorial.
- [simple-synthetic-eeg-generator](https://github.com/simple-eeg/simple-synthetic-eeg-generator):
  the code that creates the synthetic example.
- [simple-oxford](https://github.com/simple-eeg/simple-oxford): the Petal workflow
  and downstream analyses.
- [simple-strasbourg](https://github.com/simple-eeg/simple-strasbourg): the
  NOCI-Prem workflow and descriptive checks.

## Licence and attribution

The data and documentation in this repository are licensed under
[Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE). You may
copy, adapt, and redistribute them, including for commercial use. Credit the
SIMPLE project contributors, link to this repository and the licence, and
indicate any changes.
For scholarly work, please also cite the accompanying SIMPLE paper.

The four software repositories use Apache 2.0 for code. The three analysis
repositories use CC BY 4.0 for their NRF template data; see their licence notices
for the scope.
