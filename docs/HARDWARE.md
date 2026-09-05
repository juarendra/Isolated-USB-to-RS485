# Hardware Reference

## Signal Path

```text
USB Type-C
  |
  +-- FT231XS-R USB-to-UART
          |
          +-- TXD / RXD / TXEN
                  |
                  +-- ADuM1201ARZ digital isolation
                          |
                          +-- MAX485CSA+ half-duplex transceiver
                                  |
                                  +-- protected A/B connector
```

## Power Domains

| Domain | Nets | Purpose |
|---|---|---|
| USB side | `+5V`, `GND`, `+3V3` | USB connector and FT231XS |
| Isolated bus side | `VCC`, `GNDA` | MAX485, RS485 connector, protection |

`IL0505S` transfers power across the isolation barrier. The two ADuM1201 devices transfer data and direction control without a galvanic signal connection.

## RS485 Configuration

`S1` is associated with the 120 ohm termination network. `S2` is associated with the 4.7 kOhm bias network. Confirm switch position and assembled resistance using a meter because termination must not be enabled at every node.

Recommended topology:

- One termination at each physical end of the main cable.
- Bias enabled at one intentional location, unless the system design specifies otherwise.
- Short stub connections.
- Twisted-pair cable with a suitable characteristic impedance.

## Protection Devices

- `SM712-02HTG`: RS485 line transient suppressor.
- `TBU-CA065-200-WH`: series fault-current limiting devices.
- `TISP4240M3BJR-S`: surge protection devices.
- `0ZCJ0010FF2E`: resettable USB input protection.

Protection performance depends on layout, grounding, surge return path, component tolerances, and installation wiring. Component presence is not equivalent to a compliance rating.

## Indicators

- `LED1`: local power indication.
- `LED3`: FTDI CBUS1 indication, intended for receive activity.
- `LED4`: FTDI CBUS2 indication, intended for transmit activity.

Exact LED behavior depends on FTDI CBUS configuration programmed into the device.
