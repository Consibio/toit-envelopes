# Variants

Each directory is one envelope variant. The envelope tool from
[toitlang/envelopes](https://github.com/toitlang/envelopes) turns it into a build:

- `sdkconfig.defaults.patch`: changes to Toit's `toolchains/<chip>/sdkconfig.defaults`.
  Applied with `patch`, so it must match the defaults of the Toit version being built.
- `partitions.csv`: the partition table (optional; Toit's default otherwise).
- `README.md`: what the variant is for.

`sdkconfig.base` records the Toit commit the patches were written against
(currently `v2.0.0-alpha.199`). See the repository README for how to migrate the
patches when moving to a newer SDK.

| Variant | Chip | Notes |
|---|---|---|
| `esp32-consibio` | ESP32 | Bluetooth off, 0x1d0000 OTA partitions. Same as upstream. Kept for reference; too big for the Logger from alpha.195 on. |
| `esp32-consibio-lite` | ESP32 | The Logger's envelope: `esp32-consibio` without Ethernet, WPA3 and unused TLS options, so it fits the OTA partition. See its README. |
| `esp32s3-consibio-spiram-octo` | ESP32-S3 | Octal flash/SPIRAM, Bluetooth off, 0x1d0000 OTA partitions. Same as upstream. Kept for reference. |
| `esp32s3-consibio-spiram-octo-lite` | ESP32-S3 | The S3 Logger's envelope: `esp32s3-consibio-spiram-octo` with the same removals as `esp32-consibio-lite`. |

## This branch: Toit SDK v2.0.0-alpha.195

Artemis publishes its service image only up to SDK alpha.195, so the Logger pods
use alpha.195 until Artemis supports a newer SDK. The patches on this branch are
written against Toit alpha.195 (`esp32-consibio` and `esp32s3-consibio-spiram-octo`
are upstream's alpha.195 patches; `esp32-consibio-lite` applies the same changes as
on `main`). Build with the workflow from this branch and `toit-version: v2.0.0-alpha.195`.
