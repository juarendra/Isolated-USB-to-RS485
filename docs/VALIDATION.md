# Validation Plan

Complete these checks on the exact assembled revision before selling or publishing compliance claims.

## Electrical Checks

- Measure USB-side to isolated-side resistance and insulation resistance.
- Confirm isolated output voltage at minimum and maximum expected USB input.
- Confirm output ripple and converter temperature under load.
- Measure RS485 A-B termination in every switch position.
- Measure bias voltage and current in every switch position.
- Confirm MAX485 `DE` and `/RE` direction timing.
- Confirm no unintended copper, mounting hardware, or shield path bridges the isolation barrier.

## RS485 Protection Characterization

Record measured values against the exact component datasheets and test fixture:

| Measurement | Test condition | Result |
|---|---|---|
| `A` to `GNDA` withstand/clamp | Defined surge or fault waveform | TBD |
| `B` to `GNDA` withstand/clamp | Defined surge or fault waveform | TBD |
| `A` to `B` withstand/clamp | Defined differential waveform | TBD |
| TBU trip current/time | Defined source impedance and pulse | TBD |
| TBU recovery behavior | After pulse and after fault removal | TBD |
| TISP trigger/clamp behavior | Defined pulse and return path | TBD |
| SM712 clamp voltage | Defined current and pulse duration | TBD |
| MAX485 short-circuit duration | A/B shorted under controlled supply | TBD |

Do not enter a voltage or time as a product rating merely because it appears in a component datasheet. The board rating is limited by the complete current path: connector, copper, TBU, TISP, TVS, ground return, MAX485, spacing, and enclosure.

## Functional Checks

- USB enumeration on supported operating systems.
- UART loopback test.
- RS485 transmit and receive test.
- Modbus RTU request/response test.
- Repeated direction changes at the target baud rate.
- Operation with and without termination enabled.
- Operation with representative cable length and node count.

## Protection and Environmental Checks

- Contact and air discharge ESD testing at accessible points.
- EFT testing on USB and RS485 cables.
- Surge testing using the intended installation and return path.
- RS485 short-to-ground and line-to-line fault testing.
- Hot and cold operating tests.
- Long-duration traffic and thermal soak test.

Record test equipment, revision, wiring, pass/fail criteria, and results. Do not use this document as a certification statement.
