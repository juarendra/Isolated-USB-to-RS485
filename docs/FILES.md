# Repository Map

## Main Folders

| Folder | Contents |
|---|---|
| `CAD-CAM/` | Manufacturing output archives |
| `DOC/` | Buyer-facing images and mechanical documents |
| `PDF/` | Printable schematic documentation |
| `PCB-EAGLE/` | Eagle source files and custom libraries |
| `3D/` | Board, enclosure, and mechanical models |
| `docs/` | Product, hardware, buyer, and validation documentation |

## Production Outputs

Use these files for the current manufacturing package:

| Output | Location |
|---|---|
| Production Eagle board | [`PCB-EAGLE/IndustrialUSBtoModbus_Production.brd`](../PCB-EAGLE/IndustrialUSBtoModbus_Production.brd) |
| Production Gerber/ODB++ archive | [`CAD-CAM/Gerber_Production.zip`](../CAD-CAM/Gerber_Production.zip) |
| Production CAM job | [`CAD-CAM/IndustrialUSBtoModbus v2.cam`](../CAD-CAM/IndustrialUSBtoModbus%20v2.cam) |

The production archive includes copper, solder mask, solder paste, silkscreen, board profile, drill, job, ODB++ data, and front-side pick-and-place output. Confirm the PCB revision and fabrication house rules before ordering.

## Naming Convention

New files should use:

- Uppercase folder names only for legacy design folders.
- Lowercase `docs/` for GitHub documentation.
- Lowercase, hyphen-separated names for new documentation files.
- Descriptive asset names, for example `rs485-adapter-pinout.png`.
- Stable revision suffixes when output changes, for example `gerbers-r02.zip`.

Existing Eagle source names are retained to avoid breaking library links and manufacturing references.

## Legacy Files

Files with names such as `IndustrialUSBtoModbus.b#1` are Eagle backup artifacts. They are retained for traceability but should not be used as the primary source. Use the `.sch` and `.brd` files listed above.
