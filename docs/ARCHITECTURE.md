# Architecture Proposal

## 1. Guiding idea

Keep the simulation core independent from visualization engines and external environments. Adapters should translate between stable project data formats and optional tools.

## 2. Proposed layers

### Core simulation

Owns domain types and deterministic simulation rules:

- road graph and lane topology
- vehicle state and motion parameters
- agent decisions
- simulation clock and event scheduling
- metrics and reproducible scenario configuration

### Adapters

Translate between the core model and external tools. An adapter must document supported versions, data formats, limitations, and licensing constraints.

Potential future adapters may target visualization engines or import/export scenario formats. No commercial-game integration is implemented at this stage.

### Visualization

Displays simulation state, diagnostics, and replay data. A real-time engine can be used here without becoming the owner of the simulation's source of truth.

### Testing and evaluation

Provides deterministic unit tests, scenario regression tests, and benchmark datasets. Metrics should be defined before performance claims are made.

## 3. Initial data concepts

A first prototype may use the following conceptual entities:

- **RoadNode**: a junction or network endpoint.
- **RoadSegment**: a directed connection with length, capacity, and speed constraints.
- **VehicleAgent**: an entity with position, velocity, route, and behavior state.
- **Scenario**: a versioned network, initial conditions, and simulation parameters.
- **MetricSample**: a timestamped measurement such as throughput, travel time, queue length, or collision count.

Units and coordinate conventions must be explicit in any implementation.

## 4. Suggested first technical slice

Implement a small directed road graph, route planning, and a deterministic vehicle update loop. Add tests for route validity, boundary conditions, and repeatability before adding 3D rendering or external integrations.

## 5. Non-goals for the initial milestone

- Reimplementing a commercial game.
- Shipping third-party game assets.
- Claiming physically accurate crash simulation.
- Depending on proprietary game internals.
- Building a city-scale simulator before a minimal scenario works.
