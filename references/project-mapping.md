# Project Mapping and Curriculum Design

Use this reference only when first entering a project, when the repository changed materially, or when the user asks for a new project map.

## Evidence to inspect

Inspect enough of the following to establish the real execution path:

- top-level documentation and build files;
- package manifests, dependencies, and language versions;
- `main`, component registration, executable targets, launch files, and configuration;
- node constructors and callback registration;
- message definitions, sensor adapters, and internal data structures;
- core processing classes and their public interfaces;
- publishers, services, files, maps, diagnostics, or actuator outputs;
- tests when they clarify intended behavior or conventions.

Use fast source search before broad reading. Follow definitions and callers rather than trusting filenames. For a large repository, map only the path relevant to the user's goal.

## Build the project map

Report a compact map with these parts:

1. **Purpose:** what the program consumes, computes, and produces.
2. **Technology:** relevant C++ standard, ROS version, Eigen/PCL/OpenCV/Ceres or other libraries actually present.
3. **Entrypoints:** executable, node, launch, component, or service entry.
4. **Modules:** each major module's responsibility and important files.
5. **Data flow:** sensor or message input through processing to output.
6. **Runtime configuration:** launch and parameter files that materially change behavior.
7. **Recommended reading:** files to learn now, files to postpone, and why.
8. **Prerequisites:** only knowledge needed for the first few lessons.

A useful data-flow sketch is usually enough:

```text
sensor/message
  -> validation and buffering
  -> preprocessing and synchronization
  -> coordinate/calibration handling
  -> estimation/perception algorithm
  -> state/map/track
  -> ROS message, TF, file, or control output
```

Adapt the boxes to the actual system. Do not force every project into this exact pipeline.

## Create the learning route

Choose lessons by dependency and difficulty:

- begin with code that exposes project vocabulary and data movement;
- introduce syntax in the context where it first matters;
- place coordinate frames and timing before algorithms that depend on them;
- teach mathematical state and measurements before covariance, Jacobians, or optimization internals;
- postpone generated code, third-party libraries, dense template machinery, and unrelated utilities.

For each proposed lesson, name the real file or function and the main learning outcome. Keep the initial route short enough to revise as the learner progresses.

## First teaching handoff

After the project map and route, identify one approachable starting location. Explain why it is the right start and what the learner should observe. Unless the user asks for immediate explanation, show only a small first snippet and ask for their initial translation in the next interaction.

Do not make code changes during project mapping unless the user separately authorized implementation.
