# ESP32S3-CONSIBIO-SPIRAM-OCTO-LITE-DEBUG

The debug version of `esp32s3-consibio-spiram-octo-lite`: identical, but with ESP-IDF
error messages kept on the serial console, for bench debugging (98,976 bytes bigger base
image, so check that the firmware still fits).

Like `esp32s3-consibio-spiram-octo-lite`, it is `esp32s3-consibio-spiram-octo` (octal flash and
SPIRAM, 32MB flash, Bluetooth off, 0x1d0000 OTA partitions), with the same features
removed as in `esp32-consibio-lite` so the firmware fits the OTA partitions on
devices in the field:

- Ethernet (`CONFIG_TOIT_ENABLE_ETHERNET=n`, `CONFIG_ETH_USE_SPI_ETHERNET=n`). The S3
  has no built-in Ethernet MAC, so only the SPI Ethernet drivers are removed.
- WPA3 (`CONFIG_ESP_WIFI_ENABLE_WPA3_SAE=n`, `CONFIG_ESP_WIFI_ENABLE_WPA3_OWE_STA=n`).
- Unused TLS options: PSK key exchanges, DHE-RSA, static ECDH, AES-CCM suites, and
  the secp192/224, secp*k1 and Brainpool curves.

The network and server requirements are the same as for `esp32-consibio-lite`; see
its README. The partition table is identical to `esp32s3-consibio-spiram-octo`.
