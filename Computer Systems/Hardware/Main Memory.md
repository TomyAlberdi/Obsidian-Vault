### Characteristics:

* It is used to temporarily store data or information. 
* The processor can directly access the stored data. 
* It can be volatile, meaning the information is only saved while the computer is on. 
* Its capacity is limited. Currently, it can reach up to 64 Gigabytes. 
* Access to memory is done through the data bus. 
* Higher speed. 
* Higher cost.
### Types of main memory:

- **ROM (Read Only Memory):** Can only be read, not written. Stores the instructions necessary for the computer to start.
- **Cache:** Located between the CPU and RAM. The CPU copies the most relevant data it will use from RAM to access it more quickly.
- **RAM (Random Access Memory):** Used by the CPU, where it accesses instructions and stores immediate results. It is volatile.
## RAM:
RAM connects to the CPU through a slot. This slot has multiple pins that connect the slot to the memory modules. A motherboard can have more than one slot. The CPU can access RAM through:
- **Single Channel:** Uses a single signal at a determined bandwidth and frequency.
- **Dual Channel:** Allows simultaneous access to two memory modules. For this, all modules must have the same capacity, speed, frequency, latency, and manufacturer.
#### Characteristics:
- **Speed:** The time it takes for RAM to receive a request from the processor and access the information. The speed of memory is measured in megahertz (MHz) or millions of cycles per second.
- **Capacity:** The amount of data that can be stored in RAM. Capacity is measured in Gigabytes (GB).
- **Latency:** The number of clock cycles that elapse between a request and its response.
- **Voltage:** Refers to the energy consumed by the RAM module.
### Types of RAM:
- **VRAM:** RAM optimized for video adapters. They have two ports so that video data can be written simultaneously. The video adapter regularly reads the memory to refresh the monitor screen.
- **DDR RAM:** Launched in 2000, although it did not start being used until around 2002, it operated at 2.5V and 2.6V, and its maximum density was 128MB (so there were no modules with more than 1 GB) with a speed of 266 MT/s (Million transfers per second or 100-200MHz).
- **DDR2 RAM:** Launched in 2004, it operated at a voltage of 1.8V, 28% less than its predecessor. Its maximum density doubled to 256MB (2GB per module). Naturally, its maximum speed also multiplied, reaching up to 533MHz.
- **DDR3 RAM:** Launched in 2007 and was a revolution because XMP profiles were implemented here. To begin with, memory modules operated at 1.5V and 1.65V, with base speeds of 1066MHz but went much further, and density reached up to 8GB per module.
- **DDR4 RAM:** Launched in 2014. Voltage was reduced to 1.05V and 1.2V, although many modules operate at 1.35V. Speed has significantly increased, but its base started at 2133MHz. Currently, there are already 32GB modules, although this is gradually expanding.
- **DDR5 RAM:** Launched in mid-2020, it reaches bandwidths of up to 6.4GBps in its initial models. It is the first DDR memory with dual channel on a single chip. Its base frequency is 4800MHz, and its consumption is reduced by the classic voltage reduction, this time to 1.1V. Its maximum storage capacity in a memory module is 128GB.
## Registers:
A register is a very high-speed memory used in processors to quickly access important information. The CPU has 5 internal registers:
- **PC:** Program Counter.
- **IR:** Instructions Register.
- **MAR:** Memory Address Register.
- **MDR:** Memory Data Register.
- **Accumulator.**
## Cache:
An important support for the processor, divided into a total of three general levels, with a fourth that is not very common. The differentiation between L1, L2, and L3 (and in some cases, L4) cache memories follows a hierarchy based on proximity to the processor, speed, and capacity.