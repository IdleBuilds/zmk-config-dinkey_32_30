# ZMK Config — Dinkey 32|30

ZMK firmware configuration for the **Dinkey 32|30**, a 32 or 30-key low-profile wireless split keyboard by [Idle Builds](https://idlebuilds.com).

<div align="center">
<img src="docs/images/dinkey_32_30_32_key_config_zmk.png" alt="Dinkey 32|30" width="800"/>
</div>

---

## About the Dinkey 32|30

The Dinkey 32|30 is the refined endgame version of the Dinkey keyboard lineup. It shares the same PCB footprint as the Dinkey 34 but removes the outermost pinky column key, giving you a cleaner, more minimal layout. The "32|30" name reflects the modular pinky column design: the 4th pinky column accommodates either one or two switches without any firmware changes, letting you choose your own key count.

The Dinkey 32|30 shares its keymap structure and firmware logic with the Dinkey 34 — the difference between the two boards is in the PCB design and hardware pin assignments, not the keymap or ZMK behavior layer.

---

## Specs

### Wireless Build (Nice!Nano v2)

| | |
|---|---|
| **Keys** | 32 or 30 (user selectable, no firmware change required) |
| **Layout** | 3×5 column stagger + 2 thumb keys per side |
| **Switches** | Kailh Choc V1 (PG1350), hot-swap |
| **Hot-swap Sockets** | Mill-Max Low Profile |
| **Controller** | Nice!Nano v2 (nRF52840) |
| **Display** | Nice!View (SPI, Memory-in-Pixel) |
| **Connectivity** | Bluetooth 5.0 / USB-C |
| **Battery** | 110mAh LiPo |
| **Split** | Wireless BLE (no TRRS required) |
| **Firmware** | ZMK (this repo) |

### Wired Build (Pro Micro)

| | |
|---|---|
| **Keys** | 32 or 30 (user selectable, no firmware change required) |
| **Layout** | 3×5 column stagger + 2 thumb keys per side |
| **Switches** | Kailh Choc V1 (PG1350), hot-swap |
| **Hot-swap Sockets** | Kailh Choc hotswap sockets |
| **Controller** | Pro Micro (ATmega32U4) |
| **Display** | 128×32 OLED (optional) |
| **Connectivity** | USB-C (TRRS split cable included) |
| **Firmware** | QMK / Vial (see main repo) |

---

## Gallery

<div align="center">

| 32-key config (ZMK) | 30-key config (ZMK) |
|:---:|:---:|
| <img src="docs/images/dinkey_32_30_32_key_config_zmk.png" width="420"/> | <img src="docs/images/dinkey_32_30_30_key_config_zmk.png" width="420"/> |

| ZMK front | No case |
|:---:|:---:|
| <img src="docs/images/dinkey_32_30_zmk_front.png" width="420"/> | <img src="docs/images/dinkey_32_30_32_key_no_case.png" width="420"/> |

| Side profile | Case only |
|:---:|:---:|
| <img src="docs/images/dinkey_32_30_32_key_side.png" width="420"/> | <img src="docs/images/dinkey_32_30_case.png" width="420"/> |

| PCB (back) | Controller detail |
|:---:|:---:|
| <img src="docs/images/dinkey_32_30_naked.png" width="420"/> | <img src="docs/images/dinkey_32_30_no_case_controller.png" width="420"/> |

</div>

---

## Getting Started

### Option 1 — Fork and build (recommended for customization)

1. Fork this repository
2. GitHub Actions will automatically build firmware on every push
3. Go to the **Actions** tab → select the latest run → download the `firmware` artifact
4. Extract the zip — you'll find `.uf2` files for left half and right half

### Option 2 — Download pre-built firmware

Pre-built firmware is available from the [Releases](../../releases) page.

---

## Flashing

1. Double-tap the reset button on your Nice!Nano — it will appear as a USB drive named `NICENANO`
2. Drag and drop the appropriate `.uf2` file onto the drive
3. The drive will disconnect automatically when flashing is complete

Flash the **left** `.uf2` to the left half and the **right** `.uf2` to the right half.

> **First flash or pairing issues?** Flash `settings_reset` to both halves first to clear stale pairing data, then reflash left and right firmware.

---

## Customizing Your Keymap

Edit `config/dinkey_32_30.keymap` to change your layout. After saving, commit and push to trigger a new GitHub Actions build.

Refer to the [ZMK documentation](https://zmk.dev/docs/keymaps) for keymap syntax and available behaviors.

---

## Build Guide

Full assembly instructions are available at [idlebuilds.com/build-guide](https://idlebuilds.com/build-guide).

---

## File Structure

```
zmk-config-dinkey_32_30/
├── build.yaml                            # GitHub Actions build matrix
├── config/
│   ├── dinkey_32_30.keymap               # Keymap definition
│   ├── dinkey_32_30.conf                 # Firmware configuration
│   └── west.yml                          # ZMK dependency manifest
├── boards/shields/dinkey_32_30/
│   ├── Kconfig.defconfig                 # Shield Kconfig defaults
│   ├── Kconfig.shield                    # Shield detection
│   ├── dinkey_32_30.dtsi                 # Matrix transform + kscan base
│   ├── dinkey_32_30-layouts.dtsi         # Physical key layout (ZMK Studio)
│   ├── dinkey_32_30_left.overlay         # Left half pin assignments
│   └── dinkey_32_30_right.overlay        # Right half pin assignments
└── .github/workflows/build.yml           # GitHub Actions workflow
```

---

## Purchasing

The Dinkey 32|30 is available as a kit or complete build from [Idle Builds](https://idlebuilds.com).

| Option | Price |
|---|---|
| Kit — Wired | from $80 |
| Kit — Wireless | from $195 |
| Complete Build — Wired | from $175 |
| Complete Build — Wireless | from $275 |

Prices subject to change due to component availability and tariffs.

---

## Related

- [zmk-config-dinkey_34](https://github.com/IdleBuilds/zmk-config-dinkey_34) — ZMK config for the Dinkey 34
- [Idle Builds Dinkey](https://github.com/IdleBuilds/Dinkey) — Hardware files, QMK, Vial, and build guides
- [ZMK Documentation](https://zmk.dev/docs)
- [Idle Builds](https://idlebuilds.com)

---

## Contact

Questions about the build, firmware, or purchasing? Reach out at [clayton@idlebuilds.com](mailto:clayton@idlebuilds.com)

---

## License

MIT © Idle Builds
