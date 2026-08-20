# Architecture

## Purpose

The target is a compact APB-connected GPIO peripheral with programmable digital I/O and interrupt support.

The architecture is intentionally split into independent responsibilities so that the eventual RTL can be developed and verified block by block.

## Top-level view

```text
                    APB MASTER
                        │
             PADDR / PWRITE / PWDATA
             PSEL / PENABLE / PREADY
             PRDATA / PSLVERR
                        │
                        ▼
             ┌─────────────────────┐
             │     APB SLAVE       │
             │ transaction control │
             └──────────┬──────────┘
                        │
                        ▼
             ┌─────────────────────┐
             │    Register Bank    │
             └───────┬─────┬───────┘
                     │     │
          ┌──────────┘     └───────────┐
          ▼                            ▼
   ┌──────────────┐             ┌──────────────┐
   │ GPIO control │             │ IRQ control  │
   │ + datapath   │             │ + event      │
   └──────┬───────┘             └──────┬───────┘
          │                            │
          ▼                            ▼
       GPIO I/O                       IRQ
```

## Design boundaries

### APB layer
Owns bus protocol timing and transaction acceptance. It should not contain GPIO-specific behaviour.

### Register layer
Translates APB addresses into configuration and status accesses.

### GPIO layer
Owns direction, output and input paths. It should not depend on APB timing beyond register-controlled configuration.

### Interrupt layer
Observes the relevant GPIO events and applies the configured interrupt policy before driving the interrupt output.

## Reset

Reset behaviour will be specified together with the final register map. Reset values must be deterministic and must leave GPIO outputs and interrupt state in a safe, documented condition.

## Implementation rule

No implementation from the reference project is being imported. This document captures the intended problem and architectural decomposition only.
