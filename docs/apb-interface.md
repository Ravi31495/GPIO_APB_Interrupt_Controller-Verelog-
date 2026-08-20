# APB Interface

The controller is intended to behave as an APB peripheral.

## Signals

The final RTL will define the exact signal widths and naming, but the interface concept is:

| Signal | Direction | Role |
|---|---|---|
| `PCLK` | input | APB clock |
| `PRESETn` | input | Active-low reset |
| `PSEL` | input | Peripheral selected |
| `PENABLE` | input | Access phase indicator |
| `PWRITE` | input | Read/write selection |
| `PADDR` | input | Register address |
| `PWDATA` | input | Write data |
| `PRDATA` | output | Read data |
| `PREADY` | output | Transfer completion |
| `PSLVERR` | output | Error indication |

## Transfer phases

```text
SETUP                 ACCESS
┌────────────┐       ┌────────────┐
│ PSEL = 1   │──────►│ PSEL = 1   │
│ PENABLE=0  │       │ PENABLE=1  │
│ Addr valid │       │ Data valid │
└────────────┘       └────────────┘
```

The implementation will be written and checked against the APB protocol rather than assuming that a simple clocked register interface is sufficient.

## Planned checks

- setup/access ordering
- stable address and control during access
- read-data validity
- write-data capture
- ready/error behaviour
- reset during/around transactions
