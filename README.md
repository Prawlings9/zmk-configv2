# Sofle ZMK Firmware

This repo builds and publishes firmware for a Sofle keyboard running ZMK on **nice!nano v2** controllers.  
Each push/PR to this repo automatically produces firmware artifacts for flashing.

---

## 🔧 Build Targets

Defined in [`build.yaml`](./build.yaml):

- `nice_nano_v2 + sofle_left`
- `nice_nano_v2 + sofle_right`
- `nice_nano_v2 + settings_reset` (wipe stored settings/bonds)

---

## ⬇️ Downloading Firmware

1. Go to [Actions](../../actions) → open the latest successful run.
2. Under **Artifacts**, download:
   - `sofle_left` → flash to the **left half**
   - `sofle_right` → flash to the **right half**
   - `settings_reset` *(optional)* → only if you need to wipe settings on a half.

---

## 💾 Flashing Guide

1. **Enter bootloader mode**:  
   Double-tap the reset button on your nice!nano. A USB drive named `NICENANO` will appear.

2. **Flash firmware**:  
   Drag & drop the correct `.uf2` onto the drive:
   - Left build → left nice!nano  
   - Right build → right nice!nano  

3. **Reboot automatically**:  
   The drive will disappear, and the half will reboot into ZMK firmware.

---

## 🔌 Bluetooth Pairing

On the **RAISE** layer:
- `BT_CLR` → clear old bonds
- `BT1…BT5` → select Bluetooth profile slots

On your computer/phone, pair the Sofle when it appears in Bluetooth devices.  
Repeat for each slot you want to use.

---

## 🌈 RGB Controls Cheatsheet

Hold **LOWER + RAISE** to enter the **ADJUST** layer:

### Power
- `RGB_TOG` → Toggle underglow ON/OFF  
- `EP_TOG` → Toggle external LED power (if wired that way)  

### Effects
- `RGB_EFF` → Cycle through:
  1. Solid  
  2. Breathing  
  3. Rainbow Swirl  
  4. Rainbow Mood  
  5. Rainbow Chase  
  6. Twinkle ✨  
  7. Flicker 🔥  

### Adjustments
- `RGB_HUI` / `RGB_HUD` → Hue up/down (color wheel)  
- `RGB_SAI` / `RGB_SAD` → Saturation up/down (vivid ↔ white)  
- `RGB_BRI` / `RGB_BRD` → Brightness up/down  

#### Hue Reference
| Range | Colors |
|-------|--------|
| 0–30  | Red → Orange → Yellow (warm) |
| 60–180| Green → Cyan |
| 180–300 | Blue → Purple → Pink |
| 300–360 | Back to Red |

### Quick Recipes
- **Warm White** → Hue near orange/yellow + lower saturation  
- **Cool White** → Hue near cyan/blue + lower saturation  
- **Soft Ambient** → Any hue + low brightness/saturation  
- **Bold Pop** → Any hue + max saturation + high brightness  

---

## ⚡ Defaults (from this config)

- Lights **ON at startup**  
- Default effect = **Twinkle ✨**  
- Speed = **3/5 (medium)**  
- Brightness = **80%**  
- Saturation = **100% (vivid)**  

---

## 🛠️ Troubleshooting

- **Wrong half flashed?** → Re-flash with the correct `.uf2`.  
- **Weird behavior?** → Flash `settings_reset`, then re-flash normal firmware and re-pair Bluetooth.  
- **No lights?** → Confirm `CONFIG_ZMK_RGB_UNDERGLOW=y` in [`config/sofle.conf`](./config/sofle.conf).  
- **Display blanks when RGB off?** → Uncomment  
  ```ini
  CONFIG_ZMK_RGB_UNDERGLOW_EXT_POWER=n


RGB Controls (hold LOWER + RAISE to enter ADJUST)
• RGB_TOG: On/Off
• RGB_EFF: Next effect (Solid → Breathe → Rainbow Swirl → Rainbow Mood → Rainbow Chase → Twinkle → Flicker → …)
• RGB_HUI / RGB_HUD: Hue up/down (color)
• RGB_SAI / RGB_SAD: Saturation up/down (vivid ↔ white-ish)
• RGB_BRI / RGB_BRD: Brightness up/down
• EP_TOG: External LED power (if your build uses it)

## 🌈 RGB Controls Cheatsheet

Hold **LOWER + RAISE** to enter the **ADJUST** layer and use these keys:

### 🔌 Power
- `RGB_TOG` → Toggle underglow ON/OFF  
- `EP_TOG` → Toggle external LED power (if wired that way)  

### 🎨 Color & Modes
- `RGB_EFF` → Cycle through effects:  
  1. **Solid** (steady color)  
  2. **Breathing** (fade in/out)  
  3. **Rainbow Swirl**  
  4. **Rainbow Mood**  
  5. **Rainbow Chase**  
  6. **Twinkle** (sparkling stars)  
  7. **Flicker** (candle/fire-like)  
  → then loops back to Solid

### 🎛️ Adjustments (work in Solid & effects)
- `RGB_HUI` / `RGB_HUD` → Hue up/down (move around the color spectrum)  
- `RGB_SAI` / `RGB_SAD` → Saturation up/down (vivid ↔ white)  
- `RGB_BRI` / `RGB_BRD` → Brightness up/down  

#### Hue Reference
| Range (approx) | Colors |
|----------------|--------|
| 0–30           | Red → Orange → Yellow (warm) |
| 60–180         | Green → Cyan |
| 180–300        | Blue → Purple → Pink |
| 300–360        | Back to Red |

### 🔥 Quick Recipes
- **Warm White** → Hue near orange/yellow + lower saturation  
- **Cool White** → Hue near cyan/blue + lower saturation  
- **Soft Ambient** → Any hue + low brightness/saturation  
- **Bold Pop** → Any hue + max saturation + high brightness  

### ⚡ Defaults (from this config)
- Lights **ON at startup**  
- Default effect = **Twinkle ✨**  
- Speed = **3/5 (medium)**  
- Brightness = **80%**  
- Saturation = **100% (vivid)**

# ⌨️ Sofle Keymap Layers

This firmware is built for the Sofle with **nice!nano v2**, OLED displays, encoders, and RGB underglow.  
It uses four main layers:

- **Default** → typing & media
- **Lower** → symbols & function keys
- **Raise** → navigation, editing, Bluetooth
- **Adjust** → RGB & power controls (activated by holding LOWER + RAISE)

---

## 🅰️ Default Layer

**How to enter:**  
- This is the **default typing layer**. It is always active unless you hold a layer key (LOWER/RAISE).  

Everyday typing layer with standard QWERTY layout.

- **Encoders**:  
  - Left encoder → Volume up/down  
  - Right encoder → Page up/down  
- **Special keys**:  
  - `C_MUTE` → Mute system audio  
  - Standard modifiers (`CTRL`, `ALT`, `GUI`, `SHIFT`)  

![Default layer]
<img width="1918" height="900" alt="Screenshot 2025-09-07 104403" src="https://github.com/user-attachments/assets/3474d72d-6d5a-40c9-bd01-770c82e16380" />

---

## 🔽 Lower Layer
**How to enter:**  
- Hold the **LOWER** key (mapped to the thumb cluster).  

Symbols, shifted symbols, and function keys.

- **Top row**: F1–F12  
- **Numbers row**: 1–0 with shifted symbols  
- **Special symbols**: `=`, `-`, `+`, `{}`, `[]`, `;:`, `\|`  

![Lower layer] 

<img width="1916" height="898" alt="Screenshot 2025-09-07 105141" src="https://github.com/user-attachments/assets/2a91aa47-4f5f-4603-98b8-09044b5f2849" />

---

## 🔼 Raise Layer
Navigation, Bluetooth, and editing controls.

**How to enter:**  
- Hold the **RAISE** key (mapped to the thumb cluster).  

- **Bluetooth**:  
  - `BT_CLR` → Clear all bonds  
  - `BT_SEL0–4` → Switch between 5 Bluetooth profiles  
- **Navigation**:  
  - `PG_UP`, `PG_DN`, arrow keys  
- **Editing**:  
  - `INS`, `DEL`, `UNDO`, `CUT`, `COPY`, `PASTE`  
- **System**:  
  - `PSCRN`, `CAPS`  

![Raise layer]

 <img width="1914" height="894" alt="Screenshot 2025-09-07 105508" src="https://github.com/user-attachments/assets/8397f21d-7d30-4296-8649-fc2ca95f73e1" />
 
---

## 🎨 Adjust Layer

**How to enter:**  
- Hold **LOWER + RAISE** at the same time.  
- This activates the **ADJUST** layer. 

RGB underglow + external power. 

- **Power**:  
  - `RGB_TOG` → Toggle RGB on/off  
  - `EP_TOG` → Toggle external LED power  
- **RGB effects**:  
  - `RGB_EFF` → Cycle effects (Solid, Breathing, Rainbow Swirl, Rainbow Mood, Rainbow Chase, Twinkle, Flicker)  
- **RGB tuning**:  
  - `RGB_HUI/HUD` → Hue up/down (color wheel)  
  - `RGB_SAI/SAD` → Saturation up/down (vivid ↔ white)  
  - `RGB_BRI/BRD` → Brightness up/down  
- **Bluetooth**: Same as Raise layer (`BT_CLR`, `BT_SEL0–4`)  

![Adjust layer]

<img width="1915" height="900" alt="Screenshot 2025-09-07 105702" src="https://github.com/user-attachments/assets/5637fc53-66a2-40b2-b29c-02a7564c16e8" />

---

