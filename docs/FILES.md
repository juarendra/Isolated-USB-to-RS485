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
