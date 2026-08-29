# 🛸 Standalone ZMK Bluetooth Cirque Trackpad

An open-source, standalone wireless trackpad built using the **Seeed Studio XIAO BLE (nRF52840)** microcontroller and a **40mm Cirque GlidePoint Trackpad** running ZMK firmware. 

This project features full gesture support (Tap-to-Click, Double-Tap, and Bottom-Right Quadrant Right-Click) along with custom **Circular Rim Scrolling**—allowing you to scroll up and down by tracing your finger clockwise or counter-clockwise around the edge of the circle.

---

## 📦 European Shopping List

To simplify sourcing within the European Union and avoid customs import duties or delays, the electronics can be ordered together from Amazon Germany, and the boutique keyboard trackpad from Keycapsss.

| Component | Purpose | Sourcing Link |
| :--- | :--- | :--- |
| **Seeed Studio XIAO BLE Sense** | Main Microcontroller (with pre-soldered headers) | [Amazon Germany](https://amazon.de) |
| **Seeed Studio Grove Shield** | Expansion base breakout with built-in power switch | [Amazon Germany](https://amazon.de) |
| **EEMB 3.7V 1S 250mAh Battery** | Rechargable Lithium Polymer battery | [Amazon Germany](https://amazon.de) |
| **LightingWill 30 AWG Wires** | Ultra-flexible heat-resistant silicone soldering wires | [Amazon Germany](https://amazon.de) |
| **40mm Cirque GlidePoint Kit** | Circular trackpad module & FFC I2C adapter board | [Keycapsss](https://keycapsss.com) |

---

## 🔌 Hardware Configuration & Wiring Guide

### ⚠️ Step 1: Configure Trackpad for I2C Mode
Most Cirque trackpads ship in SPI communication mode by default. You **must change it to I2C mode** before wiring it to the Grove Shield:
1. Turn over the trackpad module to inspect the back circuit board.
2. Locate the tiny surface pads labeled **R1** and **R2**.
3. **Remove** the resistor or clear any solder bridging across **R1** (disables SPI).
4. **Close/Bridge** the solder connection or ensure a resistor sits across **R2** (enables I2C).

### ⚡ Step 2: The Solder Routing Blueprint
Mount your XIAO BLE firmly into the header sockets on top of the Grove Shield. Cut, strip, and tin your 30 AWG silicone wires, slide a piece of the included heat-shrink tubing onto each wire, and solder the components using this pinout mapping:

#### 🔋 Power Connections
* Connect the **Red (Positive)** wire of your LiPo battery to the pad marked **`BAT+`** on the back of the Grove Shield.
* Connect the **Black (Negative)** wire of your LiPo battery to the pad marked **`GND`** on the back of the Grove Shield.

#### 📊 Data Signal Routing
Solder your flexible silicone lines from the side pin columns of the Grove Shield over to the terminal holes on your Keycapsss Cirque FFC adapter module:

| Grove Shield Pin Layout | Interconnect Wire Line | Cirque FFC Adapter Board Terminal |
| :--- | :---: | :--- |
| **3.3V** | ➡️ | **VCC** (System Power) |
| **GND** | ➡️ | **GND** (System Ground) |
| **D4** | ➡️ | **SDA** (I2C Data line) |
| **D5** | ➡️ | **SCL** (I2C Clock line) |
| **D3** | ➡️ | **DR** (Data Ready / Interrupt) |

---

## 🛠️ Software Gestures Reference

This repository is optimized for complete, single-finger on-surface touch mapping without needing secondary physical mouse buttons:

* 🖱️ **Pointer Movement:** Glide your finger freely anywhere within the inner **88%** circle of the surface.
* 👆 **Left Click:** Tap once quickly anywhere on the center trackpad surface.
* ✌️ **Double Click:** Tap twice quickly anywhere on the center trackpad surface.
* 📑 **Right Click:** Tap once specifically within the **bottom-right quadrant** area of the circle surface.
* 🌀 **Circular Scrolling:** Place your finger directly onto the outermost **12% rim/edge** of the trackpad. Tracing your finger in a **clockwise** arc scrolls downward. Tracing a **counter-clockwise** arc scrolls upward.

---

## 🚀 Flashing the Firmware

When your GitHub Action finishes compiling successfully, download and flash the payload using these steps:
1. Extract the downloaded `firmware.zip` folder to get the **`xiao_ble-zmk.uf2`** asset.
2. Link your stacked XIAO BLE board to your PC using a standard USB-C data cable.
3. Use a small tweezer tip or paperclip to press the physical tiny **Reset Button** on the side of the board twice rapidly.
4. The device will reboot and appear on your computer filesystem as an external thumb drive named **`XIAO-SENSE`**.
5. Drag and drop your **`xiao_ble-zmk.uf2`** file directly into the drive folder. 
6. The board will automatically swallow the file, flash its memory storage, and disconnect. Turn your hardware power switch on, pair it via your OS Bluetooth settings panel, and your trackpad is ready for use!
