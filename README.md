# RC F Dynamics Lab

**Status: Research and specifications only. No replay, speed, or drift measurements have been computed.**

An open engineering project to investigate a *reported* 360-degree maneuver involving a **2016 Lexus RC F** from a single 15 s cabin video at the intersection of **E Brooklyn Village Avenue and S Brevard Street in Charlotte, NC**. The goal is a transparent visual reconstruction: original footage, time-aligned OpenCV annotations, a scaled overhead car, and a full-width bottom telemetry panel that explains the evidence and uncertainty behind every derived quantity.

This is a retrospective computer-vision and modeling exercise, not an authoritative accident reconstruction, verified velocity record, or stunt tutorial. Factory peak engine power/torque are **not** event-specific measurements.

## Deliverables (in order)

1. **Interactive UI mockup, with illustrative/unmeasured values only.** Original portrait video on left, top-down map and car on right, synchronized transparent CV overlays toggled over the video, telemetry across bottom. **STOP for visual approval.**
2. Scoped scientific feasibility + map/image and privacy calibration plan. **STOP for approval.**
3. Offline OpenCV and constrained vehicle dynamics analysis, with confidence and failure diagnostics. **STOP for data review.**
4. Approved static GitHub Pages interactive replay, no Python backend at runtime. **STOP before publishing media.**
5. **Only after replay approval:** separate portfolio blog post documenting actual methods, failed tests, evidence, and limitations.

See [AGENTS.md](AGENTS.md) for Codex instructions and [docs/PROJECT_SPEC.md](docs/PROJECT_SPEC.md) for the complete master brief. Research notes are in [docs/](docs/).

## Current inputs (private, not included)

- `IMG_1375.mp4`: original H.264 portrait video, 512×910, 30 fps, 450 frames, 15.0 s. Filename is not a public asset path.
- `IMG_8450.jpeg`: marked-up Apple Maps reference screenshot (private reference, **not authorized for automatic public redistribution**).
- `IMG_8449.jpeg`: marked-up Google map backup (private reference).
- Exact VIN, other identifying information, and raw material are **deliberately omitted**.

Put private media in `assets/raw/` and reference screenshots in `assets/reference/` on your own Mac. Both directories are gitignored. A *new* clean/approved video and a properly licensed map source will be chosen before publishing.

## Mac handoff

The public repository is available now. Clone into your Downloads folder:

```bash
cd ~/Downloads
git clone https://github.com/lalithu/rcf-ebrooklyn-clt.git
cd rcf-ebrooklyn-clt
```

To begin Codex: open this folder, tell it **"Read AGENTS.md and docs/PROJECT_SPEC.md; complete Gate 0, then show me the working Gate 1 mockup. Stop for approval."**

No Homebrew or OpenCV assumption: Codex should inspect your environment before selecting dependencies. See [docs/OPENCV_SETUP.md](docs/OPENCV_SETUP.md).

## Research and limitations

| Quantity | Evidence level before analysis |
|---|---|
| Manufacturer specs | Referenced from Lexus and independent specification listings |
| Steering wheel *rotation* | Potentially visible, subject to occlusion; not yet tracked |
| Absolute road-wheel steer angle | Unknown steering rack mapping; not automatically recoverable |
| Body heading / yaw rate | Potentially estimable from static exterior landmarks; unmeasured |
| Position / speed | Needs map scale and calibrated visual landmarks; may remain underdetermined |
| Sideslip | Highly model-dependent without independent ground velocity |
| Event-specific torque / tire force | Not identifiable from this video alone |

Full source list: [docs/SOURCES.md](docs/SOURCES.md). License: [Apache-2.0](LICENSE) for the original code/docs; excluded proprietary media and third-party imagery carry **no license grant** from this repository.

**Repository:** https://github.com/lalithu/rcf-ebrooklyn-clt — public research/code only; raw video and third-party map screenshots are intentionally absent.
