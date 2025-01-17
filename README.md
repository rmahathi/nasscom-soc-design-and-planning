<div align="center">

# Nasscom & VSD SOC Design and Planning

</div>


![Alt text](assets/Cover.png)
> 2 Week digital VLSI SoC design and planning workshop with complete RTL2GDSII flow organised by VSD in collaboration with NASSCOM

<p align="justify"> 

# Chip Design and Validation Workflow

An overview of the **chip design and validation workflow** from initial specifications to final applications. The workflow ensures validation consistency across all stages: **O1 = O2 = O3 = O4**.  

<details><summary> 
  
### Click to learn about the workflow stages </summary>

## **Workflow Stages**

### **O1: Specifications (C Model)**
- The design begins with defining specifications in a high-level **C model**.
- A **testbench** (in C language) is used to validate functionality early on.

---

### **O2: RTL Design (Verilog)**
- The hardware is implemented as a **soft copy** using **RTL (Verilog)**.
- Major components:
  - **Processor**
  - **Peripherals/IPs**
  - **Analog IPs**
- The design is synthesized, producing a **Gate-Level Netlist** for further validation.

---

### **O3: SoC Integration**
- Modules (processor, peripherals, macros, and analog IPs) are integrated into a **System-on-Chip (SoC)**.
- Physical design steps include:
  - **Floorplanning**
  - **Placement**
  - **Routing**
- The design undergoes:
  - **Design Rule Checks (DRC)**
  - **Layout vs. Schematic (LVS)**  
- Output: **GDSII file** for fabrication.
  
---

### **O4: Final Chip Design**
- The final chip design includes **peripherals** operating in the target frequency range.
- The **testbench** continues validating the design to ensure:
  - **O1 = O2 = O3 = O4**

---

Below are the diagrams that visually represent the chip design workflow:

### Workflow Stages (O1 to O3)
<div align="center">
  <img src="assets/Chipdesign1.jpg" alt="Chip Design Workflow - O1 to O3">
</div>

### Final Validation and Applications (O4)
<div align="center">
  <img src="assets/Chipdesign2.jpg" alt="Chip Design Validation and Applications - O4">
</div>
</details>
</p>

# Section 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK 

<details>
<summary> 

## Introduction to QFN-48 Package, chip, pads, core, die and Ips 
</summary>

### Overview of an Embedded Board Design
<div align="center">
  <img src="assets/EmbeddedBoardDesign.png" alt="Embedded Board Design">
</div>

### Inside a Package
<div align="center">
  <img src="assets/Package.png" alt="Package View">
</div>

### Connecting the chip to the pins 
<div align="center">
  <img src="assets/ChipToPin.png" alt="Chip to pins connections">
</div>

### Chip Overview
<div align="center">
  <img src="assets/ChipOverview.png" alt="Chip Overview">
</div>

<br />
<p align="justify"> 
Foundry IPs are pre-designed and pre-verified blocks provided by semiconductor foundries to streamline chip design. These include critical components such as analog-to-digital converters (ADCs), digital-to-analog converters (DACs), SRAM, GPIO interfaces, and Phase-Locked Loops (PLLs).

For example, the PLL is a crucial IP block in chip design. Its primary function is to take an input clock signal (which may be of lower frequency) and generate a stable output clock signal at a higher frequency, phase-locked to the input. This is essential for processors to operate at their required high-frequency clock rates while maintaining synchronization with the input clock source.

By using foundry IPs, designers save time and effort, leveraging proven and reliable building blocks optimized for the foundry's process technology.
</p>
</details>

---

<details>
<summary> 

## Introduction to RISC-V
</summary>

### RISC-V Architecture Implementation
<div align="center">
  <img src="assets/riscv.png" alt="RISC-V">
</div>
<p align="justify"> 
<br />
RISC-V Architecture specifications can be implemented in the Layout using a HDL.
</p>
</details>

---

<details>
<summary> 

## From Software Applications to Hardware
</summary>

### Software Flow
<div align="center">
  <img src="assets/swflow.png" alt="Software Flow">
</div>
<br />
<p align="justify"> 
To run an application on hardware, several processes occur. The application enters the system software, which converts it into binary language. Key components of system software include the Operating System (OS), compiler, and assembler.  
<br />
<br />
The OS produces functions in high-level languages (e.g., C, C++, Java), which the compiler converts into hardware-specific instructions. These instructions are then processed by the assembler, which translates them into binary code (machine language). Finally, this binary code is fed to the hardware, enabling it to execute the required functions.
</p>

### Stopwatch App as an example
<div align="center">
  <img src="assets/stopwatchex.png" alt="Stopwatch App">
</div>
<br />
<p align="justify"> 
For instance, consider a stopwatch app running on a RISC-V core. The operating system generates a small C function, which is processed by the compiler to produce RISC-V instructions. These instructions are then passed through an assembler, which converts them into binary code. This binary code is subsequently loaded onto the chip's layout for execution.
</p>

### Instruction Set Architecture (ISA)
<div align="center">
  <img src="assets/isa.png" alt="ISA">
</div>
<br />
<p align="justify"> 
The instructions, which are part of the Instruction Set Architecture (ISA), are written in assembly language or high-level language. These are passed through an assembler (or compiler), which converts them into machine code (binary format) that the hardware can understand and execute. The RTL (Register Transfer Level) description, written in a hardware description language (e.g., Verilog or VHDL), is synthesized into a netlist (a representation of the design in terms of logic gates). This netlist is then used in the physical design process to create a layout, which represents the actual physical implementation of the circuit on silicon.
</p>

### ISA -> RTL & Synthesis -> Physical Design
<div align="center">
  <img src="assets/breakdown.png" alt="Breakdown">
</div>
<br />
<p align="justify"> 
This course is divided into three distinct parts:
<br />

- RISC-V ISA
- RTL and synthesis of RISC-V based CPU core - picorv32
- Physical design implementation of picorv32
</p>
</details>

---

<details>
<summary> 

## Introduction to all components of open-source digital asic design
</summary>
<p align="justify"> 
For open-source ASIC design implementation, we need the following enablers available in open-source versions:
<br />

- RTL Designs
- EDA Tools
- PDK Data
</p>

<p align="justify"> 
Initially, IC design and fabrication were closely tied and limited to companies like TI and Intel. In 1979, Lynn Conway and Carver Mead introduced the idea of separating design from fabrication by developing structured methodologies based on λ-design rules, which led to the first VLSI book, *Introduction to VLSI Systems*. This approach gave rise to "fabless" companies focused on design and "pure play fabs" for fabrication.
<br /><br />
The interface between designers and fabs became a set of files called "Process Design Kits" (PDKs), which include device models, design rules, and libraries. Due to the sensitive nature of PDKs, they were previously distributed only under NDAs.
<br /><br />
However, in 2020, Google collaborated with Skywater to open-source the 130nm PDK, making it the first open-source PDK release.
</p>

<br />

<div align="center">
  <img src="assets/ASICreq.png" alt="ASIC Requirements">
</div>

<br />

### Is Sky130nm still in use?
<div align="center">
  <img src="assets/130old.png" alt="Is sky130 old?">
</div>

<br />

<p align="justify"> 
The 130nm process accounts for 6% of the market share in pure-play IC foundry sales. It remains relevant due to its cost-effectiveness for applications that don't require the advanced performance of smaller nodes.
</p>

### Is Sky130nm fast?
<div align="center">
  <img src="assets/130fast.png" alt="Is sky130 fast?">
</div>

<br />

<p align="justify"> 
The 130nm process can still achieve high performance. For instance, Intel's Pentium 4 Extreme Edition ran at 3.46 GHz, and the OSU team achieved a 327 MHz clock frequency for a single-cycle RV32i CPU in post-layout simulations. A pipelined version can exceed 1 GHz. Additionally, using the Sky130 PDK, the RV32i design achieved a 398 MHz frequency with a 33.8 pJ PDP, demonstrating that 130nm can still deliver competitive speeds.
</p>

### EDA Tools
<div align="center">
  <img src="assets/EDAtools.png" alt="EDA Tools">
</div>

<br />

<p align="justify"> 
ASIC design is a complex process involving numerous steps, methodologies, and EDA tools. These elements are integrated into an ASIC flow, a software that combines various tools to execute the design process.
</p>
</details>

---

<details>
<summary> 

## Simplified RTL2GDS flow
</summary>

### RTL2GDS flow
<div align="center">
  <img src="assets/RTL2GDSIIflow.png" alt="RTL2GDSII flow">
</div>
<br />

### Chip Floor Planning
<div align="center">
  <img src="assets/ChipFloorPlanning.png" alt="Chip Floor Planning">
</div>
<br />

### Macro Floor Planning
<div align="center">
  <img src="assets/MacroFloorPlanning.png" alt="Macro Floor Planning">
</div>
<br />

### Power Planning
<div align="center">
  <img src="assets/PowerPlanning.png" alt="Power Planning">
</div>
<br />

### Placement
<div align="center">
  <img src="assets/Placement.png" alt="Placement">
</div>
<br />

<div align="center">
  <img src="assets/Placement2.png" alt="Placement2">
</div>
<br />

### Clock Tree Synthesis
<div align="center">
  <img src="assets/ClockTreeSynthesis.png" alt="Clock Tree Synthesis">
</div>
<br />

### Routing
<div align="center">
  <img src="assets/Routing.png" alt="Routing">
</div>
<br />

### SignOff
<div align="center">
  <img src="assets/SignOff.png" alt="SignOff">
</div>
<br />

</details>

---

<details>
<summary> 

## DAY 1 LAB -  Design Synthesis - picorv32a 
</summary>
<p align="justify"> 

Aim is to run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs and then calculate the flop ratio.

### To run Design Synthesis - picorv32a using OpenLANE flow

Commands to invoke the OpenLANE flow and perform synthesis

```bash
# Navigate to the OpenLANE flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# Use the alias 'docker' for the long Docker run command
# This alias simplifies invoking the OpenLANE Docker container
docker

```
```tcl
# Launch the OpenLANE flow in interactive mode
./flow.tcl -interactive

# Load the OpenLANE package for proper functionality
package require openlane 0.9

# Prepare the design environment for 'picorv32a' by creating necessary files and directories
prep -design picorv32a

# Run synthesis for the prepared design
run_synthesis

# Exit the OpenLANE flow interface
exit

# Exit the Docker container
exit

```

#### Terminal screenshots:

<div align="center">
  <img src="assets/one.png" alt="Screenshot of running command">
</div>
<br />

<div align="center">
  <img src="assets/two.png" alt="Screenshot of running command">
</div>
<br />

### To Calculate Flip Flop Ratio

#### Formulae:

```math
Flop\ Ratio = \frac{Number\ of\ D\ Flip\ Flops}{Total\ Number\ of\ Cells}
```
<br />

```math
Percentage\ of\ DFF's = Flop\ Ratio * 100
```
<br />

#### Terminal screenshots:

<div align="center">
  <img src="assets/three.png" alt="Screenshot of running command">
</div>
<br />

<div align="center">
  <img src="assets/four.png" alt="Screenshot of running command">
</div>
<br />

#### Highlighted Values for computation:

<div align="center">
  <img src="assets/five.png" alt="Screenshot of running command">
</div>
<br />

<div align="center">
  <img src="assets/six.png" alt="Screenshot of running command">
</div>
<br />

#### Calculation of Flop Ratio and DFF % from synthesis statistics report file:
<br />

```math
Flop\ Ratio = \frac{1613}{14876} = 0.108429
```
<br />

```math
Percentage\ of\ DFF's = 0.108429 * 100 = 10.8429\ \%
```
<br />

All picorv32a logs, reports and results can be found here:

[Section 1 Run - 02-12_18-45](https://github.com/rmahathi/nasscom-soc-design-and-planning/tree/main/02-12_18-45)

</p>
</details>
<br />

# Section 2 - Good floorplan vs bad floorplan and introduction to library cells

<details>
<summary> 

## Chip Floor Planning Considerations
</summary>

### 1. Identifying the Width of the Die and Core
<br />

<div align="center">
  <img src="assets/diecore.png" alt="diecore">
</div>
<br />

<p align="justify"> 

To determine the Utilization Factor and Aspect Ratio, the height and width of core and die areas must first be defined.

- Core is the area in a chip used for placing all the logic cells and components. It is where the logic resides in a chip.

- Die is the area encircling the core, used for placing I/O-related components.  

The height and width of the core area depend on the design's netlist. These are based on the number of components required to execute the logic. The die area's height and width depend on the core's dimensions.  

</p>

<div align="center">
  <img src="assets/netlist.png" alt="netlist">
</div>
<br />

For example, consider a netlist with two logic gates and two flip-flops, each with an area of 1 sq. unit. The total core area required is 4 sq. units.  

<div align="center">
  <img src="assets/netlist2.png" alt="netlist">
</div>
<br />

Area occupied by the above netlist on a silicon wafer

<div align="center">
  <img src="assets/netlist3.png" alt="netlist">
</div>
<br />

#### Utilization Factor 
Utilization Factor is the ratio of the core area occupied by the netlist to the total core area.  
For a good FloorPlan, the Utilization Factor should never be '1' to allow space for additional logic.  

```math
Utilization\ Factor = \frac{Area\ occupied\ by\ netlist}{Total\ core\ area}
```

#### Aspect Ratio 
Aspect Ratio is the ratio of the core's height to its width.  
If the Aspect Ratio is '1', the core is square. Otherwise, it is rectangular.  

```math
Aspect\ Ratio = \frac{Height\ of\ the\ core}{Width\ of\ the\ core}
```

#### Calculations
 
<div align="center">
  <img src="assets/netlist4.png" alt="netlist">
</div>
<br />

```math
Utilization\ Factor = \frac{4\ sq.\ units}{4\ sq.\ units} = 1
```

```math
Aspect\ Ratio = \frac{2\ units}{2\ units} = 1\ (Square\ core)
```

### 2. Define Locations of Pre-Placed Cells

Pre-placing cells refers to reusing pre-designed blocks (e.g., memory, comparators, MUX). These blocks are called macros or IPs.  

<div align="center">
  <img src="assets/prepl.png" alt="preplaced_cell">
</div>
<br />

<div align="center">
  <img src="assets/prepl2.png" alt="preplaced_cell">
</div>
<br />

<div align="center">
  <img src="assets/prepl3.png" alt="preplaced_cell">
</div>
<br />

Macros should be placed close to input pins for reduced wiring length. They are placed during the Floorplan stage, with placement blockages defined to prevent standard cells from being placed nearby, and they also reduce Time-to-Market.  

### 3. Surround Pre-Placed cells with De-Coupling Capacitors
<br />

<div align="center">
  <img src="assets/decoup.png" alt="placement_decoupling_capacitor">
</div>
<br />
<p align="justify"> 
Decoupling capacitors are used in SoC design near high-power-demanding blocks or macros to stabilize voltage by locally storing charge. They charge when signals switch from 0 to 1 and supply energy during peak current demands, reducing the reliance on distant power sources. The power supply wires have inherent resistance and inductance, which cause a voltage drop during current flow, leading to a slightly reduced voltage at the load (Vdd' < Vdd). This voltage drop becomes more pronounced over larger physical distances, making it difficult to maintain stable voltage levels. 
</p>
<div align="center">
  <img src="assets/noisemargin.png" alt="noisemargin">
</div>
<br />

If the drop pushes the voltage below the noise margin, the circuit may enter an undefined state, resulting in failures or incorrect outputs. 

<div align="center">
  <img src="assets/decoup2.png" alt="placement_decoupling_capacitor">
</div>
<br />

Decoupling capacitors mitigate this by supplying the required energy locally during switching, ensuring stable operation and preventing voltage drops from falling below safe levels.

<div align="center">
  <img src="assets/decoup3.png" alt="placement_decoupling_capacitor">
</div>
<br />

### 4. Power Planning 

In power planning for SoC design, consider a macro where a 16-bit orange bus carries a 0-to-1 signal. Being far from the power source introduces voltage drops due to resistance and inductance in the supply wires.

<div align="center">
  <img src="assets/pow.png" alt="power_planning">
</div>
<br />

To handle signal transitions, drivers (e.g., inverters) are employed. An inverter converts the input signal to its complement (0 to 1 or 1 to 0), driving the next stage effectively.

<div align="center">
  <img src="assets/pow1.png" alt="power_planning">
</div>
<br />

1-to-0 Transition - Ground Bounce:

In a 1-to-0 transition, the previously charged nodes discharge rapidly to ground. If all 16 bits discharge at once, the ground potential may fluctuate, causing a phenomenon called ground bounce. This occurs due to inductance in the ground path, leading to temporary voltage spikes. If the ground bounce crosses the noise margin, it can cause unpredictable behavior, further increasing the risk of errors in circuit operation.

<div align="center">
  <img src="assets/pow2.png" alt="power_planning">
</div>
<br />

0-to-1 Transition - Voltage Drop:

When a 0-to-1 transition occurs, the driver charges the load capacitance of the connected circuit. This charging demands significant current, especially for all 16 bits transitioning simultaneously. A voltage drop across the supply wires may occur due to the high current demand, reducing Vdd' and risking a voltage level near or below the noise margin. If the voltage drops significantly, the circuit can enter an undefined state, leading to unreliable outputs.

<div align="center">
  <img src="assets/pow4.png" alt="power_planning">
</div>
<br />

Simultaneous Switching Problem:

When multiple signals (0-to-1 or 1-to-0) switch at the same time, the cumulative current demand rises sharply. For a 0-to-1 transition, the power supply must provide a surge of current to charge the capacitors, while for a 1-to-0 transition, a large discharge current flows to ground. Both cases can result in severe voltage drops or ground bounce due to the limitations of a single-point power supply.

<div align="center">
  <img src="assets/pow5.png" alt="power_planning">
</div>
<br />

Solution: Power Mesh
The solution is to replace the single-point power supply with a power mesh. A power mesh distributes Vdd and ground throughout the chip using a network of interconnected wires, reducing the resistance and inductance between the source and various blocks. By bringing power closer to the loads and reducing the effective distance, the voltage drop and ground bounce are minimized. The power mesh ensures that all parts of the circuit can access stable supply and ground levels, even during peak current demands, maintaining signal integrity and preventing undefined states.

<div align="center">
  <img src="assets/pow6.png" alt="power_planning">
</div>
<br />

### 5. Pin Placement 

Pin placement impacts wire length and connectivity. Pins must be placed to minimize wire length.  
For example, an input pin driving two blocks should be near them.  

<div align="center">
  <img src="assets/pls1.png" alt="pin_placement">
</div>
<br />

In effective pin placement:  
1. Pin order is based on connectivity, not sequence.  
2. Clock pins are larger due to their importance and susceptibility to delays.  

<div align="center">
  <img src="assets/pls2.png" alt="pin_placement">
</div>
<br />

### 6. Logical Cell Placement Blockage

Placement blockages outside the core and inside the die prevents automated placement and routing tool from placing any other cells into the the pin-dedicated area.

<div align="center">
  <img src="assets/block.png" alt="cell_placement_blockage">
</div>
<br />

</details>

---

<details>
<summary> 

## DAY 2 LAB -  Design Floorplan- picorv32a 

</summary>

<p align='justify'>
Before initiating the floorplan stage, designers must verify and adjust crucial switches that control the floorplan's characteristics. These configuration parameters, including utilization factor and aspect ratio, must align with the project's specific requirements to ensure optimal floorplan execution. A proper review of these switches helps prevent potential issues and ensures the floorplan process proceeds as intended.
</p>

<div align="center">
  <img src="assets/eight.png" alt="Screenshot">
</div>
<br />
<div align="center">
  <img src="assets/nine.png" alt="Screenshot">
</div>
<br />
<div align="center">
  <img src="assets/ten.png" alt="Screenshot">
</div>
<br />
<div align="center">
  <img src="assets/eleven.png" alt="Screenshot">
</div>
<br />
<div align="center">
  <img src="assets/twelve.png" alt="Screenshot">
</div>
<br />

### To run Design Floorplan - picorv32a using OpenLANE flow

Commands to invoke the OpenLANE flow and run floorplan

```bash
# Navigate to the OpenLANE flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# Use the alias 'docker' for the long Docker run command
# This alias simplifies invoking the OpenLANE Docker container
docker

```
```tcl
# Launch the OpenLANE flow in interactive mode
./flow.tcl -interactive

# Load the OpenLANE package for proper functionality
package require openlane 0.9

# Prepare the design environment for 'picorv32a' by creating necessary files and directories
prep -design picorv32a

# Run synthesis for the prepared design
run_synthesis

# Initialize the floorplan for the design
init_floorplan

# Place the IO pins in the design
place_io

# Insert tap cells and decoupling capacitors
tap_decap_or

# Generate the power grid
run_power_grid_generation

# Perform detailed floorplanning after power grid generation
run_floorplan

```
<br />
<div align="center">
  <img src="assets/thirteen.png" alt="Screenshot">
</div>
<br />
<div align="center">
  <img src="assets/fourteen.png" alt="Screenshot">
</div>
<br />
<div align="center">
  <img src="assets/fifteen.png" alt="Screenshot">
</div>
<br />
<div align="center">
  <img src="assets/sixteen.png" alt="Screenshot">
</div>
<br />
<div align="center">
  <img src="assets/seventeen.png" alt="Screenshot">
</div>
<br />
<div align="center">
  <img src="assets/eighteen.png" alt="Screenshot">
</div>
<br />
<br />
<div align="center">
  <img src="assets/nineteen.png" alt="Screenshot">
</div>
<br />
<div align="center">
  <img src="assets/twenty.png" alt="Screenshot">
</div>
<br />

Steps to Open Magic

```
magic -T /home/vsduser//Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```
<br />
<div align="center">
  <img src="assets/twentyone.png" alt="Screenshot">
</div>
<br />
<div align="center">
  <img src="assets/twentytwo.png" alt="Screenshot">
</div>
<br />

### Calculate the die area in microns from the values in floorplan def.

```math
1000\ Unit\ Distance = 1\ Micron
```

```math
Die\ width\ in\ unit\ distance = 660685 - 0 = 660685 
```
  
```math
Die\ height\ in\ unit\ distance = 671405 - 0 = 671405
```

```math
Distance\ in\ microns = \frac{Value\ in\ Unit\ Distance}{1000}
```

```math
Die\ width\ in\ microns = \frac{660685}{1000} = 660.685\ Microns
```

```math
Die\ height\ in\ microns = \frac{671405}{1000} = 671.405\ Microns
```

```math
Area\ of\ die\ in\ microns = 660.685 * 671.405 = 443587.212425\ Square\ Microns
```

<br />
<div align="center">
  <img src="assets/twentythree.png" alt="Screenshot">
</div>
<br />
<div align="center">
  <img src="assets/twentyfour.png" alt="Screenshot">
</div>
<br />

All picorv32a logs, reports and results can be found here:

[Section 2 Run - 11-01_08-49)](https://github.com/rmahathi/nasscom-soc-design-and-planning/tree/main/11-01_08-49)

</details>

---

<details>
<summary> 

## Library Binding and Placement
</summary>

<div align="center">
  <img src="assets/libbin.png" alt="libbin">
</div>
<br />

<div align="center">
  <img src="assets/libbin1.png" alt="libbin">
</div>
<br />

<div align="center">
  <img src="assets/libbin2.png" alt="libbin">
</div>
<br />

Repeaters, also known as buffers, are essential components in digital designs to recondition and regenerate signals, 
ensuring that they maintain their integrity over long distances. These buffers help replicate the original signal and send 
it again without degradation. In the placement process, buffers are strategically placed based on slew analysis to optimize 
signal quality and timing, preventing signal degradation or delays. This ensures the overall performance of the design by 
maintaining proper signal strength and timing across the chip.
<br />

<div align="center">
  <img src="assets/libbin3.png" alt="libbin">
</div>
<br />

<div align="center">
  <img src="assets/libbin4.png" alt="libbin">
</div>
<br />

</details>

---

<details>
<summary> 

## DAY 2 LAB -  Design Placement- picorv32a 

</summary>

### To run Design Placement - picorv32a using OpenLANE flow

Commands to invoke the OpenLANE flow and run placement

```tcl
# Previous section sets up the design environment for 'picorv32a'
# Performs synthesis to generate a gate-level netlist
# Initializes the floorplan, places IO pins, inserts tap cells and decoupling capacitors, generates the power grid, and completes the detailed floorplanning process to prepare the design for placement and routing.

# Perform global placement
run_placement

```

<div align="center">
  <img src="assets/twentyfive.png" alt="Screenshot">
</div>
<br />

<div align="center">
  <img src="assets/twentysix.png" alt="Screenshot">
</div>
<br />

Steps to Open Magic

```
magic -T /home/vsduser//Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```

<div align="center">
  <img src="assets/twentyseven.png" alt="Screenshot">
</div>
<br />

<div align="center">
  <img src="assets/twentyeight.png" alt="Screenshot">
</div>
<br />

<div align="center">
  <img src="assets/twentynine.png" alt="Screenshot">
</div>
<br />

</details>

---

<details>
<summary> 

## Cell design and characterization flows

</summary>

### Cell Design Flow

<br />
<div align="center">
  <img src="assets/celldes1.png" alt="CellDesign">
</div>
<br />
<br />
<div align="center">
  <img src="assets/celldes2.png" alt="CellDesign">
</div>
<br />
<br />
<div align="center">
  <img src="assets/celldes3.png" alt="CellDesign">
</div>
<br />

### Inputs

- DRC & LVS Rules 

<br />
<div align="center">
  <img src="assets/celldes4.png" alt="CellDesign">
</div>
<br />

- SPICE Models

<br />
<div align="center">
  <img src="assets/celldes5.png" alt="CellDesign">
</div>
<br />

- Library & User Defined Specifications

<br />
<div align="center">
  <img src="assets/celldes6.png" alt="CellDesign">
</div>
<br />
<br />
<div align="center">
  <img src="assets/celldes7.png" alt="CellDesign">
</div>
<br />
<br />
<div align="center">
  <img src="assets/celldes8.png" alt="CellDesign">
</div>
<br />
<br />
<div align="center">
  <img src="assets/celldes9.png" alt="CellDesign">
</div>
<br />
<br />
<div align="center">
  <img src="assets/celldes10.png" alt="CellDesign">
</div>
<br />

### Design 

- Circuit Design

<br />
<div align="center">
  <img src="assets/celldes11.png" alt="CellDesign">
</div>
<br />

- Layout Design

<br />
<div align="center">
  <img src="assets/celldes12.png" alt="CellDesign">
</div>
<br />

- Characterization Flow

  <b>STEP 1: Read in the Model Files</b><br>
Load the necessary model files (such as process libraries, PDK files, or any predefined models) that are required for the characterization of the cells.<br><br>
  <b>STEP 2: Read the Extracted SPICE Netlist</b><br>
Import the SPICE netlist generated for the design, which contains the circuit elements (such as transistors, resistors, capacitors) and their connections.<br><br>
  <b>STEP 3: Recognize the Behavior of the Buffer</b><br>
Identify and analyze the behavior of the buffer cells in the netlist, focusing on how they condition and regenerate the signal.<br><br>
  <b>STEP 4: Read Subcircuits of the Inverter</b><br>
Extract and analyze the subcircuits related to inverters (which are often used for logic operations in the library) to model their performance accurately.<br><br>
  <b>STEP 5: Attach Necessary Power Sources</b><br>
Ensure that the power sources (such as VDD, ground) are connected correctly to the cells and subcircuits, enabling proper functionality during simulations.<br><br>
  <b>STEP 6: Apply the Stimulus</b><br>
Apply test stimulus (input signals) to the buffer and inverter cells, simulating realistic input conditions like rising and falling edges, transitions, and signal patterns.<br><br>
  <b>STEP 7: Provide Necessary Output Capacitances</b><br>
Define the output capacitances that are connected to the output of the cells to simulate the load conditions for the buffer and inverter circuits.<br><br>
  <b>STEP 8: Provide Necessary Simulation Commands</b><br>
Set up and run the necessary simulation commands (e.g., .tran for transient analysis) to obtain results like delays, rise/fall times, and power consumption.<br><br>

<br />
<div align="center">
  <img src="assets/celldes13.png" alt="CellDesign">
</div>
<br />


</details>

---

<details>
<summary> 

## General timing characterization parameters

</summary>

### Characterization Setup

<br />
<div align="center">
  <img src="assets/timchr1.png" alt="TimingCharacteristic 1">
</div>
<br />

### 1. Timing Threshold

### Slew Rate Thresholds
The slew rate defines the rate of change of a signal's voltage level. Thresholds for rising and falling transitions help quantify the slew rate by identifying specific voltage levels at which these transitions begin and end.

<b>slew_low_rise_thr (Lower Threshold for Rising Signal Transition):</b><br />
Represents the lower bound of the rising edge of a signal transition, commonly set to 20% of the signal's maximum amplitude (from 0). This point is where the signal starts to significantly rise.

<div align="center">
  <img src="assets/timchr2.png" alt="TimingCharacteristic 2">
</div>
<br />

<b>slew_high_rise_thr (Upper Threshold for Rising Signal Transition):</b><br />
Represents the upper bound of the rising edge of a signal transition, commonly set to 80% of the signal's maximum amplitude. This point is where the signal has nearly completed its rise.

<div align="center">
  <img src="assets/timchr3.png" alt="TimingCharacteristic 3">
</div>
<br />

<b>slew_low_fall_thr (Lower Threshold for Falling Signal Transition):</b><br />
Represents the lower bound of the falling edge of a signal transition, commonly set to 20% of the signal's maximum amplitude. This point indicates where the signal starts to significantly fall.

<div align="center">
  <img src="assets/timchr4.png" alt="TimingCharacteristic 4">
</div>
<br />

<b>slew_high_fall_thr (Upper Threshold for Falling Signal Transition):</b><br />
Represents the upper bound of the falling edge of a signal transition, commonly set to 80% of the signal's maximum amplitude. This point indicates where the signal has almost completed its fall.

<div align="center">
  <img src="assets/timchr5.png" alt="TimingCharacteristic 5">
</div>
<br />

### Input Signal Thresholds

<b>in_rise_thr (Threshold for Input Signal Rising Edge):</b><br />
Represents the threshold level for the input signal's rising edge, typically set to 50% of the signal's maximum amplitude. This point is used for accurate timing analysis of the input transition.

<div align="center">
  <img src="assets/timchr6.png" alt="TimingCharacteristic 6">
</div>
<br />

<b>in_fall_thr (Threshold for Input Signal Falling Edge):</b><br />
Represents the threshold level for the input signal's falling edge, typically set to 50% of the signal's maximum amplitude. This point is used to determine the critical timing of the input descent.

<div align="center">
  <img src="assets/timchr8.png" alt="TimingCharacteristic 8">
</div>
<br />

### Output Signal Thresholds

<b>out_rise_thr (Threshold for Output Signal Rising Edge):</b><br />
Represents the threshold level for the output signal's rising edge, typically set to 50% of the signal's maximum amplitude. This point is crucial for measuring propagation delays and output transition timing.

<div align="center">
  <img src="assets/timchr7.png" alt="TimingCharacteristic 7">
</div>
<br />

<b>out_fall_thr (Threshold for Output Signal Falling Edge):</b><br />
Represents the threshold level for the output signal's falling edge, typically set to 50% of the signal's maximum amplitude. This point is used to measure the timing when the output signal is transitioning downward.

<div align="center">
  <img src="assets/timchr9.png" alt="TimingCharacteristic 9">
</div>
<br />

### 2. Propagation Delay 

```math
\mathbf{Delay} = \text{time(out\_fall\_thr)} - \text{time(in\_rise\_thr)}
```

<br />
<div align="center">
  <img src="assets/timchr10.png" alt="TimingCharacteristic 9">
</div>
<br />

A negative propagation delay can occur when the output signal changes before the input signal reaches its threshold. This can happen if a higher, incorrect threshold is chosen for the input signal, as it fails to account for the actual timing relationship, leading to skewed or misleading delay calculations.
<div align="center">
  <img src="assets/timchr11.png" alt="TimingCharacteristic 9">
</div>
<br />

Negative delay can occur even with the correct 50% threshold if the input signal has a high slew rate. This is because the steep input transition skews the timing relationship, causing the output to react faster or appear delayed incorrectly. Proper slew rate control is crucial for accurate timing analysis.

<div align="center">
  <img src="assets/timchr12.png" alt="TimingCharacteristic 9">
</div>
<br />

<div align="center">
  <img src="assets/timchr13.png" alt="TimingCharacteristic 9">
</div>
<br />

### 3. Transition Time

### Transition Time (Rise)
Transition time for a rising edge refers to the time taken by a signal to change from a low voltage level to a high voltage level. It is a critical parameter in digital circuits, impacting the speed at which signals propagate through logic gates and affecting overall circuit performance.

```math
\mathbf{\text{Transition Time (Rise)}} = \text{time(slew\_high\_rise\_thr)} - \text{time(slew\_low\_rise\_thr)}
```

### Transition Time (Fall)
Transition time for a falling edge is the time it takes for a signal to change from a high voltage level to a low voltage level. Like the rise transition time, the fall transition time plays a significant role in the timing characteristics and performance of digital circuits, influencing how quickly signals can switch between states.

```math
\mathbf{\text{Transition Time (Fall)}} = \text{time(slew\_high\_fall\_thr)} - \text{time(slew\_low\_fall\_thr)}
```
<br />
<div align="center">
  <img src="assets/timchr14.png" alt="TimingCharacteristic 9">
</div>
<br />

</details>

---

# Section 3 - Design library cell using Magic Layout and ngspice characterization

<details>
<summary> 

## CMOS inverter ngspice theory
</summary>

<br />
<div align="center">
  <img src="assets/spice1.png" alt="Spice1"> 
</div>

<div align="center">
  <img src="assets/spice2.png" alt="Spice2">
</div>

<div align="center">
  <img src="assets/spice3.png" alt="Spice3">
</div>

<div align="center">
  <img src="assets/spice4.png" alt="Spice4">
</div>

<div align="center">
  <img src="assets/spice5.png" alt="Spice5">
</div>

<div align="center">
  <img src="assets/spice6.png" alt="Spice6">
</div>

<div align="center">
  <img src="assets/spice7.png" alt="Spice7">
</div>

<div align="center">
  <img src="assets/spice8.png" alt="Spice8">
</div>

<div align="center">
  <img src="assets/spice9.png" alt="Spice9">
</div>

<div align="center">
  <img src="assets/spice10.png" alt="Spice10">
</div>

<div align="center">
  <img src="assets/spice11.png" alt="Spice11">
</div>

<div align="center">
  <img src="assets/spice12.png" alt="Spice12">
</div>

<div align="center">
  <img src="assets/spice13.png" alt="Spice13">
</div>

<div align="center">
  <img src="assets/spice14.png" alt="Spice14">
</div>

<div align="center">
  <img src="assets/spice15.png" alt="Spice15">
</div>

<div align="center">
  <img src="assets/spice16.png" alt="Spice16">
</div>

<div align="center">
  <img src="assets/spice17.png" alt="Spice17">
</div>

<div align="center">
  <img src="assets/spice18.png" alt="Spice18">
</div>

<div align="center">
  <img src="assets/spice19.png" alt="Spice19">
</div>

<div align="center">
  <img src="assets/spice20.png" alt="Spice20">
</div>

<div align="center">
  <img src="assets/spice21.png" alt="Spice21">
</div>

</details>

---

<details>
<summary> 

## DAY 3 LAB - Design library cell using Magic Layout and ngspice characterization 
</summary>

### Using the IO placer to change the distance between tap cells

```bash

# Set IO mode to 2 (unequally spaced pins)
set ::env(FP_IO_MODE) 2

# Execute floorplanning again
run_floorplan

```

<div align="center">
  <img src="assets/thirty.png" alt="Screenshot">
</div>
<br />

<div align="center">
  <img src="assets/thirtyone.png" alt="Screenshot">
</div>
<br />

<div align="center">
  <img src="assets/thirtytwo.png" alt="Screenshot">
</div>
<br />

<div align="center">
  <img src="assets/thirtythree.png" alt="Screenshot">
</div>
<br />

### Clone custom inverter standard cell design from github repository

```bash
# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Clone the repository with custom inverter design
git clone https://github.com/nickson-jose/vsdstdcelldesign

# Change into repository directory
cd vsdstdcelldesign

# Copy magic tech file to the repo directory for easy access
cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech 

# Check contents to ensure file is present
ls -ltr

# Open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &
```

<div align="center">
  <img src="assets/thirtyfour.png" alt="Screenshot">
</div>
<br />

<div align="center">
  <img src="assets/thirtyfive.png" alt="Screenshot">
</div>
<br />

<div align="center">
  <img src="assets/thirtysix.png" alt="Screenshot">
</div>
<br />

<div align="center">
  <img src="assets/thirtyseven.png" alt="Screenshot">
</div>
<br />
