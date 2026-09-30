# System Overview

## Purpose

This document will become the canonical component-level description of AURORA.

## Components

**Reservoir Simulation** provides the numerical controlled environment and produces observations after actions are applied.

**AI Controller** produces candidate actions from the information available to the policy. The current intended family is recurrent reinforcement learning.

**Safety Controller** evaluates and, where necessary, modifies candidate actions before they reach the simulator. The intended design combines a reduced-order reservoir representation with constrained optimization.

**Data & Logging** records enough information to reproduce, inspect, and compare experiments.

**Validation** checks outputs against explicitly documented rules and constraints rather than relying on whether plots merely look plausible.

**Demo & Dashboard** exposes system state, decisions, safety interventions, and experimental behavior in a form understandable without reading terminal output.

## Open definitions

The observation/action spaces, objective, control interval, exact constraints, component contracts, failure semantics, and experiment-facing telemetry remain specification items until explicitly frozen.
