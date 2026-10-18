# esp32-consibio-no-eth-no-wpa3-tls (trial)

Size trial. Same as `esp32-consibio-no-eth-no-wpa3`, plus unused TLS options turned off:

- Key exchanges: all PSK variants, DHE-RSA, and static ECDH (ECDH-ECDSA, ECDH-RSA).
  ECDHE-ECDSA, ECDHE-RSA and plain RSA stay on.
- AES-CCM cipher suites.
- Curves: secp192r1, secp224r1, secp192k1, secp224k1, secp256k1 and the Brainpool curves.
  secp256r1, secp384r1, secp521r1 (the curves Toit's `crypto.ec` supports) and Curve25519 stay on.

The servers the Logger talks to (api.v2.consibio.com, the Supabase Artemis broker,
Azure IoT Hub) all negotiate ECDHE with AES-GCM or ChaCha20-Poly1305.
