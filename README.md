# ⚡ Star-Delta Dual-Motor Control Cabinet – EPLAN Electric P8 & Pro Panel

## 👤 Author
**Samidou-Automation** *Future Automation Engineer | Electrical Systems Designer*

---

## 📌 Project Overview
This repository showcases a complete industrial-grade **Dual-Motor Star-Delta (Wye-Delta) Starter Control Cabinet** engineered entirely within the **EPLAN** software suite. The design features a highly symmetrical power and control architecture driving two independent **2.2 kW (5A)** induction motors. 

The project delivers an advanced industrial engineering package, blending standard-compliant 2D schematic design with a fully routed 3D digital twin enclosure layout. All hardware selections strictly adhere to international engineering standards, notably **IEC 60204-1** (safety of electrical machinery) and **ISA 5.1** (instrumentation identification).

---

## 💡 Introduction to Star-Delta Starting

An induction motor draws a massive transient current during its initial startup phase—typically **4 to 8 times** its nominal running current. Directly starting high-power or high-inertia industrial loads can strain the local power grid, trigger safety devices, and introduce heavy mechanical wear on power transmissions.

The **Star-Delta starting method** resolves this electromechanical constraint by reducing winding stresses during the initial acceleration phase.

### ⚙️ How It Works
1. **Star Configuration:** Upon a start command, the system engages the Main line contactor and the Star contactor simultaneously. This forces the three-phase motor windings into a star (Y) pattern. Each winding receives only $1/\sqrt{3}$ ($\approx 58\%$) of the full line voltage, effectively cutting the starting current down to **one-third ($33\%$)** of a Direct-On-Line (DOL) start.
2. **Transition Delay:** A precision timer tracks the motor's speed ramp-up. Once the motor approaches roughly $80\%$ of its nominal operational speed, the timer opens the Star contactor.
3. **Delta Configuration:** After a brief millisecond safety gap (to prevent phase-to-phase shorts), the Delta contactor closes. The windings lock into a parallel loop ($\Delta$), receiving the full $400\text{V}$ line voltage for standard, full-torque running operation.

---

## 🛠️ Bill of Materials (BOM) & Engineering Function

The cabinet layout is meticulously partitioned using premium industrial hardware from **Schneider Electric (SE)**, **Siemens (SIE)**, **Rittal (RIT)**, and **Phoenix Contact (PXC)**:

| Device Tag | Commercial Reference | Component Type | Project Function & Application Details |
| :--- | :--- | :--- | :--- |
| **Enclosure** | `RIT.1060000` | AX Compact Cabinet | Premium sheet steel wall-mounted enclosure ($600 \times 600 \times 210\text{ mm}$). Offers IP66 protection, a zinc-plated mounting plate, and a high-durability powder-coated finish. |
| **Ducts** | `RIT.8800750` | Cable Wire Ducts | High-capacity slotted PVC wire ducts ($60 \times 80 \text{ mm}$). Provides physical protection, segregation, and clean structural routing channels. |
| **DIN Rails** | `RIT.2313150` | TS 35/15 Mounting Rails | Heavy-duty zingué slotted steel DIN rails ($35 \times 15 \text{ mm}$). Serves as the high-strength physical backbone to support all modular protection and switching gear. |
| **-F2** | `SE.18633` | Main Circuit Breaker | Acti9 iC60N 4-Pole 16A Miniature Circuit Breaker (MCB). Provides global thermal-magnetic protection and main cabinet isolation. |
| **-F3** | `SE.GV2ME10` | Motor Breaker (M1) | TeSys GV2 manual motor starter with an adjustable range of **4A to 6.3A**. Set precisely to **5A** to provide thermal-magnetic overload protection for Motor 1. |
| **-F4** | `SE.GV2ME10` | Motor Breaker (M2) | TeSys GV2 manual motor starter set to **5A** dedicated to the short-circuit and overload protection of Motor 2. |
| **-F5** | `SE.A9N15650` | Fuse Protection (M1) | Acti9 STI isolatable fuse carrier protecting the 230V AC control logic line dedicated to Motor 1. |
| **-F6** | `SE.A9N15650` | Fuse Protection (M2) | Acti9 STI isolatable fuse carrier protecting the 230V AC control logic line dedicated to Motor 2. |
| **-Q1** | `SE.LC1D09P7` | Main Contactor (M1) | TeSys D 9A (AC-3) contactor with a **230V AC coil**. Energizes the main line input of Motor 1. |
| **-Q2** | `SE.LC1D09P7` | Star Contactor (M1) | TeSys D 9A contactor. Short-circuits the secondary winding nodes of Motor 1 during startup. |
| **-Q3** | `SE.LC1D09P7` | Delta Contactor (M1) | TeSys D 9A contactor. Applies full running voltage across Motor 1 windings after transition. |
| **-T1** | `SE.RE22R1AMR` | Timer Relay (M1) | Zelio timing relay controlling the exact transition delay from Star to Delta configuration for Motor 1. |
| **-Q4** | `SE.LC1D09P7` | Main Contactor (M2) | TeSys D 9A contactor handling the primary line input for Motor 2. |
| **-Q5** | `SE.LC1D09P7` | Star Contactor (M2) | TeSys D 9A contactor executing the star configuration bridge for Motor 2. |
| **-Q6** | `SE.LC1D09P7` | Delta Contactor (M2) | TeSys D 9A contactor executing the parallel run loop for Motor 2. |
| **-T2** | `SE.RE22R1AMR` | Timer Relay (M2) | Zelio timing relay controlling the exact transition delay from Star to Delta configuration for Motor 2. |
| **-S1 / -S2** | `SE.XB4BA42` | Pushbuttons (M1) | Harmony XB4 heavy-duty metal 22mm pilot devices. **-S1 (Green, NO)** for Start; **-S2 (Red, NC)** for Stop. |
| **-S4 / -S3** | `SE.XB4BA42` | Pushbuttons (M2) | Harmony XB4 heavy-duty metal 22mm pilot devices. **-S4 (Green, NO)** for Start; **-S3 (Red, NC)** for Stop. |
| **-P2 / -P3** | `SIE.3SU1106-6AA40-1AA0` | LED Indicators (M1) | Siemens SIRIUS ACT 22mm indicators. **-P2 (Green)** indicates Motor 1 is ON; **-P3 (Red)** indicates Motor 1 is OFF/Tripped. |
| **-P4 / -P5** | `SIE.3SU1106-6AA40-1AA0` | LED Indicators (M2) | Siemens SIRIUS ACT 22mm indicators. **-P4 (Green)** indicates Motor 2 is ON; **-P5 (Red)** indicates Motor 2 is OFF/Tripped. |
| **-HLO1** | `SIE.3SU1106-6AA40-1AA0` | Control Light (M1) | White LED Indicator showing that the 230V AC control circuit for Motor 1 loop is fully under tension. |
| **-HLO2** | `SIE.3SU1106-6AA40-1AA0` | Control Light (M2) | White LED Indicator showing that the 230V AC control circuit for Motor 2 loop is fully under tension. |
| **-X1 / -X2** | `PXC.3211813` | Terminal Blocks (M1) | PT 4 series feed-through push-in blocks Gray. **-X1** routes Star signals; **-X2** routes Delta lines to Motor 1. |
| **-X3 / -X4** | `PXC.3211813` | Terminal Blocks (M2) | PT 4 series feed-through push-in blocks Gray. **-X3** routes Star signals; **-X4** routes Delta lines to Motor 2. |
| **-X5:1-3** | `PXC.3211813` | Main Phase Input | PT 4 series feed-through terminal blocks Gray dedicated to incoming Three-Phase power lines (L1, L2, L3). |
| **-X5:4** | `PXC.3211819` | Main Neutral Input | PT 4 series feed-through terminal block **Blue** dedicated to the incoming Neutral (N) line. |
| **-X6PEPE** | `PXC.3211822` | Main Ground (PE) | PT 4-PE series ground block **Green/Yellow** with automatic DIN rail grounding feet for the incoming main source PE. |
| **-X7PEM1** | `PXC.3211822` | Ground (PE M1) | PT 4-PE series ground block **Green/Yellow** dedicated to the field cable protective earth of Motor 1. |
| **-X8PEM2** | `PXC.3211822` | Ground (PE M2) | PT 4-PE series ground block **Green/Yellow** dedicated to the field cable protective earth of Motor 2. |

---

## 🔌 Smart Routing & Wiring Architecture (IEC 60204-1)

Following professional **IEC 60204-1** industrial wiring practices, the power and control circuits within the cabinet were rigorously isolated and **routed separately** across the `RIT.8800750` cable ducts.

### 🧵 Sizing and Color Code Standards
* **Power Circuit Wiring:** Sized at **2.5 mm²** (`Black` or `Brown` for active phases) to handle the 16A main cross-sections and the nominal 5A running current of both motors.
* **Control Circuit Wiring:** Sized at **1.5 mm²** (`Red` for 230V AC Phase logic, `Light Blue` for the common Neutral return path landing on the blue **-X5:4** terminal).
* **Protective Earth (PE) Grounding Layout:** * The main grounding line connects to **-X6PEPE** ($2.5\text{ mm}^2$ `Green/Yellow`), which structurally clamps onto the zingué steel `RIT.2313150` rail, transforming the entire backplate into a secure equipotential frame.
  * Outgoing field motor cables ground directly on **-X7PEM1** (Motor 1 PE) and **-X8PEM2** (Motor 2 PE) respectively, following the same color standards to guarantee total fault-current evacuation pathways.

### 📈 Design Benefits
* **EMC & Noise Reduction:** Keeping high-current three-phase motor lines segregated from low-power 230V AC control logic paths dramatically minimizes Electromagnetic Interference (EMI) and transient crosstalk.
* **Maintenance & Safety:** Separate routing improves accessibility for diagnostics, simplifies downstream system maintenance, and drastically enhances overall cabinet organization and cleanliness.

---

## 📂 Project Documentation & Layout Directory

The output documentation generated from EPLAN is structured as follows:

* 🖼️ **`01_3D_Panel_View.png`** Complete virtual isometric render of the physical digital twin assembly within the **Rittal AX 1060.000** enclosure.
* 🚪 **`02_Front_Door_Layout.png`** Dimensional layout of the HMI cluster containing the Siemens indicators and Schneider XB4 operator buttons on the enclosure door.
* 🔩 **`03_Mounting_Plate_Layout.png`** Scaled mechanical diagram for physical component mounting, rail alignments (`RIT.2313150`), and channel distribution (`RIT.8800750`) on the zinc-plated backplate.
* 🛣️ **`04_Wire_Routing_Panel_View.png`** 3D perspective mapping generated by EPLAN Pro Panel, highlighting automated wire routing through wire ducts.
* 📐 **`05_Wire_Routing_Panel_Front_View.png`** Clean orthogonal layout visualization displaying control wire density and entry vectors.
* 🗺️ **`06_Wire_Routing_Mounting_Plate_Layout_Front_View.png`** Detailed backplate blueprint specifying exact wire termination tracks and calculated path lengths for manufacturing.
* 📄 **`07_Star_Delta_Motor_Starter_Design.pdf`** Multi-page design deliverable incorporating schematics, dynamic cross-referencing maps, terminal configuration logs, and automated Bills of Materials.

---

## 💻 Software Core Competencies

* **EPLAN Electric P8:** 2D electrical engineering tool used for designing schematics, establishing electrical rules, organizing potentials, managing structural identifiers, and automating cross-references between contactor auxiliary poles.
* **EPLAN Pro Panel:** 3D engineering workspace utilized to layout the physical components, define exact panel surfaces, construct wire paths, calculate duct fill capacity, and execute smart digital-twin auto-routing.

---

## 🚀 Skills Demonstrated

* **Advanced Industrial Control Logic:** Designing fail-safe hardware interlocking schemas (NC cross-wired auxiliary pairs) preventing dangerous concurrent firing of Star and Delta loops.
* **Digital Twin Engineering:** Prototyping physical mechanical constraints virtually using authentic **Rittal** and **Phoenix Contact** templates to achieve zero manufacturing wire waste and ensure accurate enclosure hole drilling patterns.
* **Normative Engineering Compliance:** Executing electrical paths based strictly on unified wire gauge colors and global grounding criteria (protective earth continuity to mounting rails, door frameworks, and incoming field motor casings).
