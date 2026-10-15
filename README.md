# EEG-CLEAN-PIPELINE

Config-driven EEG cleaning and band-power pipeline: raw PhysioNet `.edf` in, clean Parquet out.

> **Status: work in progress.** Built step by step in public. Sections marked *planned* are not implemented yet.

## What it does

Takes raw, messy EEG recordings and turns them into clean, structured brainwave metrics.

```
raw .edf -> montage -> filter -> ICA blink removal -> band power (Welch) -> Parquet -> BIDS
```

- Input: [PhysioNet EEG Motor Movement/Imagery](https://physionet.org/content/eegmmidb/1.0.0/) (109 subjects, 64 channels)
- Output: one Parquet row per subject, channel and band (delta, theta, alpha, beta)

## Why a pipeline, not a notebook

- **Config-driven:** filter settings live in a config file, not in code
- **Tested:** filter correctness and output schema (planned)
- **Logged:** clear logs and handling for malformed files (planned)
- **Schema-stable:** the Parquet columns don't change between runs

## Output schema (planned)

| column | meaning |
| --- | --- |
| subject | subject ID |
| channel | electrode name |
| band | delta / theta / alpha / beta |
| power | relative band power |

## How to run (planned)

```bash
python -m eeg_clean_pipeline --config configs/default.yaml
```

## Results (planned)

Before/after plot showing blinks removed by ICA will go here.

## Tools

Python 3.11, [MNE-Python](https://mne.tools), NumPy, SciPy, pandas, PyArrow, mne-bids.

## License

MIT
