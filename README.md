# Tempo Flow

Mobile-first cadence-training stopwatch for GitHub Pages and Bluefy on iOS.

## Features
- Stopwatch, manual/automatic laps, adjustable per-lap metronome tempo and duration.
- Editable ascending/descending cadence pyramid and locally saved preset.
- Polar H10 Bluetooth heart-rate measurement via standard GATT Heart Rate Service (0x180D), characteristic 0x2A37.
- Parses 8/16-bit heart rate, energy-expended field when present (skipped), and RR intervals (1/1024-second units).
- Battery level, device information where exposed, lap summaries, local session history and CSV export.
- Wake Lock request and Web Audio scheduled metronome.

## Start
Enable GitHub Pages under **Settings → Pages → Deploy from a branch → main / (root)**. Open `https://obiwandac0-d.github.io/Tempo-Flow/` in **Bluefy** on iPhone. Wear and moisten the Polar H10 strap, open Polar H10 tab and tap **Connect H10**. Grant Bluetooth permission and select the sensor. Return to Workout and tap Start.

## Data capability boundaries
The **Polar H10** supports HR and RR intervals through standard Bluetooth Heart Rate Service, as well as **ECG at 130 Hz**, **three-axis acceleration** at 25/50/100/200 Hz, and internal HR recording through Polar-specific protocols. **This version only implements the standard heart-rate service**, plus battery/device information when exposed. It **does not capture ECG, acceleration or internal recordings**. Those require implementing and validating proprietary PMD/PFTP communication or a native SDK bridge. It also does not capture PPG, gyroscope, GPS, or temperature because these are not H10 sensor outputs.

See official [Polar H10 capabilities](https://github.com/polarofficial/polar-ble-sdk/blob/master/documentation/products/PolarH10.md) and [Polar BLE SDK](https://github.com/polarofficial/polar-ble-sdk).

## Privacy and reliability
Data is stored in the local browser's localStorage. GitHub hosts only the static application source, not your session data. Data is browser-specific and may be lost if browser data is cleared; export regularly. Large raw datasets may exceed storage limits. Do not use this prototype for medical diagnosis. Keep the Bluefy app foregrounded, screen awake, and verify sensor connection before each session.

## Roadmap
1. Validate H10 BLE connection and RR values on actual iPhone/Bluefy hardware.
2. Migrate raw recordings to IndexedDB for high-volume data and streaming exports.
3. Implement validated Polar PMD ECG and accelerometer streaming, with explicit sensor settings and quality checks.
4. Add live HR charts, HRV quality control, reconnect handling and background/interrupt resilience.
