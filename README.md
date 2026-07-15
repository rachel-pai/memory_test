# CounterMem-Gov v3 annotation site

GitHub Pages serves `index.html`. Participants enter the coordinator-supplied
ID; a Firestore transaction atomically assigns the first free slot from 01–10.
The same ID always resumes the same slot and cloud answer document.

## Firestore documents

- `countermem_v3_admin/countermem-gov-v3`: `assignments` maps participant IDs
  to slots; `claimed_slots` is the inverse map.
- `countermem_v3_annotations/{participant_id}`: slot, answers, answer count,
  completion state, and timestamps.

The website uses anonymous Firebase authentication. Firestore rules must allow
authenticated anonymous users to read/update the allocator document and to
read/write annotation documents. Do not place construction oracle or pair-map
files in this repository.

## Coordinator downloads

`admin.html` automatically loads all participant documents and provides
read-only JSON downloads by participant ID or as a single combined export.

To reopen the study from scratch, archive/export the two collections and delete
the allocator document and annotation documents in Firebase Console. Never
reset them after recruitment has started.
