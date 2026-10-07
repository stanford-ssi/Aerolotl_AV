# aerolotl_av: changes from aerolotl rev2

**Removed (old reference designators):**

- Servo hardware: J18–J21, F7–F10, C77–C84, D10, R66, R67, and the SERVO_UART link.
- SD D1/D2 series resistors R28/R29. The SD card now runs in SPI mode.
- VCAP caps C67/C68.

**MCU:** STM32H723VGTx → STM32G474VETx, same LQFP-100 footprint. See `AV_PINMAP.md`.

**PCB moves (old refs):** The supply and analog pins differ on the G4, so these parts were moved next to their new pins:

- VDD pins 23/24 → C56
- VDD pins 48/49 → C58
- VDD pins 63/64 → C57
- VSSA/VREF+/VDDA pins 35–37 → C65, C66, C69, C70, R65, FB3

**Both boards:**

- Every previously unnamed net now has a label: 33 on AB, 38 on AV.
- GPS decoupling caps C4/C5 got footprints and were placed on the PCB.
- Power netclasses were added.
- Everything was reannotated in sheet order, top-to-bottom and left-to-right within each sheet.
- Non-standard prefixes were normalized: CS/CIO → C, Card/CN → J, LED → D, X → Y, SAW → FL.

## Reference map (old → new)

**mcu**: C24→C1, C55→C2, C56→C3, C57→C4, C58→C5, C59→C6, C60→C7, C75→C8, C69→C9, C70→C10, C76→C11, C65→C12, C66→C13, C73→C14, C74→C15, C71→C16, C72→C17, FB3→FB1, H1→H1, H2→H2, R2→R1, R3→R2, R65→R3, SW2→SW1, SW1→SW2, U14→U1, X1→Y1, Y3→Y2

**swd**: J1→J1, R4→R4

**power**: BT3→BT1, BT4→BT2, BT5→BT3, C39→C18, C31→C19, C34→C20, C37→C21, C38→C22, C41→C23, C2→C24, C1→C25, C3→C26, D9→D1, J4→J2, J3→J3, L3→L1, Q4→Q1, R1→R5, R8→R6, R9→R7, R15→R8, R16→R9, R10→R10, R7→R11, R11→R12, R48→R13, R13→R14, R14→R15, SW4→SW3, TP1→TP1, TP2→TP2, TP3→TP3, TP4→TP4, TP5→TP5, U5→U2, U4→U3, U2→U4, U3→U5

**sensors**: AE1→AE1, C45→C27, CIO2→C28, C48→C29, CS2→C30, C4→C31, C5→C32, CS1→C33, CIO1→C34, C43→C35, C42→C36, SAW2→FL1, R47→R16, R17→R17, R18→R18, U10→U6, U1→U7, U6→U8, U9→U9, U7→U10

**indicators**: BZ1→BZ1, C49→C37, C44→C38, LED1→D2, D2→D3, D3→D4, D4→D5, D6→D6, Q1→Q2, R19→R19, R20→R20, R21→R21, R23→R22, R24→R23, R25→R24, R27→R25, R22→R26

**sd**: Card1→J4, R34→R27, R35→R28, R36→R29, R37→R30, R38→R31, R31→R32, R30→R33, R32→R34, R33→R35

**external**: J17→J5, J10→J6, CN1→J7, CN2→J8, J8→J9, J13→J10, J16→J11, J11→J12, J7→J13

**igniter**: C46→C39, C47→C40, C85→C41, C52→C42, C50→C43, C86→C44, D8→D7, D11→D8, D12→D9, D7→D10, F4→F1, F3→F2, J14→J14, J5→J15, Q5→Q3, Q7→Q4, Q6→Q5, Q8→Q6, R5→R36, R46→R37, R39→R38, R42→R39, R40→R40, R68→R41, R69→R42, R6→R43, R70→R44, R45→R45, R52→R46, R71→R47, R72→R48, R73→R49, R44→R50, R43→R51, TP6→TP6, TP7→TP7, TP8→TP8, TP9→TP9, TP10→TP10

**airlift**: U12→U11


## 2026-10-02 audit (footprints, parts, mechanics)

Full list with datasheet reasons is in `aerolotl_av_BOM.xlsx` (sheets **Changes** and **Open items**). Pre-edit copy: `pre-audit-backup/`.

- **Outline** now matches the lower CamControl PCB in Onshape: 145.29mm dia, TeleMetrum notch at the bottom, two 10mm wire slots. Rods H1/H2 sit at center +/-60mm with 10.32mm holes and washer keepouts. H3 is new: the TeleMetrum sled (2x M4, 17.4mm apart, 50mm below center).
- **Connectors:** J10/J11 are now 2.54mm 1x7 headers. J15 MAIN (top) and J14 DROGUE (bottom, hand-solder) are vertical pluggable 5.08mm headers with screw plugs. J3 is the external battery input on JST PH, bottom side. BT1-BT3 and J13 removed.
- **U11 Airlift** has a real footprint from the Adafruit Eagle files.
- **U1** pins show their configured function (KiCad alternates).
- **Parts:** C9 10n, C16/C17 4.7p with a 6pF LSE crystal (FC-135), C19 10u, C20 22u tantalum (AMS1117), C21 10u/50V 1206, L1 5.6uH FXL0630, C30/C34 1u tantalum (ADXL345/375), U7/U9 on the ADI land pattern, R12 4k99. Every symbol has LCSC Part, MPN and spec fields.
- **Firmware:** set LSEDRV to medium-high for the 6pF crystal.

## 2026-10-06 LoRa radio

- Added U12 Ra-01H (SX1276 915 MHz) on a dedicated SPI4 bus with J16 vertical SMA, C45/C46 decoupling, R52 NSS pull-up and TP11 on DIO0. The J5 SPI4 header is removed. Pin map in `AV_PINMAP.md`.
- RGB resistors: R19 270R, R20 330R, R21 100R (LCSC numbers fixed).
- AE1 GPS patch excluded from the BOM; order it from Mouser.
