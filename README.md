# 🔥 Xat0X Smart Smoke System (Aqara Linker)

> **The ultimate safety suite for Aqara (JY-GZ-01AQ) smoke detectors in Home Assistant.**

Turn your individual Zigbee smoke detectors into a professional, interconnected fire alarm system without buying an expensive hub.

![Home Assistant](https://img.shields.io/badge/Home%20Assistant-Blueprint-blue)
![Devices](https://img.shields.io/badge/Devices-Aqara%20JY--GZ--01AQ-green)
![Author](https://img.shields.io/badge/Author-Xat0X-orange)

## 🌟 Why this blueprint?

Most Zigbee smoke detectors are "dumb" isolated devices. If a fire starts in the attic, you won't hear it in the bedroom. **This blueprint fixes that.**

### Key Features
*   🔗 **Interconnected Alarms**: If one detector triggers, **ALL** detectors in your home will sound their sirens.
*   ⚠️ **Pre-Alarm Verification**: Prevents panic from burnt toast. You get a phone notification first ("Is this real?"). If you don't answer, the main alarm triggers.
*   🔦 **Emergency Mode**: Automatically turns on all lights at 100% brightness to aid evacuation.
*   🛠️ **Maintenance Wizard**: A guided, interactive walkthrough on your phone to perform monthly tests without missing a single device.
*   🔇 **Smart Mute**: Silence all detectors from your phone (with Zigbee network congestion protection).
*   🌍 **Multi-Language**: Fully translatable interface (English, Dutch, German, etc.).

---

## 📋 Requirements

1.  **Home Assistant** (2024.10 or newer).
2.  **Aqara Smoke Detectors** (Model `JY-GZ-01AQ`) connected via Zigbee (ZHA or Zigbee2MQTT).
3.  **Home Assistant Mobile App** installed on your phone.

---

## 🚀 Installation

### Option 1: Direct Import (Recommended)
1.  Click the badge below to import the blueprint directly into your Home Assistant instance.
    [![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint URL.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=LINK_TO_YOUR_GITHUB_RAW_FILE)
2.  Click **"Preview Blueprint"** and then **"Import Blueprint"**.

### Option 2: Manual Installation
1.  Copy the code from `xat0x-aqara-smoke-linker-ultimate.yaml`.
2.  Go to your Home Assistant config folder: `/config/blueprints/automation/xat0x/`.
3.  Create a file named `aqara_linker.yaml` and paste the code.
4.  Go to **Developer Tools** -> **YAML** -> **Reload Automations**.

---

## ⚙️ Configuration Guide

Create a new automation using this blueprint and follow these steps:

### 1. Devices & Notifications
*   **Smoke Detectors**: Select ALL your Aqara smoke entities here.
*   **Alarm Notification Devices**: Select the phones that must receive critical alerts (e.g., yours and your partner's).
*   **Enable Critical Alerts**: Keep this **ON**.
    *   *iOS Users*: Go to iOS Settings -> Home Assistant -> Notifications -> Allow Critical Alerts.
    *   *Android Users*: In the App settings, ensure the channel `alarm_stream` is set to "Override Do Not Disturb".

### 2. Pre-Alarm (Verification Phase)
*   **Enable Pre-Alarm**: Recommended **ON**.
*   **Timeout**: Default is 15 seconds. This is the time you have to grab your phone and say "FALSE ALARM" before the loud sirens start.

### 3. Main Alarm (Evacuation Phase)
*   **Emergency Lights**: Select your light groups here. They will turn ON (100% brightness) when the full alarm triggers.
*   **Actions**: You can add extra actions here, like unlocking smart locks (Nuki/Yale), opening blinds, or turning off the HVAC.

### 4. Maintenance (Monthly Test)
*   **Maintenance Device**: Select ONE phone that you use to walk around the house for testing.
*   **Enable Self-Test**: Keep **ON**.

---

## 🛡️ How it works

### Scenario 1: Burnt Toast (Pre-Alarm)
1.  Smoke is detected in the Kitchen.
2.  **NO sirens** go off yet.
3.  Your phone gets a **Critical Notification**: *"Smoke detected in Kitchen. Confirm Fire?"*
4.  You press **"FALSE ALARM"**.
5.  The system resets. The kids don't wake up. Peace remains.

### Scenario 2: Real Fire (Main Alarm)
1.  Smoke is detected in the Garage.
2.  You get the Pre-Alarm notification but you are not home (or asleep).
3.  After 15 seconds (timeout), the **FULL ALARM** triggers.
4.  **ALL** Aqara detectors start sirenning.
5.  **ALL** lights turn on.
6.  You get a new notification: **"FIRE - EVACUATE!"**.

### Scenario 3: Monthly Maintenance
1.  Walk to any smoke detector.
2.  Press the physical button on the device shortly.
3.  Your phone receives a notification: *"Smoke Detector Self-Test (1/6)"*.
4.  The app guides you: *"Go to Living Room. Press the button."*
5.  You confirm via the app and move to the next room until all are tested.

---

## ❓ FAQ & Troubleshooting

**Q: I pressed "Mute" on my phone, but the sirens are still going?**
A: Zigbee traffic can be heavy during an alarm. The blueprint has a "Smart Mute" loop that keeps sending the mute command every few seconds until the detectors respond. Be patient, it might take 5-10 seconds.

**Q: Do I need the "Smoke Spray Test"?**
A: This is optional. If enabled, the maintenance wizard will ask if you want to perform a real smoke test (using a spray can). If you say "Yes", the system allows a real alarm to trigger without activating the full evacuation plan (lights/locks), just to test the sensor.

**Q: Why 'Restart' mode?**
A: Safety first. If you are running a test and a REAL fire breaks out, the blueprint immediately restarts to handle the real alarm. Real danger always takes priority over testing.

---

## ⚠️ Disclaimer

**Use at your own risk.**

This blueprint and script are provided "as is", without warranty of any kind, express or implied.
The author (**Xat0X**) cannot be held responsible for any damage, injury, loss of property, or failure of the system to operate as expected.

*   This system is **NOT** a certified fire alarm system and should not replace professional, certified safety equipment.
*   Always ensure you have working, standalone smoke detectors as a primary safety measure.
*   Home Assistant, Zigbee networks, and WiFi can experience downtime; do not rely solely on this software for life-safety.

**Created with ❤️ by Xat0X**
