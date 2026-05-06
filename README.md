# ZMK Config — Dinkey 32|30

ZMK firmware configuration for the Dinkey 32|30. Runs on the nice!nano v2 with optional nice!view display.

For wired builds (QMK / Vial), see the [main repo](https://github.com/IdleBuilds/Dinkey).

---

## Hardware

| | |
|---|---|
| **Keys** | 30 or 32 (see PCB note below) |
| **Layout** | 3×5 column stagger + 2 thumb keys per side |
| **MCU** | nice!nano v2 (nRF52840), hotswap socket |
| **Display** | nice!view (SPI, optional, hotswap) |
| **Switches** | Kailh Choc V1 (PG1350), hotswap |
| **Connectivity** | Bluetooth 5.0 / USB-C |
| **Battery** | 110mAh LiPo |
| **Split** | Wireless BLE (no TRRS required) |

### PCB — Modular Pinky Column

The 32|30 has a 4th pinky column that accepts one or two switches with no firmware changes required. Populate both for 32 keys, one for 30. The firmware handles both configurations identically.

---

## Flashing

Each build produces three `.uf2` files:

| File | Purpose |
|---|---|
| `dinkey_32_30_left-...uf2` | Left half |
| `dinkey_32_30_right-...uf2` | Right half |
| `settings_reset-...uf2` | Clears BT pairing data |

Download from the **Actions** tab → latest run → **Artifacts**.

**Steps:**

1. Unzip the artifact
2. Plug in the left half via USB-C
3. Double-tap reset on the nice!nano — it mounts as `NICENANO`
4. Drag `dinkey_32_30_left-...uf2` onto the drive
5. Repeat for the right half

Flash left first. Right connects to left over BLE.

**Pairing issues?** Flash `settings_reset-...uf2` to both halves, then reflash normal firmware.

---

## ZMK Studio

Remap keys in your browser without reflashing.

**Requirements:**
- Left half connected via USB-C
- Chrome or Edge (Chromium-based)
- [studio.zmk.dev](https://studio.zmk.dev)

**Steps:**

1. Plug in the left half
2. The board defaults to BLE output — switch to USB by toggling the output key on Layer 2
3. Open [studio.zmk.dev](https://studio.zmk.dev) and click Connect
4. Select the Dinkey 32|30
5. Press **T + Y** simultaneously to unlock Studio (inner top-row keys, positions 4 and 5 — always present regardless of pinky column config)
6. Remap — changes save to the keyboard automatically

> Reflashing firmware will reset the keymap to the defaults in `config/dinkey_32_30.keymap`.

---

## Default Layout

### 32-key config (both pinky switches populated)

```
┌────┬───┬───┬───┬───┐   ┌───┬───┬───┬───┬───┐
│TAB │ W │ E │ R │ T │   │ Y │ U │ I │ O │ / │
├────┼───┼───┼───┼───┤   ├───┼───┼───┼───┼───┤
│    │ S │ D │ F │ G │   │ H │ J │ K │ L │   │
├────┼───┼───┼───┼───┤   ├───┼───┼───┼───┼───┤
│ A  │ X │ C │ V │ B │   │ N │ M │ , │ . │ P │
└────┴───┴───┼───┼───┘   └───┼───┼───┴───┴───┘
             │BSP│TAB│   │SPC│ENT│
             └───┴───┘   └───┴───┘
```

Tab and A occupy the top and bottom pinky positions on the left. / and P on the right. The home-row pinky position is unused in this layout. This is a base template — the pinky column assignments are the first thing most users will remap.

### 30-key config (one pinky switch per side, home-row position)

```
    ┌───┬───┬───┬───┐       ┌───┬───┬───┬───┐
    │ W │ E │ R │ T │       │ Y │ U │ I │ O │
┌───┼───┼───┼───┼───┤   ├───┼───┼───┼───┼───┐
│ A │ S │ D │ F │ G │   │ H │ J │ K │ L │ P │
└───┼───┼───┼───┼───┘   └───┼───┼───┼───┼───┘
    │ X │ C │ V │ B │       │ N │ M │ , │ . │
    └───┴───┴───┴───┘       └───┴───┴───┴───┘
            ┌───┬───┐   ┌───┬───┐
            │BSP│TAB│   │SPC│ENT│
            └───┴───┘   └───┴───┘
```

The single switch sits in the home-row pinky position. Top and bottom rows are 4 keys wide per side — there is no pinky position in those rows. A anchors the left; P the right. This is a base template — Q, Z, and / are typically accessed via combos or layers.

---

## Customizing the Keymap

Edit `config/dinkey_32_30.keymap`, commit, and push. GitHub Actions will build new firmware automatically.

See the [ZMK keymap docs](https://zmk.dev/docs/keymaps) for syntax and available behaviors.

---

## Building Locally

```bash
west build -s app -b nice_nano/nrf52840/zmk \
  -d build/left \
  -- -DSHIELD="dinkey_32_30_left nice_view_adapter nice_view" \
     -DCONFIG_ZMK_STUDIO=y \
     -DSNIPPET=studio-rpc-usb-uart
```

ZMK Studio is enabled on the left half only. Right half build omits the Studio flags.

---

## Repo Structure

```
config/
  boards/shields/dinkey_32_30/
    dinkey_32_30.dtsi             ← Row/col pin definitions
    dinkey_32_30_left.overlay     ← Left half pin assignments
    dinkey_32_30_right.overlay    ← Right half pin assignments
    dinkey_32_30.zmk.yml
    Kconfig.shield
    Kconfig.defconfig
  dinkey_32_30.keymap             ← Keymap definition
  dinkey_32_30.conf               ← Firmware config (BT, power, etc.)
build.yaml                        ← GitHub Actions build matrix
.github/workflows/build.yml       ← CI workflow
```

---

## Related

- [zmk-config-dinkey_34](https://github.com/IdleBuilds/zmk-config-dinkey_34) — ZMK config for the Dinkey 34
- [IdleBuilds/Dinkey](https://github.com/IdleBuilds/Dinkey) — Hardware files, QMK, Vial
- [idlebuilds.com](https://idlebuilds.com) — builds and kits
- [ZMK docs](https://zmk.dev/docs) · [ZMK Studio](https://studio.zmk.dev)

---

## License

MIT © Idle Builds
