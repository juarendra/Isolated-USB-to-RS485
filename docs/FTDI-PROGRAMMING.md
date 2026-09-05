# FTDI Production Programming

The schematic assigns FTDI CBUS pins to RS485 direction control and activity indicators. These functions are configured in FTDI EEPROM; they are not guaranteed by PCB wiring alone.

## Required Profile

Program and record one approved profile for every production batch.

| EEPROM field | Required value |
|---|---|
| VID | Use an owned/licensed VID; do not copy another vendor's VID |
| PID | Approved product PID paired with the VID |
| Manufacturer string | Product owner approved text |
| Product description | `Industrial USB to RS485` or approved text |
| Serial number | Unique per device, or explicitly disabled by policy |
| VCP driver | Enabled if the product is used as a virtual COM port |
| CBUS0 | `TXDEN` / RS485 transmit-enable function, if supported by the exact FT231XS configuration tool |
| CBUS1 | `RXLED#` activity indication |
| CBUS2 | `TXLED#` activity indication |
| Inversion | Disabled unless validated by logic measurement |

## Important Direction-Control Clarification

The schematic net `TXEN_` connects FTDI `CBUS0` through `R33` to one ADuM1201 channel. The isolated output of that channel drives MAX485 `DE` and `/RE` together.

The exact CBUS0 function must produce the required timing and polarity for half-duplex RS485. Use the FTDI transmit-data-enable function, commonly shown as `TXDEN`, when available. Do not use `TXLED#` for direction control. Validate with an oscilloscope:

- `TXD` activity.
- `TXEN_` on the USB side.
- Isolated direction signal.
- MAX485 `DE`.
- MAX485 `/RE`.
- RS485 A/B driver activity.

If CBUS0 is used as a direction-control output, select the correct FTDI mode supported by the exact FT231XS revision and validate driver turn-around timing. Keep LED functions on CBUS1/CBUS2 only if the programmed modes match the schematic intent.

### Important FTDI Clarification

`TXDEN` is a hardware transmit-enable indication generated from USB-UART transmit activity. It is not the same signal as `TXD`, and it must remain asserted long enough for the complete outgoing UART character stream. Check the exact FTDI FT231X datasheet and FT_PROG option list for the installed device revision before freezing the EEPROM profile.

The schematic currently routes `CBUS0` through `R33` and an ADuM1201 channel to both MAX485 `DE` and `/RE`. That is an intentional half-duplex arrangement: transmit mode enables the driver and disables the receiver. Confirm that the inactive state is safe during USB attach, reset, suspend, and disconnect. A temporary incorrect state can cause bus contention.

### Recommended Production Record

Store the following with each hardware revision:

- FTDI part marking and silicon revision.
- FT_PROG version.
- EEPROM profile file or captured settings.
- VID/PID ownership record.
- Product and manufacturer strings.
- Serial-number allocation range.
- CBUS0/1/2 settings and polarity.
- Oscilloscope capture showing UART, `TXEN_`, `DE`, `/RE`, and A/B.

## Production Procedure

1. Connect the board to a controlled USB host or FTDI programming fixture.
2. Read and save the original EEPROM configuration.
3. Program the approved VID, PID, strings, serial policy, VCP setting, CBUS functions, and inversion settings.
4. Power-cycle the board.
5. Confirm USB enumeration and descriptor values.
6. Confirm COM-port creation.
7. Verify TX/RX indicators.
8. Verify RS485 direction timing and loopback communication.
9. Save the programmed profile and device serial number in the production record.

Never use an unlicensed VID/PID or ship devices with an untracked serial-number policy.
