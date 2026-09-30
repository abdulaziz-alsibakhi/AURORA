# AI Controller

The AI Controller produces candidate reservoir-control actions. The current intended family is recurrent reinforcement learning, with RPPO as the planned approach.

This workstream should define observation space, action space, objective/reward, recurrent state/history, training environment, preprocessing/normalization, action bounds, training configuration, evaluation procedure, reproducibility controls, and baselines.

The learned controller proposes actions; it does not independently establish that an action satisfies the constraints enforced by the separate safety subsystem.
