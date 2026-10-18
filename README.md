# Consibio Toit envelopes

Firmware envelopes for Consibio devices (Logger on ESP32 and ESP32-S3), built from
the variant definitions in [`variants/`](variants/README.md).

Only the variants live here. The envelope tool, Makefile and build steps come from
[toitlang/envelopes](https://github.com/toitlang/envelopes), checked out at the same
tag as the Toit SDK being built. That keeps this repository small and picks up
upstream build fixes automatically.

## Building

Run the **Build envelopes** workflow (Actions → Build envelopes → Run workflow):

- `toit-version`: the Toit SDK version, e.g. `v2.0.0-alpha.199`.
- `variants`: optional, space-separated. Default: every variant in `variants/`.
- `upload-release`: publish the envelopes as a release named after the SDK version.
- `envelopes-ref`: optional ref of `toitlang/envelopes` for the tool. Default: the
  tag matching `toit-version`, or `main` if there is none.

The run summary lists, per variant, the size of the base image (firmware without
application containers) and how much of the `ota_0` partition is left for containers.

Releases are published as
`https://github.com/Consibio/toit-envelopes/releases/download/<sdk-version>/firmware-<variant>.envelope.gz`,
which is what the Artemis pod specifications reference in `firmware-envelope`.

## Building locally

Requires the ESP-IDF build dependencies (see `toit/actions/setup-build` in the Toit repository).

```sh
git clone --branch v2.0.0-alpha.199 https://github.com/toitlang/envelopes upstream
cd upstream
make TOIT_VERSION=v2.0.0-alpha.199 download-toit
make build-host
build/host/sdk/bin/toit pkg install --project-root=tools
build/host/sdk/bin/toit compile -o build/envelope-tool tools/main.toit
build/envelope-tool synthesize --toit-root=toit --output-root=synthesized \
  --sdk-path=build/host/sdk --variants-root=../variants --build-root=build \
  esp32-consibio
make -C synthesized/esp32-consibio   # -> build/esp32-consibio/firmware.envelope
```

## Moving to a newer Toit SDK

The patches in `variants/*/sdkconfig.defaults.patch` are diffs against Toit's
`sdkconfig.defaults`, which change between SDK versions. To migrate them, check out
the new Toit version in a local build (above) and run upstream's patch updater
against this repository's variants:

```sh
cd upstream
make update-patches VARIANTS_DIRECTORY=../variants
```

It updates the patches and `variants/sdkconfig.base`. Commit both, then run the
workflow for the new version.

## License

The variant files are derived from toitlang/envelopes and are under the BSD0
license (`LICENSE_BSD0`).
