# LIMO ISA --- Instruction Set Architecture


## 2.1 overview

|                               | Specification                                                                                                   | Rationale                                                                                                                                  |
| ----------------------------- | --------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| Architecture style            | 32-bit load-store                                                                                               | Restriction of memory access strictly to nka and beha to ensure complete operations in EX stage with multiple stalls                       |
| Register bank                 | 16 register files                                                                                               | Reduction of required multiplexers and, an increase in immediate bits                                                                      |
| Addressing modes              | Register direct, immediate, and register offset                                                                 | Does not require complex incrementing and keeps hardware ALU simple                                                                        |
| Memory, endianness, alignment | Byte-addressed, little-endian, word-aligned                                                                     | Enforces strict word alignment eliminates unaligned-access and multicycle memory cycle reads                                               |
| Instruction formats           | Fixed 32-bit length across the 4 instruction formats                                                            | Fixed instruction width and fixed register/opcode bit allow the ID stage to fetch source registers and decode opcode bits at the same time |
| Departures from RV321         | Reduced register file, increased immediate fields, omitted formats and lexical rule (orthography normalization) | Reuses saved register bits to expand immediate offsets for wider branch reach and simplifies logic for pipelining  



## 2.2 Register File

| Number | Sesotho name | Alias           | Type | Purpose and convention              |
| ------ | ------------ | --------------- | ---- | ----------------------------------- |
| x0     | khoamo       | Zero            | SPR  | Hard-wired to 0, writes are ignored |
| x1     | Bolulo       | ra              | SPR  | Return address                      |
| x2     | Khetsi       | sp              | SPR  | Stack pointer                       |
| x3-x4  | Karabo       | a0-a1           | SPR  | Return argument                     |
| x5-x8  | Nakoana      | t0-t3           | GPR  | temporaries                         |
| x9-x15 | boloka       | s0-s6           | GPR  | Saved                               |
| PC     | sebaka       | Program counter | SPR  | Address of current instruction      |
