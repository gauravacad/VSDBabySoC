# VSDBabySoC Simulation and Syntheis 
## Week 3 LAB Task – VSDBabySoC

### 1. Basic RTL Simulation
- **Goal**: Verify functionality of the SoC design before synthesis.
- **outcome**: Functional RTL waveform in GTKWave.
- **Tools**: iverilog and gtkwave
- **Steps**: Compile the RTL + Testbench:

### 2. Synthesis with Yosys
- **Goal**: Convert RTL into a gate-level netlist using sky130_fd_sc_hd library.
- **outcome**: Synthesized gate-level netlist (vsdbabysoc_netlist.v).
- **Tools**: Yosys, Sky130 PDK standard cell library.
- **Steps**: Compile the NETLIST + Testbench:

### 3. Gate-Level Simulation (GLS)
- **Goal**: Verify functionality of synthesized netlist against RTL.
- **outcome**:GLS waveform (dump.vcd).
- **Tools**: iverilog and gtkwave
- **Steps**: Compile with netlist, testbench, primitives, and standard cell models

### 4. Analysis – RTL vs GLS Waveforms
- **Goal**: Compare timing behavior and ensure functional equivalence.
**Checks:**
- Functional outputs should match.
- GLS waveforms may show additional gate delays not present in RTL.
- Setup/hold issues or mismatches must be investigated.
- **Deliverable**: Documented comparison of RTL vs GLS timing in GTKWave screenshots.

### 5. Documentation (Week 3 Report) Include:
- Overview of SoC modules (RISC-V core, PLL, DAC, top module).
- RTL simulation steps & screenshots.
- Synthesis flow and netlist generation.
- GLS steps & waveforms.
- Side-by-side analysis of RTL vs GLS.
- Observations and conclusion.

---- 
## VSDBabySoC
VSDBabySoC is a compact RISC-V based System-on-Chip (SoC) designed to integrate and evaluate multiple open-source IP cores along with analog IP.

<img width="700" height="700" alt="image" src="https://github.com/user-attachments/assets/869b0def-220a-49db-bbda-cd3ff7611e59" />

Fig: [Basic Architecture of the VSDBabySoC](https://github.com/manili/VSDBabySoC/tree/main)

---
### Key Components
- **PLL (avsdpll_1v8)**
- **RISC-V Core (rvmyth)**
- **DAC (avsddac_3v3) / ADC**
- **SPI Interface**
- **Current Source**
- **Crystal oscilator**

## What is RVMYTH?
RVMYTH is a simple **RISC-V based CPU**, introduced in a workshop by **RedwoodEDA** and **VSD**.  
- Developed during a 5-day workshop, where even middle-school students participated in building a processor from scratch.  
- Uses **TL-Verilog (TLV)** for faster development.  
- Contributions to the IP are open-source and made by students.  

## What is PLL?
A **Phase-Locked Loop (PLL)** is a control system that generates an output signal whose **phase is related to the phase of an input signal**.  
- Widely used for synchronization.  
- Essential for **clock generation** and **distribution** in SoCs.  

## What is DAC?
A **Digital-to-Analog Converter (DAC)** converts a **digital signal into an analog signal**.  
- Enables generation of digitally-defined transmission signals.  
- High-speed DACs are critical in **mobile communications**.  
- Ultra-high-speed DACs are used in **optical communication systems**.  

# VSDBabySoC Modeling
Please note that in the following sections we will mention some repos that we used to model the SoC. However the main source code is resided in [Source-Code Directory](src) and these modules are in [Modules Sub-Directory](src/module).

## Step by step modeling walkthrough

### LAB TASK WORK VSDBABYSoC

### 1. Requirements
Ensure you have Icarus Verilog installed for compilation and GTKWave for viewing waveform files as per WEEK-1 task. Now,
Step1. Clone the given [click here: WEEK-3 LAB](https://github.com/hemanthkumardm/SFAL-VSD-SoC-Journey/tree/main/12.%20VSDBabySoC%20Project) or set up the directory structure as follows:
```bash
VSDBabySoC/
├── Makefile                 # Build rules (simulation, synthesis, etc.)
├── README.md                # Documentation for repo
├── src/                     # Source files
│   ├── include/             # Header / include files
│   │   ├── sandpiper.vh     # TL-Verilog to Verilog include
│   │   └── other headers... # e.g., common defines/macros
│   │
│   ├── module/              # Main RTL design modules
│   │   ├── vsdbabysoc.v     # Top-level SoC integrating all components
│   │   ├── rvmyth.v         # RISC-V core (RVMyth)
│   │   ├── avsdpll.v        # PLL module (frequency generator)
│   │   ├── avsddac.v        # DAC module
│   │   └── testbench.v      # Testbench for RTL simulation
│   |   └── others...
├── output/                  # Simulation/synthesis outputs
│   └── compiled_tlv/        # Compiled TL-Verilog files (from SandPiper)
|   └── pre_synth_sim
│
└── images/                    # (optional) Add for documentation, diagrams
    └── arch_diagram.png     # Example: SoC block diagram

``` 
# Step by step modeling walkthrough
## Cloning , Setup and  Directory structure
- Clone or set up the directory structure as follows:
 
### STEP 1. To begin, clone the VSDBabySoC repository using the following command:
```
$ git clone https://github.com/manili/VSDBabySoC.git
$ cd ~/vcd/VSDBabySoC/
$ ls VSDBabySoC/
images  LICENSE  Makefile  README.md  src
```
### STEP2: TLV to Verilog Conversion for RVMYTH
Initially, you will see only the rvmyth.tlv file inside src/module/, since the RVMYTH core is written in TL-Verilog.
To convert it into a .v file for simulation, follow the steps below:
🔧 TLV to Verilog Conversion Steps

```
# Step A: Install python3-venv (if not already installed)
sudo apt update
sudo apt install python3-venv python3-pip
cd VSDBabySoC/

# Step B: Create and activate a virtual environment
python3 -m venv my_env
source my_venv/bin/activate

# Step C: Install SandPiper-SaaS inside the virtual environment
pip install pyyaml click sandpiper-saas

# Step D: Convert rvmyth.tlv to Verilog
sandpiper-saas -i ./src/module/*.tlv -o rvmyth.v --bestsv --noline -p verilog --outdir ./src/module/
```
The above conversion will be reflected in the output director in `/src/module` it uses the tool Sandpiper for conversion.
- SandPiper is a code generator that generates readable, well-structured, Verilog or SystemVerilog code from the given TL-Verilog code.
- SandPiper SaaS Edition runs as a microservice in the cloud to support easy open-source development. Install Sanpiper SaaS Edition for this project.
- To run locally, SandPiper Education Edition can be requested from RedwoodEDA.

<img width="825" height="681" alt="Image" src="https://github.com/user-attachments/assets/a9123673-02c3-49e8-9d33-0c79844b5f22" />

# Pre-Synthesis Simulation:

Before synthesis, the RTL design was verified using a testbench (testbench.v) that instantiates the vsdbabysoc module and applies a series of stimulus to validate its functionality. The simulation was run using Icarus Verilog, and the waveform was inspected in GTKWave to ensure correct operation. the following command is executed while the paths to the current directory and the files required must be at available for proper execution without failure.

``` bash
$ cd ~/vsd/VSDBabySoC/
$ mkdir -p output/pre_synth_sim
$ pwd -> `/vsd/VSDBabySoC/`
$ iverilog -o ./output/pre_synth_sim/pre_synth_sim.out -DPRE_SYNTH_SIM -I ./src/include -I ./src/module ./src/module/testbench.v 
```  
- DPRE_SYNTH_SIM defines the macro PRE_SYNTH_SIM for conditional compilation., which can be used inside Verilog files like: 
- -I<directory>: Adds an include directory for Verilog source files that use \include "file.v"` directives.
- if we wont include the -I then it will lands to error for .Vh files and other verilog files which are called by top vsdbabysoc module.

<img width="818" height="219" alt="Image" src="https://github.com/user-attachments/assets/84e05ba5-afcf-45f1-a060-9900a0d918fd" />

- Now after including all the files we have output in the given `/pre_synth_sim` folder

<img width="829" height="252" alt="Image" src="https://github.com/user-attachments/assets/5255cf15-9bd1-4f50-8bf3-da26cbdc4c47" />

### Running the next step to generate the VCD file

<img width="824" height="237" alt="Image" src="https://github.com/user-attachments/assets/d821b28a-1504-483a-b8db-6c076b5c258d" />

### Invoking the GTKwave to see the RTL simulation Also making the output view for analog type data.

<img width="908" height="825" alt="Image" src="https://github.com/user-attachments/assets/9e044de4-8953-4e98-aae6-d95f586d4ed9" />


<img width="1149" height="502" alt="Image" src="https://github.com/user-attachments/assets/287b4432-0c1a-47a9-88a7-c0ae6ad73504" />

``` bash

read_liberty -lib src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_liberty -lib src/lib/avsddac.lib
read_liberty -lib src/lib/avsdpll.lib
read_verilog src/module/vsdbabysoc.v
read_verilog -I src/include src/module/rvmyth.v
read_verilog -I src/include src/module/clk_gate.v
read_verilog src/module/avsddac_stub.v
read_verilog src/module/avsdpll_stub.v
synth -top vsdbabysoc
dfflibmap -liberty src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
opt clean -purge
abc -liberty src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
flatten

write_verilog -noattr reports/vsdbabysoc_netlist.v
show vsdbabysoc
```

## Debugging the error 
### Error 1: Missing Include File

- Root Cause: The `rvmyth` core uses `include` directives to import Verilog header files (`.vh`). Yosys was not aware of the `src/include/` directory where these files are located.
- Resolution: Add the `-I src/include` flag to required read_verilog commands in the Yosys script. This tells Yosys to add that directory to its search path for header files.


