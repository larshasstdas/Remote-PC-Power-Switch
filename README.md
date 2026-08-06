# Wireless PC Power Button
This project is about a wireless PC power button I build. A 433MHz receiver shorts the power header pins on the mainboard with the help of an relay. The sender is powered by a small battery and send only when the button is pressed.

> ⚠️ **Read the README before building!**
> This project connects to a live motherboard and skipping the README can cost you hardware.

<img width="1605" height="509" alt="WhatsApp Image 2026-06-20 dadda" src="https://github.com/user-attachments/assets/a407b295-b4e7-488d-8dff-001ab0f3c669" />

---

## Motivation
It is annoying to always reach for my PC power button so I got the idea to build a switch that lets me power my PC wirelessly without leaving my chair.

---

## How it works
The QIACHIP TX181-4 transmitter sends a 433 MHz signal when a button is pressed.
The QIACHIP QA-R-012V3 receiver (in momentary mode) has an output voltage when a signal is sent.
The receiver is connected to a relay, which shorts the power pins of the header on my motherboard when there is voltage on the input pins.
The receiver is powered by USB port which needs specific BIOS to always have power and the transmitter is powered by a button battery cell.

---

## Demo

[Youtube Demo](https://youtube.com/shorts/TQeXVGS3ae0)

---

## Bill of Materials

All electronic parts are from AliExpress. The transmitter and receiver ship together as one 433 MHz kit. The enclosure is 3D-printed (files in this repo), so its only cost is filament. Miscellaneous parts (wick, dupont wires, battery) have no dedicated link and the price is a rough estimate.

| Part                        | Description                                   | Qty | Unit Price | Link |
| --------------------------- | --------------------------------------------- | --- | ---------- | ---- |
| QIACHIP TX181-4             | 433 MHz transmitter (TX+RX kit)               | 1   | ~€4.59     | [AliExpress](https://de.aliexpress.com/item/1005008804838337.html) |
| QIACHIP QA-R-012V3          | 433 MHz receiver (same kit as above)          | 1   | –          | [AliExpress](https://de.aliexpress.com/item/1005008804838337.html) |
| 5V single-channel relay     | Shorts the motherboard power-header pins       | 1   | ~€1.85     | [AliExpress](https://de.aliexpress.com/item/1005004594181635.html) |
| Push button                 | Triggers the transmitter                       | 1   | ~€4.79     | [AliExpress](https://de.aliexpress.com/item/1005007336010480.html) |
| CR2025 battery              | Powers the transmitter                         | 1   | ~€0.50     | – |
| Desoldering wick            | Coated with solder; battery contacts (~7.5 cm) | 1   | ~€0.30     | – |
| Dupont jumper wires & pins  | Internal wiring and connectors                 | 1   | ~€0.50     | – |
| 3D-printed enclosure        | Filament for both housings (files in repo)     | 1   | ~€0.50     | – |
| **Total**                   |                                                |     | **~€13.03** | |

---

## Box

There are two 3D printed boxes with a folder each. They have the original **Creo Parametric** (`.prt`) file for editing, **STEP**
(`.step`) for use in other CAD programms, and **STL** (`.stl`) which can be sliced and printed.
The receiver housing  has a `top` and a `bottom` while the transmitter adds a `battery_cover` and a `battery_sled` that holds the cell and aligns it with the contacts. 
In the creo files there is also a full assembly of each box (`.asm`).
Furthermore there is the Bill of Material (`BOM.csv`) that are needed but it is just the same as what is written above.
### Files

```
receiver/
├── creo/
    ├── receiver_top.prt
    ├── receiver_bottom.prt
    └── receiver.asm
├── step/
    ├── receiver_top.step
    └── receiver_bottom.step
└── stl/
    ├── receiver_top.stl
    └── receiver_bottom.stl
    
transmitter/
├── creo/
    ├── transmitter_top.prt
    ├── transmitter_bottom.prt
    ├── battery_cover.prt
    ├── battery_sled.prt
    └── transmitter.asm
├── step/
    ├── transmitter_top.step
    ├── transmitter_bottom.step
    ├── battery_cover.step
    └── battery_sled.step
└── stl/
    ├── transmitter_top.stl
    ├── transmitter_bottom.stl
    ├── battery_cover.stl
    └── battery_sled.stl
BOM.csv
```
---

## Wiring overview

The transmitter is a 433 MHz RF board with just two connections: + and GND, powered by a button cell battery. The transmitter only transmits whhen the button is pressed. Each press sends a signal the receiver receives and responds with an output voltage.

<img width="690" height="478" alt="image" src="https://github.com/user-attachments/assets/51204a8b-f7ad-47fd-8ddf-78119028ba95" />

The receiver is powered from the PC's USB 2.0 header. When the receiver gets a signal, the relay shorts the power pins and the motherboard thinks it is a normal power button press. You need to check your mainboard manuel if your pinout on the mainboard is the same to be safe but there shouldn't be any major differences.

<img width="1636" height="901" alt="image" src="https://github.com/user-attachments/assets/a55c320c-1035-4445-bd5f-fae411301ceb" />


---

## Pairing the receiver (momentary mode)

1. Reset: press the receiver's Learning button **8** times → LED flashes and goes out
2. Press the Learning button **once** → LED stays on
3. Trigger the transmitter → LED flashes and goes out = paired
4. Test: the relay should close only **while** the transmitter is sending

---

## Assembly

### Receiver Assembly

1. **Crimp the wires.** Crimp Dupont connectors onto the wires that link the
  box with the motherboard pins.
2. **Wire the relay.** Screw the wires into the relay module's terminals as shown
   in the [Wiring overview](#wiring-overview) above.
   
   <img width="1411" height="530" alt="WhatsApp Image 2026-06-14 at 21 59 54" src="https://github.com/user-attachments/assets/3740e503-358f-443d-9474-8a36710977ed" />

3. **Place the modules.** Seat the receiver module and the relay module in their
   designated spots in the enclosure.
4. **Route the wires.** Two wires must run underneath the relay. Bend the remaining wires into place so nothing is getting pinched when closing the box.
   
  <img width="1724" height="719" alt="WhatsApp Image 2026-06-14 at 23 08 51" src="https://github.com/user-attachments/assets/7efd94c3-04e8-44d2-98d2-17314b9d80d3" />


5. **Close the case.** Bring the box halves together.

<img width="1724" height="719" alt="WhatsApp Image 2026-06-14 at 23 08 51" src="https://github.com/user-attachments/assets/79259a96-b5d3-481e-9abc-e5f0b4a84310" />

---

### Transmitter Assembly

1. **Coating the desoldering braid with solder.** Coat the two pieces of desoldering braid with
   solder, one needs to be **3.5 cm**, the other one **4 cm**. They are the battery contacts.

2. **Place the contacts.** Fit the 3.5 cm braid into the **battery cover** and the
   4 cm braid into the **bottom half** of the housing.
   
   <img width="1386" height="591" alt="WhatsApp Image 2026-06-17 at 16 34 40" src="https://github.com/user-attachments/assets/128bfe7a-561f-43b3-be90-433e0b27058d" />

3. **Solder the Dupont pins.** Solder a shortened Dupont pin to each contact.
   Hold steady as the surrounding plastic will melt.
   
    <img width="466" height="438" alt="WhatsApp Image 2026-06-19 at 16 45 19" src="https://github.com/user-attachments/assets/b00c6bde-3258-47e0-89b9-328961b65948" />
    
4. **Wire the button.** Solder the wires to the push-button as shown in the
   [Wiring overview](#wiring-overview) above. All battery connections use dupont
   plugs.

   <img width="950" height="1259" alt="WhatsApp Image 2026-06-18 at 18 13 57" src="https://github.com/user-attachments/assets/b2e540fb-4941-4692-89c1-a017a660d76a" />

5. **Mount the module and button.** Feed the transmitter module through the button
   opening and fix the button in place with its nut.
6. **Place and route.** Seat the module in its designated spot, then bend the
   antenna and wires into place.

    <img width="1121" height="750" alt="WhatsApp Image 2026-06-19 at 22 16 51" src="https://github.com/user-attachments/assets/40862b54-9a4c-4986-bc98-e97118ced9f4" />

7. **Insert the battery cover.** Set the battery cover in and connect its pins.
8. **Close the case.** Carefully bring the enclosure halves together.
9. **Insert the battery.** Slide the battery sled in with the battery installed.

<img width="875" height="901" alt="WhatsApp Image 2026-06-21 at 11 59 23" src="https://github.com/user-attachments/assets/29671b41-5d62-4ef6-9958-254db20cba80" />



---

## Getting 5V while the PC is off

The circuit needs power in the soft-off state (S5) so the receiver can listen for the signal. A normal USB port is usually dead when the PC is off so you have to enable standby power in the BIOS, or use an always-on source.

| Setting | Value | Why |
|---------|-------|-----|
| `ErP Ready` | **Disabled** | Keeps standby power flowing in S5 instead of cutting it for power saving |
| `Resume By USB Device` | **Enabled** | Provides standby power on the USB rails so the port stays live when the PC is off |

**Verify with a multimeter** that the USB VCC pin actually carries 5V while the PC is shut down.

### Alternative power sources

- **External 5V supply**: always on, fully independent of the PC and BIOS. The simplest option, and it works because the relay contact is potential-free.
- **5V standby**: the purple wire on the 24-pin ATX connector, always live whenever the PSU is connected and switched on at the back.

---

## ⚠️ Warnings

The relay contact **must be potential-free**. Never feed supply voltage into the motherboard header. Use only COM + NO across the two power-switch pins.
As this project connects to a live PC only work on the motherboard with the PC comletly powered down (flip the switch on the back when shut off or pull the cable). 
Do this at your own risk.

---







