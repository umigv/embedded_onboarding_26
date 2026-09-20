# 04. Altium Designer PCB Tutorial & Troubleshooting

- **Quick Links:** [Altium Downloads (Windows)](https://www.altium.com/products/downloads) | [Altium Student License](https://www.altium.com/education/students) | [Altium Getting Started Guide](https://resources.altium.com/p/getting-started-pcb-design) | [JLCPCB Component Search](https://jlcpcb.com/parts/all-electronic-components) | [Embedded Stack PCB Repo](https://github.com/umigv/Embedded_Stack_ROS2/tree/master/PCB_TestProject)
- **Contacts:** Chihyun, Bany, Jared

---

## 1. Introduction to Altium

Altium Designer is the industry-standard EDA software used to design Printed Circuit Boards (PCBs). It integrates schematic capture, 3D PCB layout, component management, and manufacturing output generation.

### Software Download & Setup
- **Windows:** Download installer from [Altium Downloads](https://www.altium.com/products/downloads).
- **macOS:** Altium Designer is Windows-only. macOS users must use [U-M CAEN Remote Desktop / VMware](https://teamdynamix.umich.edu/TDClient/76/Portal/KB/ArticleDet?ID=5309).
- **Student License:** Register for a free renewable 6-month license via [Altium Student Portal](https://www.altium.com/education/students).

### Component Selection Guidelines
- Search the [JLCPCB Catalog](https://jlcpcb.com/parts/all-electronic-components) first to verify part availability and stock.
- Import footprints/symbols directly into Altium or drag downloaded footprint files into your workspace.

### Git Version Control with Altium
Command-line workflow:
```bash
git pull                   # Fetch recent project updates
git checkout -b <branch>   # Create working branch
```
*Note on multi-sheet projects:* Ensure parent schematics update block references to child schematic files properly after pulling.

---

## 2. Project Structure & Document Setup

Create a **Design Project Group** (`File > New > Design Project Group`) containing:
1. **Schematic Library (`.SchLib`):** Custom component symbols.
2. **PCB Library (`.PcbLib`):** Custom component footprints and pin pads.
3. **Schematic Document (`.SchDoc`):** Component placement & logical wiring connections.
4. **PCB Layout Document (`.PcbDoc`):** Physical board outlines, footprint placement, traces, and planes.

---

## 3. Creating Footprints & Schematics

### PCB Footprint Creation (`.PcbLib`)
1. Place pads (`Place > Pad`).
2. Set unique pad numbers matching component pinouts.
3. Edit pad properties (`Radius`, `Hole Size`) in the **Properties** panel (Default pad radius: `30 mil` / `0.762 mm`).

### Schematic Entry (`.SchDoc`)
1. Search and drag components using **Manufacturer Part Search**.
2. Connect pins using **Place Wire** (`Ctrl+W`) and **Place Net Label / Ground**.
3. Assign unique designators (`R1`, `C1`, `U1`).

### Syncing Schematic to PCB
1. Validate Schematic: `Project > Validate PCB Project`.
2. Push to PCB: In `.SchDoc`, click `Design > Update PCB Document <filename>.PcbDoc`.
3. Click `Validate Changes` -> `Execute Changes`.

---

## 4. PCB Routing & Board Rules

- **Traces:** Use `Place > Interactive Routing`. Avoid `<90°` acute turns and overlapping traces.
- **Trace Width:** Recommended default width is `25-30 mils` for general power/signals. Use trace width calculators for high-current tracks.
- **Vias:** Use `Place > Via` to transition between top and bottom copper layers.
- **Copper Pour (Ground Plane):** Switch to Bottom Layer -> `Place > Polygon Pour` -> outline board perimeter.
- **Board Shape:** `View > Board Planning Mode` (`1`) -> `Design > Redefine Board Shape`.
- **Mandatory Branding:** Place ARV Logo on **Top Overlay (Silkscreen)** layer: `Place > Graphics` -> import logo image (uncheck *inverted*).

---

## 5. Manufacturing Documentation (JLCPCB Output)

Generate production files from `.PcbDoc`:
1. **Gerber Files:** `File > Fabrication Outputs > Gerber Files`
   - Units: Inches | Format: 2:5 | Suppress Leading Zeros
   - Plot Layers: `Select Used`
2. **NC Drill Files:** `File > Fabrication Outputs > NC Drill Files`
   - Units: Inches | Suppress Leading Zeros
3. **Pick and Place Files:** `File > Assembly Outputs > Generates pick and place files`
4. Zip all generated output files inside the `Project Outputs` directory for submission.

---

## 6. Keyboard Shortcuts Reference Table

| Category | Shortcut | Function |
| :--- | :--- | :--- |
| **General** | `F1` | Open contextual documentation |
| | `Ctrl+S` / `Ctrl+Alt+S` | Save / Save as revision |
| | `Ctrl+Tab` | Cycle open document tabs |
| **Editing** | `Space` / `Shift+Space` | Rotate component 90° CCW / CW |
| | `Ctrl+W` | Interactive Wire / Routing mode |
| | `Delete` | Delete selected item |
| **View Modes** | `1` / `2` / `3` | Switch Board Planning / 2D / 3D Layout |
| | `L` | Open View Configuration / Layer Settings |
| | `F5` | Toggle Net Color Override |
| **Movement & Grid** | `Arrow Keys` | Move cursor 1 snap unit |
| | `Shift + Arrow Keys` | Move cursor 10 snap units |
| | `Shift+Ctrl+L/R/T/B` | Align Left / Right / Top / Bottom |
| | `Shift+Ctrl+H / V` | Distribute horizontally / vertically |

---

## 7. Starter Projects

1. **Temperature Sensor Board:** Simple analog sensor breakout.
2. **ESP32 Peripheral Board:** Microcontroller host interface board.
3. **2-Channel Relay Board:** High-current switching PCB (Reference: [2-Channel Relay PCB Tutorial](https://www.youtube.com/watch?v=dixfFs9lQa4)).

https://docs.google.com/document/d/1yrIzyZlFPnch-mY-_tWLNksymTi5gc8PwfDM4sK8tzc/edit?usp=sharing
https://docs.google.com/document/d/1x2ErE5xBzpctNxbyjo1b4DQJRqkUs0O5Z7XGj1CZxFg/edit?tab=t.0
