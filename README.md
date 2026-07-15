# CounterMem simplified balanced 15-item study

GitHub Pages serves `index.html`. Prolific supplies `PROLIFIC_PID`, `STUDY_ID`,
and `SESSION_ID` as URL parameters. After consent, a Firestore transaction
atomically assigns the first free slot from 01–20. The same participant ID
always resumes the same slot and cloud answer document.

Each slot receives 15 main items: three from each of the five relations. Every
main item appears in exactly three slots. The five practice items contain
feedback; main-item oracle labels are not shipped to the browser.

- `?preview=1` runs the 15-item slot-01 preview locally without claiming a slot.
- `?all=1` runs all 100 main items locally without claiming a slot.

## Firestore documents

- `countermem_v3_admin/countermem-simplified-balanced-v3-15`: `assignments` maps participant hashes
  to slots; `claimed_slots` is the inverse map.
- `countermem_simplified_v3_15_annotations/{participant_hash}`: slot, answers, answer count,
  completion state, and timestamps.

The website uses anonymous Firebase authentication. Participants may read and
write only their own 15-item response document. Do not place construction
oracle or pair-map files in this repository.

## Coordinator downloads

`admin.html` remains the legacy v3 export page. New study records are kept
private by Firestore rules and should be exported through Firebase Console or a
separately authenticated coordinator tool.

To reopen the study from scratch, archive/export the two collections and delete
the allocator document and annotation documents in Firebase Console. Never
reset them after recruitment has started.
