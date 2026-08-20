# Verification Plan

The verification environment will be created independently with the RTL.

## Layers

### 1. APB protocol

Verify legal setup/access sequencing, read/write behaviour, completion and reset handling.

### 2. Register functionality

For every register:

- reset value
- write/read behaviour
- writable/read-only fields
- reserved-bit behaviour

### 3. GPIO functionality

- output programming
- input observation
- direction changes
- reset behaviour

### 4. Interrupt functionality

- configured event detection
- enable/mask operation
- status/pending behaviour
- clear/acknowledge behaviour
- simultaneous or repeated events

### 5. Integration

Exercise realistic software-like APB sequences while GPIO activity changes asynchronously or synchronously according to the final design assumptions.

## Evidence to collect

The final repository should contain reproducible evidence such as:

- simulation logs
- representative waveforms
- directed-test results
- assertions
- coverage summary
- synthesis results where applicable

No verification result is claimed at this stage because the implementation has not yet been recreated.
