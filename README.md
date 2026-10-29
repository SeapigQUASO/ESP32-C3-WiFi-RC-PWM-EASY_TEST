# ESP32-C3-WiFi-RC-PWM-EASY_TEST
Control and test RC ESCs and servos from your phone using an ESP32-C3 Wi-Fi web interface.
# ESP32-C3 WiFi RC Controller

**Control RC ESCs and servos directly from your smartphone — no app, no router, no internet required.**

ESP32-C3 WiFi RC Controller is an open-source web-based controller for RC ESCs (Electronic Speed Controllers) and servos. It creates its own Wi-Fi access point and hosts a responsive control panel that you can access from your smartphone, tablet, or computer browser.

No dedicated mobile application is required. Simply connect to the ESP32's Wi-Fi network and open the control page.

## ✨ Features

- **Standalone Wi-Fi Access Point** — Connect directly to the ESP32-C3 without a router or internet connection.
- **Browser-Based Control Panel** — Control your hardware using Safari, Chrome, or another modern browser.
- **ESC Throttle Control** — Adjustable throttle from 0% to 100%.
- **Servo Position Control** — Adjust servo position from 0° to 180°.
- **Real-Time PWM Information** — View the current control pulse width in microseconds.
- **Quick Controls** — Return to minimum throttle, set 25% throttle, adjust by small increments, or center the servo.
- **Failsafe Timeout** — If control commands stop arriving, the output returns to minimum throttle or servo center.
- **Lightweight and Easy to Customize** — Built with the Arduino framework, ESP32Servo, and the built-in ESP32 WebServer library.

## 🧰 Hardware

Tested target:

- ESP32-C3 Super Mini

Compatible hardware may include other ESP32 boards with suitable GPIO and PWM support.

You will also need:
- An RC ESC and brushless motor, or a compatible servo
- An appropriate external power supply
- USB data cable for initial programming

## 🔌 Wiring

The default signal output is **GPIO4**.

| ESP32-C3 | ESC / Servo |
|---|---|
| GPIO4 | PWM signal |
| GND | Signal ground |
| External power | ESC or servo power, according to device specifications |

**Important:** Connect the ESP32 and ESC signal grounds together. Never connect a motor directly to an ESP32 GPIO pin. Do not connect the ESC battery positive lead to a GPIO pin.

## 🚀 Getting Started

### 1. Install the software

1. Install the Arduino IDE.
2. Install the ESP32 board package.
3. Install the `ESP32Servo` library.
4. Open `ESP32C3_WiFi_RC_Controller.ino`.
5. Select `ESP32C3 Dev Module` or the appropriate board configuration.
6. Compile and upload the firmware.

### 2. Connect to the controller

After the ESP32 starts, connect your phone or computer to the following Wi-Fi network:

| Setting | Default |
|---|---|
| SSID | `ESP32-RC-Control` |
| Password | `rccontrol` |
| Control panel | `http://192.168.4.1` |

If your phone reports that the network has no internet access, choose to remain connected.

### 3. Select a control mode

**ESC Mode**
- Throttle range: 0–100%
- Default pulse range: 1000–2000 µs
- Quick access to minimum throttle and 25% throttle

**Servo Mode**
- Position range: 0–180°
- Default pulse range: 500–2500 µs
- Center position: 90°

Pulse ranges may need to be adjusted for your specific ESC or servo.

## ⚙️ PWM Configuration

The controller uses a nominal 50 Hz RC-style control signal.

| ESC throttle | Pulse width |
|---:|---:|
| 0% | 1000 µs |
| 25% | 1250 µs |
| 50% | 1500 µs |
| 75% | 1750 µs |
| 100% | 2000 µs |

These percentages describe the configured control pulse range, not actual motor RPM, torque, or thrust. Motor response is not necessarily linear.

## 🛡️ Safety

**Remove all propellers before testing.**

- Secure the motor and ESC before applying power.
- Verify your ESC's supported input signal and arming procedure.
- Some ESCs require throttle calibration before use.
- Servo pulse limits vary. Reduce the configured range if the servo buzzes, overheats, or reaches its mechanical stops.
- The failsafe is a basic software timeout, not a certified flight-control safety system.
- Do not use this project as the sole control or failsafe system for an aircraft.

Use at your own risk.

## 🔧 Customization

You can modify the following settings in the source code:

- `SIGNAL_PIN` — PWM output GPIO
- `ESC_MIN_US` / `ESC_MAX_US` — ESC pulse limits
- `SERVO_MIN_US` / `SERVO_MAX_US` — Servo pulse limits
- `FAILSAFE_MS` — Command timeout
- `AP_SSID` / `AP_PASSWORD` — Wi-Fi credentials

## 📋 Dependencies

- Arduino ESP32 core
- ESP32Servo library

The web interface is embedded in the firmware, so no external web server or frontend build system is required.

## 🤝 Contributing

Contributions, bug reports, hardware compatibility notes, and improvements are welcome.

If you test this project with a different ESP32 board, ESC, or servo, feel free to share your configuration and results.

## 📄 License

This project is intended for open-source distribution. Add a `LICENSE` file to specify the terms under which others may use, modify, and redistribute the code.

---

**Built for hobbyists, makers, and RC experimenters.**

If you find this project useful, consider giving the repository a ⭐ on GitHub.
