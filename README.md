## What is a SoC?
- In general an Integrated Circuit (aka IC) that integrates multiple components of asystem onto a single chip is SOC (System-on-Chip).
- In addition to IC, SoC consists of software and interconnection structure for integration.
- A System on a Chip (SoC) is like a mini-computer built on a single chip.
- Instead of having separate parts for each function, an SoC combines everything into one small package. In general, the design flow of SoCs consists of: Hardware and Software Modules
- Hardware blocks of SoCs are developed from pre-qualified hardware elements and software modules integrated using software development environmentThis makes it especially useful for devices where space, power, and efficiency are important, like smartphones, smartwatches, and tablets.

## What are the elements of a SoC?
> These components typically include:
- Processor cores -  CPU, GPU, DSP, etc.
- Memory - RAM, ROM, Cache.
- Appilication Binary Interface (ABI).
- Peripherals – USB, UART, SPI, I2C, etc.
- On-chip interconnection (busses, network, AMBA (AXI, AHB, APB), Network-on-Chip (NoC), etc.)
- Power Management – Voltage regulators, clock management.
- AI/O interfaces – GPIOs, ADC/DAC, etc.
- Custom Logic – Application-specific circuits (e.g., image processors, ML accelerators).
- if mixed signal soc then Analog circuits ae there.
- Software – OS, Application, etc.
- Firmware

<img width="908" height="642" alt="image" src="https://github.com/user-attachments/assets/3704c031-d2a2-446c-b9e9-0dfca6eed8d6" />

Components of a System-on-Chip

## SoC Design Tradeoffs:- Five Big Issues for SoC Design
- Time: Cycle time relates to Performance
- Chip Area: It also determines the IC cost
- Power Consumption: Performance as well as Implementation
- Reliability: It relates to deep submicron effects.
- Configurability: Standardization in manufacturingand customization for application.

## ## Why SoCs Are Awesome? 
- A System-on-Chip (SoC) is an integrated circuit that contains all the required electronic circuits for a fully functional system. 
- Designing SoCs involves hardware and software to control the processor, peripherals, and interfaces.
- **Space Saving**: By combining everything into one chip, SoCs help make devices smaller and more portable.
- **Energy Efficient**: Because all the parts are so close together, they use less power, which is especially important for battery-operated devices.
- **High Performance**: Since data doesn't have to travel far, SoCs can process information faster.
- **Cost Effective**: Building a single chip is often cheaper than using multiple parts, reducing the cost for manufacturers and, ultimately, for consumers.
- **Reliable**: Fewer parts mean fewer points of failure, making devices with SoCs generally more dependable.

### Where You’ll Find SoCs

- **Smartphones & Tablets**: Almost all modern mobile devices use SoCs because of their compact size and efficiency.
- **Wearables**: Devices like smartwatches rely on SoCs for their small size and low power use.
- **IoT Gadgets**: Internet of Things devices, like smart home sensors, often use SoCs to handle tasks like monitoring and connecting to Wi-Fi.
- **Cars, TVs, and More**: Embedded systems in cars, TVs, and appliances may also use SoCs to manage their internal functions

## SoC-based devices


<img width="585" height="564" alt="image" src="https://github.com/user-attachments/assets/0a91c063-fec9-4e37-8be5-76d0573d4f76" />


  
## What is the difference between a processor and a microprocessor?
### 🔸 Key Differences

| **Feature**     | **Processor**                                         | **Microprocessor**                                     |
|------------------|-------------------------------------------------------|--------------------------------------------------------|
| **Scope**        | General term for any data-processing unit             | Specific kind of processor on one chip                 |
| **Form factor**  | Can be multi-chip or multi-component                  | Always a single-chip solution                          |
| **Examples**     | CPU, GPU, DSP                                         | Intel Core i9, AMD Ryzen, ARM Cortex                   |
| **Used in**      | Computers, servers, devices                           | PCs, embedded systems, microcontrollers                |

### In Summary
- All microprocessors are processors, but not all processors are microprocessors.
- A microprocessor is a specific, modern implementation of a processor – compact and integrated into one chip.

## IV What is a computer architecture? 
### 🔸 Key Aspects of Computer Architecture

| **Component**                  | **Description**                                                                 |
|-------------------------------|---------------------------------------------------------------------------------|
| **Instruction Set Architecture (ISA)** | The set of instructions a processor can execute. Defines how software controls hardware. |
| **Microarchitecture**          | The internal design of the processor—how the components are arranged to implement the ISA. |
| **System Architecture**        | How all hardware components (CPU, memory, I/O) are connected and communicate.   |


<img width="930" height="347" alt="image" src="https://github.com/user-attachments/assets/914844ad-7cf5-4091-b2c2-e34ad268c3a2" />

Figure 1 General computer architecture with minimum of elements (global hardware view; Dec. = Decoder)

---
##  Steps in designing a SoC

<img width="654" height="669" alt="image" src="https://github.com/user-attachments/assets/be13f580-f93e-4192-b82e-04235b90bc9f" />


- But this include the various cost involved from die manufacturing to design to packaging.
<img width="309" height="37" alt="image" src="https://github.com/user-attachments/assets/c0233329-c0e1-4678-8648-bd335087b6a3" />





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

- SOCs usually have die sizes of about 10-15 mm on aside like our babySOC as shown in picture

<img width="1461" height="1467" alt="image" src="https://github.com/user-attachments/assets/5f5698c1-86e4-4eb1-ade0-db6e1051f14b" />


 [Basic Architecture of the VSDBabySoC — SoC based on RVMYTH ](https://github.com/manili/VSDBabySoC/tree/main)

## RVMYTH modeling

As we mentioned in [What is RVMYTH](#what-is-rvmyth) section, RVMYTH is designed and created by the TL-Verilog language. So we need a way for compile and trasform it to the Verilog language and use the result in our SoC. Here the `sandpiper-saas` could help us do the job.

1. [Here](https://github.com/shivanishah269/risc-v-core) is the repo we used as a reference to model the RVMYTH
2. [Here](https://github.com/vsdip/rvmyth_avsddac_interface?tab=readme-ov-file) is similar Repo which can also be looked upon for the same.

## PLL and DAC modeling

It is not possible to sythesis an analog design with Verilog, yet. But there is a chance to simulate it using `real` datatype. We will use the following repositories to model the PLL and DAC cores:

  1. [Here](https://github.com/vsdip/rvmyth_avsdpll_interface) is the repo we used as a reference to model the PLL
  2. [Here](https://github.com/vsdip/rvmyth_avsddac_interface) is the repo we used as a reference to model the DAC

**CAUTION:** In the beginning of the project, we get our verilog model of the PLL from [here](https://github.com/vsdip/rvmyth_avsdpll_interface). However, by proceeding the project to the physical design flow we realize that this model needs a little changes to become sufficient for a real IP core. So we changed it a little and created a new model named `AVSDPLL` based on [this](https://github.com/lakshmi-sathi/avsdpll_1v8) IP.


-

