# Figure source data

This guide identifies the data available for each of the four main figures
and thirteen supplementary figures in the SIMPLE manuscript. Oxford refers
to the Petal dataset; Strasbourg refers to NOCI-Prem.

The CSV files below are unchanged outputs of the study workflows. Their
original filenames are preserved, with separate dataset folders to distinguish
files that have the same name. The [JASP data and saved analyses](../jasp/README.md)
provide additional sources for Figure 4.

## Files

An **epoch** is a segment of EEG around an event. An **item** is one event
occurrence at one EEG channel. True-event epochs contain heel lance in Petal or
venepuncture in NOCI-Prem. Internal-reference epochs contain EEG from before
the true event, from the same recording and channel.

**Quality-control (QC) features** describe properties of the signal used
during manual review. A **neurodynamic response function (NRF)** is a
predefined response shape fitted to the EEG; its fitted magnitude quantifies
the response. The e-NRF represents the early sensory response, the n-NRF the
later noxious-evoked response, and the p-NRF the preterm noxious response.

| Dataset | File | Contents |
| --- | --- | --- |
| Oxford / Petal | [pooled_screened_eeg_qc_features.csv](data/oxford/pooled_screened_eeg_qc_features.csv) | Nine QC features for all 208 candidate items, with screening flags. |
| Oxford / Petal | [pooled_screened_eeg_nrf_features.csv](data/oxford/pooled_screened_eeg_nrf_features.csv) | NRF measurements for those items: 416 rows, because both e-NRF and n-NRF were fitted to each item. |
| Strasbourg / NOCI-Prem | [pooled_screened_eeg_qc_features.csv](data/strasbourg/pooled_screened_eeg_qc_features.csv) | Nine QC features for all 78 candidate items, with screening flags. |
| Strasbourg / NOCI-Prem | [pooled_screened_eeg_nrf_features.csv](data/strasbourg/pooled_screened_eeg_nrf_features.csv) | p-NRF measurements for those items: 78 rows. |

“Screened” means that decisions to retain or exclude items after manual review
have been added. Excluded rows remain in these four files. `Exclude` is a
numeric flag: `0` means retained, and `1` means excluded. The Oxford tables
contain nine excluded items; the Strasbourg tables contain one. Oxford's NRF
table repeats each item's flag across its two template rows.

## Figure guide

Individual clinical EEG time series and their power spectral density (PSD)
data are not included here. These pseudonymised newborn clinical research
data remain subject to the consent, ethical approval, and institutional
governance of the respective studies, as described in the manuscript's Data
Availability statement. Separately, this repository does not include the
group-average waveforms, time-frequency arrays, or PSD arrays in Figure 3.
The guide below identifies the derived measurements that are shared.

| Figure | Available sources and scope |
| --- | --- |
| **Main Figure 1** | Conceptual workflow schematic; no underlying numerical dataset. |
| **Main Figure 2** | The nine QC swarms use the **199 retained Oxford items** in the Oxford QC CSV (`Exclude = 0`). Individual EEG and PSD data are not included. See [QC plots](#qc-plots). |
| **Main Figure 3** | The fourth row of A and B uses paired NRF measurements from the corresponding Oxford and Strasbourg NRF CSVs. Saved estimates and intervals are given [below](#figure-3-paired-nrf-comparisons). The numerical data behind the group-average plots in the first three rows are not included. |
| **Main Figure 4** | Counts and individual measurements come from [jasp_data_all.csv](../jasp/data/jasp_data_all.csv). Statistical results are in [jasp_data_all.jasp](../jasp/data/jasp_data_all.jasp); the figure script also contains C's displayed summaries. See the [panel guide](#figure-4-petal-applications). |
| **Supplementary Figure 1** | The nine QC swarms use **all 208 Oxford items**, including excluded items, in the Oxford QC CSV. Individual EEG and PSD data are not included. |
| **Supplementary Figure 2** | Individual Petal true-event EEG and PSD data; not included. |
| **Supplementary Figure 3** | Individual Petal true-event EEG and PSD data; not included. |
| **Supplementary Figure 4** | Individual Petal true-event EEG and PSD data; not included. |
| **Supplementary Figure 5** | Individual Petal true-event EEG and PSD data; not included. |
| **Supplementary Figure 6** | Individual Petal true-event EEG and PSD data; not included. |
| **Supplementary Figure 7** | Individual Petal internal-reference EEG and PSD data; not included. |
| **Supplementary Figure 8** | Individual Petal internal-reference EEG and PSD data; not included. |
| **Supplementary Figure 9** | Individual Petal internal-reference EEG and PSD data; not included. |
| **Supplementary Figure 10** | Individual Petal internal-reference EEG and PSD data; not included. |
| **Supplementary Figure 11** | The nine QC swarms use **all 78 Strasbourg items**, including the excluded item, in the Strasbourg QC CSV. Individual EEG and PSD data are not included. |
| **Supplementary Figure 12** | Individual NOCI-Prem true-event EEG and PSD data; not included. |
| **Supplementary Figure 13** | The plotted NRF templates and plotting script are already shared in the software repositories. See [NRF templates](#supplementary-figure-13-nrf-templates). |

## Reading the tables

`subjectID`, `sessionID`, and `runID` identify the participant and recording;
`epoch_index` identifies the event within that recording. Import the identifiers
as text to preserve leading zeros. The labels are specific to each dataset and
should not be matched between Oxford and Strasbourg.

`channel` is text (`CZ` or `Cz` here). `eventtype` distinguishes the true
event from its internal reference:

| Dataset | True event | Internal reference |
| --- | --- | --- |
| Oxford / Petal | `lance` | `lance_prestim` |
| Strasbourg / NOCI-Prem | `cannula` | `cannula_prestim` |

The Strasbourg event label `cannula` refers to the venepuncture event
described in the manuscript. `eventannotation` is an additional text field.
QC measurements and NRF fit measures are numeric; `NaN` denotes a missing
or undefined value, not zero.

### QC plots

Each QC CSV contains one row per item and these nine plotted columns:

| Column | Measurement | Units |
| --- | --- | --- |
| `maxAbsEpoch` | Maximum absolute amplitude | µV |
| `sdEpoch` | Population standard deviation | µV |
| `invSdEpoch` | Inverse standard deviation, with a lower limit on the standard deviation to avoid division by zero | µV⁻¹ |
| `MeanAbsDiffNorm` | Mean absolute successive difference after robust normalisation | Dimensionless |
| `MaxAbsDiffNorm` | Maximum absolute successive difference after robust normalisation | Dimensionless |
| `RobustSlopeNorm` | Absolute robust slope after normalisation | ms⁻¹ |
| `AutoCorrLag1Pos` | Fisher transform of lag-one autocorrelation | Dimensionless |
| `AutoCorrLag1Neg` | One minus lag-one autocorrelation | Dimensionless |
| `KatzFDNorm` | Katz fractal dimension after robust normalisation | Dimensionless |

Each point in a QC swarm plot represents one true-event or internal-reference
item at Cz. Select the items specified in the figure guide, then use each
feature column, ignoring missing or infinite values. Horizontal position is
the feature value; vertical jitter separates overlapping points and is not
another measurement.

The comparison points are fixed when the viewer opens. Figure 2 shows the
retained items; Supplementary Figures 1 and 11 show all candidate items.
A screenshot's currently selected item or “This view” count therefore does
not define which points appear in the swarm plots. The
[Oxford viewer](https://github.com/simple-eeg/simple-oxford/blob/main/scripts/step_6_screen_2_viewer_rate_epochs.m)
and [Strasbourg viewer](https://github.com/simple-eeg/simple-strasbourg/blob/main/scripts/step_6_screen_2_viewer_rate_epochs.m)
provide the plotting details and box overlays.

The Oxford [JASP CSV](../jasp/data/jasp_data_all.csv) also contains the retained
QC measurements, in columns prefixed `HL_BL_` for internal-reference items
and `HL_ER_` for true-event items. Excluded measurements are missing there.
It therefore supplies Figure 2's retained values, but not all the points
in Supplementary Figure 1. It contains no Strasbourg measurements. Use the
QC CSVs in this folder for all candidate items.

### Figure 3 paired NRF comparisons

These plots compare each event's fitted response with its reference from
the same recording.

Use the numeric `fglsCoef` column, which contains NRF magnitude in µV. Select
Cz (case-insensitive), retained rows (`Exclude = 0`), and the appropriate
template:

| Panel | `NRFName` | Complete pairs |
| --- | --- | --- |
| 3A, Petal | `noxious_NRF_500Hz` | 98 pairs from 98 participants |
| 3B, NOCI-Prem | `noxious_preterm_NRF_500Hz` | 38 recording pairs from 26 participants |

Within each dataset, match the true and reference events using `subjectID`,
`sessionID`, `runID`, and `channel`. Do not pair on `epoch_index`, because
the two events have different epoch indices. Keep pairs only when neither
measurement is missing or infinite. Oxford has 99 retained true events and
100 retained references; three incomplete recording pairs are omitted.
Strasbourg has 38 retained true events and 39 retained references; one
incomplete pair is omitted.
Repeated Strasbourg recordings remain separate pairs.

The paired difference is **true-event magnitude minus internal-reference
magnitude**. The fourth row plots each observation and its connection to its
partner, followed by the median paired difference and its 95% confidence
interval. The saved numerical summaries are:

| Panel | Median difference (µV) | Lower 95% limit (µV) | Upper 95% limit (µV) |
| --- | ---: | ---: | ---: |
| 3A, Petal | 48.393869718875251 | 21.376659358848201 | 69.604696421937206 |
| 3B, NOCI-Prem | 51.351497937254152 | 5.5589510000224962 | 125.22438665500135 |

These are the saved analysis results, not additional columns in the NRF
CSVs. The intervals use the bias-corrected and accelerated (BCa) bootstrap
with 100,000 complete-pair resamples, seed 1, and MATLAB's `twister`
generator. The [Oxford comparison script](https://github.com/simple-eeg/simple-oxford/blob/main/scripts/step_7_check_7_sep_check_nrf.m)
and [Strasbourg comparison script](https://github.com/simple-eeg/simple-strasbourg/blob/main/scripts/step_7_check_7_sep_check_nrf.m)
specify the filtering, pairing, and calculation. The NRF CSVs also retain
the other fitted measures and diagnostics produced by those workflows;
`fglsCoef` is the measure used in these manuscript plots.

### Figure 4 Petal applications

All references in this section are to the Oxford
[jasp_data_all.csv](../jasp/data/jasp_data_all.csv) and the saved
[jasp_data_all.jasp](../jasp/data/jasp_data_all.jasp). The CSV has one row
for each of 104 participants with time-locked EEG.

The **current set** contains the 99 participants with a retained true-event
measurement. The **published set** is the 82-participant membership used in the original
Petal analysis. Both sets use measurements calculated by the current workflow;
the published-set measurements were not copied from the earlier publication.

| Panel | Source |
| --- | --- |
| 4A | Row count and `HL_ER_nNRF_mag_Screening` / `HL_ER_nNRF_mag_pub_Screening` supply the 104 available, 99 current-retained, and 82 published-retained counts. The 112 randomised total is a study constant shown in the figure and specified in the figure script; the other eight participants are not CSV rows. |
| 4B | Count `Included` and `Excluded` participants separately for each `trial_arm`, using those two screening columns. Current retained/excluded counts are 51/3 Control and 48/2 Intervention; published retained/excluded counts are 43/11 Control and 39/11 Intervention. |
| 4C | Saved Bayesian Mann–Whitney results in JASP; the displayed medians and 95% credible intervals are also fixed inputs in the figure script and listed below. |
| 4D | `HL_ER_eNRF_mag`, grouped by `HL_sleep_state`, with missing values omitted: 99 observations, comprising 72 Asleep and 27 Awake. |
| 4E | `HL_ER_nNRF_mag`, grouped by `HL_sleep_state`, with missing values omitted: the same participants, 72 Asleep and 27 Awake. |

The screening columns use the text labels `Included` and `Excluded`.
The five current-set and 22 published-set exclusions are among the 104
available EEG participants. Figure 4A expresses these counts as 4.5% and
19.6% of the 112 randomised participants. All 82 published-set participants
are also in the current set of 99.

Figure 4C displays a dimensionless treatment effect, δ (Control minus
Intervention), rather than an NRF magnitude:

| Retained set | n | Posterior median δ | Lower 95% credible limit | Upper 95% credible limit |
| --- | ---: | ---: | ---: | ---: |
| Current | 99 | −0.004 | −0.375 | 0.368 |
| Published | 82 | 0.109 | −0.292 | 0.519 |

These values are given at the precision used in the figure. The
[Figure 4 script](https://github.com/simple-eeg/simple-oxford/blob/main/scripts/step_10_gen_1_figure_4_base.m)
contains these display values and derives the counts from the CSV. Panels D
and E were exported from JASP; their underlying NRF magnitudes are in µV.
The JASP archive contains the statistical settings, results, and plot outputs.

### Supplementary Figure 13 NRF templates

The plotted templates are already available as MATLAB files:

- e-NRF: [early_NRF_500Hz.mat](https://github.com/simple-eeg/simple-oxford/blob/main/NRFs/early_NRF_500Hz.mat).
- n-NRF: [noxious_NRF_500Hz.mat](https://github.com/simple-eeg/simple-oxford/blob/main/NRFs/noxious_NRF_500Hz.mat).
- p-NRF: [noxious_preterm_NRF_500Hz.mat](https://github.com/simple-eeg/simple-oxford/blob/main/NRFs/noxious_preterm_NRF_500Hz.mat).

These are the stored templates used for fitting. Each has zero mean and is
scaled so that the sum of its squared values is one. Their plotted amplitudes
are unitless. The
[template figure script](https://github.com/simple-eeg/simple-oxford/blob/main/scripts/step_8_gen_3_nrf_details.m)
plots their samples and time coordinates. The files are linked here rather
than copied into this folder.
