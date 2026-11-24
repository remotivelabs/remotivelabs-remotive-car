---
id: jupyter
title: Jupyter notebook
summary: Drive a running topology from a notebook with buttons and plots
category: visualize
example: .
domains: [lighting]
protocols: [CAN]
key_files:
  - common/jupyter/car.ipynb
  - common/jupyter/jupyter.instance.yaml
  - common/jupyter/pyproject.toml
related: [3d-visualization, python-models]
run:
  build: [instances/hello_world/main.instance.yaml, settings/can_over_udp.settings.instance.yaml]
  profiles: [jupyter]
  after: Open http://localhost:8888 and run the notebook.
screenshot:
  kind: static
  source: studio
  view: graph
  file: instances/hello_world/main.instance.yaml
---

# Jupyter notebook

Using RemotiveTopology framework from Jupyter notebook allows you to interact with a running instance and easily create custom user interfaces.

- Part of the [RemotiveCar example](../DOCS.md)
- Example notebook [car.ipynb](../common/jupyter/car.ipynb)
- Control how to run [jupyter.instance.yaml](../common/jupyter/jupyter.instance.yaml)
- Python project: [pyproject.toml](../common/jupyter/pyproject.toml)

Start topology and jupyter:

```bash
remotive topology build ...
docker compose -f ... --profile jupyter up
```

Example with `hello_world` instance:

```bash
remotive topology build -f instances/hello_world/main.instance.yaml build
docker compose -f build/remotive_car_hello_world/docker-compose.yml --profile jupyter up --build
```

Notice:
- Jupyter is run in a container as part of the topology.
- By using a profile you can use the same instance and use the profile to control if Jupyter should run or not.
- In this example the same Dockerfile is used for all python code in order to reuse the same base image. You can of course use separate Dockerfile for each container.
