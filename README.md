# sys-controller

A collection of small QoL scripts I made for myself — they live in `~/.local/bin/` and are on `$PATH`. All are written for my own machines (Arch-based, Hyprland), so take them as-is or adapt.

## Scripts

- **sysclean** — periodic disk cleanup. Reclaims the pacman package cache, systemd journal, unused flatpak runtimes/caches, language/tool package caches, the XDG cache dir and trash. Never touches documents, browser profiles, game saves, app settings, `~/.hermes`, Steam, or `node_modules` (unless `--deep`). Supports `--dry-run`, `--no-privileged`, `--deep`, `--all`, `--no-trash`.
- **sysupdate** — updates the whole system in one command: pacman, then yay (AUR), then flatpak (user + system). Reports orphaned packages and `.pacnew` files afterwards. Supports `--dry-run`, `--noconfirm`, `--no-privileged`, `--skip-pacman` / `--skip-yay` / `--skip-flatpak`.
- **server-mode** — puts a machine into a server-like state so it stays reachable (e.g. over Tailscale/SSH) when left unattended: no suspend/hibernate, no lid-switch suspend, no screen lock. `server-mode on` masks the sleep targets, holds systemd inhibitors, and writes a logind override (applies at next reboot); `server-mode off` undoes it; bare `server-mode` prints the status.
- **restore-usb-mic-gain** — raises the hardware capture gain on USB headsets (currently the Logitech G733 dongle, ALSA card id `Headset`). USB audio devices reset their own mixer when they re-enumerate, and `alsa-restore.service` replays `/var/lib/alsa/asound.state` at every boot, so a stale low gain leaves the mic at -74 dB while PipeWire shows 100% and unmuted. Runs from `usb-mic-gain.service` at login and from `usb-mic-gain.timer` every 60 s, so hot-plugging the dongle is covered too.

## Notes

- Run everything as your normal user; the scripts ask for sudo themselves when they need root.
- No test suite for this repo.
