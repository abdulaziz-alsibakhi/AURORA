# Safety Controller

The safety subsystem evaluates and, when required, modifies a candidate action before it reaches the reservoir simulator.

The intended design combines a reduced-order reservoir model, model-mismatch characterization, constrained optimization / quadratic programming, and explicitly documented operating constraints.

A central AURORA question is what happens when the simplified model used for safety decisions differs from the higher-fidelity numerical environment. Safety claims must therefore be phrased as enforcement of encoded constraints within the modeled experiment, not unconditional real-field safety.
