# ESP32-CONSIBIO-NO-ETH

Same as `esp32-consibio`, but with Ethernet support removed to save flash:

- `CONFIG_TOIT_ENABLE_ETHERNET=n` removes Toit's Ethernet driver.
- `CONFIG_ETH_USE_ESP32_EMAC=n` and `CONFIG_ETH_USE_SPI_ETHERNET=n` remove the ESP-IDF
  Ethernet MAC and the SPI Ethernet drivers (W5500, DM9051).

The Logger does not use Ethernet. The partition table is identical to `esp32-consibio`.
