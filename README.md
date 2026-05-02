# dirty_motor_board
DRV8461-based stepper motor driver board for Brain_Board, designed for a 17HS4412B NEMA 17 motor with SPI configuration, STEP/DIR control, VM input protection, and chunky motor-output routing.

DRV8461-based stepper motor driver daughter board for Brain_Board.

Dirty_MTR_Board handles the noisy motor-power side of the system: VM input protection, DRV8461 current-regulated stepper drive, motor output routing, and SPI/STEP-DIR control from Brain_Board.

## Overview

This board is designed for a 17HS4412B two-phase stepper motor rated for 3.9 V and 1.2 A/phase. The motor is not powered directly from 3.9 V. Instead, the DRV8461 is supplied from a higher VM rail and regulates coil current internally.

## Key Specs

| Item | Value |
|---|---|
| Driver | TI DRV8461 |
| Motor | 17HS4412B |
| Motor current | 1.2 A/phase |
| VM input | 5-24 V labeled |
| Control | STEP, DIR, EN, nSLEEP, nFAULT |
| Configuration | SPI |
| VM protection | Fuse + SMBJ26A TVS |
| VM bulk cap | 100 µF / 50 V |
| Board role | Motor driver daughter board for Brain_Board |

## Connectors

### J1 - VM Power Input

| Pin | Signal |
|---:|---|
| 1 | GND |
| 2 | VIN / VM |

### J2 - Motor Control

| Pin | Signal |
|---:|---|
| 1 | GND |
| 2 | +3V3 |
| 3 | EN |
| 4 | nSLEEP |
| 5 | nFAULT |
| 6 | STEP |
| 7 | DIR |
| 8 | DRV_CS |

### J3 - SPI

| Pin | Signal |
|---:|---|
| 1 | GND |
| 2 | +3V3 |
| 3 | SPI_MISO |
| 4 | SPI_MOSI |
| 5 | SPI_SCK |
| 6 | GND |

### M1 - Motor Output

| Pin | Signal |
|---:|---|
| 1 | AOUT2 |
| 2 | BOUT1 |
| 3 | BOUT2 |
| 4 | AOUT1 |

Measured motor coil pairs:

- Coil A: pins 1 and 4
- Coil B: pins 2 and 3

## Design Notes

- VM is fused and protected with an SMBJ26A TVS diode.
- VM bulk capacitance is provided by a 100 µF / 50 V radial electrolytic capacitor.
- nSLEEP has a 100 kΩ pulldown so the driver defaults to sleep.
- VREF includes a 100 nF capacitor to ground and a DNP 0 Ω option to ground.
- The DRV8461 exposed pad is tied to V-GND with thermal vias.
- Motor output traces are routed wide for 1.2 A/phase operation.
