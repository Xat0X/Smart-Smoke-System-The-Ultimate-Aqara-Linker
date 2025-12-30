# 🚨 Xat0X Smart Smoke System (Ultimate Edition)

> **The ultimate safety suite for Aqara (JY-GZ-01AQ) smoke detectors in Home Assistant.**

Turn your individual Zigbee smoke detectors into a professional, interconnected fire alarm system without buying an expensive hub.

![Home Assistant](https://img.shields.io/badge/Home%20Assistant-Blueprint-blue)
![Devices](https://img.shields.io/badge/Devices-Aqara%20JY--GZ--01AQ-green)
![Author](https://img.shields.io/badge/Author-Xat0X-orange)

## 🌟 Why this blueprint?

Most Zigbee smoke detectors are "dumb" isolated devices. If a fire starts in the attic, you won't hear it in the bedroom. **This blueprint fixes that.**

### Key Features (Ultimate Edition)
*   🔗 **Interconnected Alarms**: If one detector triggers, **ALL** detectors in your home will sound their sirens.
*   ⚠️ **Pre-Alarm Verification**: Prevents panic from burnt toast. You get a phone notification first ("Is this real?"). If you don't answer, the main alarm triggers.
*   ✅ **Guided Self-Test Wizard**: A specialized interactive mode. You trigger the test in HA, and your phone guides you room-by-room to physically press the buttons.
*   🌫️ **Smoke Spray Mode**: Optional post-test phase to safely use canned smoke spray without triggering the full evacuation plan.
*   🐕 **Watchdog Protection**: If a **REAL** fire is detected during a self-test, the test is immediately aborted, and the full alarm sounds.
*   ⚡ **Custom Actions**: Fully customizable main alarm actions (turn on lights, unlock doors, open blinds, etc.).

---

## 📋 Requirements

1.  **Home Assistant** (2024.10 or newer).
2.  **Aqara Smoke Detectors** (Model `JY-GZ-01AQ`) connected via Zigbee (ZHA or Zigbee2MQTT).
3.  **Home Assistant Mobile App** installed on your phone.
4.  **Mobile Settings (CRITICAL):**
    *   **iOS:** Enable 'Critical Alerts' in iOS Settings -> Home Assistant -> Notifications.
    *   **Android:** Notifications are sent to channel `alarm_stream`. Configure this channel in Android Settings to "Override Do Not Disturb".

---

## 🚀 Installation

### Option 1: Direct Import (Recommended)
1.  Click the badge below to import the blueprint directly into your Home Assistant instance.
    [![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint URL.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2FXat0X%2FSmart-Smoke-System-The-Ultimate-Aqara-Linker%2Fblob%2Fmain%2Fxat0x-aqara-smoke-linker-ultimate.yaml)
2.  Click **"Preview Blueprint"** and then **"Import Blueprint"**.

### Option 2: Manual Installation
1.  Copy the code from the `.yaml` file.
2.  Go to your Home Assistant config folder: `/config/blueprints/automation/xat0x/`.
3.  Create a file named `xat0x-aqara-smoke-linker-ultimate.yaml` and paste the code.
4.  Go to **Developer Tools** -> **YAML** -> **Reload Automations**.

---

## ⚙️ Configuration Guide

Create a new automation using this blueprint. The settings are organized into collapsible sections:

### 1. 📟 Devices & Triggers
*   **Smoke Detectors**: Select ALL your Aqara smoke entities here.
*   **Test Start Trigger**: Create a Helper (Button or Toggle) in Home Assistant. Select it here. **Pressing this button starts the Self-Test Wizard.**
*   **Alarm Notification Devices**: Phones for the whole family (Critical Alerts).
*   **Maintenance Device**: The specific phone that will receive the interactive test instructions.

### 2. 🛡️ Pre-Alarm
*   **Enable Pre-Alarm**: Recommended **ON**.
*   **Timeout**: Time (default 15s) to confirm "False Alarm" on your phone before the loud sirens and main actions trigger.

### 3. 🔥 Main Alarm
*   **Main Alarm Actions**: This is where you define your evacuation plan.
    *   *Example:* Add actions to Turn on all lights 100%, Unlock Nuki/Yale locks, Turn off HVAC/Gas.
*   **Mute Duration**: How long sirens stay silent when you press "Mute".

### 4. ✅ Self-Test & Spray
*   **Enable Self-Test**: Required for the wizard.
*   **Enable Smoke Spray Test**: If enabled, the wizard asks after the physical check if you want to perform a real smoke test.

---

## 🛡️ How it works

### Scenario 1: Burnt Toast (Pre-Alarm)
1.  Smoke is detected in the Kitchen.
2.  **NO sirens** go off yet (if Pre-Alarm is enabled).
3.  Your phone gets a **Critical Notification**: *"Smoke detected in Kitchen. Confirm Fire?"*
4.  You press **"False Alarm"**.
5.  The system resets. The house stays quiet.

### Scenario 2: Real Fire (Main Alarm)
1.  Smoke is detected in the Garage.
2.  You don't answer the notification within 15 seconds.
3.  **FULL ALARM** triggers.
4.  **ALL** Aqara detectors start sirens.
5.  **Main Alarm Actions** run (Lights turn on, doors unlock).
6.  Phones receive: **"FIRE - EVACUATE!"**.

### Scenario 3: Monthly Maintenance
1.  **You press the "Test Start Trigger"** (Helper button) in your Dashboard.
2.  Your phone receives: *"Smoke Detector Self-Test (1/6)"*.
3.  You walk to the indicated room (e.g., Living Room) and press the physical button on the detector.
4.  The system detects the beep, logs it, and notifies you to move to the next room.
5.  (Optional) At the end, you can choose to run a "Smoke Spray Test".

---

## ❓ FAQ

**Q: How do I start the Self-Test?**
A: Unlike older versions, you do not start by pressing a smoke detector button. You must create an `input_button` helper in Home Assistant, assign it in the Blueprint settings ("Test Start Trigger"), and press that helper in your dashboard to begin the wizard.

**Q: I pressed "Mute" on my phone, but the sirens are still going?**
A: Zigbee traffic allows limited bandwidth. The blueprint uses an aggressive loop to send the mute command repeatedly. Please wait 5-10 seconds for the network to catch up.

**Q: What happens if I am testing and a real fire starts?**
A: The "Watchdog" feature is always active. If a detector *other than the one you are currently testing* reports smoke, the test aborts immediately, and the full alarm triggers.

---

## ⚠️ Disclaimer

**Use at your own risk.**

This blueprint is provided "as is", without warranty of any kind. The author (**Xat0X**) cannot be held responsible for any failure of the system to operate as expected.

*   This system is **NOT** a certified fire alarm system.
*   Always ensure you have working, standalone smoke detectors as a primary safety measure.
*   Home Assistant, Zigbee networks, and WiFi can experience downtime; do not rely solely on this software for life-safety.

**Created with ❤️ by Xat0X**
