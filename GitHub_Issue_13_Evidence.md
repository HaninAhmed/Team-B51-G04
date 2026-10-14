# GitHub Issue #13 — DFD Evidence

This package includes the corrected local DFD contribution for the Issue #13 scope: Level 0, Level 1, Level 2 for Process 4.0, balancing checklist, report, exports and Visual Paradigm source. This file records local package evidence; it does not assert the current state of a GitHub issue, pull request, branch or merge.

## Acceptance criteria evidence

- [x] Context DFD has one process, five external entities and no stores.
- [x] Level 1 contains numbered major processes and logical data stores.
- [x] Process 4.0 is decomposed into 4.1–4.5.
- [x] Process numbering and flow direction are consistent across levels.
- [x] Boundary balancing is documented in `Boundary_Flow_Checklist.md`.
- [x] Diagrams are present in `PearlMart_Milestone1.vpp` and exported as PNG/SVG.
- [x] Corrected diagrams are included in `Member1_PearlMart_DFD_Report.docx`.

## Validation notes

- The Visual Paradigm database passed `PRAGMA integrity_check` and its flow endpoints were checked against the specification.
- The Visual Paradigm application was not available to open and render the native canvas in this environment.
- The supplied archive contained a zero-byte `G4.docx` and no group-level report/evidence beyond the DFD slice; see the root `GROUP_REPORT_STATUS.md`.

## GitHub submission

Use this package to update the intended branch/PR after reviewing the native `.vpp` file in Visual Paradigm. Verify issue closure and merge status on GitHub itself; those remote actions are not performed by this local package edit.
