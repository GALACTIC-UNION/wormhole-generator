# Integration Guide — Wormhole Generator (WHG)

## ASTRAL-GUARDIAN Core Bus

This module communicates with the ASTRAL-GUARDIAN core over gRPC.

### Registering the Module

```python
from astral_guardian.client import AstralGuardianClient

client = AstralGuardianClient.connect("astral-guardian-core:50051")
client.register_module(
    module_id="wormhole-generator",
    capabilities=['topology', 'stability', 'exotic_matter', 'simulation'],
    safety_class="A",
)
```

### Telemetry Publishing

The module publishes operational telemetry every 10 seconds:

```python
telemetry = {
    "module": "wormhole-generator",
    "status": "operational",
    "power_w": current_power,
    "safety_interlocks": "clear",
}
client.publish_telemetry(telemetry)
```

## Safety Interlocks

Before any high-power operation:

1. Request authorization from GALACTIC-UNION Safety
2. Confirm ASTRAL-GUARDIAN watchdog is registered
3. Verify no conflicting field operations from sibling modules
4. Execute with continuous safety monitor running

## Alert Routing

Alerts are routed to:
- `astral_guardian_core` — primary safety response
- `galactic_union_council` — Tier-A events requiring human oversight
- `nexus_prime` — synthesis and strategic response
