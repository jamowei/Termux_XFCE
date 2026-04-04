# Termux XFCE Desktop Setup

This repository provides a script to set up an XFCE desktop environment and a Debian proot installation within Termux. The setup utilizes the Termux-X11 server, which will be installed during the process. You will be prompted to allow Termux to install the corresponding Android APK.

## Key Features
- **User-Friendly Setup**: Simply choose your username and follow the on-screen prompts.
- **Storage Requirements**: Approximately 4GB of storage space is required. Note that additional applications will consume more space.
- **Detailed Documentation**: Please review the full README for comprehensive information about this setup.

## Installation

To install, execute the following command in Termux:

```bash
curl -sL https://raw.githubusercontent.com/jamowei/Termux_XFCE/main/install.sh -o install.sh && bash install.sh
```

## Support and Community

For questions, assistance, or suggestions, join our Discord community:  
[Discord Invite Link](https://discord.gg/pNMVrZu5dm)

## Screenshots

![Desktop Screenshot](screenshot2.png)

## Starting the Desktop

To start the desktop, use the following command:

```bash
start
```

This command initiates a Termux-X11 session, starts the XFCE4 desktop, and opens the Termux-X11 app directly into the desktop.

To access the Debian proot environment from the terminal, use:

```bash
debian
```

Note: The display is pre-configured in the Debian proot environment, allowing you to launch GUI applications directly from the terminal.

## Hardware Acceleration & Proot

Several aliases are provided to simplify launching applications:

### Termux XFCE:
- `prun`: Execute commands from the Debian proot environment directly in the Termux terminal without entering the proot shell.
- `zrun`: Launch applications in Debian proot with hardware acceleration.
- `zrunhud`: Launch applications with hardware acceleration and FPS HUD.

### Debian Proot:
`debian` To enter the Debian proot environment, from there, you can install additional software using `sudo apt`.

## Additional Utilities

- `cp2menu`: Copy `.desktop` files from Debian proot to the Termux XFCE menu for easy access.
- `app-installer`: Easy to use GUI app to manage installing additional apps not available in Termux or Debian repositories.

## Troubleshooting

### Process Completed (Signal 9) - Press Enter

### 1. Disable via Developer Options (Android 12L+)

- ​On some devices running Android 12L, Android 13, or Android 14 (especially Pixel or "Stock" Android devices), you might find a toggle switch within the Developer Options.
​Steps:
- ​Enable Developer Options:
- ​Go to Settings > About phone.
- ​Tap repeatedly on the Build number (or MIUI version, etc., depending on your manufacturer) until you see a message stating you are now a developer.
- ​Disable the Restriction:
- ​Go back to Settings > System (or Additional Settings) > Developer options.
- ​Look for an option called Disable child processes restrictions (or something similar).
- ​Toggle this switch ON to disable the Phantom Process Killer feature.

### 2. Disable via ADB Commands (For most devices)
- ​If the option above is not available (which is often the case on custom UIs like Samsung One UI, Xiaomi MIUI, etc.), you can use ADB (Android Debug Bridge) commands. This requires a computer and ADB setup.
  ​Prerequisites:
- ​A computer with ADB and Fastboot tools installed.
- ​USB Debugging enabled on your phone (in Developer Options).
- ​A USB cable to connect your phone to the computer.

​Steps:

1. Connect your phone to your computer via USB.
2. Open a Command Prompt (Windows) or Terminal (macOS/Linux) on your computer.
3. Verify the connection by typing:
   `adb devices`
   You should see your device listed. If a pop-up appears on your phone, allow USB debugging.
4. Execute the following commands one by one to disable the Phantom Process Killer:
   `adb shell "settings put global settings_enable_monitor_phantom_procs false"
   adb shell "settings put global settings_phantom_process_kill_timeout 30000"`
   - The first command disables the phantom process monitor.
   - The second command increases the timeout before termination, providing an extra safeguard.
5. Restart your phone to ensure the changes take effect.
   - Note: You can also perform this manipulation directly on your phone using the Termux application with wireless ADB, but the procedure is more complex.


### 3. Per-App Solution (Less Effective)

- For specific applications that are being killed in the background (like Termux, for example), you can sometimes work around the issue by changing the battery management settings for that app:
- Go to Settings > Apps (or Apps & notifications).
- Find the application in question (Termux).
- Go to Battery (or Battery usage).
- Select Unrestricted (or Non restricted) for background usage.\n
- This may prevent the system from killing the app's process due to excessive battery use, but it does not disable the Phantom Process Killer feature system-wide.
#### 🚨 Important Considerations:
- Disabling the Phantom Process Killer may increase battery consumption and affect system performance, as it allows background apps to use more resources.
- The ADB method is the most reliable on non-stock devices but requires basic technical knowledge.
