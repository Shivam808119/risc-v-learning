# RISC-V and FPGA Learning Documentation

This document explains the important concepts discussed: RISC-V, CPU cores, firmware, OpenR5, FPGA workflow, verification, memory, security, interfaces, benchmarks, and the scope of learning.

---

# PART 1 — RISC-V FUNDAMENTALS

## 1. What is RISC-V?

RISC-V is an open-standard instruction set architecture, or ISA. An ISA defines the instructions that a processor can understand and execute.

RISC-V is not a processor or chip by itself. It is a specification. Different companies, universities, and developers can build their own processor cores that implement the same RISC-V instructions.

RISC-V is pronounced “risk-five.”

### Key features

- Open standard ISA
- Modular design
- Supports 32-bit and 64-bit implementations
- Allows standard and custom extensions
- No ISA-level royalty
- Suitable for embedded systems, microcontrollers, SoCs, AI accelerators, and servers

### RISC-V base ISAs

| Base ISA | Meaning |
|---|---|
| RV32I | 32-bit integer base instruction set |
| RV64I | 64-bit integer base instruction set |
| RV32E | Reduced embedded 32-bit variant |
| RV64E | Reduced embedded 64-bit variant |

### Common extensions

| Extension | Purpose |
|---|---|
| M | Integer multiplication and division |
| A | Atomic memory operations |
| F | Single-precision floating point |
| D | Double-precision floating point |
| C | Compressed instructions |
| V | Vector processing |
| Zicsr | Control and status registers |
| Zifencei | Instruction-fetch synchronization |

A name such as RV64GC generally means a 64-bit RISC-V processor with general-purpose extensions, including compressed instructions and floating-point support.

## 2. RISC-V history

RISC-V began at the University of California, Berkeley, around 2010. Early contributors included Krste Asanović, Andrew Waterman, Yunsup Lee, and David Patterson.

Important milestones:

- 2010: RISC-V project began at UC Berkeley.
- 2011: First RISC-V processors were fabricated.
- 2015: RISC-V Foundation was founded.
- 2020: The organization became RISC-V International.
- Present: RISC-V is used in embedded systems, IoT, automotive, AI accelerators, and data-center projects.

RISC-V was created to provide an open, modular, and extensible ISA that avoids dependence on one company’s proprietary architecture.

## 3. Privilege modes

RISC-V has privilege levels that separate software responsibilities:

| Mode | Purpose |
|---|---|
| Machine mode, M-mode | Highest privilege; firmware, boot code, low-level control |
| Supervisor mode, S-mode | Operating-system kernel mode |
| User mode, U-mode | Normal applications |

Firmware commonly runs in M-mode. An operating system such as Linux may run in S-mode, while applications run in U-mode.

---

# PART 2 — CPU CORE AND FIRMWARE

## 4. What is a CPU core?

A CPU is the processor chip. A CPU core is one independent processing unit inside that CPU.

A core reads instructions, decodes them, performs operations, and writes results.

### Main parts of a core

| Part | Purpose |
|---|---|
| Control unit | Controls instruction execution |
| Registers | Small, fast storage inside the CPU |
| ALU | Performs arithmetic and logic operations |
| Cache | Small, fast memory near the core |
| Execution units | Perform integer, floating-point, load/store, and branch operations |

### Instruction execution cycle

```text
Fetch instruction
→ Decode instruction
→ Execute operation
→ Access memory if needed
→ Write result back
```

A RISC-V core is a CPU core that implements the RISC-V instruction set.

### CPU vs core vs thread

| Term | Meaning |
|---|---|
| CPU | The complete processor chip |
| Core | One independent processing unit inside the CPU |
| Thread | A stream of work executed by a core |
| Clock speed | Number of cycles per second |

A CPU with 8 cores can handle more independent work than a single-core CPU, provided the software can use multiple cores.

## 5. What is firmware?

Firmware is low-level software stored inside a hardware device, usually in non-volatile memory such as flash. It remains stored even when power is removed.

Firmware tells hardware how to start, control its components, and communicate with other hardware.

### Examples of firmware

- BIOS/UEFI in computers
- Bootloader in embedded boards
- Microcontroller programs
- SSD controller firmware
- Wi-Fi or Bluetooth module firmware
- Smartwatch, drone, router, and camera firmware

### Firmware in a RISC-V system

```text
Power on
→ Boot ROM or bootloader
→ Firmware initializes CPU, memory, clocks, peripherals
→ Firmware loads an OS or runs an embedded application
→ Application runs
```

Firmware often runs in RISC-V Machine mode. It may provide services to the operating system through interfaces such as the Supervisor Binary Interface, or SBI.

### Firmware vs normal software

| Firmware | Normal software |
|---|---|
| Controls and initializes hardware | Provides user-facing features |
| Stored in flash or ROM | Installed on storage and run by an OS |
| Close to specific hardware | Usually works through an operating system |
| Examples: bootloader, BIOS, motor-control code | Examples: browser, app, Python program |

---

# PART 3 — OPENR5

## 6. What is OpenR5?

OpenR5 is a family of RISC-V processor cores from OR5 Labs. The website describes it as a family of 19 RISC-V processor cores.

OpenR5 includes RTL designs, testbenches, documentation, verification support, FPGA flows, and benchmark examples.

### Publicly linked cores

The OpenR5 website publicly links three cores:

| Core | Repository |
|---|---|
| Kavacha | https://github.com/OR5-LABS/kavacha |
| Takshaka | https://github.com/OR5-LABS/takshaka |
| Gandiva | https://github.com/OR5-LABS/gandiva |

### Full 19-core family

| Core | Purpose |
|---|---|
| Kavacha | Small secure multi-cycle RV32IMC core |
| Takshaka | 3-stage pipelined RV32IMACB core |
| Gandiva | 5-stage pipelined RV32IMACB core |
| Vajra | Microcontroller SoC |
| Trishul | 64-bit application-class SoC |
| Netra | Root-of-trust core |
| Kavacha-FT | Fault-tolerant controller |
| Paasha | Hardware memory-safety core |
| Sharanga | Vector and SIMD core |
| Surya | SIMT many-lane core |
| Prajna | Machine-learning inference core |
| Naada | Digital signal processing core |
| Setu | Packet-processing core |
| Meru | Multi-hart shared-memory core |
| Chakra | Superscalar core |
| Garuda | Out-of-order completion core |
| Agni | Floating-point embedded core |
| Brahmastra | Family-integration design |
| Nandaka | IEEE-754 floating-point unit |

Only Kavacha, Takshaka, and Gandiva have clearly public repository links on the website. The remaining cores are listed by name, but their source is described as “available on request.”

Therefore, “18 cores” or “19 cores” likely refers to the OpenR5 family, not necessarily 19 repositories personally built by the seniors.

## 7. Who made OpenR5?

OpenR5 is presented as a project by OR5 Labs. The website footer identifies it as “OpenR5 — RISC-V processor cores by OR5 Labs.”

The website does not publicly name individual founders, team members, or a college. Therefore, it cannot be confirmed from the website alone that college students created it.

The site may be maintained by a small company, research group, independent developers, or a college-affiliated team using a separate brand name.

---

# PART 4 — FPGA DESIGN FLOW

## 8. FPGA workflow

The tasks assigned in the spreadsheet follow the standard FPGA development flow:

```text
Understand the RISC-V core
→ Simulate the design
→ Synthesize the design
→ Place and route
→ Verify timing
→ Generate bitstream
→ Program FPGA board
→ Test through serial terminal
→ Measure resource use and performance
```

### Simulation

Simulation checks whether the RTL design behaves correctly before it is implemented on hardware. A testbench provides inputs, observes outputs, and compares actual behavior with expected behavior.

### Synthesis

Synthesis converts Verilog or SystemVerilog RTL into logic gates and FPGA resources.

### Place and route

Place and route decides where logic elements are placed on the FPGA and how wires connect them.

### Timing verification

Timing analysis checks whether signals arrive at the correct time for the chosen clock frequency. A design can be functionally correct in simulation but fail timing on real hardware.

### Bitstream

A bitstream is the configuration file that programs an FPGA. It tells the FPGA how its internal resources should be connected and configured.

### Serial debugging

PuTTY or another serial terminal can connect to an FPGA board through UART. It is used to view logs, test results, boot messages, and program output.

## 9. FPGA resources

| Resource | Full form | Purpose |
|---|---|---|
| LUT | Look-Up Table | Implements combinational logic |
| FF | Flip-Flop | Stores one bit; used for registers and state |
| DSP | Digital Signal Processing block | Fast multiply-accumulate operations |
| BRAM | Block RAM | On-chip memory for data, instructions, buffers, and caches |

Resource utilization shows how much of the FPGA the design consumes. Lower resource use can allow a design to fit on a smaller or cheaper FPGA.

## 10. Libero and PolarFire SoC

Libero is Microchip’s FPGA design software. It is used for project creation, synthesis, place and route, timing analysis, bitstream generation, and programming Microchip FPGA devices.

PolarFire SoC is a FPGA family that includes RISC-V processor capability. Running a RISC-V core on a PolarFire SoC involves building the design, programming the board, and testing its behavior.

---

# PART 5 — VERIFICATION AND TESTING

## 11. Verification tasks

The assigned verification tasks include:

- Build and configuration testing
- Smoke test
- Functional verification
- Golden-model co-simulation
- Debug module testing
- PMP and ePMP testing
- U-mode and MML testing
- Register-file ECC testing
- AXI4-Lite testing
- ISA tests
- Full regression
- CoreMark
- Dhrystone

### Smoke test

A smoke test checks whether the basic system works. It does not prove every feature is correct, but it confirms that the design builds, runs, and produces basic expected output.

### Functional verification

Functional verification checks whether the processor behaves according to its specification. It tests instructions, memory access, branches, interrupts, exceptions, and other behavior.

### Golden-model co-simulation

A golden model is a trusted reference model. The RTL design and the golden model execute the same program. If their results differ, the RTL may contain a bug.

### Regression testing

Regression testing reruns many tests after changes are made. It ensures that a new change did not break previously working features.

### Debug module

A debug module allows developers to inspect and control a processor during development. It may support halting execution, reading registers, setting breakpoints, and loading programs.

## 12. Security-related verification

| Test | Meaning |
|---|---|
| PMP | Physical Memory Protection |
| ePMP | Enhanced Physical Memory Protection |
| U-mode | User-mode execution |
| MML | Machine Mode Lockdown |
| Register-file ECC | Error-correcting code for register storage |
| AXI4-Lite | Memory-mapped peripheral interface |

PMP restricts which memory regions software can access. ePMP provides enhanced memory-protection features. ECC detects and may correct memory bit errors. These features are important for secure and reliable systems.

---

# PART 6 — COMPUTER ARCHITECTURE

## 13. Pipelining

Pipelining divides instruction execution into stages so multiple instructions can be processed at different stages simultaneously.

Common stages:

```text
Fetch → Decode → Execute → Memory → Writeback
```

Pipelining improves throughput but introduces hazards.

### Hazards

| Hazard | Meaning |
|---|---|
| Data hazard | An instruction needs a result that has not yet been written |
| Control hazard | A branch changes the expected instruction flow |
| Structural hazard | Two instructions need the same hardware resource at the same time |

### Solutions

- Forwarding passes results directly between pipeline stages.
- Stalls pause the pipeline until data is ready.
- Bubbles are empty pipeline stages inserted during stalls.
- Branch prediction guesses the direction of a branch to reduce delays.

## 14. Performance

Performance depends on several factors:

| Factor | Meaning |
|---|---|
| CPI | Cycles per instruction |
| Clock frequency | Number of clock cycles per second |
| Fmax | Maximum stable clock frequency |
| IPC | Instructions per cycle |

A simple relationship is:

```text
Performance depends on instructions, CPI, and clock frequency
```

A processor with a higher clock frequency is not always faster if it requires more cycles per instruction or has a weaker memory system.

## 15. Memory hierarchy

Memory hierarchy balances speed, size, and cost:

```text
Registers
→ Cache
→ Main memory
→ Storage
```

### Cache

A cache stores frequently used data close to the CPU. It improves performance when programs reuse the same data or access nearby memory locations.

Important cache concepts:

- Cache hit
- Cache miss
- Cache line
- Temporal locality
- Spatial locality
- Replacement policy
- Write-through and write-back

### Virtual memory

Virtual memory gives each process its own address space. It isolates programs from each other and allows the operating system to manage memory more flexibly.

### TLB

The Translation Lookaside Buffer, or TLB, stores recent virtual-to-physical address translations. It speeds up virtual-memory address translation.

### Coherence and consistency

Cache coherence ensures that multiple cores see a consistent view of shared memory. Memory consistency defines the order in which memory operations appear to occur.

### NUMA

NUMA means Non-Uniform Memory Access. In NUMA systems, a processor can access some memory faster than other memory depending on physical location.

## 16. Advanced CPU concepts

| Concept | Meaning |
|---|---|
| In-order execution | Instructions execute in program order |
| Out-of-order execution | Instructions may execute when their inputs are ready |
| Superscalar | Multiple instructions can be issued in one cycle |
| ILP | Instruction-level parallelism |
| Reorder buffer | Tracks instructions until they can safely complete |
| Branch prediction | Predicts branch direction to reduce pipeline stalls |

---

# PART 7 — INTERFACES AND PROTOCOLS

## 17. External interfaces

| Interface | Purpose |
|---|---|
| UART | Serial communication and debugging |
| GPIO | General-purpose input/output pins |
| SPI | High-speed serial communication |
| I2C | Low-speed communication with sensors and peripherals |
| JTAG | Debugging and programming hardware |

### UART

UART is commonly used to connect an FPGA board to a computer terminal. It is useful for viewing boot messages, logs, and program output.

### GPIO

GPIO pins can be configured as inputs or outputs. They are used for buttons, LEDs, sensors, and simple control signals.

### SPI

SPI is a high-speed serial protocol used for displays, flash memory, sensors, and other peripherals.

### I2C

I2C is a two-wire protocol used to communicate with sensors, EEPROMs, and other low-speed devices.

## 18. Internal interfaces

| Interface | Purpose |
|---|---|
| AXI | High-performance on-chip interconnect |
| AXI4-Lite | Simpler memory-mapped control interface |
| AHB/APB | Other common on-chip bus protocols |
| RVFI | RISC-V Formal Interface for verification |

AXI4-Lite is often used to connect a RISC-V core to peripherals such as UART, GPIO, timers, and control registers.

---

# PART 8 — BENCHMARKS

## 19. What are benchmarks?

Benchmarks measure processor performance using defined workloads. They help compare different cores, configurations, compilers, and hardware platforms.

### Common benchmarks

| Benchmark | Purpose |
|---|---|
| CoreMark | Modern embedded-processor benchmark |
| Dhrystone | Older integer-performance benchmark |
| EMBench | Embedded benchmark suite |
| Fmax | Maximum stable clock frequency |

### Important benchmark rules

A benchmark result is meaningful only when the comparison is fair:

- Same compiler and compiler flags
- Same ISA extensions
- Same memory system
- Same FPGA board or silicon target
- Same measurement method
- Same workload and input data

A higher number does not automatically mean a better processor if the test conditions differ.

---

# PART 9 — SCOPE: WHAT YOU NEED TO LEARN

## 20. Learning sequence

### Stage 1 — Digital logic

Learn:

- Binary, hexadecimal, and two’s complement
- Logic gates
- Multiplexers and decoders
- Flip-flops and latches
- Registers
- Finite-state machines
- Timing diagrams

### Stage 2 — Computer organization

Learn:

- CPU structure
- Registers
- ALU
- Memory
- Buses
- Instructions
- Interrupts
- Input/output

### Stage 3 — RISC-V ISA

Learn:

- RISC-V registers
- Instruction formats
- Arithmetic instructions
- Logic instructions
- Load and store instructions
- Branches and jumps
- Function calls
- Calling convention and ABI
- CSRs
- Privilege modes

### Stage 4 — Processor microarchitecture

Learn:

- Single-cycle CPU
- Multi-cycle CPU
- Pipelined CPU
- Pipeline stages
- Data hazards
- Control hazards
- Structural hazards
- Forwarding
- Stalls and bubbles
- Branch prediction
- Caches
- Virtual memory
- TLB
- Memory protection

### Stage 5 — Verification

Learn:

- Testbenches
- Simulation
- Waveform debugging
- Assertions
- Golden-model co-simulation
- Regression testing
- Coverage
- ISA compliance testing
- RVFI

### Stage 6 — FPGA implementation

Learn:

- RTL coding
- Synthesis
- Place and route
- Timing constraints
- Static timing analysis
- Fmax
- Resource utilization
- Bitstream generation
- FPGA programming
- Serial debugging
- Board bring-up

### Stage 7 — SoC and interfaces

Learn:

- SoC architecture
- Memory map
- Interconnects
- AXI, AXI-Lite, APB, AHB
- UART, GPIO, SPI, I2C
- Interrupt controllers
- DMA
- Peripherals
- Boot flow

### Stage 8 — Security

Learn:

- Privilege modes
- PMP
- ePMP
- MML
- Secure boot
- Root of trust
- ECC
- Debug security
- Memory isolation
- Common hardware attack concepts

### Stage 9 — AI hardware concepts

Learn:

- Vector processing
- SIMD
- Matrix operations
- Quantization
- Inference latency
- Throughput
- Memory bandwidth
- Edge AI
- AI accelerators
- Hardware-software co-design

## 21. How to study the 10 cores

For each core, prepare a one-page analysis:

1. Core name
2. Purpose
3. Base ISA and extensions
4. Pipeline type
5. Register file structure
6. Memory structure
7. Peripherals
8. Interconnect
9. Security features
10. Verification tests
11. Benchmarks
12. FPGA resource utilization
13. Strengths
14. Limitations
15. Real-world use cases

Ask these questions for every core:

- What problem does this core solve?
- What type of processor is it?
- How does it execute instructions?
- How does it access memory?
- How does it connect to peripherals?
- What security features does it include?
- How is it verified?
- What benchmark results are available?
- How much FPGA area does it use?
- Where could it be used in real life?

## 22. Practical task checklist

Complete these tasks in order:

- [ ] Install required tools
- [ ] Clone one RISC-V core repository
- [ ] Read its documentation
- [ ] Understand its top-level module
- [ ] Run simulation
- [ ] Read simulation waveforms
- [ ] Run smoke tests
- [ ] Run ISA tests
- [ ] Run regression tests
- [ ] Run golden-model co-simulation
- [ ] Run CoreMark
- [ ] Run Dhrystone
- [ ] Run synthesis
- [ ] Check LUT usage
- [ ] Check FF usage
- [ ] Check DSP usage
- [ ] Check BRAM usage
- [ ] Run place and route
- [ ] Verify timing
- [ ] Find Fmax
- [ ] Generate bitstream
- [ ] Program FPGA board
- [ ] Connect using PuTTY
- [ ] Observe output
- [ ] Document the complete flow

## 23. Documentation template

For every completed task, write:

```text
Task name:
Date:
Core used:
Tools used:
Steps performed:
Commands used:
Expected result:
Actual result:
Problems faced:
How problems were solved:
Resource utilization:
Benchmark result:
Screenshots or waveforms:
What I learned:
```

## 24. Important distinctions

| Term | Meaning |
|---|---|
| ISA | Defines instructions |
| Microarchitecture | Defines how a specific CPU implements instructions |
| RTL | Register-transfer-level hardware description |
| Simulation | Checks functional behavior |
| Synthesis | Converts RTL into hardware logic |
| Bitstream | FPGA configuration file |
| Fmax | Maximum stable clock frequency |
| Verification | Proves design correctness |
| Validation | Checks whether the system meets intended requirements |

## 25. Core types

| Core type | Meaning |
|---|---|
| Single-cycle | One instruction completes in one clock cycle |
| Multi-cycle | One instruction takes multiple clock cycles |
| Pipelined | Multiple instructions are processed in overlapping stages |
| Superscalar | Multiple instructions can be issued per cycle |
| In-order | Instructions complete in program order |
| Out-of-order | Instructions may complete when dependencies are ready |
| Vector/SIMD | One instruction operates on multiple data elements |
| Multi-hart | Multiple hardware threads or cores exist in one design |

---

# PART 10 — CAREER SCOPE

## 26. Career areas

RISC-V and FPGA knowledge can lead to work in:

| Area | Typical work |
|---|---|
| RTL design | Writing Verilog/SystemVerilog for CPUs and digital blocks |
| Design verification | Testing hardware correctness using simulation and formal methods |
| FPGA engineering | Implementing and testing designs on FPGA boards |
| Embedded systems | Programming microcontrollers and embedded devices |
| SoC design | Integrating CPUs, memory, peripherals, and interconnect |
| Physical design | Converting designs into manufacturable chip layouts |
| AI hardware | Building accelerators and edge-AI systems |
| Semiconductor research | Improving processor architecture, security, and performance |

## 27. Important skills

| Skill | Why it matters |
|---|---|
| Digital logic | Foundation for all hardware design |
| Verilog/SystemVerilog | Used to describe hardware |
| C programming | Used for firmware, tests, and embedded software |
| RISC-V assembly | Helps understand instruction execution |
| Computer architecture | Needed to design and optimize processors |
| Verification | Ensures hardware works correctly |
| FPGA tools | Needed to implement designs on real hardware |
| Linux and RTOS | Needed for system software and embedded products |
| Scripting | Automates simulation, synthesis, and testing |
| Documentation | Needed for teamwork and professional engineering |

## 28. Simple learning rule

Do not only read theory. Follow this pattern:

```text
Read a concept
→ See it in RTL code
→ Run a simulation
→ Observe waveforms or output
→ Write short notes
→ Explain it to someone else
```

This converts theory into practical understanding.

## 29. Final scope summary

The main things to learn are:

1. Digital logic
2. Computer organization
3. RISC-V ISA
4. Processor microarchitecture
5. Pipelining and hazards
6. Memory hierarchy
7. Virtual memory
8. Security and memory protection
9. Verification
10. FPGA implementation
11. SoC design
12. Interfaces and protocols
13. Benchmarks
14. AI hardware concepts
15. Technical documentation

These topics together explain how a RISC-V instruction becomes a working system on an FPGA board.
