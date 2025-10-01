# VSDBabySoC Simulation and Syntheis 
## Week 3 LAB Task – VSDBabySoC
### 1. Basic RTL Simulation
- **Goal**: Verify functionality of the SoC design before synthesis.
- **Tools**: iverilog and gtkwave
- **Steps**: Compile the RTL + Testbench:

## RVMYTH CORE SIMULATION
I tried the individual component to simulate and later synthesis to understand the BABYVSDsoc completely. In that task when I simulated the files the RTL anaysis is mathching the 


## LAB TASK WORK VSDBABYSoC

### 1. Requirements
Ensure you have Icarus Verilog installed for compilation and GTKWave for viewing waveform files. This project assumes a Unix-like environment (macOS/Linux).
Step1. Clone the given [click here: WEEK-3 LAB](https://github.com/hemanthkumardm/SFAL-VSD-SoC-Journey/tree/main/12.%20VSDBabySoC%20Project) or set up the directory structure as follows:
```verilog
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
│
├── output/                  # Simulation/synthesis outputs
│   └── compiled_tlv/        # Compiled TL-Verilog files (from SandPiper)
│
└── docs/                    # (optional) Add for documentation, diagrams
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
