# Buyer Guide

## What This Product Does

Industrial USB to RS485 Adapter provides a USB serial port for an isolated RS485 network. Typical applications include:

- Modbus RTU commissioning and service
- PC-to-PLC communication
- Industrial sensor and meter networks
- Building automation and instrumentation
- Embedded Linux or single-board computer gateways

## What To Confirm Before Ordering

- Host has USB 2.0 support and a suitable USB Type-C data cable.
- Target equipment uses 2-wire half-duplex RS485.
- Target wiring identifies `A` and `B` polarity clearly; vendor naming is not always consistent.
- Bus has only two physical termination points.
- Adapter position in bus is known before selecting termination and bias switches.
- Required baud rate and cable length are within the tested system limits.
- Isolated 5 V output current requirement is compatible with IL0505S capability.
- Enclosure, connector, and mounting requirements match the included mechanical files.

## Included Design Package

- Production Gerber archive
- Eagle schematic and PCB source
- Custom component libraries
- Schematic PDF
- Board dimension PDF
- STEP board model
- STL enclosure models
- Connector pinout and hardware images

## Not Included

- USB cable
- FTDI driver support from this repository
- Modbus software or protocol stack
- RS485 cable or termination accessories
- Regulatory certification
- Guaranteed assembled hardware unless supplied separately by the seller

## Safe Wiring Sequence

1. Power down the connected RS485 system.
2. Verify connector pin numbers against the silkscreen and pinout image.
3. Connect `A` to `A` and `B` to `B`; reverse only after checking equipment documentation.
4. Connect `GNDA` only where the installation requires a reference conductor.
5. Check for shorts and unwanted connection between USB ground and `GNDA`.
6. Connect USB and configure the serial port.
7. Test with low-rate traffic before increasing bus speed.

## Purchase Acceptance Checklist

- USB device enumerates.
- TX, RX, and power indicators operate as expected.
- RS485 transmit and receive operate in both directions.
- USB ground and `GNDA` remain electrically isolated.
- Termination switch produces the specified resistance.
- Bias switch produces the specified idle-bus bias.
- Protection and isolation tests pass the agreed acceptance criteria.
