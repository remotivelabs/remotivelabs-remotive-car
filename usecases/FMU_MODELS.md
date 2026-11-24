---
id: fmu
title: FMU models
summary: Run an exported FMU as the behavior of an ECU
category: simulate
example: .
domains: [lighting]
protocols: [CAN]
key_files:
  - models/bcm/fmu/bcm
  - instances/ecus/BCM/fmu.instance.yaml
  - instances/fmu/main.instance.yaml
related: [python-models, pytest]
run:
  build: [instances/fmu/main.instance.yaml, settings/can_over_udp.settings.instance.yaml]
screenshot:
  kind: static
  source: studio
  view: graph
  file: instances/fmu/main.instance.yaml
---

# FMU models

Using Functional Mock-up Units (FMUs) allows you to integrate standardized simulation models as ECU behavior. This is
useful when the model of an ECU already exists as an FMU, for instance exported from a modelling tool, and you want to
run it against the real communication of the rest of the platform.

RemotiveTopology maps network signals onto the input variables of the FMU, steps the FMU, and publishes its output variables
back onto the bus. The model itself needs no knowledge of the platform.

- Part of the [RemotiveCar example](../DOCS.md)
- Instance: [RemotiveCar FMU instance](../instances/fmu)
- FMU model: [bcm/fmu](../models/bcm/fmu/bcm)
- Instance file: [BCM/fmu.instance.yaml](../instances/ecus/BCM/fmu.instance.yaml)

The `BCM` of the RemotiveCar example has two interchangeable implementations, a
[python behavioral model](../models/bcm/python/bcm) and an [FMU](../models/bcm/fmu/bcm). Both
are driven by the same signals and verified by the same tests, so the two instances are a direct comparison of the two
approaches.

Notice:
- FMU support is an optional dependency of the library, install it as `remotivelabs-topology[fmu]`.
- The FMU declares its own step size, and RemotiveTopology steps it at that rate. The `BCM` FMU uses 50 ms.
- Which signal feeds which FMU variable is declared as data, in the `INPUT_MAPPING` of the model. Only the outputs need
  a few lines of code, to publish them on the restbus.
