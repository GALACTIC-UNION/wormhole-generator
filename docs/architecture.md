# Architecture — Wormhole Generator (WHG)

## System Overview

```
┌─────────────────────────────────────────────────────────────┐
│                   Wormhole Generator (WHG)                    │
├──────────────┬──────────────┬──────────────┬────────────────┤
│ topology     │ stability    │ exotic_matter │ api            │
└──────────────┴──────────────┴──────────────┴────────────────┘
                              │
              ASTRAL-GUARDIAN Core Bus
              │                     │
    NEXUS-PRIME            GALACTIC-UNION Safety
```

## Component Responsibilities

| Module | Responsibility |
|--------|----------------|
| `src/topology/` | Topology operations |
| `src/stability/` | Stability operations |
| `src/exotic_matter/` | Exotic Matter operations |
| `src/simulation/` | Simulation operations |
| `src/api/` | REST interface for external consumers |

## Integration Points

- **ASTRAL-GUARDIAN Core**: Primary control bus; receives field parameters and emits telemetry
- **NEXUS-PRIME**: Receives status and anomaly reports for system-wide synthesis
- **GALACTIC-UNION Safety**: Authorization gate for high-power operations
- **ELYSIUM-CORE**: Compliance monitoring and audit logging

## Failsafe Design

All high-power operations include watchdog-monitored failsafes. On watchdog timeout or abort signal, the system returns to its lowest-power safe state within the configured shutdown window.
