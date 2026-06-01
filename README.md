# makecode-arcade-rpi-kiosk
Building a MakeCode Arcade Kiosk with Raspberry Pi devices.

Reference: <https://github.com/TOLDOTECHNIK/Raspberry-Pi-Kiosk-Display-System>

Simplified version:

# Step One: Create Raspberry Pi Disk

Follow official Raspberry Pi instructions.

-   Use current version of Raspberry OS Lite.
-   Configure Wi-Fi if needed.
-   Enable SSH.

# Step Two: Update OS

```bash
$ sudo apt update
$ sudo apt upgrade
$ sudo apt full-upgrade
$ sudo apt autoremove
$ sudo reboot
```

# Step Three: Install Wayland and Chromium

```bash
$ sudo apt install --no-install-recommends \
  wlr-randr labwc seatd greetd chromium
```

# Step Four: Edit `/etc/greetd/config.toml`

```text
[terminal]
vt = 7

[default_session]
command = "/usr/bin/labwc"
user = "pi"
```

# Step Five: Enable greetd

```bash
$ sudo systemctl enable greetd
$ sudo systemctl set-default graphical.target
```

# Step Six: Create `~/.config/labwc/autostart`

```bash
#!/bin/sh

CHROMIUM="$(command -v chromium)"
URL="https://arcade.makecode.com/--kiosk"

$CHROMIUM_BIN \
  --incognito --autoplay-policy=no-user-gesture-required \
  --kiosk --no-memcheck \
  "URL"
```

```bash
$ chmod +x ~/.config/labwc/autostart
```

# Step Seven: Reboot

```bash
$ sudo reboot
```
