# kball3 ZMK Firmware

ZMK Firmware repository for **kball3**, a custom BLE trackball keyboard built with **Seeed Studio XIAO nRF52840** and a **PMW3610 optical trackball sensor breakout board**.

---

## 🛠 Hardware Mapping

| Function | XIAO Pad | Pin Name | Description |
| :--- | :--- | :--- | :--- |
| **BTN1** | Pad 2 / D1 | `P0.03` | Left Click (`&mkp LCLK`) |
| **BTN2** | Pad 3 / D2 | `P0.28` | Middle Click (`&mkp MCLK`) |
| **BTN3** | Pad 4 / D3 | `P0.29` | Right Click (`&mkp RCLK`) |
| **SCLK** | Pad 6 / D5 | `P0.05` | PMW3610 SPI Clock |
| **SDIO** | Pad 5 / D4 | `P0.04` | PMW3610 SPI Data (Bi-directional) |
| **nCS** | Pad 8 / D7 | `P1.12` | PMW3610 Chip Select |
| **MOTION** | Pad 11 / D10 | `P1.15` | PMW3610 Motion Interrupt |
| **VCC** | Pad 12 | `3V3` | Power Supply |
| **GND** | Pad 13 | `GND` | Ground |

---

## 🚀 How to Build & Flash Firmware

### 1. Push to GitHub
If you haven't pushed this repository to GitHub yet, run the following commands on your Mac terminal:

```bash
cd /Users/kotoba489/.gemini/antigravity/scratch/kball3
git remote add origin https://github.com/kotoba489/kball3.git
git branch -M main
git push -u origin main --force
```

### 2. Automatic GitHub Actions Build
1. Go to your GitHub repository: `https://github.com/kotoba489/kball3`
2. Click the **Actions** tab.
3. Wait for the build workflow to finish (~3 minutes).
4. Download the `firmware.zip` artifact from the completed workflow run.
5. Extract `firmware.zip` to get `zmk.uf2`.

### 3. Flash to XIAO nRF52840
1. Connect your XIAO nRF52840 to your Mac via USB-C cable.
2. Double-press the small **RESET** button on the XIAO board quickly.
3. A USB mass storage drive named `XIAO-SENSE` (or `NO_NAME`) will appear on your Mac.
4. Drag and drop `zmk.uf2` into the USB drive.
5. The device will reboot automatically upon flashing completion.

---

## 📱 Pairing with Android / Mac

1. Turn on Bluetooth on your Android smartphone or Mac.
2. Search for new Bluetooth devices.
3. Select **`kball3`** from the list to pair.
4. Test trackball cursor movement and mouse clicks!
