#Section 1

Table 

| PC  | Opcode   | src1_addr | src1_out | src2_addr | src2_out     | dst_addr | dst_data     |
| --- | -------- | --------- | -------- | --------- | ------------ | -------- | ------------ |
| 0   | 0x23     | 0         | 0        | 0         | 0            | 0        | 0            |
| 4   | 0x23     | 0         | 0        | 2         | 0            | 0        | 0            |
| 8   | 0        | 2         | 0        | 2         | 0            | 0        | 0            |
| 12  | 0x2B     | 0         | 0        | 3         | 0            | 0        | 0            |
| 16  | 0        | 3         | 0        | 2         | 0            | 2        | 0x00000056   |
| 20  | 0x08     | 3         | 0        | 5         | 0            | 3        | 0            |
| 24  | 0        | 5         | 0        | 3         | 3            | 0        | 0x00000084   |
| 28  | 0        | 6         | 0        | 2         | 0x00000056   | 4        | 0            |
| 32  | 0        | 6         | 0        | 2         | 0x00000056   | 5        | 0x000000C    |
| 36  | 0        | 5         | 0x000000C| 4         | 0            | 6        | 0            |
| 40  | 0x04     | 5         | 0x000000C| 0         | 0            | 7        | 0x00000056   |
| 44  | 0x23     | 0         | 0        | 8         | 0            | 8        | 0xFFFFFFA9   |
| 48  | 0        | 0         | 0        | 0         | 0            | 6        | 0            |
| 52  | 0        | 0         | 0        | 0         | 0            | 31       | 0x000000C    |
| 56  | 0        | 0         | 0        | 0         | 0            | 8        | 0            |



#section 2

 Data hazards happen when an instruction depends on a previous instruction’s result that has not yet been written back, this is usually fixed with some type of data forwarding. This causes stalls and delays in register updates. Control hazards happen from branch instructions, where the pipeline may fetch the wrong instruction before the branch outcome is determined. For example, add $v1, $v0, $v depends on the lw $v0, 31($zero) to load a value into $v0. This mean that add would have to wait into the load word is properly executed.


 #section 3
```asm
lw $v0, 31($zero)  
or $t1, $zero, $zero 
add $v1, $v0, $v0  
sw $v1, 132($zero)  
sub $a0, $v1, $v0  
addi $a1, $v1, 12  
and $a2, $a1, $v1  
or $a3, $a2, $v0  
nor $t0, $a2, $v0  
slt $a2, $a1, $a0  
beq $a2, $zero, -8  
lw $t0, 132($zero)  


This would help avoid a stall since it adds a delay between the 1st and 3rd lines, which allows the pipeline to complete the memory read before $v0 is needed.