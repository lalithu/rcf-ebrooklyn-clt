# Computer-vision research plan

No tracking or ML has run yet. Recorded clip metadata (verify on Mac): H.264, 512×910 portrait, 30 fps, 450 frames, 15 seconds. Preserve original timestamps. Frames can be occluded by cabin objects, hands, variable exposure, reflections and traffic.

## Observations, in order

1. Ingest with OpenCV/ffprobe; preserve source. Record presentation timestamps, codec, orientation, sample contact sheet and ROI visibility intervals.
2. Label ROI for steering wheel, static cabin stabilizers and external scene. Exclude hands, moving vehicles, reflective windows, sky, pedestrians and unreliable regions.
3. Track steering-rim/spoke points across frames using Shi–Tomasi corners + pyramidal Lucas–Kanade optical flow; stabilize against static cabin geometry. Unwrap turns, track landmark symmetry, occlusion and unknown steering zero. Compare against manual annotations on held-out frames.
4. Track exterior stationary candidates with KLT/ORB correspondences + robust RANSAC; report image-space flow inliers/outliers, parallax/occlusion and camera motion. Homography only where plane assumptions fit, not a magic 3D vehicle pose estimate.
5. Derive supported orientation changes / yaw estimates with confidence. Phone motion can masquerade as car rotation. Missing landmarks must yield nulls or uncertainty, never manufactured exact values.
6. Use a pretrained segmentation/keypoint model only if classical tracking demonstrably fails. Do not train a new deep network on ~450 video frames by default.
7. Export time-indexed coordinate arrays, provenance, observation confidence, masks and diagnostic frames to offline JSON. Overlays are drawn in the browser; original pixels remain untouched.

## Candidate APIs

OpenCV: goodFeaturesToTrack, calcOpticalFlowPyrLK, ORB_create, BFMatcher, findHomography/RANSAC, optional Farneback for dense-flow visualization. Optical flow is measured in image pixels per frame, not mph. Camera calibration, scene depth, independent motion constraints and scale are necessary before metric translation.

## Validation

Count per-frame valid steering keypoints, stationary-scene inliers, residual motion, occlusion dropout, and reviewer corrections. Annotate selected frames manually. Use time-block holdouts and sensitivity sweeps on masks, thresholds, geometric priors. Report any periods where 360° heading is unsupported.

References: [OpenCV optical flow](https://docs.opencv.org/4.x/d4/dee/tutorial_optical_flow.html), [OpenCV calibration and geometry](https://docs.opencv.org/4.x/dc/d6b/group__calib3d.html).
