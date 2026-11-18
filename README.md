# Smart City Energy Management Simulator

Open-source smart city energy management simulator. Model solar, wind, batteries, EVs and grid demand, test control strategies, and compare scenarios through a web dashboard.

> **Status:** Early development. The project is at the initial setup stage and the simulation engine is not yet implemented.

## Overview

This project lets planners, researchers and students model how a city's energy system behaves under different conditions before anything is built. You define a district, choose its assets, set a scenario, run a simulation, and see how cost, renewable share, CO₂ and peak load change.

The core question the MVP answers:

> How does adding more solar capacity or battery storage change peak grid import, cost and emissions over a 24-hour day?

## How it works

The simulator advances time in fixed steps (for example every 15 minutes or every hour). Each step:

1. Updates weather and scenario events
2. Calculates generation from each source and demand from each zone
3. Balances supply and demand: renewables first, then battery discharge, then grid import or backup generation
4. Checks constraints such as line capacity, battery limits and shortages
5. Records metrics: cost, CO₂, reliability and efficiency

A control layer decides how storage and flexible loads are managed, for example "charge batteries when solar is high and prices are low".

### Modeled entities

| Category | Examples |
|---|---|
| Supply | Solar, wind, grid import, backup plants, battery storage |
| Demand | Residential, commercial, industrial, EV charging, street lighting |
| Network | Substations and lines with capacity limits |

### Fidelity

Version 1 uses a **simplified supply and demand balance model**. It does not model voltages, line losses or full power flow.

## Planned architecture

```
.
├── engine/   # Simulation engine (Python, NumPy/Pandas), deterministic and testable
├── api/      # FastAPI service exposing run, scenario and results endpoints
├── web/      # React/Next.js dashboard with map and charts
└── docs/     # Architecture notes, scenario schema, assumptions
```

| Layer | Planned technology |
|---|---|
| Engine | Python, NumPy, Pandas |
| Backend | FastAPI, WebSockets for live updates |
| Frontend | React or Next.js, Leaflet or Mapbox, Recharts or ECharts |
| Database | PostgreSQL (TimescaleDB for time-series) |

## Roadmap

- [ ] **MVP:** one district, solar, grid, battery and residential demand, 24-hour run, supply vs demand chart
- [ ] **V2:** multi-zone map, weather inputs, EV demand, scenario saving and comparison
- [ ] **V3:** real data sources, forecasting, optimization strategies, report export
- [ ] **V4:** collaboration, user roles, API access, live sensor data integration

## Getting started

Setup instructions will be added once the engine and API are in place.

```bash
git clone https://github.com/BoluwatifeOsifule/SmartCityEnergyManagement.git
cd SmartCityEnergyManagement
```

## Contributing

Contributions are welcome. Until a full contributing guide exists:

1. Fork the repository and create a branch from `main` using a prefix such as `feat/`, `fix/` or `docs/`
2. Keep changes focused and include tests where relevant
3. Open a pull request describing what changed and why

## License

Released under the [MIT License](LICENSE).
