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

## 2026-10-06 1S battery, ERC clean-up, re-annotation

Pre-edit copy: `pre-1S-backup/`. Details and datasheet reasons are in `aerolotl_av_BOM.xlsx` (**Changes**, **Open items**, **Ref map**). The refs below are the new ones.

- **1S pack on J2.** The LMR51430 buck and the AMS1117 LDO are gone. The TPS2116 (U4) now picks USB VBUS first (above 4.3 V) and +VBAT otherwise, and feeds VSYS. A TPS63802 buck-boost (U3, L1 0.47 µH XFL4015, C20 10 µF, C22/C23 22 µF, R13/R14 511k/91k) makes +3V3. New footprint `TI_VSON-HR-10_2x3mm_P0.5mm_DLA0010A` from TI's land pattern.
- **Nets:** +12V → +VBAT, +12V_ARM → +VBAT_ARM.
- **Low-Vgs PMOS:** Q1, Q5, Q6 → DMP2022LSS-13. **D1** → SMBJ5.0A. **R10** → 22k (battery sense). **R41/R43** → 10k, **R49/R50** → 4.7k (igniter). **R26** → 330R (ARM LED).
- **MCU:** STM32G473VET6. PA4 is no-connect.
- **ERC:** every warning and error in ERC.rpt was fixed.
- **Re-annotated** in sheet order, then by X and Y within each sheet. The PCB follows by symbol path.

**Reference map (old → new, renumbered parts only):** C2→C1, C3→C2, C4→C3, C5→C4, C12→C5, C13→C6, C6→C7, C7→C8, C8→C9, C9→C10, C10→C11, C11→C12, C14→C13, C1→C14, C19→C18, C24→C19, C26→C21, C25→C24, C36→C25, C31→C26, C32→C28, C35→C29, C29→C30, C33→C31, C34→C32, C28→C33, C30→C34, C37→C35, C38→C36, C45→C37, C46→C38, C42→C40, C40→C41, C43→C42, C41→C43, D10→D8, D8→D9, D9→D10, J3→J2, J2→J3, J16→J4, J4→J5, J7→J6, J9→J7, J10→J9, J11→J10, J6→J11, J14→J13, J15→J14, Q4→Q3, Q6→Q4, Q3→Q5, Q5→Q6, R3→R1, R1→R2, R2→R3, R6→R5, R7→R6, R5→R7, R13→R8, R14→R9, R15→R10, R10→R11, R11→R15, R17→R16, R18→R17, R16→R18, R26→R19, R19→R20, R20→R21, R21→R22, R22→R23, R23→R24, R24→R25, R25→R26, R52→R27, R33→R28, R32→R29, R34→R30, R35→R31, R27→R32, R28→R33, R29→R34, R30→R35, R31→R36, R40→R37, R51→R38, R50→R40, R37→R41, R38→R42, R45→R43, R46→R44, R36→R45, R43→R46, R41→R47, R47→R48, R42→R49, R48→R50, R44→R51, R49→R52, SW2→SW1, SW1→SW2, TP11→TP6, TP6→TP7, TP7→TP8, TP8→TP9, TP9→TP10, TP10→TP11, U4→U2, U5→U4, U8→U5, U10→U6, U6→U7, U7→U8, U12→U10

New parts: U3, L1, C20, C22, C23, R13, R14. Deleted (old refs): U2, U3, L1, C18, C20, C21, C22, C23, R8, R9.

### 2026-10-06 follow-up

- **J2** is now JST XH (B2B-XH-A, C158012, 3 A/contact with AWG22). Harness: XHP-2 + SXH-001T-P0.6. SW3 is also XH 2-pin, so key or label the two harnesses.
- **C45** 47 µF/10 V X5R 1206 (C96123) added at U11 VIN/GND for the ESP32 transmit spikes.
- **D1 correction:** the SMBJ5.0A only handles ESD and small transients. It starts conducting at 6.4–7.07 V, above the 6 V abs max of U3/U4. An OVP stage is still an open item.
- **E-match (MJG BP Rocket Starter):** 1.0 ± 0.2 Ω, all-fire 0.60 A, recommended ≥ 0.75 A, nominal 1.0 A, max test current 40 mA.
- **Igniter current limit:** each channel now has 2 × 1 Ω Bourns CRM2512 resistors (C840604, 2 W, 2512) in series: R45 + R47 on drogue, R46 + R48 on main. They sit between the PMOS drain (IGNx_HS, where continuity and fire sense are measured) and the terminal (IGNx_OUT). The firing current is about 0.86 A at 3.0 V and 1.27 A at 4.2 V. A shorted output puts about 3.4 W in each resistor; the Bourns pulse curve allows about 6 W for 1 s. **Keep the firmware fire pulse at 1 s or less.**
- **Second re-annotation:** igniter refs shifted to keep the order. Old R45–R52 are now R49–R56. On the power sheet, C19 and C20 swapped, because you moved the TPS63802 input cap in KiCad. The BOM "Ref map" sheet shows the full old → new list.
- **RADIO_ANT is now in the RF net class.** I added the pattern `*RADIO_ANT*` to `.kicad_pro`, next to `*GPS_RF*`. That gives it a 0.306 mm width, 0.2032 mm clearance, and the existing DRC rule "RF CPWG: 8 mil gap to ground pour". Before this it was in the Default class (0.2 mm). I also added a note on the lora sheet.

## 2026-10-07 connectors, grommet holes, KiCad library footprints

Pre-edit copy: `pre-connector-swap-backup/`. Footprint swaps are applied with **Update PCB from Schematic (F8)**.

- **J13/J14** → `TerminalBlock_Kangnex_WJ128V-5.0-2P_C8269` (LCSC C8269, 5.00mm pitch, LCSC 3D mesh). Courtyard tightened to body + 0.5mm.
- **J2** → AMASS XT30UPB-M vertical male (C428721), `Connector_AMASS:AMASS_XT30UPB-M_1x02_P5.0mm_Vertical`. Battery lead uses XT30U-F.
- **H1/H2** → `MountingHole_3-8in_Grommet_Heyco_G1123_D14.3mm`: 14.3mm NPTH for the Heyco G1123 grommet, 20.1mm keepout (19.1mm flange + 0.5mm).
- **KiCad library footprints/models** (LCSC/MPN unchanged): Q1/Q5/Q6 `Package_SO:SOIC-8_3.9x4.9mm_P1.27mm`, D1 `Diode_SMD:D_SMB`, D3–D6 `LED_SMD:LED_0805_2012Metric`, F1/F2 `Fuse:Fuse_1812_4532Metric`, Y1 `Crystal:Crystal_SMD_3225-4Pin_3.2x2.5mm`.
- Q1/Q5/Q6 PCB orientation pre-rotated +90° (the pads are unchanged) because the EasyEDA SOIC-8 frame is 90° off from KiCad's.
- 17-21SUYC_TR8 LED symbol: K is now pin 1 and A is pin 2, to match KiCad's LED pad 1 = cathode. Wiring and nets are unchanged.
- J3 USB-C stays on the KiCad HRO TYPE-C-31-M-12 footprint with a custom STEP, because KiCad ships no model for it. J5 stays TF-102-15 (custom).

## 2026-10-07 courtyards + floorplan pass

Pre-edit copy: `pre-floorplan-backup/`. Picture: `floorplan_before_after.png`. Board diameter unchanged (145.29 mm / 5.72 in).

- **Courtyards** (library + PCB): J5 TF-102-15 now covers the whole socket body (old: none), StemmaQT J6/J7/J8, FL1, U6 BMP581 got courtyards, D2 enlarged to its 3D body. SD resistors R28–R36 were under the J5 body; moved 3.2 mm back.
- **LoRa**: U10 Ra-01H + J4 SMA moved to the right edge below H2 (ANT pin 1 faces J4, ~6 mm RF run), with C37/C38/R27/TP6. ~90 mm from GPS, ~70 mm from Airlift, ~85 mm from the buck-boost.
- **Battery input** (J2, Q1, D1, R8, TP1, TP2, TP5) moved as a block into the old LoRa spot. In2 +VBAT plane is now the rectangle (166,79)–(197.5,103.5) around that block; the rest of In2 is +3V3 (incl. under the LoRa).
- **Buck-boost** (U3, L1, C19, C22, C23, R13, R14) moved 12 mm left, away from the IMUs; **power mux** (U4, C20, C24, R11, R12, R15) moved out of the igniter area next to it.
- **Igniters**: bottom band is now igniter-only. J13 (bottom side) moved from beside the USB into the left lobe next to CH0 (tangent to the edge, like J14). F2 moved to clear J14's courtyard.
- **USB-C J3**: turned 180° so the opening faces outward (pad row was facing the edge) and moved out so the shell front is 0.1 mm inside the board edge, radial.
- Small fixes: TP3 out of the H1 keepout, R4 out of J1's courtyard, R8/R56/SW1 nudged off neighbours. 12 GND stitching vias that hit other-net pads were removed. Zone fills cleared — press **B** in KiCad to refill.

## 2026-10-08 test points, BOOT switch, 3D models, silkscreen, stitching vias

Pre-edit copy: `pre-silk-backup/`. Datasheets used: `libs/C126888_DSWB01LHGET.pdf`, `libs/C428721_XT30UPB-M.pdf`, `libs/C172771_KOA_RCTCTE.pdf`.

- **TP1–TP11** → KOA RCTCTE checker chip (C172771), new footprint `aerolotl_custom:TestPoint_KOA_RCTCTE_2.0x1.25mm` (0805 land, both pads = pin 1, 4.0×3.0 mm courtyard for hook access) + STEP model. LCSC/MPN/Manufacturer fields added in the schematic.
- **SW2 BOOT** → Kingtek DSWB01LHGET 1-pos slide DIP switch (C126888), THT, 7.62 mm pin spacing, Ø1.0 mm holes per datasheet. New footprint `aerolotl_custom:SW_DIP_SPSTx01_Kingtek_DSWB01LHGET_W7.62mm` + STEP. Same SPST topology (BOOT0 ↔ +3V3, R3 pull-down): ON = system bootloader, OFF = flash.
- **3D models** (generated from datasheet dimensions, `libs/aerolotl_custom.3dshapes/`): `AMASS_XT30UPB-M.step` (J2), `KOA_RCTCTE_2.0x1.25x1.45mm.step`, `Kingtek_DSWB01LHGET.step`. F1/F2 now use `F1812_L4.5-W3.2-H1.0.step`.
- **Silkscreen**: hid part-number values (U5–U9), moved 50+ reference designators off pads/other silk/edges, deleted the stale "DROGUE (J14 on bottom)" text, shortened "MAIN (CH1)"/"DROGUE (CH0)" (dropped +/-; e-matches are non-polar) and moved them clear, removed J3 silk crossing the board edge. R5, C27, SW2 nudged ≤0.25 mm.
- **Stitching vias**: 56 of the GND vias deleted during re-placement restored where they clear pads (≥0.25 mm), courtyards, keepouts and other vias.

## 2026-10-08 autorouting pass

Pre-route copy: `pre-route-backup/` (PCB, DRU, PRO). Overview: `routing_overview.png`.

- SW2: silkscreen "ON" + arrow beside the switch (slide toward the arrow = BOOT0 high / bootloader). Fit the switch so its printed "ON" matches.
- Test points: `duplicate_pad_numbers_are_jumpers yes`, so the two RCTCTE pads count as one connection.
- Routed with a custom grid router: 950 tracks (614 F.Cu, 290 B.Cu, 46 In2.Cu) and 290 vias (63 GND + 35 +3V3 plane fan-outs, 192 signal). Signals 0.2 mm; +BATT/+VBAT/+VBAT_ARM/IGN0_RTN 2.0 mm where it fits (1.0 mm on some +VBAT / IGN0_HS runs); VSYS 0.5 mm with one 0.2 mm section to widen. Checked against netclass clearances, PWR_HI 0.3 mm, 0.3 mm edge, keepouts, hole-to-hole: 0 violations.
- DRU: U1 courtyard now uses the same 0.15 mm fine-pitch clearance as J3/U2/U3/U4 (109 spots rely on it). Those rules now match when *either* item touches the courtyard.
- Still open: /External/GPIO.PE9, /Igniter/SENSE_I1, /Indicators/LED.G, /MCU/SDSPI.SCK, /MCU/SPI1.INT_BMP, /Sensors/M10S.TX; 7 GND + 3 +3V3 pads without a plane via (most may connect through the F.Cu GND pour after refill).
- Zone fills are empty: press B in KiCad.

## 2026-10-08 DRC.rpt clean-up (213 items)

Pre-edit copy: `pre-drcfix-backup/`.

**Real copper errors, fixed:**
- +3V3 staircase too close to SPI1.INT_IMU_ACC, +VBAT_ARM 0.2986 mm from Q5 gate, M10S.RX crossing a J1 locating-peg hole, and VSYS vs U3.9: all rerouted. The router and checker now use exact round-end geometry and include NPTH holes.
- Removed a 0.026 mm dangling +3V3 stub. Added a C4.2 → U1.48 GND link and a via for R35.1 +3V3.
- Test points: each RCTCTE now has a short track joining its two pads, so DRC sees one connection.
- One extra GND stitching via in an isolated F.Cu pour island.
- Starved thermals: J3 A1/A12/B1/B12, U1.48/63/99, U7.4 and C4.2 set to solid zone connection.
- Rewrote track coordinates at full precision (no rounding of your own routing).

**False positives, resolved at the source:**
- Keepouts: H1/H2/H3 and the Airlift antenna keepout now allow pads, so the parts' own NPTH holes no longer trip them (tracks, vias and pours are still blocked). Library footprints updated too.
- J1 Samtec pegs: DRU rule allows 0.15 mm hole clearance inside J1 only (manufacturer land pattern).
- Field mismatches: synced all schematic fields onto the PCB footprints, and the SW2 LCSC number is now C126888. TP symbols set to *in BOM*, since they're real parts now.
- Lib mismatches for custom parts: re-exported every aerolotl_custom footprint from the board. J2, J3, F1/F2 and U5 (custom 3D models) moved into aerolotl_custom so a library update can't strip their models.
- Text: 27 labels 0.7 → 0.8 mm with 0.15 mm stroke, and the project minimum text height is now 0.8 mm (JLC prints 0.8). The H3 bottom-side text is mirrored.
- Silkscreen: about 60 reference/value labels re-placed with ≥0.19 mm clearance. The ON arrow moved 0.7 mm right, the DROGUE label moved off the J13 outline, and three U11 pin labels were nudged.

**Still for you:** route GPIO.PE9, SENSE_I1, LED.G, SDSPI.SCK, SPI1.INT_BMP and M10S.TX; GND on U6.3; +3V3 between U7.11 and C30.1. Then run Tools → Update Footprints from Library for the KiCad-library parts. Zone fills are cleared: press B, then run DRC.
