---
id: pytest
title: Test cases with pytest
summary: Integration tests as Python code, run as part of the topology
category: test
example: .
domains: [lighting]
protocols: [CAN, LIN]
key_files:
  - tests/pytest/test_simulate_driver.py
  - tests/pytest.instance.yaml
  - tests/pyproject.toml
related: [behave, python-models, behavioral-model-test]
run:
  build: [instances/hello_world/main.instance.yaml, settings/can_over_udp.settings.instance.yaml]
  profiles: [tester]
  up_args: [--abort-on-container-exit]
screenshot:
  kind: static
  source: studio
  view: graph
  file: instances/hello_world/main.instance.yaml
---

# Test cases in python (pytest)

Using pytest to write test cases is a simple way to express your test cases as code.

- Part of the [RemotiveCar example](../DOCS.md)
- Example test case: [test_simulate_driver.py](../tests/pytest/test_simulate_driver.py)
- Control how to run tests: [pytest.instance.yaml](../tests/pytest.instance.yaml)
- Python project: [pyproject.toml](../tests/pyproject.toml)

Start topology and run tests:

```bash
remotive topology build ...
docker compose -f ... --profile tester up --abort-on-container-exit
```

Optionally first start topology and then run tests (useful when writing tests)

```bash
# build and start
remotive topology build ...
docker compose -f ... up
# run tests in separate shell (dont forget --build)
docker compose -f ... up tester --build
```

Example with `hello_world` instance:

```bash
remotive topology build -f instances/hello_world/main.instance.yaml build
docker compose -f build/remotive_car_hello_world/docker-compose.yml --profile tester up --abort-on-container-exit --build
```

Notice:
- Tests are run in a container as part of the topology.
- By using a profile you can use the same instance and use the profile to control if the tests should run or not.
- In this example the same Dockerfile is used for all python code in order to reuse the same base image. You can of course use separate Dockerfile for each container.
