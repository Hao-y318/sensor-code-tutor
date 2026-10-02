# Guided Lesson Protocol

Use this reference for interactive source-code lessons.

## Select one coherent region

Default to 20-80 continuous lines that implement one understandable action. Use 3-20 lines when the learner is studying a single C++ construct, Eigen expression, callback, message field, or equation. Avoid hundreds of lines and avoid fragments so small that control flow becomes misleading.

State briefly:

- which module and function contain the region;
- who calls it or what event triggers it;
- where its result goes;
- why this region is the next useful lesson.

## Prediction before explanation

Show the necessary code, then ask the learner to translate or predict it. Prefer one to four focused questions, such as:

- What object or container is read and what receives the result?
- What does this symbol change about ownership, mutability, or control flow?
- Which coordinate frame contains the input and output?
- What physical quantity might this variable represent?
- What happens when this condition is false?

Do not reveal the full answer in the question. If the learner says they do not know, teach directly without making them guess repeatedly.

## Correct and connect the layers

After the learner answers, address their exact interpretation first. Then use only the layers relevant to this region:

1. **C++ syntax:** function, parameter, class, struct, object, member, pointer, reference, `const`, `auto`, template, lambda, smart pointer, STL, callback, threading, lifetime, or control flow.
2. **Type and data structure:** exact or aliased types, dimensions, container element, ownership, and copy/reference behavior.
3. **Program logic:** why the program performs this action here and what changes afterward.
4. **Eigen/ROS:** matrix/vector/quaternion operations, messages, nodes, topics, TF, services, timers, parameters, and bags.
5. **Mathematics:** formula, dimensions, derivation, assumptions, and code-variable correspondence.
6. **Sensor meaning:** measurement, units, axes, timestamp, calibration, noise, validity, and physical interpretation.
7. **Algorithm meaning:** role in prediction, update, matching, filtering, optimization, mapping, tracking, or another pipeline stage.

Do not mechanically include every layer. Omit layers that add no understanding.

## Translate mathematics back to code

For a mathematical statement, explicitly connect both directions.

Example:

```cpp
P = F * P * F.transpose() + Q;
```

Explain as needed:

- `P`, `F`, and `Q` types and matrix dimensions;
- `*` as Eigen matrix multiplication and `transpose()` as a member call;
- the formula `P_k = F P_{k-1} F^T + Q`;
- `F` propagating prior uncertainty and `Q` adding process uncertainty;
- which state and time interval these variables represent in this project.

For coordinates, always write a direction-check equation such as:

```text
p_target = T_target_source * p_source
```

Name every frame, the frame in which translations and vectors are expressed, and the multiplication order. Do not trust names such as `body`, `world`, or `transform` without tracing their source.

## Drill an unfamiliar symbol

When one symbol blocks reading, use this order:

1. name the syntax;
2. state what it does;
3. show a minimal ordinary C++ example;
4. return immediately to the project line;
5. ask the learner to translate that original line.

Distinguish similar forms explicitly when they are the source of confusion, for example `.` versus `->`, `T` versus `T&`, `const T&` versus trailing `const`, `window_->reset()` versus `window_.reset()`, or template arguments versus function arguments.

## Finish each lesson

Return to the original code and give a natural-language reading of the whole region. Then ask one small check that tests the current concept rather than a new topic.

Move on once the learner demonstrates understanding. If their answer exposes one misconception, correct only that misconception before adding new material.

When several lessons are complete, reconnect them to the project data flow so the learner sees how local statements contribute to the system.
