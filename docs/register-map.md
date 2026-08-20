# Register Map

The register map is intentionally **not frozen yet**.

The repository currently documents the functional groups that the software interface will need without copying addresses, bit fields or implementation choices from the reference project.

## Planned groups

| Group | Purpose |
|---|---|
| GPIO direction | Select input/output behaviour |
| GPIO output | Program output values |
| GPIO input | Read current/sampled input state |
| Interrupt enable | Enable selected interrupt sources |
| Interrupt configuration | Select supported event conditions |
| Interrupt status | Observe pending events |
| Interrupt clear/control | Clear or acknowledge events |

## Freeze criteria

Before RTL implementation, the following will be explicitly recorded:

- register address width
- register offsets
- reset values
- read/write permissions
- field widths
- reserved bits
- interrupt source mapping
- interrupt clearing semantics

Once frozen, the table in this document becomes the single source of truth for the RTL and testbench.
