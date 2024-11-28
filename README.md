<div align="center">

# Nasscom & VSD SOC Design and Planning

</div>


![Alt text](assets/Cover.png)
> 2 Week digital VLSI SoC design and planning workshop with complete RTL2GDSII flow organised by VSD in collaboration with NASSCOM

<p align="justify"> 

# Chip Design and Validation Workflow

An overview of the **chip design and validation workflow** from initial specifications to final applications. The workflow ensures validation consistency across all stages: **O1 = O2 = O3 = O4**.
<details> 
  <summary> Click to learn about the workflow stages </summary>

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

# Section 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK (28/03/2024 - 29/03/2024)

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
<br /><br />
Initially, IC design and fabrication were closely tied and limited to companies like TI and Intel. In 1979, Lynn Conway and Carver Mead introduced the idea of separating design from fabrication by developing structured methodologies based on λ-design rules, which led to the first VLSI book, *Introduction to VLSI Systems*. This approach gave rise to "fabless" companies focused on design and "pure play fabs" for fabrication.
<br /><br />
The interface between designers and fabs became a set of files called "Process Design Kits" (PDKs), which include device models, design rules, and libraries. Due to the sensitive nature of PDKs, they were previously distributed only under NDAs.
<br /><br />
However, in 2020, Google collaborated with Skywater to open-source the 130nm PDK, making it the first open-source PDK release.
</p>

<br />

<div align="center">
  <img src="assets/ASICreq.png" alt="BASIC Requirements">
</div>

<div align="center">
  <img src="assets/130old.png" alt="Is sky130 old?">
</div>

<div align="center">
  <img src="assets/130fast.png" alt="Is sky130 fast?">
</div>

<div align="center">
  <img src="assets/EDAtools.png" alt="EDA Tools">
</div>
