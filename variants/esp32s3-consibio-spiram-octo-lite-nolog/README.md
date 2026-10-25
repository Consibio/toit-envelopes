# ESP32S3-CONSIBIO-SPIRAM-OCTO-LITE-NOLOG (trial)

Size trial: `esp32s3-consibio-spiram-octo-lite` with ESP-IDF logging off (`CONFIG_LOG_DEFAULT_LEVEL_NONE=y` instead of
`CONFIG_LOG_DEFAULT_LEVEL_ERROR=y`). Removes ESP-IDF error messages from the serial console;
crash dumps and Toit/Artemis logs are unaffected.
