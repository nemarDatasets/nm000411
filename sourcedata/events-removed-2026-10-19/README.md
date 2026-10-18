# Events removed on 2026-10-19 (version 1.0.3)

`sub-08/ieeg/sub-08_task-ictal_events.tsv` as released (byte-for-byte), moved here from the BIDS tree. Its 4 rows are the
4 EDF+ annotations of `sub-08_task-ictal_ieeg.edf` (`+518.000000` and `EEGonset` at 517.959 s, `+543.000000` and `....` at
542.906 s). The file is a 71-s EDF+C clip (71 data records of 1 s, record onsets 0-70 s), so all 4 lie 447-472 s after its
end. They are timed on another clock, most likely that of the longer recording the clip was cut from; the position of the
clip in that recording is not in the release, so they cannot be placed in the clip. See README.md, section "sub-08 ictal
annotations outside the clip".
