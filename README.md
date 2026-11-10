# RackPowerDistributionUnit

A smart, rack-mountable power distribution unit (PDU). It distributes 230 VAC and
provides per-outlet power measurement and switching, plus network/USB connectivity
for remote monitoring and control.

The project is split into three sub-repositories (git submodules):

| Directory | Repository | Contents |
|---|---|---|
| [`hw/`](hw/) | [RackPowerDistributionUnit_HW](https://github.com/znibb/RackPowerDistributionUnit_HW) | PCB design (KiCad), changelog, bring-up test procedure, reference documents |
| [`mech/`](mech/) | [RackPowerDistributionUnit_Mech](https://github.com/znibb/RackPowerDistributionUnit_Mech) | Mechanical design (enclosure / rack mounting) |
| [`sw/`](sw/) | [RackPowerDistributionUnit_SW](https://github.com/znibb/RackPowerDistributionUnit_SW) | Firmware (STM32CubeMX project, reference documents) |

## Hardware (`hw/`)
- Single PCB, 16 A / 230 V input via IEC C20 inlet, protected by fuses
- Switched outlet channels, each with a relay (G5Q-1A4-EU, 12 V coil), optocoupler
  isolation (LTV-824S/844S) and current/power sensing (ACS37800). The schematic has two
  `channel` sheets and the firmware config defines 8 channels (Ch1-Ch8); the exact count is
  still to be confirmed
- Trunk (input) monitoring with its own ACS37800 measurement
- Temperature monitoring (TMP1075)
- Power: 12 V in, 3V3 regulator (TPS54331)
- MCU: STM32F407VET6, with 10/100 Ethernet (DP83848I PHY, RMII) and USB-C 2.0
- SWD programming via TagConnect TC2030
- Current release: v1.0.1 (see [`hw/CHANGELOG.md`](hw/CHANGELOG.md)); bring-up steps in
  [`hw/BRINGUP_TEST_PROCEDURE.md`](hw/BRINGUP_TEST_PROCEDURE.md)

> **Warning:** the board carries mains voltage. Follow the safety notes in the bring-up procedure.

## Mechanical (`mech/`)
Enclosure and rack-mount design. Not yet populated.

## Software (`sw/`)
Firmware for the STM32F407 (STM32CubeMX project in `sw/stm32cubemx/`), with peripherals
configured for Ethernet (RMII), USB OTG FS, I2C1/I2C3, SPI3 (master) and USART6.
Early stage: only the CubeMX configuration exists so far.

## Getting started
```bash
git clone --recurse-submodules git@github.com:znibb/RackPowerDistributionUnit.git
```
