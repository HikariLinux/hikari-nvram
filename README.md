# hikari-nvram

<img src="assets/hikari-linux.svg" alt="Hikari Linux" width="128">

NVRAM and boot-selection utilities for Apple Silicon Macs running Linux.

| Command | Purpose |
| --- | --- |
| `hikari-nvram` | Read and write Apple NVRAM variables |
| `hikari-bless` | Select the active boot partition |
| `hikari-btsync` | Import Bluetooth pairing keys from macOS |
| `hikari-wifisync` | Import Wi-Fi credentials from macOS |

The shared `apple-nvram` library keeps its hardware-oriented name.

## Building

On Linux, install Rust, Cargo, `pkg-config`, and the D-Bus development library, then run:

```sh
cargo build --workspace --release --locked
cargo test --workspace --locked
```

The Bluetooth service and udev rule are under `hikari-btsync/etc/`. They invoke
`hikari-btsync` and `hikari-btsync.service`; packaging must install those names.
Install the unit and rule in the distribution's vendor directories. Packaging
must conflict with the old `asahi-btsync` package: installing both udev rules
would start two services that write the same Bluetooth state.

These tools retain the snapshot's hardware support. Rebranding alone does not
validate NVRAM writes on M6. Incorrect NVRAM writes can require a DFU restore.

## Origin and license

Based on the preserved MIT [snapshot of asahi-nvram](https://github.com/HikariLinux/asahi-nvram/tree/3df52c939fbcedb03344212090d25c98afe4dec1),
commit `3df52c939fbcedb03344212090d25c98afe4dec1`. The original history and
`snapshot-2026-11-08` tag are retained. Hikari Linux maintains this project
independently; it is not an official Asahi Linux release.

Original copyright notices are preserved. Hikari Linux changes and artwork
are also provided under the [MIT license](LICENSE).
