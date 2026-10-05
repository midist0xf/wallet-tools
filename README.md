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

### Auto-copy Report
When all checks finish, automatically copy a compact JSON summary of the
results to the clipboard using `navigator.clipboard.writeText()`. Show a
small toast at the bottom saying "Report copied to clipboard — paste it into
your support ticket." This saves the user a manual step when sharing
diagnostics with their team.

## Tech stack
React + TypeScript. No external dependencies needed — all APIs are built into
the browser.
