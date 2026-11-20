# RemotiveCar example
By following the steps below, you will generate and run an instance of a topology containing multiple communication protocols and multiple ECUs.

RemotiveCar is the larger example of [RemotiveTopology](https://developer.remotivelabs.com/docs/remotive-topology). For smaller examples, start with
[remotivelabs-topology-examples](https://github.com/remotivelabs/remotivelabs-topology-examples).

## Prerequisites

To run this example, you'll need:
- A valid RemotiveTopology subscription (free trial available)
- RemotiveCLI and RemotiveTopology installed, see <https://developer.remotivelabs.com/docs/remotive-topology/install>

Run all commands below from the root of this repository.

## Getting started
Generate the instance
```bash
remotive topology build -f instances/hello_world/main.instance.yaml -f settings/can_over_udp.settings.instance.yaml build
```

Start it
```bash
docker compose -f build/remotive_car_hello_world/docker-compose.yml --profile jupyter up --build
```

Use [RemotiveStudio](https://developer.remotivelabs.com/docs/remotive-studio) to view signals.

Browse to [http://localhost:8888/lab?token=remotivelabs](http://localhost:8888/lab?token=remotivelabs) to interact with the instance through a Jupyter notebook.

The `BCM` of this example is also available as an FMU, see the [FMU instance](./instances/fmu/README.md).

## Documentation
Detailed documentation is available here:

- [Overview](./DOCS.md) - Platform and file structure
- [Example usecases](https://github.com/remotivelabs/remotivelabs-topology-examples/blob/main/USECASES.md) - The usecases this example is showing

## License

The example code in this repository is licensed under the [MIT License](./LICENSE), so you are free to copy, modify and reuse it in your own projects.

Running the example, however, requires a RemotiveLabs account. The RemotiveLabs software the example depends on (such as RemotiveBroker, RemotiveTopology and RemotiveCLI) is not covered by the MIT License; it is provided under the RemotiveLabs Terms of Use at https://www.remotivelabs.com/license.

Some parts include third-party files that keep their original licenses, as noted in those files.

## Support

Contact support@remotivelabs.com if you have any problems or questions!
