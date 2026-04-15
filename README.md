# openmotion-electrical

PCB design files for the [Open-Motion](https://github.com/OpenwaterHealth) near-infrared optical blood flow imaging platform — an open-source system for non-invasive cerebral blood flow measurement using diffuse correlation spectroscopy (DCS).

This repository contains the electrical schematics and manufacturing packages for every printed circuit board in the Open-Motion hardware stack.

## System Architecture

Open-Motion uses a modular sensor architecture with three board types:

```
                    ┌──────────────┐
                    │   Host PC    │
                    │  (USB-C)     │
                    └──────┬───────┘
                           │
                    ┌──────┴───────┐
                    │ Console Board│  ← Power conditioning, laser control,
                    │              │    host PC communication
                    └──┬───────┬───┘
                       │       │
              ┌────────┴──┐ ┌──┴────────┐
              │Aggregator │ │Aggregator │  ← Up to 2 aggregator modules
              │  Board    │ │  Board    │    per console
              └─┬─┬─┬─┬──┘ └──┬─┬─┬─┬──┘
                │ │ │ │        │ │ │ │
               8× Sensor     8× Sensor     ← 8 camera sensor boards
                 Boards        Boards         per aggregator
```

**Console Board** — Houses the power conditioning electronics, laser control electronics, and components for connecting the two aggregator boards to the host PC. Receives 12V from an external power supply and connects to the host via USB Type-C.

**Camera Aggregator Board** — Collects data from up to eight camera sensor boards. Connects to the console board via a 10-pin cable. Up to two aggregator modules may be connected to the console at a time.

**Camera Sensor Board** — Individual near-infrared sensor units. Eight sensor boards connect to a single aggregator board.

## Repository Structure

```
openmotion-electrical/
├── 710-00019-Rev1.zip       # PCB manufacturing package (Gerber, BOM, drill files)
├── 710-00021-Rev1.zip       # PCB manufacturing package
├── 710-00024-Rev1.zip       # PCB manufacturing package
├── 720-00005-Rev1.pdf       # Schematic / electrical documentation
├── 720-00007-Rev1.pdf       # Schematic / electrical documentation
├── 720-00010-Rev1.pdf       # Schematic / electrical documentation
├── LICENSE                  # AGPL-3.0
└── README.md
```

### Part Number Convention

| Prefix | Type | Description |
|--------|------|-------------|
| `710-xxxxx` | Manufacturing package (.zip) | Gerber files, drill files, and BOM for PCB fabrication and assembly |
| `720-xxxxx` | Documentation (.pdf) | Schematics and electrical documentation |

> **Note:** Open-Motion is in active development. Files in this repository represent prototype designs. Updated electrical files are published here when major releases occur.

## File Formats

| File Type | Contents | Software |
|-----------|----------|----------|
| `.zip` (710-series) | Gerber files, drill files, BOM | [Altium](https://www.altium.com/), or any Gerber viewer |
| `.pdf` (720-series) | Circuit schematics and documentation | Any PDF viewer |

## Related Repositories

This repo contains the PCB designs. The rest of the Open-Motion platform lives here:

| Repository | Description |
|------------|-------------|
| [openmotion-mechanical](https://github.com/OpenwaterHealth/openmotion-mechanical) | Mechanical engineering CAD files and enclosure designs |
| [openmotion-console-fw](https://github.com/OpenwaterHealth/openmotion-console-fw) | Console board firmware |
| [openmotion-bloodflow-app](https://github.com/OpenwaterHealth/openmotion-bloodflow-app) | Blood flow imaging application |
| [openmotion-test-app](https://github.com/OpenwaterHealth/openmotion-test-app) | QML-based hardware test application |
| [openmotion-camera-fpga](https://github.com/OpenwaterHealth/openmotion-camera-fpga) | Camera FPGA design files |
| [openmotion-ta-fpga](https://github.com/OpenwaterHealth/openmotion-ta-fpga) | Timing/aggregator FPGA design files |
| [opw_bloodflow_gen2_ai](https://github.com/OpenwaterHealth/opw_bloodflow_gen2_ai) | Deep learning blood flow classification model |

## Getting Started

**To view schematics:** Open the `720-xxxxx` PDF files directly.

**To inspect or fabricate PCBs:** Extract the `710-xxxxx` zip archives and import the Gerber files into [Altium](https://www.altium.com/) (free, open-source) or your preferred EDA tool. Send Gerber and drill files to your PCB fabricator, and reference the included BOM for component sourcing.

**To integrate with mechanical designs:** See the [openmotion-mechanical](https://github.com/OpenwaterHealth/openmotion-mechanical) repository for enclosure CAD files and assembly references.

## Contributing

We welcome contributions from the hardware community. Please read our [Contributing Guide](https://github.com/OpenwaterHealth/.github/blob/main/CONTRIBUTING.md) before submitting changes.

For hardware contributions specifically:

- **Schematic changes** — export updated PDFs alongside source files
- **Manufacturing packages** — follow the existing part-number and revision naming convention (e.g., `710-00024-Rev1`)
- **New board revisions** — increment the revision number and include both the zip manufacturing package and PDF documentation

## License

This project is licensed under the [GNU Affero General Public License v3.0](LICENSE) (AGPL-3.0).

## About Openwater

[Openwater](https://openwater.health) is building open-source platforms to democratize medical imaging and neuromodulation technology — reducing medical device development costs through collaborative, open-source engineering.
