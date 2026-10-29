# 10BASE-T1S PMOD

10BASE-T1S PMOD is a 3.3 V IEEE 802.3cg 10BASE-T1S transceiver module using a
Microchip LAN8670 in RMII. The host must provide the MAC. The first intended
host is an Arty A7-100T, plugged into JB.

The project is **KiCad 9.0.8**, revision **0.2**, dated 2026-10-26. Open
[kicad/step0.kicad_pro](kicad/step0.kicad_pro). The four-layer, 1.6 mm board is
70 × 20.32 mm with 2 mm corner radii and 48 footprints.

This revision uses an Arty JB direct-plug pinout: CLK50 on pin 1, TXD0 on
pin 10, with separate 33 Ω series resistors on the oscillator outputs to the
PHY and to the FPGA. ERC reports 0 errors and 93 expected open-stub warnings.
DRC with schematic parity reports 0 violations and 0 unconnected items.

## PMOD connections

**J1** is the 12-pin PMOD header for Arty A7 JB. This pinout is specific to
that host.

| PMOD pin | Signal | Function |
| --- | --- | --- |
| 1 | CLK50 | 50 MHz from this module to Arty E15/SRCC |
| 2 | TXD1 | RMII transmit data |
| 3 | TXEN | RMII transmit enable |
| 4 | CRS_DV | RMII carrier / data valid |
| 5 | GND | Ground |
| 6 | 3.3 V | Supply from host |
| 7 | RXD0 | RMII receive data |
| 8 | RXD1 | RMII receive data |
| 9 | RST_N | PHY reset, also pulled up on the module |
| 10 | TXD0 | RMII transmit data |
| 11 | GND | Ground |
| 12 | 3.3 V | Supply from host |

**J2** is the 5.00 mm-pitch cable terminal: pin 1 TRX_P, pin 2 TRX_N.
**J3** is the MDIO header: pin 1 MDC, pin 2 MDIO, pin 3 GND.
**JP1** and **JP2** enable the 100 Ω end-node termination when both shunts are
fitted. Leave both open for a drop node.

The PHY address is 0. PLCA node ID is a register, programmed over MDIO.
MODE[1:0] is 10 (RMII). The oscillator is a Kyocera KC2520Z 50 MHz part,
`KC2520Z50.0000C1KX00`. RBIAS is 12.4 kΩ 1%. The analog chain is PHY TRXP/TRXN,
0 Ω, TDK ACT1210D CMC, 100 nF 100 V, then J2. ESD parts are Panasonic
EZA-EG3W11AV.

## Files in this revision

| Path | Role |
| --- | --- |
| [kicad/step0.kicad_pro](kicad/step0.kicad_pro) | KiCad 9 project |
| [kicad/step0.kicad_sch](kicad/step0.kicad_sch) | Schematic |
| [kicad/step0.kicad_pcb](kicad/step0.kicad_pcb) | Board |
| [kicad/fp-lib-table](kicad/fp-lib-table) | Local footprint table (`${KIPRJMOD}`) |
| [kicad/sym-lib-table](kicad/sym-lib-table) | Local symbol table (`${KIPRJMOD}`) |
| [kicad/libs/step0.kicad_sym](kicad/libs/step0.kicad_sym) | LAN8670 and PMOD symbols |
| [kicad/libs/pmod.kicad_sym](kicad/libs/pmod.kicad_sym) | Upstream PMOD symbols |
| [kicad/libs/pmod-conn_6x2.pretty/](kicad/libs/pmod-conn_6x2.pretty/) | PMOD 6×2 land |
| [kicad/libs/ACT1210.pretty/ACT1210D.kicad_mod](kicad/libs/ACT1210.pretty/ACT1210D.kicad_mod) | TDK ACT1210D land |
| [kicad/output_files/BOM-step0.csv](kicad/output_files/BOM-step0.csv) | BOM, 48 components |
| [kicad/output_files/CPL-step0.csv](kicad/output_files/CPL-step0.csv) | Pick-and-place |
| [kicad/output_files/gerbers/](kicad/output_files/gerbers/) | Gerbers and PTH/NPTH drill |

U2 clock qualification, Arty host timing and physical mating, stackup/DFM,
ferrite land acceptance, and assembler placement preview remain open. Clean
ERC/DRC is not fabrication approval.

The inherited [Lone Dynamics notice](KATZE-LICENSE.md) and
[PMOD library notice](kicad/libs/pmod-LICENSE) accompany this redistribution.
