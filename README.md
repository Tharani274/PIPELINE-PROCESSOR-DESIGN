# PIPELINE-PROCESSOR-DESIGN

COMPANY:CODETECH IT SOLUTIONS

NAME:MUZAMMIL AHMED

INTERN ID:CT06DF2017

DOMAIN:VLSI

DURATION:6 WEEKS

MENTOR:NEELA SANTHOSH

The pipeline_cpu Verilog module implements a compact, four-stage pipelined processor with a minimal instruction set, utilizing instruction memory (instr_mem), a register file (reg_file), and data memory (data_mem) to execute 8-bit operations, and it demonstrates the core principles of instruction-level parallelism common in pipelined CPU architectures. At its core, the design comprises four pipeline stages—Fetch (IF), Decode (ID), Execute (EX), and Write-Back (WB)—each connected by pipeline registers that carry both control and data signals from one stage to the next, enabling multiple instructions to be in-flight simultaneously (one at each stage), a fundamental advantage of pipelined architecture that dramatically improves instruction throughput even though individual instruction latency remains around four cycles.The Fetch stage increments a 4-bit program counter (pc) on each clock edge (or resets on reset), loading the next instruction into IF_ID_instr. In the subsequent Decode stage, the upper bits of the instruction are extracted as opcode, rs1, rs2, and rd, and the corresponding register contents from reg_file are read and stored into the ID_EX pipeline registers. This stage illustrates the textbook separation between instruction fetching and operand retrieval, aligning with standard pipeline flow . In the Execute stage, a simple ALU interprets a 2-bit ID_EX_opcode to perform an ADD (code 00), SUB (code 01), or a memory LOAD (code 10) operation, with the alu_result forwarded to the EX_WB registers along with destination register ID_EX_rd and a write-enable flag. This stage mimics the MEM and EX phases merged in a small pipeline, while also handling a memory-access behavior during LOAD through data_mem[ID_EX_data1]. Finally, the Write-Back stage checks the EX_WB_write_enable signal and writes the result into reg_file[EX_WB_rd], completing the instruction execution. The pipeline registers (IF_ID, ID_EX, EX_WB) provide necessary buffering between stages, typical of pipelined microarchitectures seen in academic examples and research prototypes . Despite exemplifying pipelining, this CPU lacks advanced features such as hazard detection, data forwarding, or stall logic, making it vulnerable to data hazards (e.g., Read-After-Write dependencies) and control hazards should branches be added later.In pipelined CPUs with greater sophistication—such as 5‑stage MIPS pipelines—these hazards are mitigated by inserting pipeline stalls, forwarding units, or branch prediction mechanisms, which retain performance while improving correctness.Without such controls, your processor will function correctly only when instructions have no interdependencies—essentially producing ideal, hazard-free behavior. Notwithstanding, this design still captures the essential idea of pipelining: by dividing the instruction path into discrete, register-separated stages (IF, ID, EX, WB), multiple instructions can advance each cycle, considerably boosting throughput compared to scalar, single-cycle CPUs where each instruction begins only after the previous one completes the full cycle.Your implementation is a powerful educational demonstration: it showcases how pipeline registers buffer intermediate values, how the instruction fetch and decode flow work, and how simple arithmetic and memory operations are performed in a staged manner. Even with its educational simplicity, the design maps directly to hardware—pipeline stage registers simplify timing closure, synchronous updates stabilize outputs, and the straightforward stage separation aligns well with FPGA or ASIC implementation models seen in university curricula.In summary, the module offers a well-structured, scalable foundation for students or hobbyists exploring pipelined design: it's compact enough to be digestible, yet rich enough to illustrate the transformative performance benefits and complexity considerations that arise when instruction latency and throughput are decoupled by pipelining.


OUTPUT

<img width="1342" height="636" alt="Image" src="https://github.com/user-attachments/assets/ac40e15f-c23f-47ce-b6da-7230c6ba59f4" />


