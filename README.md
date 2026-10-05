# 📑 AM3X-LABS Digital Business Card PCB

An ultra-minimalist, battery-free, wireless networking device designed within standard credit card dimensions (**ID-1 format**). Combining structural PCB art with high-frequency radio interaction, this card allows you to tap it against any modern smartphone to instantly launch a web-based portfolio landing page—giving visitors immediate options to view your GitHub, LinkedIn, or download your CV.

---

## 🚀 Core Features

* 🔋 **100% Passive Operation:** Zero batteries, external charging, or power management circuits required [●].
* ⚡ **Dual LED Tap Indicators:** Two blue surface-mount LEDs light up instantly upon contact to confirm successful data transfer.
* 🎨 **Premium Industrial Aesthetics:** Designed with a sleek matte-black solder mask backdrop, crisp white silkscreen typography, and exposed **ENIG Gold** accents.
* ⚙️ **Invisible Component Architecture:** All physical components and trace routing are contained exclusively on the back layer; the front face remains perfectly smooth and free of visible electronics.

---

## 🛠️ Hardware & Component Specs

### 📐 Mechanical Dimensions
* **Form Factor:** Standard ID-1 (`85.60 mm` width × `53.98 mm` height)
* **Corner Profiles:** `3.18 mm` fillet radius
* **Substrate Thickness:** Ultra-slim **`0.80 mm`** or **`1.00 mm`** FR4 fiberglass *(to mimic standard credit card slimness instead of standard thick 1.60 mm boards)*.

### 📋 Bill of Materials (BOM)

| Reference | Qty | Description | Package Style | Function |
| :---: | :---: | :--- | :---: | :--- |
| **U1** | 1 | NTAG I2C Plus (Dynamic NFC Tag) | `TSSOP-8` | Wireless energy harvester & NDEF storage [●] |
| **D1, D2** | 2 | High-Brightness Blue Indicator LEDs | `0603 Reverse-Mount` | "Glow-through" visual feedback dots |
| **R1** | 1 | Current Limiting Resistor (100 Ω, 5%) | `0603 SMD` | Protects indicator LEDs from power surges |
| **ANT1** | 1 | Custom 4-Turn Spiral PCB Coil Antenna | `Hand-drawn on B.Cu` | 13.56 MHz RF inductive power receiver [●] |

---

## ⚡ How It Works (Theory of Operation)

### 1. RF Induction & Energy Harvesting
The card operates via Inductive Coupling at a resonant frequency of **13.56 MHz (NFC Type 2/4 Tag Standard)** [●]. When a smartphone brings its active NFC reader within **4 cm** of the card, the phone emits an alternating magnetic field. This field cuts through the card’s **4-turn perimeter copper loop antenna**, inducing an AC voltage. 

The **NXP NT3H2111 chip** receives this AC voltage through its `LA` and `LB` pins, routes it through an internal bridge rectifier, and outputs a steady DC voltage at **Pin 5 (`VOUT`)** [●].

### 2. Hardware LED Activation
Instead of an expensive, battery-draining microcontroller, the design leverages the chip's native hardware **Field Detect (`FD`) pin**. 
* **Standby State:** Pin 3 (`FD`) acts as an open switch (floating), keeping the circuit broken.
* **Active Scan State:** The exact microsecond the chip successfully detects a phone's RF command, an internal MOSFET closes, pulling Pin 3 (`FD`) hard to **Ground**. 
* **Result:** This completes the circuit loop from `VOUT` through the LEDs and down to Ground, causing the two blue indicator lights to instantly flash under the phone's harvested power.

---

## 🤝 Contributing & License
Distributed under the **MIT License**.
