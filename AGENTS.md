# Codex Operating Agreement — RC F Dynamics Lab

Read these in order: `README.md`, `docs/PROJECT_SPEC.md`, `docs/DECISION_LOG.md`, `docs/RESEARCH_LOG.md`, and research files under `docs/`.

## Core mandate
Build an evidence-first interactive replay of the reported maneuver. **Approval gates override any impulse to finish the whole project in one pass.**

### First run: Gate 0 and Gate 1 only
1. Inventory repository and actual local Mac environment (`python3`, `pip`, `node`, `npm`, `ffmpeg`, `cv2`, `gh`, Git). Do not assume Homebrew exists or install globally. Prefer `.venv` and lockfile/project-local dependencies.
2. Locate private media in gitignored folders or request local paths. Do not ask again for confirmed year/model/intersection/video metadata. Ask at most 4–6 high-value questions only when material.
3. Check the existing portfolio framework/design if its repo is available; do not edit it yet. Start this standalone UI prototype inside `replay/` with a static-friendly approach.
4. Make a real runnable **interactive mockup**: the original portrait video, a top-down RC F on a provisional intersection visualization, toggles for `None`, `Steering`, `Exterior features`, `Optical flow`, `Combined`, and a full-width bottom telemetry rail + synchronized scrubber. All placeholder motion/telemetry must visibly state `Illustrative · unmeasured`.
5. Open or serve the UI locally and provide a preview URL. **STOP, present a tight change summary, and wait for explicit design approval.**

### Later gates (never auto-skip)
- Gate 2: Define provable quantities, calibration, license/privacy, approval for actual analysis.
- Gate 3: Run CV/dynamics, produce uncertainty and diagnostics, stop for scientific review.
- Gate 4: Integrate real outputs and validate static publishing; obtain approval before deployment and public media.
- Gate 5: Blog **only after** replay has been approved and shipped.

## Scientific integrity
- Separate `observed`, `inferred`, `scenario`, and `unavailable` at data and UI layers. All telemetry needs provenance, units, assumptions, and confidence. **Never hallucinate plausible-looking speeds or torque.**
- No-slip bicycle model is insufficient during large sideslip. Steering-wheel rotation != front road-wheel angle. Camera optical flow != metric speed without geometry, calibration, and scene depth.
- Do not fit an exact 360° just because that was the reported maneuver. Treat blue hand-drawn path as a hypothesis only; resist retrofitting to it.
- Use independent video observations, map landmarks, hand-labeled frames, model comparisons, and sensitivity analysis. Null out unsupported intervals.

## Public repository privacy / rights
- Absolutely do **not** commit `IMG_1375.mp4`, source screenshots, VIN, EXIF-bearing private files, license plates, identifiable people, or personal metadata. `assets/raw/`, `assets/reference/`, and public-media staging are gitignored.
- A marked-up Apple/Google Maps screenshot is PRIVATE design guidance only. For public use, evaluate Apple MapKit JS / Maps Web Snapshots with proper authorization, a licensed imagery provider, or an original schematic; preserve required attribution.
- Do not publish the clip without consent, identity/plate/audio review, and explicit user approval. Do not edit unrelated portfolio pages.

## Reporting after each gate
Report changed files, findings supported by evidence, tests run, unsupported hypotheses, open decisions, and the **specific approval sought**. Keep `docs/RESEARCH_LOG.md` and `docs/DECISION_LOG.md` updated with true observations, not fictional retrospectives.