# Physics and identifiability

This is an inverse problem, not a known ground-truth recording. Prioritize observable quantities before modeling. Fitting a trajectory that visually traces the hand-drawn circle is NOT evidence of a 360° measurement.

## Coordinates and state

Use ground-frame x (east, meters), y (north, meters), yaw ψ (radians), body-frame longitudinal/lateral velocities u/v (m/s), yaw rate r (rad/s). Derive body heading separately from world velocity direction; sideslip β = atan2(v,u) when u,v are actually constrained. Use physical time stamps, not assumed equal intervals if video metadata contradicts nominal frame rate.

## Model hierarchy

- Constant-velocity/heading or kinematic bicycle baseline: sanity checks only; no-slip assumptions break during drifting.
- Planar dynamic bicycle / rigid-body model with lateral velocity, yaw inertia, tire force and unknown steering/throttle inputs. Distinguish steer-wheel input from unknown front tire angle.
- Robust batch smoothing / weighted least squares or constrained filtering against image-heading candidates, steering rotation observations and manually calibrated map anchors. Carry model parameters as priors with sensitivity bounds, rather than exact vehicle-specific measurements.
- Separate scenario bands for wheel torque, surface friction, tire stiffness, drivetrain loading. They are not inferred facts without gear, RPM, throttle, OBD, IMU or GPS.

## Estimate eligibility

| Metric | Intended output |
|---|---|
| Steering-wheel change | Observed when visible, with tracking uncertainty |
| Yaw / yaw rate | Inferred only where exterior orientation constraints exist |
| Position/speed | Inferred only if ground calibration + motion constraints are defensible; otherwise unavailable |
| Slip angle | Strongly model-dependent unless velocity direction independently observed |
| Actual engine torque | Unavailable |
| Factory peak torque | Reference specification, explicitly not event telemetry |

Use robust losses, bounds, held-out landmark checks, multiple hypotheses and confidence intervals. A beautifully smooth single fit is not proof. Store null where data is unidentifiable. For units, keep SI internally and convert to mph/deg visually. Reference: [SciPy least_squares](https://docs.scipy.org/doc/scipy/reference/generated/scipy.optimize.least_squares.html).
