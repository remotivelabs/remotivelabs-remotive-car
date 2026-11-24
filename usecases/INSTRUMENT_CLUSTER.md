---
id: instrument-cluster
title: Instrument cluster
summary: A real Qt instrument cluster as the DIM ECU, reading CAN over SocketCAN
category: visualize
example: .
domains: [driver-information]
protocols: [CAN]
requires: [remotivebus]
key_files:
  - instances/agl_cluster/main.instance.yaml
  - instances/ecus/DIM/agl_cluster.instance.yaml
  - instances/agl_cluster/cluster.dashboard.json
  - models/dim/agl_cluster
related: [3d-visualization, android-cuttlefish]
run:
  build: [instances/agl_cluster/main.instance.yaml]
  profiles: [3dcar]
  after: Open http://localhost:6080 for the cluster, or http://localhost:3000/?clusterIframe=http://localhost:6080 to see it inside the 3D car.
screenshot:
  kind: static
  source: studio
  view: graph
  file: instances/agl_cluster/main.instance.yaml
---

# Instrument cluster

Running real ECU software in the topology lets you see how it behaves on the same signals as the rest of the platform.
Here the Driver Information Module (`DIM`) is a real instrument cluster in a container instead of a plain
RemotiveBroker: a Qt/QML application derived from the
[AGL cluster demo dashboard](https://gerrit.automotivelinux.org/gerrit/admin/repos/apps/agl-cluster-demo-dashboard).

- Part of the [RemotiveCar example](../DOCS.md)
- Instance: [agl_cluster](../instances/agl_cluster/README.md), the same topology as hello world with the cluster as the `DIM`
- Instance file: [DIM/agl_cluster.instance.yaml](../instances/ecus/DIM/agl_cluster.instance.yaml)
- Container image and application: [models/dim/agl_cluster](../models/dim/agl_cluster)
- Dashboard to drive it: [cluster.dashboard.json](../instances/agl_cluster/cluster.dashboard.json)

The container is attached directly to the DIM CAN buses, so the cluster reads the real CAN frames over SocketCAN,
decoded with the same DBC files as every other ECU. Nothing else in the topology knows what runs inside: replace the
container with any other cluster that speaks CAN and the rest of the platform is unchanged.

Build and start it:

```bash
remotive topology build -f instances/agl_cluster/main.instance.yaml build
docker compose -f build/remotive_car_agl_cluster/docker-compose.yml --profile 3dcar up --build
```

The cluster is served as a web page on <http://localhost:6080>. The [3D car](3D.md) can show it as its instrument
cluster: open <http://localhost:3000/?clusterIframe=http://localhost:6080>.

Notice:
- The cluster reads SocketCAN directly, so it needs Linux with [RemotiveBus](https://developer.remotivelabs.com/docs/remotive-bus).
- No display is needed on the host. The cluster is rendered in the container and viewed in a browser.
- See the [instance README](../instances/agl_cluster/README.md) for driving the cluster from the dashboard or the
  command line, running it with Android, and its tests.
