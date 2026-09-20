# AirKeys 🪄📱

<p align="center">
  <img src="https://raw.githubusercontent.com/airkeys/art/main/banner.png" alt="AirKeys Banner" width="100%" onerror="this.style.display='none'"/>
</p>

<p align="center">
  <strong>Turn your Android smartphone into an authentic LG Magic Remote & Air Mouse for webOS Smart TVs.</strong>
</p>

<p align="center">
  <a href="https://github.com/releases"><img src="https://img.shields.io/badge/Release-v1.0.0-blue.svg?style=for-the-badge&logo=github" alt="Release v1.0.0"></a>
  <a href="https://android.com"><img src="https://img.shields.io/badge/Platform-Android_8.0+-3DDC84.svg?style=for-the-badge&logo=android&logoColor=white" alt="Platform: Android 8.0+"></a>
  <a href="https://kotlinlang.org"><img src="https://img.shields.io/badge/Kotlin-2.0+-7F52FF.svg?style=for-the-badge&logo=kotlin&logoColor=white" alt="Kotlin"></a>
  <a href="https://developer.android.com/jetpack/compose"><img src="https://img.shields.io/badge/UI-Jetpack_Compose_M3-4285F4.svg?style=for-the-badge&logo=jetpackcompose&logoColor=white" alt="Jetpack Compose M3"></a>
  <a href="#license"><img src="https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge" alt="License: MIT"></a>
</p>

---

## 🌟 Overview

**AirKeys** is a native, high-performance Android remote control tailored specifically for **LG webOS Smart TVs** (webOS 4.0 through webOS 24+). Built entirely with modern **Kotlin**, **Jetpack Compose (Material 3)**, and **Coroutines / StateFlow**, AirKeys bridges the physical gap of missing or broken LG Magic Remotes by streaming real-time hardware gyroscope motion directly to the webOS pointer input socket.

Whether pointing your phone in the air to direct the on-screen cursor, gliding across the multi-mode trackpad, launching streaming apps with one tap, or inputting text directly via native webOS IME, AirKeys delivers a zero-latency, tactile experience.

---

## ✨ Key Features

### 🪄 1. Floating Gyro Cursor (Air Mouse)
* **Real-time 3D-to-2D Projection**: Uses your smartphone's internal gyroscope sensor (`Sensor.TYPE_GYROSCOPE`) to translate physical wrist rotation (Yaw & Pitch) into fluid on-screen pointer movement.
* **Deadband Jitter Filtering**: Custom deadband thresholding eliminates hand tremor jitter and stops annoying mouse-cursor auto-scroll drift when pointing at webOS menus.
* **Exponential Moving Average (EMA)**: 60 FPS tick interpolation delivers silky-smooth cursor gliding across large 4K and 8K displays.
* **Dual Control Modes**:
  * **Hold-to-Move Trigger**: Hold down the haptic center dial to move the cursor; release to rest your hand.
  * **Continuous Mode**: Toggle for always-on pointer tracking.
* **Custom Speed Slider**: Adjust cursor sensitivity dynamically from 1.0x to 6.0x.

### 🖲️ 2. Precision Dual-Mode Trackpad
* **Large Touch Surface**: Tap to click, double tap to open, and drag to guide the cursor with pixel precision.
* **Dual Scroll Strip**:
  * **App Shelves Mode (YouTube / Netflix / Prime)**: Sends clean directional navigational steps through horizontal and vertical carousels.
  * **Web Wheel Mode**: Dispatches discrete pointer wheel ticks for smooth web browsing without runaway scrolling speeds.
* **Hardware-Style Action Buttons**: Dedicated Left Click and Right Click (Back) bottom pads.

### 📺 3. Full Smart TV Remote
* **Omnidirectional D-Pad**: Up, Down, Left, Right navigation with a prominent Center OK / Select button.
* **Volume & Channel Rockers**: Tactile twin rockers with haptic feedback and dedicated Mute toggle.
* **Media Deck**: Instant Rewind, Play, Pause, and Fast-Forward controls.
* **webOS Color Keys**: Full support for Red, Green, Yellow, and Blue shortcut keys.
* **Numeric Keypad**: Dedicated 0–9 dialog for quick channel dialing and PIN entry.
* **System Shortcuts**: Instant access to TV Home, Back, Settings Menu, Info, and Power Off.

### 🚀 4. Live TV App Launcher
* Automatically queries the TV's application manager (`ssap://com.webos.applicationManager/listLaunchPoints`) upon connection.
* Displays all installed streaming apps (YouTube, Netflix, Prime Video, Disney+, Apple TV, Spotify, Web Browser, HDMI inputs) in a clean grid.
* Launch any TV app or switch video inputs with a single tap.

### 🔍 5. Direct Keyboard Input & Search
* Injects text directly into focused TV text boxes via standard webOS IME protocol (`replace: false`), completely eliminating the chore of pecking letter-by-letter on the TV screen.
* Dedicated **YouTube Search** launcher that fires queries directly into the YouTube app without opening virtual keyboards.

### 📡 6. Zero-Config SSDP Auto-Discovery
* Instant UDP multicast discovery (`239.255.255.250:1900`) searches and lists active LG TVs on your Wi-Fi network.
* Manual IP & Port entry fallback for complex subnets, VLANs, or hidden SSIDs.
* Persistent device memory with cached client pairing keys.
* One-tap **"Re-Pair"** button to cleanly renegotiate permissions if keys ever expire.

---

## 📱 Screenshots

| Remote View | Precision Trackpad | Floating Air Mouse | TV App Launcher |
|:---:|:---:|:---:|:---:|
| <img src="docs/screenshots/remote.png" width="220" alt="Remote Tab"/> | <img src="docs/screenshots/trackpad.png" width="220" alt="Trackpad Tab"/> | <img src="docs/screenshots/airmouse.png" width="220" alt="Air Mouse Tab"/> | <img src="docs/screenshots/apps.png" width="220" alt="Apps Tab"/> |

*(Screenshots can be added to `docs/screenshots/`)*

---

## 📺 How to Setup Your LG TV

Before connecting AirKeys, ensure your TV is configured to accept network connections:

1. Turn on your **LG webOS TV**.
2. Press the **Settings (Gear)** button on your physical remote.
3. Depending on your webOS version:
   * **webOS 22 / 23 / 24+**:
     * Navigate to **All Settings** → **Connection** → **Mobile Connection Management**.
     * Turn ON **Mobile TV On** and enable **"Turn on via Wi-Fi"**.
   * **webOS 4.0 - 6.0**:
     * Navigate to **All Settings** → **General** → **Network** → **LG Connect Apps**.
     * Switch **LG Connect Apps** to **ON**.
4. **Connect Wi-Fi**: Make sure your phone and LG TV are connected to the **same Wi-Fi network** (and the same subnet/frequency band if your router uses AP Isolation).
5. **Authorize Connection**: Launch AirKeys, tap your TV in the discovery list, and select **"Accept"** on the prompt that appears on your TV screen.

---

## 🛠️ Tech Stack & Architecture

AirKeys is engineered following clean MVVM architecture and Android modern development best practices:

* **Language**: Kotlin 2.0+
* **UI Toolkit**: Jetpack Compose with Material Design 3
* **Asynchronous Programming**: Kotlin Coroutines & StateFlow / SharedFlow
* **Networking**:
  * [OkHttp 4.12](https://square.github.io/okhttp/): WebSocket communication with custom SSL bypass for local webOS self-signed certificates.
  * UDP Datagram Sockets: SSDP discovery protocol.
* **Protocols**:
  * **LG SSAP (Smart TV Socket Application Protocol)** over WebSocket (`ws://` on port 3000 or `wss://` on port 3001).
  * Dedicated **Pointer Input Socket** (`ssap://com.webos.service.networkinput/getPointerInputSocket`) streaming binary micro-packets for cursor motion.
* **Sensors**: Android `SensorManager` (`Sensor.TYPE_GYROSCOPE`) running at game refresh rate (`SENSOR_DELAY_GAME`).

---

## 📥 Installation

### Download Pre-built APK
Get the latest stable release from the [GitHub Releases](https://github.com/releases) page:
1. Download `app-release.apk` (or `app-debug.apk`).
2. Open the APK on your Android device (ensure *Install from Unknown Sources* is enabled in system settings).
3. Follow the prompt to install and launch AirKeys.

---

## 🏗️ Building from Source

### Prerequisites
* **Android Studio**: Ladybug (2024.2.1) or newer
* **JDK**: Version 21
* **Android SDK**: API level 35 (Compile) / API level 26+ (Minimum)

### Build Steps

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/your-username/airkeys.git
   cd airkeys
   ```

2. **Open in Android Studio**:
   * Open Android Studio.
   * Select **Open an Existing Project** and browse to the cloned `airkeys` folder.
   * Allow Gradle to sync dependencies.

3. **Build via Command Line**:
   * **Debug Build**:
     ```powershell
     # Windows
     .\gradlew.bat assembleDebug

     # Linux / macOS
     ./gradlew assembleDebug
     ```
   * The generated APK will be located at:
     ```
     app/build/outputs/apk/debug/app-debug.apk
     ```

4. **Install onto Device via ADB**:
   ```bash
   adb install -r app/build/outputs/apk/debug/app-debug.apk
   ```

---

## 🔧 Troubleshooting

<details>
<summary><strong>1. TV is not discovered automatically</strong></summary>

* Check that both your phone and LG TV are connected to the exact same Wi-Fi SSID.
* If your router separates **2.4 GHz** and **5 GHz** bands with **AP Isolation** or "Guest Mode", disable AP Isolation so devices can communicate over UDP broadcast.
* Use the **"Manual IP"** option in the AirKeys discovery dialog to enter your TV's IP address directly (found on your TV under *Settings → Network → Wi-Fi Connection → Advanced Settings*).
</details>

<details>
<summary><strong>2. "Pairing Prompt" does not show on the TV</strong></summary>

* Go to TV *Settings → General → Connection → Mobile Connection Management* (or *LG Connect Apps* on older models) and verify it is turned ON.
* In AirKeys, open the TV list and tap the **Sync / Re-Pair** icon next to your TV to clear cached credentials and force a fresh pairing prompt.
</details>

<details>
<summary><strong>3. Mouse pointer doesn't show or move on TV</strong></summary>

* Some TV screens (like native system settings submenus or certain third-party HDMI screens) disable cursor pointer input by default. Launch the Web Browser or Home Screen to test pointer movement.
* In AirKeys, check the top pointer indicator. If it displays `TV Pointer: Connecting...`, tap the refresh button to renegotiate the pointer socket.
* If your phone lacks a hardware gyroscope, AirKeys displays an alert banner—simply switch to the **Trackpad** tab for full touch-based cursor navigation.
</details>

---

## 🤝 Contributing

Contributions, feature requests, and bug reports are welcome!
1. Fork the Project.
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`).
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`).
4. Push to the Branch (`git push origin feature/AmazingFeature`).
5. Open a Pull Request.

---

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

---

<p align="center">
  Built with ❤️ for webOS TV owners.
</p>
