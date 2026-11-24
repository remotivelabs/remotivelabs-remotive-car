---
id: python-models
title: Python behavioral models
summary: Model ECUs that don't exist yet, in a few lines of Python
category: simulate
example: .
domains: [lighting, powertrain]
protocols: [CAN, SOME/IP]
key_files:
  - models/bcm/python/bcm
  - models/gwm/python/gwm
  - models/bcm/python/tests
  - instances/ecus/BCM/python.instance.yaml
  - instances/ecus/GWM/python.instance.yaml
related: [fmu, pytest, jupyter]
run:
  build: [instances/hello_world/main.instance.yaml, settings/can_over_udp.settings.instance.yaml]
  profiles: [jupyter]
  after: Open http://localhost:8888 and use the notebook to press the buttons that the models react to.
screenshot:
  kind: static
  source: studio
  view: graph
  file: instances/hello_world/main.instance.yaml
---

# Behavioral models in python

Writing behavioral models in python is a very simple way of creating models for ECUs that don't yet exist. For more complex models it is also useful to create unit tests.

- Part of the [RemotiveCar example](../DOCS.md)
- Behavioral models: [bcm](../models/bcm/python/bcm) and [gwm](../models/gwm/python/gwm)
- Unit tests: [tests](../models/bcm/python/tests)
- Instance files: [BCM/python](../instances/ecus/BCM/python.instance.yaml) and [GWM/python](../instances/ecus/GWM/python.instance.yaml)

Notice:
- The platform is included in each instance, since the instance depends on the platform. However, in a larger platform it would probably make sense to only include the part of the platform describing each ECU.
- In this example the same Dockerfile is used for all python code in order to reuse the same base image. You can of course use separate Dockerfile for each container.

## Running unit tests

Complex behavioral models should have unit tests. To run the unit tests for BCM:

```bash
cd models/bcm/python/bcm
uv sync
uv run poe test
```
