---
id: behave
title: Scenario tests with behave
summary: Tests written as scenarios that domain experts can read
category: test
example: .
domains: [lighting]
protocols: [CAN]
key_files:
  - tests/behave/features/hazard_light.feature
  - tests/behave/features/blink_left.feature
  - tests/behave/features/steps/example_steps.py
  - tests/behave.instance.yaml
related: [pytest, traceability]
run:
  build: [instances/hello_world/main.instance.yaml, settings/can_over_udp.settings.instance.yaml]
  profiles: [behave]
  up_args: [--abort-on-container-exit]
screenshot:
  kind: static
  source: studio
  view: graph
  file: instances/hello_world/main.instance.yaml
---

# Test cases in python (behave)

Using behave to write test cases allows your domain experts to more easily understand the tests that are being run.

- Part of the [RemotiveCar example](../DOCS.md)
- Example features: [blink_left.feature](../tests/behave/features/blink_left.feature) and [hazard_light.feature](../tests/behave/features/hazard_light.feature)
- Example step implementation [example_steps.py](../tests/behave/features/steps/example_steps.py)
- Control how to run tests: [behave.instance.yaml](../tests/behave.instance.yaml)
- Python project: [pyproject.toml](../tests/pyproject.toml)

Start topology and run tests:

```bash
remotive topology build ...
docker compose -f ... --profile behave up --abort-on-container-exit
```

Optionally first start topology and then run tests (useful when writing tests)

```bash
# build and start
remotive topology build ...
docker compose -f ... up
# run tests in separate shell (dont forget --build)
docker compose -f ... up behave --build
```

Example with `hello_world` instance:

```bash
remotive topology build -f instances/hello_world/main.instance.yaml build
docker compose -f build/remotive_car_hello_world/docker-compose.yml --profile behave up --abort-on-container-exit --build
```

Notice:
- Tests are run in a container as part of the topology.
- By using a profile you can use the same instance and use the profile to control if the tests should run or not.
- In this example the same Dockerfile is used for all python code in order to reuse the same base image. You can of course use separate Dockerfile for each container.
