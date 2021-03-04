# grpc-php-plugin && grpc-python-plugin

At the time of this repo creation [the official way][1] of getting `grpc-php-plugin` artifact was to build it manually:

> It should already been compiled when you run `make` from the root directory of this repo.
> The plugin can be found in the `bins/opt` directory.
> _We are planning to provide a better way to download and install the plugin in the future._

Python gRPC plugin is not provided as standalone `protoc` plugin as well
with the [recommendation to use python module][6]:

> `python -m pip install grpcio-tools`
> `$ python -m grpc_tools.protoc -I../../protos --python_out=. --grpc_python_out=. ../../protos/helloworld.proto`

This repository is a temporary solution for building and storing `grpc-php-plugin` and `grpc-python-plugin` artifacts
to use as `protoc` plugins, until a better way will be found.

## How it works

Repo is not storing any [grpc code][2] but GitHub Actions pipeline and prebuilt artifacts in releases.

The flow is the following:
- as soon as we need the fresh version of the plugins we create a release with the same version
  as [gRPC library release/tag][3] (e.g. `v1.35.0`)
- GitHub Actions pipeline checks out the code of the library with corresponding version, builds artifacts
  (should be two per plugin - for `linux@amd64` and `darwin@amd64`) and attaches them to the release
- projects/tools interested in the prebuilt artifacts can download and use them as they would normally do
  with other plugins (e.g. [grpc-go][4] already provides prebuilt artifacts)

## License

The content of this repository is licensed under [Apache License 2.0][5].
All the derived works are licensed under their own licenses.

[1]: https://grpc.io/docs/languages/php/quickstart/#php-protoc-plugin
[2]: https://github.com/grpc/grpc
[3]: https://github.com/grpc/grpc/releases
[4]: https://github.com/grpc/grpc-go/releases
[5]: https://github.com/hellofresh/grpc-php-plugin/blob/master/LICENSE
[6]: https://grpc.io/docs/languages/python/quickstart/#grpc-tools
