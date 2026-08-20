# Interrupt Model

The interrupt subsystem will convert selected GPIO activity into a host-visible interrupt.

## Conceptual path

```text
GPIO state
   │
   ▼
Event detector
   │
   ▼
Event qualifier
   │
   ├──────────────► status / pending state
   │
   ▼
Enable / mask
   │
   ▼
 IRQ output
```

## Decisions to make during reimplementation

- edge versus level detection
- rising/falling or equivalent event selection
- whether multiple sources can remain pending simultaneously
- interrupt clear mechanism
- behaviour when a new event arrives while an interrupt is already pending
- reset state of interrupt status and enable bits

These decisions will be made independently and then encoded in the final register map and RTL.
