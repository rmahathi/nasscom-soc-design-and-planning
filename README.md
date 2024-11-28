<div align="center">

# Nasscom & VSD SOC Design and Planning

</div>


![Alt text](assets/Cover.png)
> 2 Week digital VLSI SoC design and planning workshop with complete RTL2GDSII flow organised by VSD in collaboration with NASSCOM

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

# Section 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK (28/03/2024 - 29/03/2024)

## SKY_L1 - Introduction to QFN-48 Package, chip, pads, core, die and Ips

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

 --- 

Foundry IPs are pre-designed and pre-verified blocks provided by semiconductor foundries to assist in chip design. These include essential components like analog-to-digital converters (ADCs), digital-to-analog converters (DACs), PLLs (Phase-Locked Loops), SRAM blocks, and I/O interfaces such as GPIO and communication ports. They are optimized for the foundry's process technology, ensuring compatibility and performance. By using these IPs, designers can save time and effort, focusing on the custom logic of the System-on-Chip (SoC) while leveraging proven and reliable building blocks for critical functionalities.
