# Li-Fi Data Transmission (Arduino + Processing)

A simple Li‑Fi (Light Fidelity) demo that transmits data using visible light and visualizes ultrasonic ranging on a radar UI. It includes:

- Arduino Uno sketch for sweeping a servo‑mounted ultrasonic sensor and streaming angle/distance over serial
- Processing sketch that renders a real‑time radar visualization from the serial data
- Arduino Nano sketch that demonstrates a basic Li‑Fi receiver using an LDR to decode light pulses

Video reference: https://www.youtube.com/watch?v=IdU6eCJ9Rh0

## Project structure

- `arduino/uno/uno_radar.ino`: Servo + HC‑SR04 radar transmitter (serial output)
- `processing/radar_visualizer.pde`: Processing UI (reads serial `angle,distance.` stream)
- `arduino/nano/nano_receiver.ino`: Li‑Fi receiver (LDR based) sample

## Requirements

- Arduino IDE (or Arduino CLI)
- Processing 3 or later
- Hardware:
  - Arduino Uno + SG90 (or similar) servo + HC‑SR04 ultrasonic sensor
  - Arduino Nano (optional, for Li‑Fi receiver) + LDR + LED

## Wiring (Uno radar)

- Servo signal → pin `12`
- HC‑SR04 `Trig` → pin `10`
- HC‑SR04 `Echo` → pin `11`
- Power and GND as per component specs

## Run: Arduino Uno + Processing

1) Flash `arduino/uno/uno_radar.ino` to the Uno at 9600 baud.
2) Open `processing/radar_visualizer.pde` in Processing and set the serial port to match your system:
   - Windows: `"COMx"`
   - macOS: something like `"/dev/tty.usbmodemXXXX"` or `"/dev/tty.usbserialXXXX"`
3) Run the Processing sketch. You should see the sweeping radar. Objects closer than ~40 cm render in red.

## Run: Arduino Nano Li‑Fi receiver (optional)

- Flash `arduino/nano/nano_receiver.ino` to the Nano
- Connect an LDR to `A2` (voltage divider) and an LED to `D3` if you want to emit test light pulses
- Monitor serial at 9600 baud to view decoded characters

## Create and push a GitHub repository

If you use GitHub CLI and are already authenticated:

```bash
cd /Users/chethanar/Li-Fi-Data-Transmission
git add .
git commit -m "Initialize Li‑Fi project with Arduino & Processing sketches"
# Create a new private repo (change --private to --public if you prefer)
gh repo create Li-Fi-Data-Transmission --source=. --remote=origin --private --push
```

If you are not using GitHub CLI, create an empty repo on GitHub first, then:

```bash
cd /Users/chethanar/Li-Fi-Data-Transmission
git remote add origin https://github.com/<your-username>/Li-Fi-Data-Transmission.git
git branch -M main
git push -u origin main
```

## Notes

- In `processing/radar_visualizer.pde`, update the serial port string to match your system.
- Adjust `THRESHOLD` and `PERIOD` in the Nano sketch for your LDR/LED setup and ambient light conditions.

## Screenshots

Add your images to `assets/` with these names (or update the paths below):

- UI screenshot: `assets/radar_ui.png`
- Wiring diagram: `assets/wiring.png`

![Radar UI](assets/radar_ui.png)

![Wiring Diagram](assets/wiring.png)
