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


