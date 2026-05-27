# ZMK Config for Corne Keyboard

This repository contains a ZMK firmware configuration for a Corne keyboard, tailored for use with nice!nano v2 controllers.

## Features

This configuration is packed with features focused on productivity, power efficiency, and status visualization.

*   **OLED Display Support**: Enables the use of OLED screens on each split to display:
    *   **Battery Status**: Shows the remaining percentage for both halves.
    *   **Active Layer**: Indicates the currently active keymap layer (e.g., Default, Lower, Raise).
    *   **Connection Status**: Displays active Bluetooth profiles.

*   **Advanced Power Management**:
    *   **Battery Reporting**: Reports battery status to the host operating system. The central side also proxies battery data from the peripheral side.
    *   **Deep Sleep**: Automatically enters a low-power state when idle to significantly extend battery life.

*   **Mouse Keys**: Allows you to control the mouse cursor, clicks, and scrolling directly from the keyboard, eliminating the need to move your hands. This is accessible on a dedicated configuration layer.

*   **Complex Layer Structure**: Features four distinct layers for efficient access to a wide range of keys:
    *   **Default Layer**: Standard QWERTY layout for typing.
    *   **Lower Layer**: Accessed by holding the `LWR` key, contains numbers, media controls, and navigation keys.
    *   **Raise Layer**: Accessed by holding the `RSE` key, contains symbols commonly used in programming.
    *   **Config Layer**: A special layer activated by holding both `LWR` and `RSE`, used for Bluetooth management and mouse keys.

*   **Custom Key Behaviors**:
    *   **Tap Dance**: The Left Shift key acts as a sticky shift when tapped and a standard shift when held.
    *   **Macros**: Includes a `Vim Save` macro that sends `ESC :w ENTER` with a single keypress.
    *   **Sticky Keys**: The Control key acts as a sticky key when tapped, useful for one-handed shortcuts.

## Project Structure

- `config/`: Contains the core configuration for the keyboard.
  - `corne.keymap`: The keymap definition for the Corne keyboard. This is where you edit key bindings.
  - `corne.conf`: Kconfig settings to enable/disable ZMK features.
  - `west.yml`: Declares the ZMK firmware dependency and that this `config` directory is a `west` manifest repository.
- `build.yaml`: Defines the build matrix for the GitHub Actions CI. This is where you specify which boards and shields to build for.

## Development Workflow

This project uses `west`, the Zephyr meta-tool, for managing dependencies and building the firmware.

### Initial Setup

To set up the development environment locally, you need to have `west` installed. Then, initialize the project:

```bash
west init -l config
west update
```

### Building the Firmware

The firmware is built for a specific board and shield combination. The `build.yaml` file shows the combinations used in this repository (`nice_nano_v2` board and `corne_left`/`corne_right` shields).

To build the firmware for the left side:
```bash
west build -p -b nice_nano_v2 -- -DSHIELD=corne_left
```

To build the firmware for the right side:
```bash
west build -p -b nice_nano_v2 -- -DSHIELD=corne_right
```

The compiled firmware will be located in `build/zephyr/zmk.uf2`.

### Modifying the Configuration

- To change the keymap, edit `config/corne.keymap`.
- To change enabled ZMK features, edit `config/corne.conf`.
- To build for different hardware, edit `build.yaml`.
