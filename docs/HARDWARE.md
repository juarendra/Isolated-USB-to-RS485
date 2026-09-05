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

## USB-C Configuration

The current revision includes USB-C sink pull-down resistors:

```text
CC1 -> R4 = 5.1 kOhm -> GND
CC2 -> R8 = 5.1 kOhm -> GND
```

These resistors identify the board as a USB device/sink to a USB-C host. `SBU1` and `SBU2` remain unused for this USB 2.0 design.

## RS485 Configuration

`S1` is associated with the single 120 ohm termination resistor `R6`. `S2` is associated with the 4.7 kOhm bias network. Confirm switch position and assembled resistance using a meter because termination must not be enabled at every node.

Recommended topology:

- One termination at each physical end of the main cable.
- Bias enabled at one intentional location, unless the system design specifies otherwise.
- Short stub connections.
- Twisted-pair cable with a suitable characteristic impedance.

### Bias Calculation

The schematic uses `R2 = 4.7 kOhm` from `VCC` to `A` and `R5 = 4.7 kOhm` from `B` to `GNDA`, enabled by `S2`.

For the single 120 ohm termination and an ideal 5 V isolated supply:

```text
I_bias = 5 V / (4.7 kOhm + 120 ohm + 4.7 kOhm)
       = approximately 0.525 mA

V(A) - V(B) = I_bias x 120 ohm
            = approximately 63 mV
```

This is lower than the commonly used 200 mV fail-safe design target. It is not automatically wrong because MAX485 and connected nodes contribute their own behavior, but the complete bus must be calculated and measured. Consider lower bias values only after checking total bus loading, driver current, termination count, and idle common-mode voltage.

With `S2` enabled, record:

- `V(A)` relative to `GNDA`.
- `V(B)` relative to `GNDA`.
- `V(A) - V(B)`.
- Bias current.

Enable bias at one intentional location only. Multiple bias networks can overload the bus and alter common-mode voltage.

### Protection and Fault Specification

The following are design targets and component-level references, not guaranteed board ratings. Fill in the final values after testing the assembled PCB and intended cable installation.

| Parameter | Current design reference | Final value/status |
|---|---|---|
| RS485 common-mode operating range | MAX485 and system specification | TBD by system test |
| Maximum A/B continuous voltage | MAX485 absolute maximum and protection coordination | TBD |
| Maximum line-to-`GNDA` voltage | TBU/TISP/TVS coordination | TBD |
| RS485 short-circuit duration | MAX485 thermal/fault test | TBD |
| TVS standoff voltage | SM712-02HTG datasheet | Verify against bus voltage |
| TBU trigger/current rating | TBU-CA065-200-WH datasheet | Verify per revision |
| TISP voltage/surge rating | TISP4240M3BJR-S datasheet | Verify per test waveform |
| SM712 clamp voltage | SM712-02HTG datasheet and test current | Verify at specified current |
| Surge return path | A/B -> protection -> `GNDA` -> installation return | Validate layout and wiring |

Do not convert these component references into an IEC, EMC, or surge claim without a defined test method and a passing test report.

### Protection Pin Review

Verify the exact manufacturer datasheet and package drawing against the Eagle library before assembly:

| Reference | Part | Required verification |
|---|---|---|
| `D4`, `D5` | `TBU-CA065-200-WH` | Current path pin 1 to pin 3, center pad/pin 2 treatment, package and orientation |
| `D1`, `D6` | `TISP4240M3BJR-S` | Pin polarity, line-to-ground connection, surge path, package |
| `D2` | `SM712-02HTG` | `TVS1`, `TVS2`, `COMMON` mapping, bidirectional behavior, package |

Use a pin-to-pin checklist, not symbol appearance alone:

1. Compare manufacturer pinout with Eagle symbol pin names.
2. Compare symbol pins with package pads in the board file.
3. Trace each line from connector to protection device to `MAX485`.
4. Confirm the TVS common pin returns to `GNDA`.
5. Confirm surge current does not cross the USB isolation barrier.
6. Recheck the physical footprint orientation using a populated-board drawing.

For the current Eagle library, the TBU symbol exposes only pins 1 and 3, while the package contains a center pad/pin 2. Do not infer an electrical function for pin 2 from the symbol. Confirm whether the selected manufacturer package defines it as no-connect, thermal pad, or another connection, then update the library and PCB if required.

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
