Most of today's computers are inspired by the Von Neumann model. Despite the years that have passed since its publication, the internal structure of the computers we use today still retains most of the characteristics proposed by the Hungarian mathematician and physicist.
#### The first computers:
The first computers had fixed programs. Some very simple devices still use this design. For example, a desktop calculator has a fixed program that can solve basic math calculations. The first computers were designed to perform specific calculations. When possible, they could be "reprogrammed," but this was a laborious process that involved an engineering redesign and a long process of physical rewiring and reconstruction of the machine.
## Von Neumann Model or Architecture:
![[Pasted image 20240824170851.png]]
It is a conceptual model that shows how a [[Computer]] works. It consists of:
- The [[CPU]] or Central Processing Unit. This in turn contains:
	* An ALU or Arithmetic Logic Unit 
	* Processor registers.
    - A control unit
    - A program counter.
- The main [[Memory]].
- The input and output mechanisms.
### CPU:
It is responsible for interpreting and processing the instructions received from a program. The CPU contains the ALU, the control unit, and a set of registers.
##### ALU or Arithmetic Logic Unit:
It only performs arithmetic and logical operations on the data. It performs addition, subtraction, multiplication, and division calculations, but also logical operations such as AND, OR, or NOT.
##### Control Unit:
It controls the operation of the ALU, memory, and the computer's input and output devices. It will manage the process of moving data and programs to and from memory and executing program instructions.
##### Registers:
Registers are high-speed storage areas in the CPU. All data must be stored in a register before it can be processed. The memory address register contains the location in memory of the data to be accessed. The memory data register contains the data being transferred to memory. The program counter calculates the number of execution cycles and points to the next instruction to be executed.
### Operation:
This architecture works using the so-called machine cycle, using four simple steps: fetch, decode, execute, store. Instructions are obtained by the CPU from memory. The CPU then decodes and executes these instructions. The result is stored back in memory after the instruction execution cycle is complete.
![[Pasted image 20240824171342.png]]