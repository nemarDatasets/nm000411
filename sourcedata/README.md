# sourcedata

Original release files of the source dataset, as far as they can be redistributed.

## Release files stored under their release names (added 2026-10-11)

15 release files of Zenodo record 5675459 (https://doi.org/10.5281/zenodo.5675459) are listed under `sourcedata/zenodo-5675459/` with their release paths.
They take no extra storage: each is a git-annex pointer to the same content as the BIDS file named in
`sourcedata/SOURCEDATA_POINTERS.tsv`.

- 8 are `identical`: byte for byte the released file.
- 7 are `scrubbed`: the privacy-scrubbed copy used in the BIDS part, not the released bytes. In the scrubbed interictal EDFs the patient's name in the first EDF+ annotation was overwritten with X (same length); all other bytes are as released. The MRI/CT volumes and the earlier subset record 5494990 are not included.

The unscrubbed originals are not redistributed here; they remain available from the public source.
