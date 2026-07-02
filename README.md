# Wireless RF PC Power Button
This repository is about a wireless remote power switch for your PC. It is built with a 433 MHz RF transmitter and receiver. The receiver drives a relay whose potential-free contact bridges the motherboard's power-switch header. If you press the button on the transmitter it powers the PC on from across the room.

> ⚠️ **Read the entire README before building or wiring anything.**
> This project connects to a live motherboard — skipping the README can cost you hardware.

<img width="1605" height="509" alt="WhatsApp Image 2026-06-20 dadda" src="https://github.com/user-attachments/assets/a407b295-b4e7-488d-8dff-001ab0f3c669" />

---

## Motivation
My PC is in a hard to reach spot so getting up to reach the physical power button is a hassle. So I built a small RF receiver that lets me switch the system on wirelessly without leaving my chair.

---

## How it works
A QIACHIP TX181-4 transmitter sends a 433 MHz signal on button press.
A QIACHIP QA-R-012V3 receiver, set to momentary mode, switches its output only while the signal is sent.
The receiver output powers a relay module, whose contact is wired across the two power-switch pins of the motherboard header and shorts the power pins.
The whole circuit is powered from a USB port.

---

## Demo

▶️ [Watch the demo (YouTube Short)](https://youtube.com/shorts/TQeXVGS3ae0)

---


## Hardware

| Part | Description |
|------|-------------|
| QIACHIP TX181-4 | 433 MHz RF handheld transmitter |
| QIACHIP QA-R-012V3 | 433 MHz RF receiver module |
| Relay module | 5 V single-channel |
| Button | The button used for sending the signal |
| CR2025 Battery | Battery used to power the transmitter |
| desoldering wick | used as a battery contact |
| Misc | dupont jumper wires and pins,  3D-printed enclosure |

### Links

Links for the parts i used and that fit my 3D-print enclosure. I wont list any miscellaneous parts. All my parts are from AliExpress.

| Part | Link |
|------|------|
| Transmitter + Receiver | https://de.aliexpress.com/item/1005008804838337.html?spm=a2g0o.order_list.order_list_main.11.23b118025INdwz&gatewayAdapt=glo2deu |
| Relay module | https://de.aliexpress.com/item/1005004594181635.html?spm=a2g0o.order_list.order_list_main.17.23b118025INdwz&gatewayAdapt=glo2deu |
| Button | https://de.aliexpress.com/item/1005012177068665.html?spm=a2g0o.cart.0.0.22e638daetG5uO&mp=1&pdp_npi=6%40dis%21EUR%21EUR+42.10%21EUR+16.39%21%21EUR+16.39%21%21%21%400b8848e317819510011406436e0fbb%2112000057680737414%21ct%21DE%218046212832%21%211%210%21&gatewayAdapt=glo2deu |

---

## Enclosure

The 3D-printed enclosure is split into two folders — one for each device — with every
part provided in three formats: native **Creo Parametric** (`.prt`) for editing, **STEP**
(`.step`) for use in any other CAD package, and **STL** (`.stl`) which can be sliced and printed.
The receiver housing  has a `top` and a `bottom` while the transmitter adds a `battery_cover` and a `battery_sled` that holds the cell and aligns it with the contacts. 
In the creo files there is also a full assembly of each box (`.asm`).

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
    └── battery_sled.step
```
---

## Wiring overview

The transmitter is a 433 MHz RF board with just two connections: + and GND, fed from a button cell battery. A button sits in the positive line, so the board is only powered and only transmits while the button is pressed. Each press sends the RF signal the receiver listens for.

<img width="690" height="478" alt="image" src="https://github.com/user-attachments/assets/51204a8b-f7ad-47fd-8ddf-78119028ba95" />

The receiver is powered from the PC's USB 2.0 header (see pinout). When the receiver gets a signal, the relay shorts the power pins and the motherboard reads it as a normal power-button press. You need to check your mainboard manuel if your pinout on the mainboard is the same to be safe but there shouldn't be any major differences.

<img width="1636" height="901" alt="image" src="https://github.com/user-attachments/assets/a55c320c-1035-4445-bd5f-fae411301ceb" />


---

## Pairing the receiver (momentary mode)

1. Reset: press the receiver's Learning button **8×** → LED flashes and goes out
2. Press the Learning button **1×** → LED stays on
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
4. **Route the wires.** Two wires must run *underneath* the relay; gently bend
   the remaining wires into place so nothing is getting pinched.
   
  <img width="1724" height="719" alt="WhatsApp Image 2026-06-14 at 23 08 51" src="https://github.com/user-attachments/assets/7efd94c3-04e8-44d2-98d2-17314b9d80d3" />


5. **Close the case.** Bring the enclosure halves together.

<img width="1724" height="719" alt="WhatsApp Image 2026-06-14 at 23 08 51" src="https://github.com/user-attachments/assets/79259a96-b5d3-481e-9abc-e5f0b4a84310" />

---

### Transmitter Assembly

1. **Tin the desoldering braid.** Tin two lengths of desoldering braid with
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

## Getting 5 V while the PC is off

The circuit needs power in the soft-off state (S5) so the receiver can listen for the signal. A normal USB port is usually dead when the PC is off so you have to enable standby power in the BIOS, or use an always-on source.

| Setting | Value | Why |
|---------|-------|-----|
| `ErP Ready` | **Disabled** | Keeps standby power flowing in S5 instead of cutting it for power saving |
| `Resume By USB Device` | **Enabled** | Provides standby power on the USB rails so the port stays live when the PC is off |

**Verify with a multimeter** that the USB VCC pin actually carries ~5 V while the PC is shut down.

### Alternative power sources

- **External 5 V supply**  — always on, fully independent of the PC and BIOS. The simplest option, and it works because the relay contact is potential-free.
- **5 V standby ** — the purple wire on the 24-pin ATX connector, always live whenever the PSU is connected and switched on at the back.

---

## ⚠️ Warnings

- The relay contact **must be potential-free** — never feed supply voltage into the motherboard header. Use only COM + NO across the two power-switch pins.
- The receiver needs **≥ 3.6 V**, and the 5 V relay coil won't pull in reliably below ~4 V. 
- Use **momentary mode** on the receiver (Learning button × 1, then trigger the transmitter) so the relay only pulses briefly, like a real power button.
- If pairing is lost ("worked once, then nothing"), reset the receiver (Learning button × 8) and re-pair in momentary mode.
- Keep at least 30–50 cm between transmitter and receiver during bench testing — these cheap super-regen receivers can go deaf in the near field.

---


## Safety

This project connects to a live PC. Work on the motherboard header only with the system fully powered down. Double-check the relay contact is potential-free and that you are wiring to the correct JFP1 power-switch pins before powering anything on. Do this at your own risk.









