# Petal data and saved JASP analyses

This folder contains the participant-level table and saved statistical analyses
for the Oxford Petal application in the SIMPLE manuscript. The table has one
row for each of 104 participants and 28 columns. It contains derived EEG
measurements and study variables, not EEG recordings.

## Files

- [jasp_data_all.csv](data/jasp_data_all.csv): the table prepared by
  [SIMPLE Oxford](https://github.com/simple-eeg/simple-oxford) for import into JASP.
  It can also be read in a spreadsheet application or other statistical software.
- [jasp_data_all.jasp](data/jasp_data_all.jasp): the saved JASP project, containing
  the imported table, analysis settings, statistical results, and plots. Open it
  in [JASP](https://jasp-stats.org/) to inspect the saved work; inspecting the
  saved results does not require rerunning the analyses. Use a copy for new work.

Both files retain their original names and contents. The CSV preserves more
decimal places than JASP's embedded table: the numerical values agree to ten
significant digits, with matching category labels and missing values.

The [figure source-data guide](../figure-source-data/README.md) identifies the
columns used in each relevant figure and points to the additional pooled tables
for Petal and NOCI-Prem.

## Reading the columns

`subjectID` is the participant identifier. Keep it as text when importing the CSV
so that leading zeros are preserved.

Measurement names beginning with `HL_BL_` refer to the internal-reference epoch;
names beginning with `HL_ER_` refer to the true heel-lance event epoch. Each
prefix is followed by a QC feature name or an NRF magnitude name.

The nine QC features are `maxAbsEpoch`, `sdEpoch`, `invSdEpoch`,
`MeanAbsDiffNorm`, `MaxAbsDiffNorm`, `RobustSlopeNorm`, `AutoCorrLag1Pos`,
`AutoCorrLag1Neg`, and `KatzFDNorm`. Each has one internal-reference column and
one true-event column, giving 18 QC columns. For example, `HL_ER_maxAbsEpoch`
contains maximum absolute amplitude for the true-event epoch. Feature
definitions are given in the manuscript's Supplementary Table 5 and in the
[Oxford QC calculations](https://github.com/simple-eeg/simple-oxford/blob/main/functions/quality_control_features.m).

The four columns ending in `eNRF_mag` or `nNRF_mag` contain fitted response
magnitudes in microvolts (µV). The e-NRF describes the early sensory response,
and the n-NRF describes the later noxious-evoked response. These magnitudes are
the `fglsCoef` values from the pooled NRF table; the stored NRF template vectors
themselves are dimensionless.

| Study or analysis column | Meaning |
| --- | --- |
| `trial_arm` | `Control` or `Intervention`; 54 and 50 participants, respectively. |
| `HL_sleep_state` | Pre-heel-lance state, `Asleep` or `Awake`; 75 and 29 participants across the full table. |
| `HL_ER_nNRF_mag_Screening` | Current true-event retention: `Included` for 99 participants and `Excluded` for five. |
| `HL_ER_nNRF_mag_pub` | The current n-NRF magnitudes restricted to the 82 participants retained in the published Petal analysis. These are not measurements copied from that earlier publication. |
| `HL_ER_nNRF_mag_pub_Screening` | Published-set membership: `Included` for 82 participants and `Excluded` for 22. |

## Screening and missing values

All 104 participant rows remain in both files. QC and NRF measurements for an
excluded epoch were replaced with `NaN` before import into JASP; `NaN` means a
missing value, not zero. True-event and internal-reference epochs were screened
separately, so a participant can have measurements for one and missing values
for the other.

All 104 rows are enabled by the saved JASP global filter. Individual analyses
use the participants with the measurements they require. There are 99
participants with current true-event measurements, including 72 asleep and
27 awake. The comparison with the published retained set uses 82 participants.

The CSV therefore supplies the retained QC values shown in main Figure 2,
but not the excluded values also shown in Supplementary Figure 1. The
[pooled Oxford QC table](../figure-source-data/data/oxford/pooled_screened_eeg_qc_features.csv)
retains all 208 candidate items and their exclusion flags.
