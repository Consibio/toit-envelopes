# ESP32S3-CONSIBIO-SPIRAM-OCTO

A variant of the ESP32-S3 envelope for the S3 Logger: octal flash and octal SPIRAM,
Bluetooth disabled.

It sets the size of the OTA partitions to 0x1d0000 and the programs partition to
0x040000 (262144) bytes, matching `esp32-consibio`.

Sets the flash size to 32MB.
