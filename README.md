# VSDBabySoC
VSDBabySoC is a small yet powerful RISCV-based SoC. The main purpose of designing such a small SoC is to test three open-source IP cores .


RISC-V's open architecture enables us to create processors highly tailored for specific
computational challenges. 


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

Icarus Verilog is a Verilog simulation and synthesis tool.

3. GTKWave:

GTKWave is a waveform viewer.
