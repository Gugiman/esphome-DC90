# ESPHome DC90 RF Awning Control (Raw Codes)

This repository contains an **ESPHome configuration** for controlling an **awning (markise)** using a **DC90 RF remote control protocol**.

It uses the ESPHome `remote_transmitter` component and sends **raw RF timing codes** for:

- ✅ Open
- ✅ Close
- ✅ Stop

The configuration exposes the awning as a **Home Assistant cover entity** (`device_class: awning`).

---

## Features

- ESPHome compatible (ESP8266 / ESP32)
- Raw RF transmission using `remote_transmitter.transmit_raw`
- Home Assistant `cover` integration
- Works with DC90-style RF remotes
- Includes repeat + wait timing for better reliability

---

## Hardware Requirements

You will need:

- An ESP8266 (e.g. Wemos D1 Mini) or ESP32
- A 433 MHz RF transmitter module (or the correct frequency used by your awning remote)
- Correct wiring between ESP and RF module

---

## Wiring

This config uses:

- **D3** as transmitter output pin

```yaml
remote_transmitter:
  pin: D3
  carrier_duty_percent: 100%
```

Connect your RF transmitter DATA pin to D3.

## Notes About Reliability

Raw RF protocols often require repeated transmissions.
This config uses:

```yaml
repeat:
  times: 6
  wait_time: 15ms
```

If your awning responds unreliably, try:

increasing times (e.g. 8–12)
increasing wait_time (e.g. 20ms)

## Capturing Your Own Remote Codes

If your remote uses different codes, enable the remote_receiver section:
```yaml
remote_receiver:
  pin: D2
  dump: raw
  tolerance: 50%
  filter: 600us
  idle: 4ms
  buffer_size: 2kb
```

---

## Home Assistant Integration

ESPHome will automatically expose a cover entity:
Awning Cover
It will appear in Home Assistant under:
Settings → Devices & Services → ESPHome

---

## Disclaimer

This project sends RF signals and may control physical devices.
Use at your own risk and ensure the awning mechanism is safe to operate.
