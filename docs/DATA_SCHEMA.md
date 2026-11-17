# Proposed static replay data contract (not generated yet)

Per video timestamp t (seconds), store observed video points at intrinsic 512×910 coordinates, validity masks and tracking confidence. Fitted state, IF identifiable: ground x/y meters, yaw radians, velocity and yaw rate with uncertainty. Use explicit kind observed / inferred / scenario / unavailable for EVERY metric and preserve evidence references and units. Do not write sample numerical telemetry that could be mistaken for measurements.

Suggested project objects: media (duration, frame timestamps, crop, privacy), map (projection, source, transform, RMS error), vehicle (dimensions, factory spec citations), tracks (pixel keypoints, flow vectors and inlier flags), states (fitted pose and interval uncertainty), evidence (source frame, method, assumptions, calibration ID, residual), annotations (manual labels/owner review).

The browser uses one time-indexed master timeline to sync video overlays, map car, bottom graphs and metric inspector. Null fields are normal and should be rendered as unavailable, never silently interpolated.
