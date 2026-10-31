# RISC-V, FPGA, and AI Startup Learning Plan
**Prepared for:** A student founder interested in AI products, with a side interest in RISC-V/FPGA hardware  
**Date:** October 31, 2026

---

# PART 1 — WHAT YOU NEED TO LEARN AND HOW

## 1. Your main goal

Your primary goal is to build an AI product/startup that solves a real problem for real users.  
Your secondary goal is to understand RISC-V, processor cores, memory, security, and FPGA workflows deeply enough to become a stronger technical founder and keep hardware/AI-hardware career options open.

You do **not** need to become a full-time chip designer unless you later decide to build AI hardware. But the tasks assigned by your seniors are genuinely valuable because they teach how software instructions become working hardware.

## 2. Is the assigned work relevant?

Yes. The tasks cover the standard path from RISC-V RTL to a working FPGA system:

```text
Understand RISC-V core
→ Simulate
→ Synthesize
→ Place and route
→ Verify timing
→ Generate bitstream
→ Program FPGA board
→ Test through serial terminal
→ Measure performance and resources
```

This is relevant to careers in:

- RTL design
- Design verification
- FPGA engineering
- Embedded systems
- SoC design
- AI accelerators and edge AI
- Semiconductor research and development

## 3. What each assigned task means

### A. Run MIST-ES on PolarFire SoC

This means running a RISC-V-based design or system on a Microchip PolarFire SoC FPGA board. You will learn board setup, FPGA programming, embedded software, and hardware-software interaction.

### B. Find LUT, FF, DSP, and BRAM

These are FPGA resources:

| Resource | Full form | Purpose |
|---|---|---|
| LUT | Look-Up Table | Implements combinational logic |
| FF | Flip-Flop | Stores one bit; used for registers and state |
| DSP | Digital Signal Processing block | Fast multiply-accumulate operations; useful for DSP and AI |
| BRAM | Block RAM | On-chip memory for data, instructions, caches, buffers |

Finding these tells you how much FPGA area and memory your core consumes.

### C. Make a script to run the core in Libero

Libero is Microchip’s FPGA design suite. A script automates steps such as:

- Creating a project
- Adding RTL files
- Running synthesis
- Running place and route
- Checking timing
- Generating a bitstream
- Programming the board

Automation is important because real hardware teams repeat these steps many times.

### D. Build/configuration testing

This means checking whether the processor builds correctly with different configuration options, such as:

- RV32I vs RV32IMC
- With or without floating point
- With or without debug module
- With or without security features
- Different memory or peripheral configurations

### E. Smoke test

A smoke test checks whether the most basic system works:

- Does it compile?
- Does it simulate?
- Does it load onto hardware?
- Does it produce expected basic output?

It does not prove everything works; it proves the system is not completely broken.

### F. Functional verification

Functional verification checks whether the processor behaves according to its specification. For example:

- Does `add` actually add?
- Does a branch jump correctly?
- Does load/store access memory properly?
- Do interrupts work?

### G. Golden-model co-simulation

A golden model is a trusted reference model of the processor. The RTL design and the golden model run the same instructions. If their outputs differ, there may be a hardware bug.

This is a professional verification method.

### H. Debug module

The debug module lets engineers inspect and control the processor during development. It can read registers, halt execution, set breakpoints, and load programs.

### I. PMP and ePMP

- **PMP:** Physical Memory Protection. It restricts which memory regions software can access.
- **ePMP:** Enhanced PMP. It adds more flexible memory-protection features.

These are important for secure embedded systems.

### J. U-mode and MML

- **U-mode:** User mode, where normal applications run.
- **MML:** Machine Mode Lockdown, a security feature that restricts certain privileged operations.

These topics relate to privilege separation and system security.

### K. Register-file ECC

ECC means Error-Correcting Code. It detects and sometimes corrects memory bit errors. In a processor, ECC on the register file improves reliability, especially in automotive, space, industrial, and safety-critical systems.

### L. AXI4-Lite

AXI4-Lite is a simple memory-mapped interface protocol used to connect a CPU to peripherals such as UART, GPIO, timers, and control registers.

### M. ISA tests and regression

ISA tests check whether the processor correctly implements RISC-V instructions. Regression testing reruns many tests after changes to ensure nothing broke.

### N. CoreMark and Dhrystone

These are benchmark programs used to measure processor performance.

- **CoreMark:** Modern, widely used embedded-processor benchmark.
- **Dhrystone:** Older integer-performance benchmark.
- **EMBench:** Another embedded benchmark suite.
- **Fmax:** Maximum stable clock frequency after timing analysis.

Benchmarks are useful, but they must be compared fairly: same compiler flags, same memory system, same board, and same measurement method.

### O. Computer-architecture topics

You are also expected to learn:

- Pipelining
- Hazards, stalls, bubbles
- CPI, clock frequency, Fmax
- Caches and memory hierarchy
- Virtual memory and TLB
- Cache coherence and consistency
- NUMA
- Memory protection
- Branch prediction
- Forwarding
- In-order vs out-of-order execution
- Superscalar processors
- Instruction-level parallelism
- Reorder buffer

These are core computer-architecture concepts.

### P. Interfaces and protocols

You must understand both external and internal hardware interfaces:

| Interface | Use |
|---|---|
| UART | Serial communication and debugging |
| GPIO | General-purpose input/output pins |
| SPI | High-speed serial communication with sensors, displays, flash |
| I2C | Low-speed communication with sensors and peripherals |
| AXI/AXI-Lite | On-chip interconnect for CPUs, memory, and peripherals |
| JTAG | Debugging and programming hardware |

## 4. What you should learn first

Do not try to learn everything at once. Follow this order:

### Stage 1 — Foundations

1. Digital logic: gates, flip-flops, registers, multiplexers, finite-state machines.
2. Binary, hexadecimal, two’s complement.
3. C programming.
4. Basic RISC-V assembly.
5. Computer organization: CPU, memory, buses, instructions.

### Stage 2 — RISC-V basics

1. RISC-V registers.
2. Instruction formats.
3. Arithmetic and logic instructions.
4. Load/store instructions.
5. Branches and jumps.
6. Function calls and ABI.
7. Machine mode, supervisor mode, user mode.
8. CSRs and interrupts.

### Stage 3 — Core understanding

1. Fetch, decode, execute, memory, writeback stages.
2. Single-cycle vs multi-cycle vs pipelined CPUs.
3. Hazards: data hazards, control hazards, structural hazards.
4. Forwarding and stalls.
5. Branch prediction.
6. Memory hierarchy: registers, cache, main memory.
7. Virtual memory and TLB.
8. Memory protection: PMP/ePMP.

### Stage 4 — Verification

1. What a testbench is.
2. Simulation waveform reading.
3. Assertions.
4. Golden-model co-simulation.
5. Regression testing.
6. Coverage.
7. Debugging failing tests.

### Stage 5 — FPGA implementation

1. Synthesis.
2. Place and route.
3. Timing constraints and timing analysis.
4. Fmax.
5. Resource utilization: LUT, FF, DSP, BRAM.
6. Bitstream generation.
7. Programming an FPGA.
8. Serial debugging with PuTTY.

### Stage 6 — Systems and AI hardware

1. SoC architecture.
2. Interconnects and protocols.
3. Peripherals.
4. Embedded Linux or RTOS.
5. Edge AI concepts.
6. Vector/SIMD processing.
7. AI accelerator basics.
8. Quantization and inference performance.

## 5. Your realistic weekly plan

Because your main priority is your AI startup, do not give RISC-V a full day. Use a fixed side-track schedule.

### Weekly target: 4–6 hours

| Day | Time | Task |
|---|---|---|
| Monday | 45–60 min | Read one concept and make short notes |
| Tuesday | 45–60 min | Run one simulation or inspect one RTL module |
| Thursday | 45–60 min | Do one practical task: build, test, or debug |
| Saturday | 90 min | Complete one deliverable |
| Sunday | 15–20 min | Review and plan next week |

### Monthly milestones

| Month | Goal |
|---|---|
| Month 1 | Understand RISC-V basics; run one core simulation; explain fetch-decode-execute |
| Month 2 | Understand pipelining, hazards, caches; run ISA tests and CoreMark |
| Month 3 | Complete FPGA flow: synthesis, place-route, timing, bitstream, board test |
| Month 4 | Analyze one OpenR5 core deeply; create documentation |
| Month 5 | Build or modify a small feature; measure resource use and performance |
| Month 6 | Connect RISC-V knowledge to an AI use case: edge inference, vector processing, or accelerator concept |

## 6. How to study each core

For every core, create a one-page note:

1. Core name and purpose
2. Base ISA and extensions
3. Pipeline type
4. Register file and memory structure
5. Peripherals and interconnect
6. Security features
7. Verification tests
8. Benchmarks
9. FPGA resource use
10. Strengths and weaknesses

Do not merely read. After each core, answer:

- What problem does this core solve?
- What makes it different from the previous core?
- What would break if I removed one feature?
- How would I test it?
- Where could it be used in real life?

## 7. How this connects to your AI startup

You do not need custom hardware to start an AI company. Start with software, users, and a real problem.

But RISC-V knowledge becomes valuable if your product needs:

- Offline or on-device AI
- Privacy-preserving inference
- Low-power devices
- Robots, drones, cameras, or industrial systems
- Real-time control
- Custom sensors
- Edge AI accelerators

The correct startup sequence is:

```text
Find a painful repeated problem
→ Talk to users
→ Build a small AI software MVP
→ Get real users and feedback
→ Improve accuracy and workflow
→ Consider edge/hardware only if necessary
```

## 8. Career paths from this learning

| Path | Main skills | Typical roles |
|---|---|---|
| RTL design | Verilog/SystemVerilog, architecture, synthesis | RTL engineer, CPU design engineer |
| Verification | UVM, assertions, simulation, coverage | DV engineer, verification lead |
| FPGA | Vivado/Libero, timing, board bring-up | FPGA engineer, prototyping engineer |
| Embedded | C, RTOS, Linux, peripherals | Embedded software engineer |
| SoC design | Interconnect, memory, peripherals, integration | SoC design/integration engineer |
| AI hardware | Vector extensions, accelerators, memory systems | AI accelerator engineer |
| AI startup | Product, users, AI APIs, data, deployment | Founder, AI product engineer |

## 9. Important principles

- Do not confuse **ISA** with **microarchitecture**. ISA defines instructions; microarchitecture defines how a specific CPU implements them.
- Do not trust a benchmark without knowing compiler flags, memory system, board, and baseline.
- Simulation proves functional correctness, not final hardware speed.
- A design can pass simulation but fail timing on real hardware.
- Security is not one feature; it includes privilege separation, memory protection, secure boot, debug control, and reliable updates.
- Documentation is part of engineering. If you cannot explain it, you do not fully understand it.

---

# PART 2 — SUMMARY OF OUR CONVERSATION

## 1. RISC-V basics

RISC-V is an open-standard instruction set architecture, or ISA. It defines the instructions a processor can understand. It is not itself a chip; companies and students can build different processor cores that implement the same ISA.

RISC-V is modular:

- Base ISA: RV32I or RV64I
- Extensions: M, A, F, D, C, V, and others
- Profiles: standardized combinations for particular product classes
- Custom extensions: organization-specific instructions

RISC-V began at UC Berkeley around 2010 and became an international open standard through RISC-V International. Its major advantages are openness, customization, scalability, and no ISA-level royalty.

## 2. CPU core meaning

A CPU is the processor chip. A **core** is one independent processing unit inside that CPU. Each core fetches, decodes, executes, and writes back instructions.

A RISC-V core is a CPU core that implements the RISC-V instruction set.

Example:

```text
CPU chip = office building
Core = one worker inside the building
Instruction = task given to the worker
Firmware = instructions stored inside the device
```

More cores can run more independent work simultaneously, but performance also depends on clock speed, cache, memory, compiler, software parallelism, and workload type.

## 3. Firmware meaning

Firmware is low-level software stored inside hardware, usually in flash memory. It tells a device how to start, control its components, and communicate with other hardware.

Examples include BIOS/UEFI, bootloaders, microcontroller programs, SSD controller code, and device firmware.

In a RISC-V system:

```text
Power on
→ Boot ROM/bootloader
→ Firmware initializes hardware
→ Firmware loads OS or runs embedded application
→ Application runs
```

Firmware often runs in RISC-V Machine mode, the highest privilege level.

## 4. Why learn RISC-V?

You do not need RISC-V for every career. It is most useful if you want to understand computers deeply or work in:

- Processor design
- SoC design
- FPGA
- Verification
- Embedded systems
- AI hardware
- Semiconductor companies

For an AI software startup, RISC-V is optional but valuable as a technical foundation. It helps you understand computation, memory, performance, power, and edge AI.

## 5. Your startup direction

You want to build an AI startup, but not an AI-chip startup initially. That is sensible because software startups usually require less capital, move faster, and reach users sooner.

Your main focus should be:

1. Find a specific user group.
2. Find a repeated, costly, annoying problem.
3. Interview users.
4. Build a small AI software MVP.
5. Test whether people use it and would pay.
6. Improve based on feedback.
7. Consider hardware only if the product truly requires it.

Good early AI opportunities include document-heavy workflows, repetitive decisions, unstructured data, and specialized business processes.

## 6. Your seniors’ work

Your seniors appear to be working on RISC-V processor cores and FPGA implementation. They are asking students to:

- Understand RISC-V core libraries
- Run simulations
- Synthesize designs
- Perform place and route
- Verify timing
- Generate bitstreams
- Program FPGA boards
- Test through PuTTY
- Analyze multiple cores
- Study memory, security, caches, protocols, and benchmarks

This is serious engineering training, not timepass, provided the tasks are actually completed and understood.

## 7. OpenR5 clarification

OpenR5 is a family of 19 RISC-V processor cores from OR5 Labs. However, only three cores have clearly public repository links on the site:

- Kavacha: https://github.com/OR5-LABS/kavacha
- Takshaka: https://github.com/OR5-LABS/takshaka
- Gandiva: https://github.com/OR5-LABS/gandiva

The other 16 cores are named on the website, but their source is listed as “available on request.” Therefore, “18 or 19 cores” likely refers to the OpenR5 family, not necessarily 19 repositories your seniors personally built.

The website belongs to OR5 Labs. It does not publicly identify individual founders or confirm any college affiliation.

## 8. Your interest level

You said:

- You may not learn RISC-V if seniors were not guiding you.
- You are interested mainly because it can lead to a full-time career space.
- You prefer building products people can use easily.
- You can handle CPU internals, debugging, and hardware topics, but they are not your main passion.
- You cannot give a full day because your startup and college work matter too.

This means your motivation is mostly career-driven, not deeply intrinsic. That is acceptable, but you should use a limited, structured schedule rather than trying to become a full-time hardware engineer immediately.

## 9. Your practical decision

Your best approach is:

```text
Main track: AI startup and product building
Side track: RISC-V/FPGA fundamentals
Time split: Startup first, college second, RISC-V third
Commitment: 45–60 minutes, 4–5 days per week
```

Tell your seniors clearly that you want to learn seriously but cannot commit full days. Ask for small tasks with clear deliverables.

Example message:

> “I want to learn RISC-V seriously and contribute, but I am also building an AI startup and managing college work. I can consistently give 45–60 minutes, 4–5 days a week. Please give me small, outcome-based tasks. I will complete them properly and document what I learn.”

## 10. Final recommendation

Learn RISC-V in parallel, but do not make it your identity yet.

Your priority order should be:

1. Build AI products and talk to users.
2. Maintain college performance.
3. Learn RISC-V through small, consistent, practical tasks.
4. Reassess after one month.
5. Choose hardware deeply only if your startup or career direction truly requires it.

The assigned tasks are valuable because they teach the complete path from RISC-V code to real hardware. But your startup goal should remain your main mission.
