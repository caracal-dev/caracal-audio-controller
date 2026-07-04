[![Codacy Badge](https://app.codacy.com/project/badge/Grade/d9a70ae2e26848efa51c316836fecc67)](https://app.codacy.com/gh/caracal-dev/caracal-audio-controller/dashboard?utm_source=gh&utm_medium=referral&utm_content=&utm_campaign=Badge_grade)

# Caracal Audio Controller

`caracal-audio-controller` is a small KDE tray utility for running Caracal OS audio maintenance commands without opening a terminal first.

It is intentionally separate from `caracal-software-installer`: the installer is a foreground catalog app, while this controller is a resident tray app for repeat audio tasks after software has already been installed.

## Tray Actions

- left-click the tray icon to run `ujust update-audio`
- sync Windows VSTs with yabridge
- switch to a notification tray icon when the Wine VST3 folder changes after the last recorded yabridge sync
- notify when a new Caracal OS image is available
- route packaged system plugins into user scan directories
- clear regenerated plugin convolution and cab cache files
- restart PipeWire
- open the Bluetooth headset profile toggle
- enable or remove legacy JACK D-Bus compatibility
- enable or remove legacy MIDI bridge setup
- open Caracal Software Installer

The yabridge reminder watches `~/.wine/drive_c/Program Files/Common Files/VST3` and records the last synced fingerprint in `~/.local/state/caracal-audio-controller/yabridge-vst3.fingerprint`.

The Caracal update reminder checks `bootc upgrade --check` when available, falling back to `rpm-ostree upgrade --check`.

## Development

```bash
python3 -m py_compile src/caracal_audio_controller/app.py
python3 src/caracal_audio_controller/app.py
```

The app uses Qt's native system tray support via PySide6. On Fedora/KDE packaging, install `python3-pyside6`.
