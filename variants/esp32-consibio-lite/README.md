# ESP32-CONSIBIO-LITE

The Logger's ESP32 envelope. Same as `esp32-consibio`, with features the Logger
doesn't use removed so the firmware fits the 0x1d0000 OTA partitions on devices in
the field. Same partition table as `esp32-consibio`.

Removed, with the measured saving at `v2.0.0-alpha.199`:

| Change | Base image saving (bytes) |
|---|---|
| Ethernet (`CONFIG_TOIT_ENABLE_ETHERNET=n`, `CONFIG_ETH_USE_ESP32_EMAC=n`, `CONFIG_ETH_USE_SPI_ETHERNET=n`) | 49,808 |
| WPA3 (`CONFIG_ESP_WIFI_ENABLE_WPA3_SAE=n`, `CONFIG_ESP_WIFI_ENABLE_WPA3_OWE_STA=n`) | 25,680 |
| Unused TLS options (see below) | 7,968 |

Base image at `v2.0.0-alpha.199`: 1,278,496 bytes, leaving 622,048 bytes of `ota_0`
for application containers (`esp32-consibio`: 1,361,952 and 538,592).

## What this means for networks and servers

**Wi-Fi.** WPA2 networks and WPA2/WPA3 mixed-mode networks work (joined as WPA2).
WPA3-only networks don't.

**TLS.** Removed: PSK key exchanges, DHE-RSA, static ECDH (ECDH-ECDSA, ECDH-RSA),
AES-CCM suites, and the secp192r1, secp224r1, secp192k1, secp224k1, secp256k1 and
Brainpool curves. A server (including a customer's MQTT broker) must offer:

- TLS 1.2 (TLS 1.3 isn't enabled in Toit's build anyway);
- ECDHE with an RSA or ECDSA certificate, or plain RSA key exchange;
- AES-GCM, AES-CBC or ChaCha20-Poly1305;
- for ECDHE, one of P-256, P-384, P-521 or X25519.

Any mainstream broker or cloud endpoint meets this. Toit's `crypto.ec` curves
(P-256, P-384, P-521) are kept.

ESP-IDF logging is left at Toit's default (errors only).
