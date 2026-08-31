# Infineon "FAQs: XENSIV MEMS microphone flex kit" — captured 2026-08-29

Source: https://community.infineon.com/t5/Knowledge-Base-Articles/FAQs-XENSIV-MEMS-microphone-flex-kit/ta-p/1035567
(Infineon states no schematic/drawing of the flex kit is published.)

## Facts read from the article and photos

- Flex board: 25 mm x 4.5 mm. The tail has **8 contact fingers at 0.5 mm pitch across the full 4.5 mm width**
  (fig2, fig4). A 4.5 mm tail needs an **8-circuit** 0.5 mm ZIF (Molex 52745 series: FPC width = 0.5*(N+1) mm ->
  6 ckt = 3.5 mm, 8 ckt = 4.5 mm). The 6-circuit 52745-0697 on EN_Probe_VR_2 (J5) cannot accept it.
- Adapter board (fig2 right): ZIF with 8 contacts; the six header pins are labelled **8 6 5 4 3 1** = the ZIF
  circuit numbers brought out (2 and 7 not brought out). These are the numbers used in the brief v02 table and on
  the slideshow (slides 2/3/10).
- Analog flex pads on the mic face (fig4): V (VDD), P (OUT+), N (OUT-), G (GND).

## Table 1 — flex pad labels
| Digital pad | Digital | Analog pad | Analog |
|---|---|---|---|
| V | VDD | V | VDD |
| D | PDM data | P | OUT+ (OUT for single-ended) |
| C | PDM clock | N | OUT- |
| S | Select | – | not used (single-ended) |
| G | GND | G | GND |

## Table 3 — 6-pin adapter (ZIF circuit numbering)
| Pin | Digital | Analog |
|---|---|---|
| 1 | Not used | Not used |
| 3 | L/R select | Not used |
| 4 | Clock | OUT- |
| 5 | Data | OUT+ |
| 6 | VDD | VDD |
| 8 | VDD2 | Not used |
| Back side | GND | GND |

## Table 2 — 4-pin adapter (adapter header, NOT the flex)
1 VDD, 2 Data/OUT+, 3 Clock/OUT-, 4 Select/GND, back side GND.

## Resolution (superseded the first reading below)

Deeper analysis of the adapter board's copper (its 2nd-from-each-end ZIF tails hook into vias to the
adapter's back ground plane, with matching stitching vias on the flex neck) established:

- **GND is on fingers 2 and 7** — exactly the two positions the adapter table omits (it lists 1,3,4,5,6,8).
  "Back side GND" refers to the adapter board's back, not the flex tail (whose back is bare stiffener).
- An earlier reading of fig4's fourth trace as "GND on finger 3" was **refuted**; finger 3 is the digital
  select (unused on the analog flex) and finger 8 is VDD2 (dual-supply mics only) — both left unconnected.
- The board (J5) is wired accordingly: 2/7 = GND, 4 = OUT-, 5 = OUT+, 6 = VDD, 1/3/8 NC.

Remaining check before fabrication: the finger-numbering **direction** (which tail end is contact 1) is
inferred, not measured. Verify on a physical flex with a continuity meter: V pad <-> finger 6,
P <-> 5, N <-> 4, G <-> fingers 2 AND 7, with 1/3/8 floating. A failure means the map is mirrored and
J5's pad nets must be re-assigned before ordering boards.
