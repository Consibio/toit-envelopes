# esp32-consibio-no-eth-no-wpa3 (trial)

Size trial. Same as `esp32-consibio-no-eth`, plus WPA3 turned off
(`CONFIG_ESP_WIFI_ENABLE_WPA3_SAE=n`, `CONFIG_ESP_WIFI_ENABLE_WPA3_OWE_STA=n`).

Devices still join WPA2 and WPA2/WPA3 mixed-mode networks (as WPA2), but not
WPA3-only networks.
