# Synthetic EEG example

This folder contains the existing demonstration dataset produced by
[simple-synthetic-eeg-generator](https://github.com/simple-eeg/simple-synthetic-eeg-generator).
All identifiers and samples are synthetic and correspond to no real person.
The example lets you try SIMPLE without access to clinical recordings.

## Files

The complete generated folder is supplied unchanged under
[`data/simple-synthetic-eeg-demo/`](data/simple-synthetic-eeg-demo/):

```text
simple-synthetic-eeg-demo/
├── dataset_list.csv
└── raw/
    ├── sub-001/ses-01/eeg/sub-001_ses-01_run-01_eeg.set
    ├── ...
    └── sub-031/ses-01/eeg/sub-031_ses-01_run-01_eeg.set
```

Each of the 31 recordings has one channel, `Cz`, and 30 seconds of data sampled
at 1,000 Hz. Each contains a `stimulus` event at 15 seconds. The `.set` files
contain their samples and metadata together; no separate `.fdt` files are
needed. Subject 31 contains an added burst for the manual-screening example.

These signals demonstrate software operation. They are not clinical data or
a model of neonatal pain. The generator's
[dataset description](https://github.com/simple-eeg/simple-synthetic-eeg-generator#dataset-design)
explains the fixed signal recipe.

## Use with SIMPLE

1. Obtain the [simple repository](https://github.com/simple-eeg/simple) and
   follow its software setup instructions.
2. Copy the contents of this dataset's `raw/` folder into `simple/data/raw/`.
3. Copy `dataset_list.csv` into `simple/data_lists/`, retaining its filename.
4. Follow the [SIMPLE synthetic tutorial](https://github.com/simple-eeg/simple#synthetic-tutorial).

The list's `path_raw` entries begin with `data/raw/`. They are relative to the
`simple` checkout and become valid after copying the files as described above.
Preserve the subject, session, and file names. Use a working copy for the
tutorial, which updates its dataset list and creates derived outputs.

To generate the example yourself, follow the
[generator instructions](https://github.com/simple-eeg/simple-synthetic-eeg-generator#first-time-setup).
Using the copy supplied here does not require running the generator or setting
up its Python environment. Screening remains a manual step in SIMPLE.
