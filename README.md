# Wireless RF PC Power Button
A wireless remote power switch for desktop PCs, built around a 433 MHz RF transmitter and receiver. The receiver drives a relay whose potential-free contact bridges the motherboard's power-switch header (JFP1), so a press on the handheld transmitter powers the machine on — exactly like pressing the case button, but from across the room.

> ⚠️ **Read the entire README before building or wiring anything.**
> This project connects to a live motherboard — skipping the README can cost you hardware.

---

## Motivation
My PC is in a hard to reach spot so getting up to reach the physical power button is a hassle. So I built a small RF receiver that taps into the motherboard's front-panel power header and lets me switch the system on wirelessly without leaving my chair.

---

## How it works
A QIACHIP TX181-4 handheld transmitter sends a 433 MHz signal on button press.
A QIACHIP QA-R-012V3 receiver, set to momentary mode, switches its output only while the signal is present.
The receiver output powers a 5 V relay module (JQC3F-05VDC), whose potential-free COM/NO contact is wired across the two power-switch pins of the motherboard header.
Because the relay contact is galvanically isolated, no voltage ever reaches the header — it only closes the circuit, mimicking a real button press.
The whole circuit is powered from a USB port that stays live in S5 (standby), enabled via BIOS.

---

## Demo

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
(`.step`) for use in any other CAD package, and **STL** (`.stl`) ready to slice and print.
The receiver housing is a simple two-piece `top` / `bottom` shell. The transmitter adds a
`battery_cover` and a `battery_sled` that holds the cell and aligns it with the contacts. 
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

The transmitter is a bare 433 MHz RF board with just two connections: + and GND, fed from a 3–24 V source. A momentary push-button sits in the positive line, so the board is only powered — and only transmits — while the button is pressed. Each press sends the RF signal the receiver listens for.

<img width="690" height="478" alt="image" src="https://github.com/user-attachments/assets/51204a8b-f7ad-47fd-8ddf-78119028ba95" />

The receiver is powered from the PC's USB 2.0 header (VCC + Ground — see pinout). Its switched output drives the relay module, whose potential-free contact is wired across the Power Switch pins of the JFP1 front-panel header. When the receiver gets a signal, the relay briefly closes that contact — the motherboard reads it as a normal power-button press.

<img width="1636" height="901" alt="image" src="https://github.com/user-attachments/assets/a55c320c-1035-4445-bd5f-fae411301ceb" />


---

## Pairing the receiver (momentary mode)

1. Reset: press the receiver's Learning button **8×** → LED flashes and goes out.
2. Press the Learning button **1×** → LED stays on (setup mode).
3. Trigger the transmitter → LED flashes and goes out = paired.
4. Test: the relay should close only **while** the transmitter is sending.

---

## Assembly

### Receiver

<img width="1080" height="1920" alt="image" src="https://github.com/user-attachments/assets/c5ae8063-5feb-434e-a205-6e50a2e919c7" />


### Transmitter

<img width="1080" height="1920" alt="image" src="https://github.com/user-attachments/assets/c90d9a84-7dec-4ff1-9ac6-76ac8ef292a7" />


---

## Getting 5 V while the PC is off

The circuit needs power in the soft-off state (S5) so the receiver can listen for the signal. A normal USB port is usually dead when the PC is off — you have to enable standby power in the BIOS, or use an always-on source.

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









