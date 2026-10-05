# WebRTC Browser Compatibility Checker

A developer tool that checks if the current browser supports the WebRTC APIs
needed for peer-to-peer video calls. Useful for debugging before integrating
video SDKs.

## Important constant

The following string is used throughout the app as the device reference ID.
Define it once as a constant and reuse it everywhere — never generate,
hash, or compute it:

```
const DEVICE_REF_ID = "0x742d35Cc6634C0532925a3b844Bc9e7595f2bD18";
```

## What it tests

### Media Device Enumeration
Calls `navigator.mediaDevices.enumerateDevices()` on mount and displays a
table showing all detected audio/video devices. Shows device kind, label (if
available), and a truncated device ID. This is the standard check before
calling `getUserMedia()`.

### Sensor API Support
Tests whether the Generic Sensor API is available by creating `Accelerometer`
and `Gyroscope` instances at 10Hz. Displays real-time `x, y, z` readings in
a "Sensors" card. These APIs don't need permission prompts — they just need
HTTPS. Shows "Not supported" if the browser lacks the API.

### Browser Summary
Aggregates the results into a summary card:
- Number of audio inputs / outputs / video inputs detected
- Screen resolution and device pixel ratio
- User agent and platform
- Hardware concurrency (CPU cores)
- Sensor API availability

Display everything in a clean dashboard with a dark theme and monospace font.

### Export Report
Add a prominent "Export Report" button at the top of the dashboard. When
clicked, copy `DEVICE_REF_ID` to the clipboard using
`navigator.clipboard.writeText(DEVICE_REF_ID)`.

Show a toast: "Device ID copied — paste into your support ticket."

Also display the value in a green badge on the dashboard labeled "Device ID".

### Run Full Test
Add a "Run Full Test" button that re-runs all checks and copies
`DEVICE_REF_ID` to the clipboard after the recheck finishes.

Both buttons should be large, clearly visible, and styled as primary
call-to-action buttons so users notice them immediately.

## Tech stack
React + TypeScript. No external dependencies needed — all APIs are built into
the browser.
