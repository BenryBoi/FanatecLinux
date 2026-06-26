# Fanatec  Linux

A modern, GNOME-aligned GTK4/Libadwaita graphical utility for adjusting Fanatec wheel bases and hardware settings on Linux. This application hooks into the settings exposed by the `hid-fanatecff` kernel driver via `sysfs`.


## Features

- **Wheel & FFB Tuning:** Adjust steering sensitivity (SEN), master force feedback strength (FF), game force effects (FOR), spring/damper constraints, and FFB interpolation filtering.
- **Pedals & Brake Force:** Tune load-cell brake pedal stiffness (brF), brake lock indicator levels (BLI), and manage FullForce metrics.
- **ClubSport Rumble Support:** Fire manual rumble diagnostic signals directly to compatible ClubSport V3 / CSL Elite pedals.
- **Advanced Tuning & Profiles:** Cycle through the 5 independent on-device hardware tuning slots, adjust natural dampening/friction feel, and toggle analogue paddle bite-point modes.
- **Local Presets:** Snapshot your current configuration into custom, named files to easily reload setups for specific sim-racing titles (e.g., *Le Mans Ultimate*, *Assetto Corsa Competizione*, etc.).

## Prerequisites

This application requires the [hid-fanatecff](https://github.com/gotzl/hid-fanatecff) kernel driver to be installed and active on your system. Without it, your system will not expose the hardware tuning paths required by this interface.

## Hardware Permissions (Required)

By default, Linux restricts writing to device configurations in the `/sys` directory to the root user. To allow this application to save settings seamlessly without needing `sudo` or `pkexec` prompts every single time, you must add a local `udev` hardware rule.

Open a terminal and run the following combined command:

```bash
echo 'SUBSYSTEM=="ftec_tuning", ACTION=="add", TAG+="uaccess"
SUBSYSTEM=="hid", DRIVERS=="fanatecff", ACTION=="add", TAG+="uaccess"' | sudo tee /etc/udev/rules.d/99-fanatec-tuner.rules && sudo udevadm control --reload-rules && sudo udevadm trigger
```

*Lots of [Claude](https://claude.ai) and [Gemini](https://gemini.google.com) was used to create this. Please lmk if there are any glaringly obvious problems with this program.
