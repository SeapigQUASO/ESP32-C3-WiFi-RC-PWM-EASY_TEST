<div align="center">

# ESP32-C3 WiFi RC Controller

**Control RC ESCs and servos from your smartphone — no app, no router, no internet required.**

[English](README.md) · [繁體中文](README.zh-TW.md)

</div>

ESP32-C3 WiFi RC Controller is an open-source web-based controller for RC ESCs (Electronic Speed Controllers) and servos. It creates its own Wi-Fi access point and hosts a responsive control panel that you can open from a phone, tablet, or computer browser.

No dedicated mobile application is required. Connect to the ESP32's Wi-Fi network and open the control page.

## Features

- **Standalone Wi-Fi access point** — connect directly without a router or internet connection.
- **Browser-based control panel** — use Safari, Chrome, or another modern browser.
- **ESC throttle control** — adjustable from 0% to 100%.
- **Servo position control** — adjustable from 0° to 180°.
- **PWM information** — display the current pulse width in microseconds.
- **Quick controls** — minimum throttle, 25% preset, incremental adjustments, and servo centering.
- **Failsafe timeout** — if control requests stop arriving, output returns to minimum throttle or servo center.
- **Easy to customize** — built with the Arduino framework, ESP32Servo, and ESP32 WebServer.

## Hardware

Primary target: **ESP32-C3 Super Mini**.

You will also need an RC ESC and brushless motor, or a compatible servo, plus an appropriate power supply and a USB data cable for programming.

## Wiring

Default signal output: **GPIO4**.

| ESP32-C3 | ESC / Servo |
|---|---|
| GPIO4 | PWM signal |
| GND | Signal ground |
| External power | ESC or servo power, according to device specifications |

Connect the ESP32 and ESC signal grounds together. Never connect a motor directly to an ESP32 GPIO. Do not connect the ESC battery-positive lead to a GPIO pin.

## Getting Started

1. Install the Arduino IDE and the ESP32 board package.
2. Install the `ESP32Servo` library.
3. Open `ESP32C3_WiFi_RC_Controller.ino`.
4. Select `ESP32C3 Dev Module` or the correct board configuration.
5. Compile and upload the firmware.

### Connect your phone

Join the Wi-Fi network created by the ESP32:

| Setting | Default |
|---|---|
| SSID | `ESP32-RC-Control` |
| Password | `rccontrol` |
| Control panel | `http://192.168.4.1` |

If your phone says the network has no internet access, choose to remain connected.

## Control Modes

### ESC mode

- Throttle: 0–100%
- Default pulse range: 1000–2000 µs
- Quick access to minimum throttle and 25% throttle

| ESC throttle | Pulse width |
|---:|---:|
| 0% | 1000 µs |
| 25% | 1250 µs |
| 50% | 1500 µs |
| 75% | 1750 µs |
| 100% | 2000 µs |

These percentages describe the configured control-pulse range, not actual motor RPM, torque, or thrust. Motor response is not necessarily linear. Confirm the pulse range and arming procedure supported by your ESC.

### Servo mode

- Position: 0–180°
- Default pulse range: 500–2500 µs
- Center: 90°

Servo pulse limits vary by model. Reduce the range if the servo buzzes, overheats, or reaches its mechanical stops.

## Customization

You can change these settings in the source code:

- `SIGNAL_PIN` — PWM output GPIO
- `ESC_MIN_US` / `ESC_MAX_US` — ESC pulse limits
- `SERVO_MIN_US` / `SERVO_MAX_US` — servo pulse limits
- `FAILSAFE_MS` — command timeout
- `AP_SSID` / `AP_PASSWORD` — Wi-Fi credentials

## Safety

**Remove all propellers before testing.**

- Secure the motor and ESC before applying power.
- Verify your ESC's supported input signal and arming procedure.
- Some ESCs require throttle calibration before use.
- Never power a motor directly from an ESP32 GPIO.
- The failsafe is a basic software timeout, not a certified flight-control safety system.
- Do not use this project as the sole control or failsafe system for an aircraft.

Use at your own risk.

## Dependencies

- Arduino ESP32 core
- ESP32Servo library

The web interface is embedded in the firmware; no external web server or frontend build system is required.

## Contributing

Bug reports, hardware compatibility notes, and improvements are welcome. If you test this project with another ESP32 board, ESC, or servo, please share your configuration and results.

## License

This project is licensed under the [MIT License](LICENSE).

---

Made for hobbyists, makers, and RC experimenters. If you find it useful, consider giving the repository a ⭐ on GitHub.
