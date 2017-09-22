# EC Lab 1
## part II:
In this lab well will explore some features of the Altera Monitor Program by using a simple application program written in the Nios II assembly language. Consider the program below, which finds the largest number in a list of 32-bit intergers that is stored in the memory.
  
```assembly

/* Program that finds the largest number in a list of integers */
.equ LIST, 0x500		/* Starting address of the list */

.global _start
_start:
	movia r4, LIST		/* r4 points to the start of the list */
	ldw r5, 4(r4)		/* r5 is a counter, initialize it with n */
	addi r6, r4, 8		/* r6 points to the first number */
	ldw r7, (r6)		/* r7 holds the largest number found so far */
LOOP:
	subi r5, r5, 1		/* Decrement the counter */
	beq r5, r0, DONE	/* Finished if r5 is equal to 0 */
	addi r6, r6, 4		/* Increment the list pointer */
	ldw r8, (r6)		/* Get the next number */
	bge r7, r8, LOOP	/* Check if larger number found */
	add r7, r8, r0		/* Update the largest number found */
	br LOOP
DONE:
	stw r7, (r4)		/* Store the largest number into RESULT */
STOP:
	br STOP			/* Remain here if done */

.org 0x500
RESULT:
.skip 4				/* Space for the largest number found */
N:
.word 7				/* Number of entries in the list */
NUMBERS:
.word 4, 5, 3, 6, 1, 8, 2	/* Numbers in the list */
.end
```

Note that some sample data is included in this program. The list starts at hex address 500, as specified by the .org
assembler directive. The first word (4 bytes) is reserved for storing the result, which will be the largest number
found. The next word specifies the number of entries in the list. The words that follow give the the actual numbers
in the list.

## How to start:
Perform the following:
1. Create a new directory; we have chosen the directory name lab1 part2. Copy the file Practica1_ParteII.s into this
directory.

2. Use the Altera Monitor Program to create a new project in this directory; we have chosen the project name
part2. When you reach the window in Figure 4.

![alt text](https://github.com/BIoodHound/EC_Pract1/blob/master/Images/Figure4.JPG "Image 4")

Choose Assembly Program but do not select a sample
program, as shown in Figure 11. Click Next.

![alt text](https://github.com/BIoodHound/EC_Pract1/blob/master/Images/Figure11.JPG)

3. Upon reaching the window in Figure 5, you have to specify your program.
Click Add and in the pop-up box.

![alt text](https://github.com/BIoodHound/EC_Pract1/blob/master/Images/Figure5.JPG)

that appears indicate the desired file name, lab1 part2.s, and its location. This should lead to the image in
Figure 12. 

![alt text](https://github.com/BIoodHound/EC_Pract1/blob/master/Images/Figure12.JPG)

Click Next to get the window in Figure 6. 

![alt text](https://github.com/BIoodHound/EC_Pract1/blob/master/Images/Figure6.JPG)

Again click Next to get to the window in Figure 7.

![alt text](https://github.com/BIoodHound/EC_Pract1/blob/master/Images/Figure7.JPG)

Make sure that the SDRAM is selected as the memory device. Note that the Start offset in device will be 0,
because the program in the program below does not indicate that it should loaded at a location that is different from
the default location 0. Click Finish.

```assembly

/* Program that finds the largest number in a list of integers */
.equ LIST, 0x500		/* Starting address of the list */

.global _start
_start:
	movia r4, LIST		/* r4 points to the start of the list */
	ldw r5, 4(r4)		/* r5 is a counter, initialize it with n */
	addi r6, r4, 8		/* r6 points to the first number */
	ldw r7, (r6)		/* r7 holds the largest number found so far */
LOOP:
	subi r5, r5, 1		/* Decrement the counter */
	beq r5, r0, DONE	/* Finished if r5 is equal to 0 */
	addi r6, r6, 4		/* Increment the list pointer */
	ldw r8, (r6)		/* Get the next number */
	bge r7, r8, LOOP	/* Check if larger number found */
	add r7, r8, r0		/* Update the largest number found */
	br LOOP
DONE:
	stw r7, (r4)		/* Store the largest number into RESULT */
STOP:
	br STOP			/* Remain here if done */

.org 0x500
RESULT:
.skip 4				/* Space for the largest number found */
N:
.word 7				/* Number of entries in the list */
NUMBERS:
.word 4, 5, 3, 6, 1, 8, 2	/* Numbers in the list */
.end
```

4. Compile and load the program.

5. The Monitor Program will display the disassembled view of the code loaded in the memory, as indicated
in Figure 13.

![alt text](https://github.com/BIoodHound/EC_Pract1/blob/master/Images/Figure13.JPG)

Note that the pseudoinstruction movia in the original program has been replaced with two
machine instructions, orhi and addi, which load the 32-bit address LIST into register r4 in two 16-bit parts
(because an immediate operand value is restricted to 16 bits).
Examine the disassembled code to see the difference in comparison with the original source program. Make sure that you understand the meaning of each instruction. Observe also that your program was loaded into memory locations with the starting
address zero. These addresses correspond to the SDRAM memory, which was selected when specifying
the system parameters. The DE2 Basic Computer has two more memories which are the on-chip memory
(i.e. the memory on the FPGA chip) and the SRAM chip on the DE2 board. See the document Basic
Computer System for Altera DE2 Board for full information. This document can be accessed by clicking on
the Documentation button in Figure 3.

![alt text](https://github.com/BIoodHound/EC_Pract1/blob/master/Images/Figure3.JPG)

6. Run the program. When the program is running, you will not be able to see any changes (such as the
contents of registers or memory locations) in the monitor windows, because the monitor program cannot
communicate with the processor system on the DE2 board. But, if you stop the program the present state of
these components will be displayed. Do so and observe that the program has stopped executing at the last
Branch instruction which is loaded in the memory location 0x34. Note that the largest number found in the
sample list is 8 as indicated by the contents of register r7. This value is also stored in the memory location
0x500, which can be seen by opening the Memory tab of the monitor window (in Figure 13).

![alt text](https://github.com/BIoodHound/EC_Pract1/blob/master/Images/Figure13.JPG)

7. Return to the beginning of the program by clicking on the icon . Now, single step through the program
by clicking on the icon . Watch how the instructions change the data in the processor’s registers.

8. Set the Program Counter to 0. Note that this action has the same effect as clicking on the restart icon.

9. This time add a breakpoint at address 0x28 (by clicking on the gray bar to the left of this address), so that
the program will automatically stop executing whenever the Branch instruction at this location is about to
be executed. Run the program and observe the contents of register r7 each time this breakpoint is reached.

10. Remove the breakpoint (by clicking on it). Then, set the Program Counter to 0x8, which will bypass the first
two instructions which load the address LIST into register r4. Also, set the value in register r4 to 0x504.
Run the program by clicking on the icon . What will be the result of this execution?

