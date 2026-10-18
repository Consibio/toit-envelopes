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
| `esp32-consibio` | ESP32 | Bluetooth off, 0x1d0000 OTA partitions. Same as upstream. |
| `esp32-consibio-no-eth` | ESP32 | `esp32-consibio` without Ethernet. |
| `esp32s3-consibio-spiram-octo` | ESP32-S3 | Octal flash/SPIRAM, Bluetooth off, 0x1d0000 OTA partitions. Same as upstream. |
