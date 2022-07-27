# Parca Snap

This repository contains the source of an unofficial snap for [Parca](https://parca.dev), a
continuous profiling tool written in Go.

## Parca App

The snap provides a base `parca` app, which can be executed as per the upstream documentation. The
snap is strictly confined, and thus can only read from certain locations on the filesystem. The
default config file from the upstream is populated in `/var/snap/parca/current/parca.yaml`.

You can start Parca manually like so:

```bash
# Install from the 'edge' channel
$ sudo snap install parca --channel edge
# Start Parca with the config file from the SNAP_DATA directory
$ parca --config-file=/var/snap/parca/current/parca.yaml
```


## Parca Service 

Additionally, the snap provides a service for Parca with a limited set of configuration options.
You can start the service like so:

```bash
$ snap start parca
```

There are a small number of config options:

storage_active_memory="$(snapctl get storage-active-memory)"
log_level="$(snapctl get log-level)"
storage_persist="$(snapctl get storage-persist)"
port="$(snapctl get port)"

| Name | Valid Options | Default | Description |
|:-----|:--------------|:--------|:------------|
|`storage-active-memory` | Any `int` | `536870912` | Total bytes in memory used for active memory storage |
|`storage-persist` | `true`, `false` | `false` | Persist data to disk (experimental). Profiles will be saved in `/var/snap/parca/current/profiles/` |
|`log-level` | `error`, `warn`, `info`, `debug` | `info` | Log level for Parca |
|`port` | 1024 > `int` > 65534 | `7070` | Port for Parca server to listen on |

Config options can be set with `sudo snap set parca <option>=<value>`