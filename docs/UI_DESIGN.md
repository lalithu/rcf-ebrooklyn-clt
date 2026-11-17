# UI plan — owner approval gate first

The FIRST output is a local runnable mock with illustrative/unmeasured motion and a visible watermark stating that. Design: minimal, sharp, dark-neutral, technical/Apple-like with subtle blue/cyan motion accents; avoid clutter. Keep actual video and accurately proportioned overhead RC F as peers, with the TELEMETRY PANEL FULL-WIDTH AT THE BOTTOM.

## Desktop composition

Header: RC F / Dynamics Lab, intersection, method labels. Left: portrait original video, Canvas overlay layer at identical logical coordinates. Right: bird's-eye map or provisional schematic, vehicle silhouette, independent heading/velocity vectors, optional path trail. Bottom: speed, steering-wheel rotation, yaw rate, sideslip, timeline, trace plots and provenance badges. Responsive small screens stack video/map and preserve accessible bottom telemetry rail.

## Controls and evidence

Global play/pause and precise time seek, speed selector if useful, frame stepping, replay, sync. Overlay modes: None, Steering, Static landmarks, Optical flow, Combined. Toggle fitted path versus raw detections, show valid/invalid features and confidence. Clicking a metric explains source frame/keypoints, units, derivation, assumption, confidence, and why unavailable. Original video never altered; Canvas overlay can be hidden completely. Do not silently fill empty estimates with simulated numbers.

## Synchronization

One HTMLVideoElement supplies master currentTime. Use requestVideoFrameCallback when available and animation-frame fallback. Align intrinsic video coordinates through object-fit contain offsets and device pixel ratio. Seek/update all layers from same timestamp; handle variable FPS, buffering, playback speed and resize. Static precomputed JSON powers replay on GitHub Pages; no inference API or Python required client-side.

## Owner approvals

Gate 1: UI appearance, layout, controls. Gate 2: science feasibility/map/privacy. Gate 3: measured data and uncertainty. Gate 4: public media and Pages deployment. Gate 5: blog only after shipping.
