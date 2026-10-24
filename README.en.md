# ChisFlash 1.0V Virtual-FRAM Instant-Save Cartridge

This is a modified GBA cartridge based on the ChisFlash virtual-FRAM design. It uses parallel NOR Flash for game storage and provides power-off save persistence through the virtual-FRAM workflow. With an external **4M SRAM** installed, it can also provide fast RTS (real-time save) caching for games using the matching patch.

## Features

- **32MB NOR Flash**, using `S29GL256S10TFI010`.
- Works as a normal virtual-FRAM cartridge without the external 4M SRAM.
- External 4M SRAM enables RTS fast-save caching.
- With Ausar's RTS and cheat patch, games can open an in-game pause menu for real-time saves and cheat functions.
- Improves the screen-corruption issue seen in some games on ordinary virtual-FRAM cartridges using `S29GL256S`.
- Firmware can be programmed through SWD with DAPLink or with a dedicated AG32 programmer.

## Firmware

This repository currently contains compiled firmware binaries only; firmware source is not included yet:

| File | Description |
|---|---|
| [`ChisFlash-1.0V-Virtual-Iron-4M+1M-External-SRAM-RTS.bin`](firmware/ChisFlash-1.0V-Virtual-Iron-4M+1M-External-SRAM-RTS.bin) | External SRAM + RTS build |
| [`ChisFlash-1.0V-Virtual-Iron-4M+1M-No-External-SRAM.bin`](firmware/ChisFlash-1.0V-Virtual-Iron-4M+1M-No-External-SRAM.bin) | Build without external SRAM |

Verify the hardware assembly and firmware choice before programming. Do not mix firmware variants.

## Using RTS

1. Assemble the cartridge according to the selected SRAM configuration.
2. Program the matching firmware.
3. Apply the [GBA RTS + cheat patch](https://archeychen.github.io/GBA-RTS-PATCH-WEB/) to the ROMs that need RTS.
4. Program the patched ROM with a compatible GBA cartridge programmer.
5. Use the patch's key combination in-game to open the pause menu and perform a real-time save or cheat operation.

Without external SRAM, use the no-external-SRAM firmware and operate it as a normal virtual-FRAM cartridge.

## Project layout

```text
ChisFlash-1.0V-main/
├── firmware/       Compiled firmware binaries
├── hardware/
│   ├── pcb/        ProDoc PCB project
│   └── gerber/     Gerber production files
├── images/         PCB preview image
└── README.md
```

## BOM summary

| Part | Quantity | Notes |
|---|---:|---|
| `S29GL256S10TFI010` | 1 | 32MB NOR Flash |
| `100nF` | 4 | Decoupling capacitors |
| `NCD0603B1` | 1 | LED |
| `NCD0603G1` | 1 | LED |
| `1kΩ` | 1 | Resistor |

See [`hardware/gerber/`](hardware/gerber/) for production files and [`hardware/pcb/`](hardware/pcb/) for the PCB project. Verify the components, footprints, layers and assembly conditions before ordering.

## Changelog

- **2025-10-22**: Updated the base firmware for normal virtual-FRAM use; external 4M SRAM support was not yet implemented.
- **2026-04-28**: Updated the instant-save firmware with support for Ausar's latest RTS + cheat patch, including the in-game pause menu for real-time saves and cheats.

## Credits

Thanks to **mori** for the PCB and firmware development, **Ausar** for the RTS patch, and the ChisFlash community members who tested the project and provided feedback.

The project page lists **GPL-3.0**. Commercial use, sales and redistribution must also follow the author's notes on the original project page. Verify the circuit and hardware compatibility before making a copy.
