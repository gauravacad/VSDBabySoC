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
│
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


## RVMYTH modeling

As we mentioned in [What is RVMYTH](#what-is-rvmyth) section, RVMYTH is designed and created by the TL-Verilog language. So we need a way for compile and trasform it to the Verilog language and use the result in our SoC. Here the `sandpiper-saas` could help us do the job.

1. [Here](https://github.com/shivanishah269/risc-v-core) is the repo we used as a reference to model the RVMYTH
2. [Here](https://github.com/vsdip/rvmyth_avsddac_interface?tab=readme-ov-file) is similar Repo which can also be looked upon for the same.

## PLL and DAC modeling

It is not possible to sythesis an analog design with Verilog, yet. But there is a chance to simulate it using `real` datatype. We will use the following repositories to model the PLL and DAC cores:

  1. [Here](https://github.com/vsdip/rvmyth_avsdpll_interface) is the repo we used as a reference to model the PLL
  2. [Here](https://github.com/vsdip/rvmyth_avsddac_interface) is the repo we used as a reference to model the DAC

**CAUTION:** In the beginning of the project, we get our verilog model of the PLL from [here](https://github.com/vsdip/rvmyth_avsdpll_interface). However, by proceeding the project to the physical design flow we realize that this model needs a little changes to become sufficient for a real IP core. So we changed it a little and created a new model named `AVSDPLL` based on [this](https://github.com/lakshmi-sathi/avsdpll_1v8) IP
