# CODEX MASTER BRIEF — RC F Dynamics Lab

You are GPT-6.1 Sol acting as an engineering collaborator, UX designer, and research assistant. Build a technically rigorous, polished, entirely static-hostable interactive replay of a reported 360-degree vehicle maneuver. Collaborate with me through explicit approval gates. **Do not jump from mockup to final implementation or blog.**

## 0. Known facts — do not re-ask

- Vehicle: **2016 Lexus RC F, standard model** (not Track Edition), 5.0L V8, RWD, 8-speed automatic.
- Factory reference values to VERIFY and cite: **467 hp, 389 lb-ft peak engine torque, 107.5-in wheelbase, 185.2-in length, 72.6-in body width**. Torsen rear LSD is standard; torque-vectoring differential is optional. Actual fitted differential unknown. Traction/stability intervention was reportedly disabled; exact control mode unknown.
- Scene: **E Brooklyn Village Avenue × S Brevard Street, Charlotte, NC**, by The Francis Apartments/Home2 Suites. Apple Maps overhead screenshot is the preferred visual reference; the hand-drawn blue curve is a rough hypothesis, not ground truth.
- Original vertical cabin video: `IMG_1375.mp4` (15 seconds, 30 fps, 450 frames, 512x910). Apple Maps reference: `IMG_8450.jpeg`; secondary Google screenshot: `IMG_8449.jpeg`. These filenames are from the supplied handoff package; locate them in the workspace, or ask me to identify their local path. Do not assume ChatGPT `/mnt/data` paths exist on my Mac.
- Footage shows steering wheel and some exterior landmarks, but parts of the maneuver are occluded or severely backlit; do not presume an unbroken 360-degree visual measurement.
- Desired UX: original video independently viewable, synchronized top-down RC F at the intersection, overlays on the ORIGINAL video that can be toggled during playback, and a **full-width bottom telemetry panel**. Minimal, premium, Apple-like typography/material treatment with restrained automotive instrumentation. The purpose is to show how every inference was derived.
- Deliverable A: standalone replay route on my existing GitHub Pages portfolio, tentatively `/experiments/rcf-360/` (adapt to real site architecture). Deliverable B: separate research blog route, tentatively `/blog/rcf-360/` **only after the replay is complete and approved**. Do not modify unrelated pages or site design.

## 1. Mandatory workflow and stop rules

**Gate 0 — Discovery / questions.** First inspect the repository and file tree; report relevant framework, existing design system, local Node/Python/FFmpeg/OpenCV availability. Ask at most 4–6 high-value questions about unresolved facts: design aesthetic, entry/exit map anchors, clean unscribbled Apple screenshot or licensed map option, observed traction mode/differential, publishing permission/privacy and portfolio repo location. Do not ask known vehicle year, location, or video details again. Recommend defaults, then proceed to UI mock after answers or reasonable provisional assumptions.

**Gate 1 — Interactive UI prototype.** PRIORITIZE THIS. Implement a real, locally runnable, visually polished static prototype using the original video and map *reference*. Allow browser playback, scrubbing, playback speed if straightforward, overlay toggles, and a placeholder synchronized car path. All mock telemetry must read `Illustrative / unmeasured`; never invent plausible real mph/torque as if measured. Build the UI, start a dev server, tell me the localhost URL and what to inspect. Ask for explicit UI approval. **STOP HERE until I approve. No costly CV processing, no dynamics fitting, no publishing, no blog.** Iterate on layout/design in response to feedback. Do not leave me with only Figma descriptions; open or serve the working UI. If graphical browser preview is available, capture screenshots; otherwise provide localhost and screenshot command.

**Gate 2 — Scientific scope and calibration approval.** After UI approval, show a matrix of observables vs inferences vs simulations, expected confidence, failure modes, and prerequisites. Confirm the overhead base, crop, image licensing/attribution, reference geometry, scale, initial route anchors, and top-down RC F silhouette. Include uncertainty for parameters, and confirm what must be labeled `not estimable`. Get explicit approval before expensive analyses.

**Gate 3 — Real CV and dynamics.** Process the supplied video offline, fit only defensible measurements/estimates, output time-aligned data with provenance and confidence, and produce diagnostic plots/annotated clips. Show findings and caveats for approval. **STOP before hard-coding results into polished output if validation fails.**

**Gate 4 — Final replay and publish.** Integrate results into the approved UI. Run cross-browser, mobile and GitHub Pages build checks; test direct route navigation, scrubbing synchronization, loading and attribution. Do not commit private/raw video or publish unreviewed footage or identifying information. Ask permission before deployment.

**Gate 5 — BLOG LAST.** Only after I approve the finished replay, draft and implement the separate portfolio article using recorded evidence from development (not fabricated retrospective storytelling). Show a draft and request approval before publication.

After EVERY gate, report: shipped artifacts, actual measured findings, unresolved uncertainties, files touched, test results, and the exact decision needed from me. Respect explicit approval barriers even if told to "finish the project" initially.

## 2. UI specification

Desktop above-the-fold layout: compact title bar (`RC F / Dynamics Lab`, case/location, method status); main row with original portrait video on the left (clear unobstructed playback when overlays OFF) and top-down intersection + precisely scaled RC F silhouette on the right. Keep the **telemetry panel spanning the bottom**; on mobile stack video/map and make telemetry a scrollable/collapsible bottom section without hiding essentials. The bottom panel includes synchronized timeline, transport/scrubber, playback time/frame number, speed estimate with range (or N/A), steering-wheel rotation, heading, yaw rate, sideslip beta when identifiable, confidence/status, and optional plot(s). Preserve native audio and video fidelity.

Video overlays: `None`, `Steering wheel`, `Exterior features`, `Optical flow`, `Combined`; optional `Masks / confidence` diagnostics. The overlay runs as transparent Canvas/SVG atop the HTML video and follows it during play/pause/seek. Draw tracked rim/spoke keypoints and reference line (wheel angle), stable-feature dots, tracked feature vectors in the windshield, inlier/outlier differentiation, stabilization cues, and small numeric labels. **Never use computer-vision marks over unrelated objects as though they are road features.** Provide a compact legend, toggles and confidence; disable misleading overlays during tracking failure. Controls must not cover the driver's hands or main visible evidence more than necessary.

Top-down overlay: Use a proportionally scaled original SVG silhouette of a 2016 RC F coupe (visible roof, hood/trunk, wheel locations; not a generic rectangle). Model length, width, and wheelbase from verified factory data; style details can be approximations and labeled. Car BODY HEADING must be independent from the TRANSLATIONAL VELOCITY vector; show separate arrows for heading, velocity, and optional lateral slip angle. Draw path / ghost trail / uncertainty envelope. Allow selecting reference anchors and adjusting transforms in a developer-only calibration view, with an explicit saved edit trail. Orient to street axes and preserve map scale; no fictional mph based on pixel movement without calibration.

Clicking a bottom telemetry field opens `How this was estimated` with the frames/keypoints/feature matches, relevant equations, assumptions, calibration parameters, confidence and which values were measured vs fitted. Include `Observations / Estimates / Model scenarios` visual semantics. No ornamental random numbers. Data quality should be visible and the UI must still look polished if a metric is unavailable.

Visual style: restraint and editorial precision; dark charcoal/slate surfaces, soft translucent layering, warm light neutrals, a restrained electric-blue accent for active computer vision, amber for heading/kinematics, clean compact type, technical monospaced numeric labels. Design polished loading/error/empty states. Respect reduced motion and keyboard controls. Make an attractive real mobile layout.

Map rights: The provided marked-up Apple Maps screenshot may be used PRIVATELY as a mock reference, but do NOT assume it can be redistributed as a cropped image or stripped of Apple's credits in a public GitHub Pages site. Investigate compliant MapKit JS / Maps Web Snapshots (credentials/security/attribution), a properly licensed satellite/static image, or a custom original map with exact geometry. GitHub Pages is static, so do not put private API signing keys in frontend source. If licensing remains unresolved, use a custom schematic/permissioned static raster for publication and clearly identify it. Request an unmarked Apple screenshot for clean visual calibration; retain screenshot provenance privately.

## 3. Offline computer-vision pipeline (Python)

Environment first: check `python3 --version`, `python3 -m pip --version`, `node -v`, `npm -v`, `ffmpeg -version`, and `python3 -c 'import cv2; print(cv2.__version__)'`. Do not assume Homebrew. Prefer project-local `.venv`: `python3 -m venv .venv` + `python -m pip install ...`. Pin a minimal compatible dependency set, e.g. `opencv-python-headless`, `numpy`, `scipy`, `matplotlib`, `pytest` (and video tools only if necessary). Install **one** OpenCV Python package, avoid global/pip/base changes, use requirements or pyproject lock. Use local CPU baseline; heavyweight ML only when demonstrated useful. Document hardware-specific choices. Front end uses existing framework if practical; otherwise Vite+React+TypeScript, Canvas2D/SVG, no runtime Python/backend.

Step A, ingest: read original FPS, presentation timestamps (handle VFR if actual timestamps differ), orientation, resolution, codec, and audio. Extract representative/contact sheets, annotate visibility and ROIs. Preserve raw media unchanged. Make per-frame data indexed by video timestamp, not by a guessed clock.

Step B, steering: track rim center, dashboard fixed reference, wheel spokes/logo landmarks with OpenCV (feature/line/circle tracking; hand occlusion masks; optional lightweight keypoint detector). Estimate camera movement relative to fixed cabin points, recover wheel ROTATION using spoke/landmark orientation, resolve symmetry/unwrap full turns, propagate confidence. Wheel-angle baseline and sign convention must be documented. **Steering-wheel degrees are not the same as front road-wheel steering degrees**; steering ratio, rack mapping, wheel center, and occlusion uncertainty must be addressed, not guessed.

Step C, windshield scene: mask interior, sky, glare, reflections, pedestrians and moving vehicles. Track stationary external features with Shi–Tomasi/ORB + Lucas–Kanade/KLT and RANSAC; inspect optical flow and outliers. Separate camera shake and panning from true car movement via cabin reference and geometrical constraints. Estimate visual heading/rotation where supported. Without camera calibration and scene depth, optic flow alone does NOT provide precise metric speed; surface that limitation. Generate raw keypoints/vectors for browser overlays and diagnostics.

Step D, map calibration: choose ground control points (paint markings, curbs, crosswalks) from a properly sourced/georeferenced base. Explicitly establish screenshot-to-map transform, street axes, scale in meters, residual error and uncertainty. Use vehicle dimensions and trusted road measurements as cross-checks, not as magic anchors. Have me manually approve entry, spin-center and exit anchors and motion direction; blue sketch is a prior only. Prefer actual WGS84/local meter coordinates or a documented affine/homography transform. If pixel-to-meter scale is indeterminate, don't report precise speed.

Step E, temporal alignment: manually review event timestamps; steering starts, yaw begins, key heading transitions, speed/exit stabilization. Cross-check world scene, camera motion and video content. Mark occluded intervals and explain if the reported 360 degrees cannot be independently verified.

Step F, vehicle dynamics: verify official Lexus 2016 RC F facts (467 hp, 389 lb-ft peak **engine** torque, 8-speed, geometry, mass, diff options, tire sizes) and cite primary sources. Start with kinematic baseline only to sanity-check map scale; recognize that a high-sideslip spin violates a no-slip bicycle model. Then use an appropriately constrained planar dynamic-bicycle or rigid-body state model: position x/y, heading psi, translational vx/vy, yaw rate, steering input, tire-force/slip assumptions, plus optional unknown control inputs. Fit observed headings/map landmarks and steering jointly using batch optimization/smoothing with priors, bounded parameters and uncertainty analysis. Don't fit friction coefficient, instantaneous wheel torque, throttle position, gear or individual tire forces as identified facts without sensors. Use scenario bands/unknowns, not seductive but false single values. Avoid forcing the path to trace the hand-drawn circle. Distinguish true heading, path tangent and slip angle beta.

Step G, validation: manually label a small set of sample frames; measure steering detection reprojection/angle consistency, feature inlier ratio, map residuals and trajectory sensitivity. Refit on withheld frames, sample plausible parameter ranges, show uncertainty intervals, gaps and model disagreements. Review whether 30 fps + occlusions make some intervals unidentifiable. If an output fails, label it `not measurable from this source` and leave it blank or replace with an explicitly illustrative simulation.

Step H, data outputs: produce compact static `analysis.json` / files that frontend loads, and diagnostic artifacts. Each timestamp stores observations (keypoints, flow inliers, angle with units), fitted pose (x_m,y_m,yaw_rad), optionally speed/yaw/beta **with uncertainties**, provenance (observed|fitted|scenario|unavailable), confidence flags, and alignment metadata. No fabricated data. Use consistent coordinate systems, radians internally, documented degrees/mph conversions in UI. Keep raw metadata/identifying VIN private.

## 4. Browser playback synchronization

Use a single HTMLVideoElement as the master timeline; advance overlays/pose from `video.currentTime` / `requestVideoFrameCallback` when supported and `requestAnimationFrame` fallback. Interpolate timestamps safely; handle seeks, pause, changed playback rate, buffering and end. Align overlay Canvas coordinates to video natural resolution with proper object-fit offsets, devicePixelRatio and responsive resizing. Place SVG or Canvas top-down trajectory in matching map-coordinate projection; identical `t` drives video overlay, car pose, vectors, chart cursors and bottom readouts. Offline analysis is okay; `real-time` means re-rendered overlays in sync with playback, NOT ML running on users' devices on GitHub Pages.

## 5. Architecture and files (adapt to existing repo)

Favor clean separation:
- `analysis/` Python environment, scripts for ingest/steering/scene/calibration/fit/evaluation; tests.
- `assets/raw/` private input media; gitignored until publication/privacy reviewed.
- `assets/reference/` reference images, source notes; keep restricted licensing materials private.
- `public/media/` only consented/optimized public video and legitimate map assets.
- `public/data/analysis.json` precomputed results (no identifying VIN).
- `src/.../VideoPlayer`, `CvOverlay`, `MapReplay`, `CarSilhouette`, `TelemetryRail`, `EvidenceInspector`, `SyncController` (or matching existing framework naming).
- `docs/methods.md`, `docs/research-log.md`, `docs/assumptions.md`, `docs/validation.md`, `docs/sources.md`, `docs/decision-log.md`.
- Separate article added later only when approved.

Respect current portfolio's typography, layout, components, routes, asset conventions and deployment strategy. Prefer adding a route rather than creating unrelated website. Build with correct GitHub Pages base-path behavior so direct navigation to standalone replay works. Don't add a backend, accounts, DB, or cloud ML API. Support local development and static deployment. Optimize video with compatible H.264/AAC and `faststart` only if justified; preserve original separately.

## 6. Public-facing integrity and privacy

- Public claims must distinguish 2016 RC F FACTORY spec from estimated event-specific physics; peak engine torque does not equal torque applied during maneuver.
- Every telemetry readout must have source, method and uncertainty; show `N/A` if fundamentally not observable.
- Do not present this as accident reconstruction, expert evidence, or confirmed exact velocities.
- Avoid glamorizing dangerous public-road driving; describe as retrospective motion-analysis research, not maneuver instructions.
- Video may contain identifiable friends, other drivers, vehicle plates, audio, location, and identifying marks. Before any public commit ask whether there is consent to publish, and whether to blur/clip/mute; consider removing original audio. No VIN on web pages, analytics, public JSON, or repo.
- Apple/Google satellite imagery and Lexus art are not automatically redistributable; validate rights and attribution or create original assets.
- Capture debugging failures and changed hypotheses; do not invent successful measurements to make the blog better.

## 7. Blog, only after replay completion

Make a separate editorial portfolio article that matches my existing blog, reads like a first-person engineering case study, and links prominently to the standalone interactive replay. Cover: project motivation; initial assumptions and available media; geo-calibration; 2016 RC F geometry/spec sources; dependency/setup; steering detection experiments; optical flow masks/inliers; camera-motion failures; equations and dynamic model tradeoffs; identifiability and honest uncertainty; failed approaches and refinements; frontend time synchronization; map/legal choice; validation plots; final demo; lessons and future instrumentation (OBD/IMU/GPS). Include selected authentic screenshots and links to reproducible code and methodology; avoid dumping every raw source or private data onto the blog. Publish no unsupported performance claim. Do not begin this until I explicitly authorize it.

## 8. Acceptance tests

1. At Gate 1, a real locally running UI shows the ORIGINAL video and map/replay side by side on desktop, with telemetry fully across bottom; all controls work, placeholders labeled.
2. After analysis, steering and exterior feature overlays visibly correspond to video frames, with masks and failure states; turning overlays off gives the untouched source video.
3. Playback, seeks and timeline scrubbing remain synchronized within approximately one displayed video frame, including at different screen sizes and playback rates.
4. Top-down RC F dimensions honor factory proportions; vehicle heading and velocity vectors are independent, and trajectory is not hand-fit purely for spectacle.
5. Each displayed metric opens evidence, a method and uncertainty; ambiguous portions are not silently interpolated with unwarranted certainty.
6. Static site builds and works at its deployed GitHub Pages path without server or exposed secrets, and on desktop/mobile Safari/Chrome.
7. Tests cover coordinate transforms, unit conversions, steering-angle unwrapping, missing data, timestamp interpolation, synchronization, and schema validation.
8. Nothing goes public until privacy, map licensing, UI, model confidence and publish permissions are approved.
9. The blog remains untouched until the standalone replay is accepted.

## 9. Your very next action

**RIGHT NOW:** inspect the repository and attached assets, check the tools without assuming OpenCV exists, summarize actual findings in a short actionable inventory, then ask only the unresolved design/asset/privacy questions. Proceed to an interactive UI mock using illustrative placeholders, open/serve it, and explicitly ask for design approval. **Do not start the real CV pipeline or blog now.**