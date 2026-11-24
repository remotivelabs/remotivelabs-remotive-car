---
id: signal-playback
title: Signal playback
summary: Recorded VSS signals, converted by models into platform signals
category: replay
example: .
domains: [chassis, telematics]
protocols: [CAN, SOME/IP]
key_files:
  - instances/android/local_playback.instance.yaml
  - recordings/platform/topology.platform.yaml
  - instances/android/playback/local/__main__.py
  - instances/android/playback/local/sccm.py
related: [android-emulator, android-cuttlefish, 3d-visualization, replay-can]
run:
  build: [instances/android/main.instance.yaml, instances/android/android_emulator_in_docker.instance.yaml, settings/can_over_udp.settings.instance.yaml, settings/vlan_using_bridge.settings.instance.yaml]
  profiles: [playback, 3dcar]
  after: Open http://localhost:3000 to watch the car follow the recorded drive.
screenshot:
  kind: static
  source: studio
  view: graph
  file: instances/android/main.instance.yaml
---

# Playback signals

Using playback of recorded data can be useful to test longer scenarios. This example show how recorded [VSS](https://covesa.github.io/vehicle_signal_specification/) signals can be fed into behavioral models that convert them into platform specific signals. In this case the signals include location, steering wheel angle, and pedal positions among others.

- Part of the [RemotiveCar example](../DOCS.md)
- Instance file: [local_playback.instance.yaml](../instances/android/local_playback.instance.yaml)
- Platform adding VSS channel: [topology.platform.yaml](../recordings/platform/topology.platform.yaml)
- Starting playback: [playback.local](../instances/android/playback/local/__main__.py)
- Behavioral models converting VSS to RemotiveCar platform: [abs](../instances/android/playback/local/abs.py), [sccm](../instances/android/playback/local/sccm.py), [tcu](../instances/android/playback/local/tcu.py)

Notice:
- In this example playback happens to be part of the Android instance, but playback is not limited to Android use cases.
- Playback is not limited to VSS. You can also add custom signals or even raw data.
- This example use CSV, but playback also support other formats, for example candump for raw CAN data.

To run playback with signals, see [Cuttlefish](./ANDROID_CUTTLEFISH.md) or [Android Emulator](./ANDROID_EMULATOR.md).
