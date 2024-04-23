# CMPE263-Project-Manos-Computer-Arithmetics

**Qatar University**  
**College of Engineering**  
**CMPE 263 Computer Architecture and Organization I Spring 2021**  
**Floating-Point Arithmetic Calculations on Mano’s Computer**

## Project Description

The goal of this project is to perform floating-point arithmetic calculations using the instruction set architecture of the computer described in the textbook "Computer System Architecture, 3rd Edition" by M. Morris Mano. The project involves multiple deliverables to be developed gradually and incrementally.

## Emulator

To develop and test the project, use the Mano’s machine emulator developed by one of our students. The emulator can be downloaded [here](https://github.com/Naheel-Azawy/Simple-Computer-Simulator). Instructions on how to use it can be found [here](https://www.youtube.com/watch?v=PmRkBWxi1Wc&feature=youtu.be).

## Project Details

Assume a non-standard floating-point representation as follows:

- Each number is represented by two consecutive 16-bit words.
- The first word represents the exponent (using 2’s representation).
- The second word represents an unsigned mantissa.
- Floating point numbers are represented using a special normalized form (0.1xxx…x).

### Examples

- The decimal number (13.25)10=(1101.01)2 is represented as follows: 
(1101.01)2= 0.110101 × 2+4  (normalized)  

	Therefore, the 16 bit **exponent** is 0000000000000100 (which is +4 in 2’s complement). The 16 bit **mantissa** is 1101010000000000. 

- The decimal number (0.3125)10=(0.0101)2 is represented as follows: 
	(0.0101)2= 0.101 × 2-1  (normalized)  
	
	Therefore, the 16 bit **exponent** is 1111111111111111 (which is -1 in 2’s complement). The 16 bit **mantissa** is 1010000000000000 

- The number zero is represented as 
**Exponent** = 0000000000000000 
**Mantissa**  = 0000000000000000 

Write assembly language programs to perform the following floating-point operations on two input floating point numbers A and B:

1. Compute C=A+B and produce a normalized floating point result C.
2. Compute D=A×B and produce a normalized floating point result D. (Note: in order to be able to perform this operation, you need to implement a subroutine that performs multiplication of two unsigned integers)

### Assumptions

1. Mantissas are unsigned.
2. A and B are non-zero values with A > B.
3. Mantissas of A and B require no more than 8-bits.
4. No overflow or underflow could occur.

### Add Algorithm

1. Align the binary point of the two values by shifting the mantissa of the smaller value (B) right.
2. Compute the result mantissa and exponent.
3. Normalize the result.

### Multiply Algorithm

1. Shift both mantissas right.
2. Multiply mantissas.
3. Compute the result exponent.
4. Normalize the result.

### Supplying Input Data

Store the input values starting at location 2048. Input format: Pointers to input and output values, Input values, Output value, Other variables if needed.

## Appendix: Mano’s Basic Computer

**Registers and Bus**

![Registers and Bus](https://i.imgur.com/0VlTmew.png)

**Instruction Format**

![Instruction Format](https://i.imgur.com/WA9WOWn.png)

**Instruction Set**

![Instruction Set](https://i.imgur.com/OpXNPre.png)
