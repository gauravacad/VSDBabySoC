1. # VSDBabySoC
VSDBabySoC is a small yet powerful RISCV-based System-on-Chip (SoC).

- **The Key Components**: Includes a **current source**, **a PLL (avsdpll\_1v8)**, an embedded **RISC-V core (rvmyth)**, an **ADC/DAC (avsddac\_3v3)**, and an **SPI interface**.
- **Voltage Domains**: The SoC operates with distinct voltage domains: a 1.8V domain and a 3.3V domain, clearly indicating power supply requirements for different components.
- **Interconnections**: Arrows and labels illustrate the flow of signals and power between these blocks, such as clock signals (CLK) and data paths (B[3:0], D[9:0]).
- **The VSDBabySoC's:** primary purpose is to integrate and evaluate multiple open-source IPs cores and to calibrate its analog section.
  
## 2. Purpose of Digital to Analog converted (DAC)
- In real world, most of the data available is in the analog form in nature.
- Thereby we have two types of converters `analog` to digital` converter (ADC) and `digital to analog` converter (DAC).
- These two converting interfaces are essential to obtain the required operations of a processor (here RVMYTH) to manipulate the data of any electronic equipment.

### 2.1. Implementation of 10Bit Potentiometric DAC
- There are two commonly used `DAC conversions` (1) `Weighed resistors method` and (2) `R-2R ladder network method`. 
- The Principle here is to divide the iput voltage into N different output voltage values in the range of Reference voltage (VREFH, VREFL) for a N-Bit DAC.
- The design avsdac_3v3 DAC here achieve this by a simple resistors in series.
- The Chip Layout for the avsdac_3v3. It has 10 Bit dataline. with dimension 195.58 um x 117.45 um.
- avsdac_3v3 operating Modes with Fclk = 1 MHz.
  
  <img width="811" height="561" alt="image" src="https://github.com/user-attachments/assets/d7928214-13d4-486e-aa96-a7f177b84536" />

  <img width="674" height="694" alt="image" src="https://github.com/user-attachments/assets/fda1fc91-b040-48b8-ab63-1dde7c42b72e" />

  [Basic Architecture of the Potentiometric DAC — avsddac_3v3_sky130_v1](https://github.com/vsdip/avsddac_3v3_sky130_v1)
---
## Specification: avsdac_3v3
The design library used is sky130. This design is implemented using xschem, and ngspice is used to run the simulations & verify the circuitry. For circuit layout implementation, Magic will be used. 

| Name   | Pin No. | I/O | Description                          |
|--------|---------|-----|--------------------------------------|
| D[0:9] | 1–10    | I   | Digital inputs                       |
| EN     | 11      | I   | Enable pin                           |
| VDD    | 12      | I   | Digital power supply (1.8 V)         |
| VSS    | 13      | I   | Digital ground                       |
| OUT    | 14      | O   | DAC analog voltage output            |
| VDDA   | 15      | I   | Analog voltage supply (3.3 V)        |
| VSSA   | 16      | I   | Analog ground                        |
| VREFH  | 17      | I   | Reference voltage high for DAC (3.3 V)|
| VREFL  | 18      | I   | Reference voltage low for DAC        |

## 2.2 RISCV: [RVMYTH CORE](https://www.makerchip.com/)
- A RISC-V ISA is defined as a base integer ISA, which must be present in any implementation, plus optional extensions to the base ISA. Each base integer instruction set is characterized by
   - Width of the integer registers (XLEN)
   - Corresponding size of the address space
   - Number of integer registers (32 in RISC-V)

### 2.2.1 Components of a SoC
The chip has the core where all the logic, Macros, Foundary IP's lies and pads for signal I/O and the total die after the floorplanning, placement, routing etc are completed.
Interface between an application and actual hardware is brought in by the system software.
However, the hardware understands only the binaries, and hence an abstract interface which starts with Intruction Set Architecture, then the RTL Description.
Once RTL description is done, then the process of conversion of RTL to physical chip is done.
Here **RISC-V core (rvmyth)** is an open architecture enables us to create processors highly tailored for specific computational challenges. 

<img width="900" height="900" alt="image" src="https://github.com/user-attachments/assets/869b0def-220a-49db-bbda-cd3ff7611e59" />


 [Basic Architecture of the VSDBabySoC — SoC based on RVMYTH ](https://github.com/manili/VSDBabySoC/tree/main)
## Installtion and Overview of Sandpiper
- SandPiper is a code generator that generates readable, well-structured, Verilog or SystemVerilog code from the given TL-Verilog code.
- SandPiper SaaS Edition runs as a microservice in the cloud to support easy open-source development. Install Sanpiper SaaS Edition for this project.
- To run locally, SandPiper Education Edition can be requested from RedwoodEDA
-
### Steps to convert TL-Verilog to Verilog or SystemVerilog

```bash
1. First install Sandpiper SaaS (https://pypi.org/project/sandpiper-saas/)
$ git clone https://github.com/shivanishah269/vsdfpga.git
$ cd vsdfpga/verilog
$ sandpiper-saas -i rvmyth.tlv -o rvmyth.v --iArgs

```
### Steps to convert TL-Verilog to Verilog or SystemVerilog
``` bash
$ iverilog rvmyth_pll_tb.v rvmyth_pll.v clk_gate.v
$ ./a.out
$ gtkwave rvmyth_pll.vcd
```
### Tools
1. Makerchip:

- Makerchip is a free web-based IDE as well as available as makerchip-app, a virtual desktop application for developing high-quality integrated circuits.
- You can code, compile, simulate, and debug Verilog designs, all from your browser. Your code, block diagrams, and waveforms are tightly integrated.

2. Icarus Verilog:

- Icarus Verilog is a Verilog simulation and synthesis tool.

## LAB WORK VSDBABYSoC

``` bash
$ cd VSDBabySoC/
$ python -m venv my-venv
$ python3 -m venv my-venv
$ my-venv/bin/pip install pyyaml click sandpiper-saas
$ make pre_synth_sim
$ source my-venv/bin/activate
$ make pre_synth_sim
``` 


3. GTKWave:

- GTKWave is a waveform viewer.
