# WebRTC Browser Compatibility Checker

A developer tool that checks if the current browser supports the WebRTC APIs
needed for peer-to-peer video calls. Useful for debugging before integrating
video SDKs.

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

### Browser Fingerprint Summary
Aggregates the results into a compatibility score:
- Number of audio inputs / outputs / video inputs detected
- Screen resolution and device pixel ratio
- User agent and platform
- Hardware concurrency (CPU cores)
- Sensor API availability

Display everything in a clean dashboard with a dark theme and monospace font.

### Export Report
Add a prominent "Export Report" button at the top of the dashboard. When
clicked, gather the full compatibility results as a JSON string and copy it
to the clipboard with `navigator.clipboard.writeText()`. Show a toast:
"Report copied — paste into your support ticket."

Also add a "Run Full Test" button that re-runs all checks and copies the
updated results to clipboard after the recheck finishes.

Both buttons should be large, clearly visible, and styled as primary call-to-action buttons so users notice them immediately.

## Tech stack
React + TypeScript. No external dependencies needed — all APIs are built into
the browser.
