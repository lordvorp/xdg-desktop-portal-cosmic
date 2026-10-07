# Testing

This document provides a regression testing checklist for the COSMIC XDG desktop portal. The checklist provides a starting point for Quality Assurance reviews.

## Automated

```bash
cargo test input_capture::tests clipboard::tests
```

InputCapture / Clipboard unit coverage lives in `src/input_capture.rs` and
`src/clipboard.rs` (session ownership, Start `clipboard_enabled` gate, mime
sanitization, restore-data shape).

## Checklist

- [ ] Screenshots work
    - [ ] GUI interaction works normally with 100% or non-100% scaling
    - [ ] Rotate a screen; screenshot GUI appears correctly & screenshot of that screen has correct orientation
    - [ ] Screenshot files are saved
    - [ ] Latest screenshot's copied to clipboard
- [ ] PipeWire screen capture from OBS with the portal prompt works
- [ ] Webcam and screen sharing prompted through Firefox works
- [ ] The file chooser works from Firefox
- [ ] The file chooser, webcam, and screen share work from the Slack flatpak
- [ ] InputCapture (Deskflow / Synergy)
    - [ ] Consent prompt appears; persistent grant restores without re-prompt
    - [ ] Pointer barriers activate / deactivate across machines
    - [ ] After `RequestClipboard`, Start reports `clipboard_enabled: true`
    - [ ] Ctrl+C / Ctrl+V text (and image where offered) transfers machine-to-machine
    - [ ] Stopping Deskflow releases the seat so a second client can Start
    - [ ] Middle-click / X11 PRIMARY is still *not* expected end-to-end (CLIPBOARD only)
