# Task 2 — Proving RISC-V Toolchain Setup (Run, Disassemble, Decode)

# This repository is part of the VSD RISC-V SoC Workshop. In Task 2, the goal is to prove that the RISC-V toolchain is correctly installed and functional on the local machine.

## The following steps were performed: -
- Compiled 4 unique C programs using `riscv64-unknown-elf-gcc`
- Embedded user, host, machine ID, and timestamps for build uniqueness
- Ran each program on the RISC-V simulator (`spike pk`)
- Captured disassembly (`.objdump`) and source-level assembly (`.s`) of each
- Manually decoded at least 5 RISC-V integer instructions
- Documented all outputs, binaries, and screenshots as evidence

## Toolchain Verification

### Spike Version and riscv64-unknown-elf-gcc -v (both in the same screenshot)
## Output
<img width="1212" height="901" alt="Screenshot 2025-08-08 154242" src="https://github.com/user-attachments/assets/4d21ebc1-38d9-413b-8654-8ea502bc4a2b" />
<img width="1200" height="906" alt="Screenshot 2025-08-08 154258" src="https://github.com/user-attachments/assets/a9b47ac7-88b6-4ccd-bd11-ce6ebf0bf589" />

### Compile Commands: -

### For factorial.c
```
riscv64-unknown-elf-gcc -O0 -g -march=rv64imac -mabi=lp64 \
-DUSERNAME="\"$U\"" -DHOSTNAME="\"$H\"" -DMACHINE_ID="\"$M\"" \
-DBUILD_UTC="\"$T\"" -DBUILD_EPOCH=$E \
factorial.c -o factorial
```
### For max_array.c
```
riscv64-unknown-elf-gcc -O0 -g -march=rv64imac -mabi=lp64 \
-DUSERNAME="\"$U\"" -DHOSTNAME="\"$H\"" -DMACHINE_ID="\"$M\"" \
-DBUILD_UTC="\"$T\"" -DBUILD_EPOCH=$E \
max_array.c -o max_array
```
### For bitops.c
```
riscv64-unknown-elf-gcc -O0 -g -march=rv64imac -mabi=lp64 \
-DUSERNAME="\"$U\"" -DHOSTNAME="\"$H\"" -DMACHINE_ID="\"$M\"" \
-DBUILD_UTC="\"$T\"" -DBUILD_EPOCH=$E \
bitops.c -o bitops
```
### For bubble_sort.c
```
riscv64-unknown-elf-gcc -O0 -g -march=rv64imac -mabi=lp64 \
-DUSERNAME="\"$U\"" -DHOSTNAME="\"$H\"" -DMACHINE_ID="\"$M\"" \
-DBUILD_UTC="\"$T\"" -DBUILD_EPOCH=$E \
bubble_sort.c -o bubble_sort
```

## Proof of Uniqueness

 Each program output includes a clearly visible `ProofID` and `RunID`, which are generated using a 64-bit FNV-1a hash based on: -

- `USERNAME`
- `HOSTNAME`
- `MACHINE_ID`
- `BUILD_UTC`
- `BUILD_EPOCH`
- `Program name`

## These fields ensure the build is unique to my machine and identity. All screenshots and output files (e.g., `factorial_output.png`, `bitops_output.png`) clearly show these values for verification.

# Compile
```
riscv64-unknown-elf-gcc -O2 -Wall -march=rv64imac -mabi=lp64 \
  -DUSERNAME="Achytuuser" -DHOSTNAME="Ubuntu" unique_test.c -o unique_test
```
# Disassemble main only
```
riscv64-unknown-elf-objdump -d unique_test | sed -n '/<main>:/,/^$/p' > main_objdump.txt
```
# Show it in terminal and take screenshot
```
cat main_objdump.txt
```
# Screenshot of ojbdumpfile
<img width="1828" height="980" alt="image" src="https://github.com/user-attachments/assets/918d84a8-9835-4c80-9f65-60bf043e5278" />

# Instruction decoding table
| Instruction         | Opcode   | rd  | rs1  | rs2 | funct3 | funct7  | Binary                                        | Operation                           |
| :------------------ | -------- | --- | ---- | --- | :----: | :-----: | --------------------------------------------- | ------------------------------------ |
| addi a4, s1, 928    | 0010011  | x14 | x9   | -   | 000    | 0000001 | 0000001110100 01001 000 01110 0010011         | a4 = s1 + 928                        |
| addi a3, s2, 936    | 0010011  | x13 | x18  | -   | 000    | 0000001 | 0000001110100 10010 000 01101 0010011         | a3 = s2 + 936                        |
| addi a2, a2, 952    | 0010011  | x12 | x12  | -   | 000    | 0000001 | 0000001110111 01100 000 01100 0010011         | a2 = a2 + 952                        |
| li a1, 256          | 0010011  | x11 | x0   | -   | 000    | 0000100 | 000010000000 00000 000 01011 0010011          | a1 = 256                             |
| addi a5, a5, 1      | 0010011  | x15 | x15  | -   | 000    | 0000000 | 000000000001 01111 000 01111 0010011          | a5 = a5 + 1                          |
| addi sp, sp, 288    | 0010011  | x2  | x2   | -   | 000    | 0000100 | 000010010000 00010 000 00010 0010011          | sp = sp + 288                        |
