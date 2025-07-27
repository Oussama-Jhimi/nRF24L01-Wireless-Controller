# ⚡️ Wireless PS/2 Controller Interface with Arduino Pro Mini & nRF24L01+

![Arduino](https://img.shields.io/badge/Arduino-Pro%20Mini-blue) ![NRF24L01](https://img.shields.io/badge/nRF24L01%2B-2.4GHz-green) ![PS2](https://img.shields.io/badge/PS%2F2-Interface-orange)

A compact, battery‑friendly system that reads a PS/2 game controller (joystick or pad) and transmits its data wirelessly over a 2.4 GHz link using the nRF24L01+ module.

---

## 🚀 Features

- 🎮 **Real‑time PS/2 input** — read button presses and joystick axes  
- 📡 **Wireless SPI transmission** via nRF24L01+ (CE, CSN, SCK, MISO, MOSI)  
- 🔄 **Full duplex** — separate sketches for **transmitter** (PS/2 → RF) and **receiver** (RF → host)  
- 🔋 **Low power** — suitable for portable/battery operation  
- 🔧 **Easy integration** for robotics, DIY gaming rigs, or remote controls  

---

## 🧩 Hardware Overview

### 1. 5 V ➔ 3.3 V Regulator  
- **AMS1117‑3.3** with input cap C1 = 10 µF, output cap C2 = 22 µF  
- Ensures stable 3.3 V supply for the radio and PS/2 port  

### 2. Arduino Pro Mini (3.3 V / 8 MHz)  
- Hosts the PS/2 reading and nRF24L01+ driver code  
- Exposes SPI pins and control lines to the radio module  

### 3. nRF24L01+ (2.4 GHz, SPI)  
- **IRQ**, **CSN**, **CE**, **SCK**, **MISO**, **MOSI**  
- Handles wireless link to the receiver module  

### 4. PS/2 Connector (6‑pin)  
- **SEL**,**CMD**,**CLK**, **DAT**, **VCC (3.3 V)**, **GND**  
- Standard PS/2 wiring for legacy controllers

### 5. PCB Layout  
- 🖥️ **Altium Designer**  
  - Les fichiers de schéma et de routage Altium (`.SchDoc` & `.PcbDoc`) sont disponibles 

---

## 🔌 Wiring Diagram

#### PS/2 → Arduino Pro Mini

| PS/2 Pin | Function | Arduino Pin |
|:--------:|:--------:|:-----------:|
| SEL      | Select   | D2          |
| CMD      | Command  | D3          |
| CLK      | Clock    | D4          |
| DAT      | Data     | D5          |
| +3.3 V   | VCC      | VCC         |
| GND      | Ground   | GND         |

#### Arduino → nRF24L01+

| Arduino Pin | nRF24L01+ Pin | Function       |
|:-----------:|:-------------:|:--------------:|
| D10         | CSN           | Chip Select    |
| D9          | CE            | Chip Enable    |
| D13 (SCK)   | SCK           | SPI Clock      |
| D12 (MISO)  | MISO          | Master In      |
| D11 (MOSI)  | MOSI          | Master Out     |
| +3.3 V      | VCC           | Power Supply   |
| GND         | GND           | Ground         |

> **Tip**: Place the AMS1117 close to the 5 V source and keep ground returns short for best stability.

---

## 🛠️ Setup & Usage

1. **Open the sketches** in the Arduino IDE  
   - 📨 `Transmitter/PS2_TX.ino`  
   - 📥 `Receiver/PS2_RX.ino`

2. **Select board & port**  
   - ⚙️ Board: *Arduino Pro Mini 3.3 V / 8 MHz*  
   - 🔌 Port: the COM port your Arduino is on

3. **Adjust pin mappings**  
   - 🔧 Edit the pin definitions at the top of each sketch to match your wiring

4. **Upload sketches**  
   - ▶️ Transmitter → master Arduino (PS/2 side)  
   - ▶️ Receiver    → slave Arduino (host side)

5. **Power up**  
   - 🔋 Supply 5 V via USB or battery to each circuit

⚠️NB :Make sure to update the pin declarations in the code so they match your actual GPIO connections and circuit layout.  
