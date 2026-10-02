# Robotics and Sensor Reading Checklists

Read only the sections relevant to the current code. These are investigation prompts, not a requirement to explain everything at once.

## All sensor paths

Trace:

- physical quantity and units;
- coordinate frame and axis convention;
- hardware timestamp, ROS timestamp, arrival time, and clock source;
- sampling rate and whether code assumes a fixed interval;
- calibration, scale, bias, saturation, range, and validity checks;
- buffering, ordering, synchronization, interpolation, and dropped data;
- noise representation and whether it is standard deviation, variance, covariance, density, or a heuristic weight.

## Coordinate transforms and poses

Determine the project's convention before explaining a transform:

- what `T_AB`, `world_from_base`, or equivalent maps from and to;
- whether translation is the source origin expressed in the target frame;
- whether vectors use column-vector multiplication;
- quaternion component order and multiplication order;
- whether a pose describes a body in a world or transforms coordinates between frames;
- whether ROS message parent/child frames agree with the mathematical convention.

For every important transform, write the source point, target point, direction, formula, and code variables. Check composition from right to left.

## LiDAR, radar, and point clouds

Look for point fields, rings/channels, intensity, per-point time, invalid values, blind range, maximum range, downsampling, deskewing, frame transforms, nearest-neighbor search, map insertion, and output frame.

Separate a single point type, a point-cloud container, and a pointer to a cloud. Explain whether filtering changes capacity, size, or point contents.

## IMU

Identify angular velocity, acceleration/specific force, units, axes, gravity convention, bias, scale, noise, integration interval, initialization assumptions, and time coverage relative to other sensors.

Distinguish raw measurement, calibrated measurement, running mean, predicted state, and estimated bias. Do not call every acceleration vector “gravity” without tracing the formula.

## Cameras and vision

Trace image encoding, camera model, intrinsics, distortion, exposure timestamp, optical-frame convention, feature/detection representation, depth source, extrinsics, and whether a pose refers to camera or robot base.

Separate image processing, geometric estimation, tracking, and downstream fusion.

## GNSS and encoders

For GNSS, trace geodetic versus local coordinates, datum/origin, covariance/fix status, antenna lever arm, heading source, and timestamp. For encoders, trace counts, direction, resolution, gear ratio, wheel geometry, slip assumptions, and conversion to velocity or displacement.

## Filtering and state estimation

Locate and name:

- state variables and the frame of each component;
- prediction input and motion model;
- measurement and observation model;
- residual definition and sign;
- covariance/noise matrices and units;
- Jacobians and the variables about which they are taken;
- update acceptance, gating, reset, and failure behavior.

Teach in this order when possible: state meaning -> data flow -> scalar/vector equations -> matrix form -> code. Postpone derivations of Jacobians, Lie algebra, or solver internals until prerequisites are present or the learner requests them.

## ROS and system integration

Trace node creation, parameters, publishers, subscriptions, callbacks, services, timers, callback groups, executors, QoS, TF ownership, launch wiring, remaps, and diagnostics.

Distinguish message queue depth from frequency. Distinguish callback arrival from algorithm update and output timer rates. When concurrency exists, identify shared state and synchronization before discussing algorithm math.

## Perception tasks

For detection or tracking, trace preprocessing, model input/output, coordinate conversions, confidence thresholds, association, track state, lifecycle, and published representation. Separate learned-model behavior from deterministic postprocessing and state estimation.

## Units and validity audit

When a line combines values, verify compatible units and frames. Watch for degrees versus radians, seconds versus nanoseconds, meters versus millimeters, standard deviation versus variance, and row-major configuration versus Eigen storage order.

If the code or configuration does not establish a convention, say what evidence is missing instead of choosing one silently.
