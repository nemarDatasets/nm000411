# BrainQuake example SEEG data (Tsinghua Yuquan Hospital)

Stereo-EEG (SEEG) recordings from 8 patients with drug-resistant epilepsy, released by Kang Wang
(Tsinghua University) as the example data of the BrainQuake toolbox:

> Cai F, Wang K, Zhao T, Wang H, Zhou W, Hong B (2022). BrainQuake: An Open-Source Python Toolbox for the
> Stereoelectroencephalography Spatiotemporal Analysis. *Frontiers in Neuroinformatics* 15:773890.
> https://doi.org/10.3389/fninf.2021.773890

Source record: Zenodo https://doi.org/10.5281/zenodo.5675459 ("SEEG, MRI, CT for BrainQuake analysis",
CC-BY-4.0, published 2021-11-11; this is the record cited in the paper's data availability statement).
An earlier Zenodo upload with the same title, https://doi.org/10.5281/zenodo.5494990 (2021-09-09), holds 5 of
these patients with the same ictal EDF files (identical MD5) and 5-minute interictal clips; this BIDS dataset
uses the later, larger record. The MD5 comparison is in `sourcedata/zenodo-5675459/b3w1_provenance.json`.

## Contents

- `sub-01` … `sub-08` (source labels S1 … S8, see `participants.tsv`).
- `task-ictal`: 71-s seizure clip per patient exported by the authors for the BrainQuake ictal module
  (Epileptogenicity Index). The release does not annotate the seizure onset time within the clip.
- `task-interictal`: interictal segment (up to about 2 h per patient) exported for the interictal module
  (high-frequency events / HFO detection).
- Sampling rate 2000 Hz, physical unit µV, SEEG depth electrodes. Channel labels are kept as released: the ictal clips
  use plain contact names (`A1`, `A'1`), the interictal files use the acquisition system's labels (`POL A3`,
  `EEG A1-Ref`, ...), so the same contact can carry different labels in the two tasks. The interictal files also contain
  `POL ECG`, `POL EMG1`, `POL EMG2` (typed ECG/EMG), `POL E` and `POL DC10` (typed MISC; meaning not documented).
  EDF header prefilter field of the ictal clips: `0.0Hz - 1000.0`. Reference and amplifier are not documented.
- The interictal files are EDF+D (discontinuous; `RecordingType` = `discontinuous`). EDF+ annotations (clinical marks
  such as `IID`, `EEG Onset`, `SZ5`, `asleep`, and a few Chinese-language notes, kept verbatim) are listed in
  `*_events.tsv`.
- Per the paper: recordings were made at the Epilepsy Center of Tsinghua Yuquan Hospital (Beijing) during
  about two weeks of pre-surgical monitoring; MRI was acquired before and CT after implantation; the study was
  approved by the hospital's ethics committee.

## Processing

No signal processing. The ictal EDF files are copied byte-for-byte from the release. In each interictal EDF file the
first EDF+ annotation (`Segment: REC START ...`) contained the patient's name; that text was overwritten with `X`
characters of the same length. Nothing else was changed: headers are identical and all signal bytes are identical
(SHA-256 over the non-annotation bytes of every data record, source vs. BIDS; recorded in
`sourcedata/zenodo-5675459/b3w1_provenance.json`). The EDF headers were already de-identified by the authors (patient
and recording fields `DEIDENTIFIED`, start date `01.01.01`), so `acq_time` is `n/a`.
Channel tables are built from the EDF headers. The release has no electrode coordinates (`electrodes.tsv` lists
contact names with `n/a` positions).

## Not included

- `S*_mri.nii.gz` (pre-implant T1) and `S*_ct.nii.gz` (post-implant CT): a surface render of these volumes
  shows reconstructable facial features (no defacing), so they are not redistributed here. They remain
  available from the CC-BY-4.0 source record. Their MD5 checksums are listed in the provenance file.
- Age and sex are not reported in the release or the paper (`n/a`).

## Licence

CC-BY-4.0, as the source record. Please cite the paper and the Zenodo record.
