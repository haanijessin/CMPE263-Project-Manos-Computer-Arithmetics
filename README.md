# CMPE263-Project-Manos-Computer-Arithmetics 

**Qatar University** 

**College of Engineering** 

**CMPE 263 Computer Architecture and Organization I Spring 2021** 

**Floating-Point Arithmetic Calculations on Mano’s Computer** 

This goal of this project is to use the instruction set architecture of the computer described in the textbook (Computer System Architecture, 3rd Edition, by M. Morris Mano, Prentice-Hall, ISBN: 0-13- 175738-5) to ***perform floating-point arithmetic calculations***. A brief summary of Mano’s instruction set architecture is shown in the appendix below. The project will involve multiple deliverables that you need to develop gradually and incrementally.  

**Deadlines and deliverables** 

The project will have several deliverables. Each deliverable has a deadline. The deadline is due at time 23:59 of the due date. These deadlines are as below: 

- Create a team by self-enrolling in a Blackboard group is due on March 2, 2021. 
- Floating-point addition is due on March 23, 2021. 
- Full project submission, which includes a program to do both floating-point multiplication and floating point addition as well as a final report, is due on April 6, 2021. 
- Possible individual and/or team project discussion meetings during the week of April 11-15, 2021. You may or may not be selected by the instructor/TA to have such meeting.   

**Emulator** 

To develop and test your project, use the Mano’s machine emulator developed last semester by one of our students. This emulator can be downloaded at[ https://github.com/Naheel-Azawy/Simple- Computer-Simulator.](https://github.com/Naheel-Azawy/Simple-Computer-Simulator) Brief and basic instructions on how to use it can be found at [https://www.youtube.com/watch?v=PmRkBWxi1Wc&feature=youtu.be.](https://www.youtube.com/watch?v=PmRkBWxi1Wc&feature=youtu.be) 

**Project description** 

Assume floating-point (non-standard) representation of numbers as follows: 

- Each number is represented by two consecutive 16-bit words 
- The first word represents the exponent (using 2’s representation).  
- The second word represents an unsigned mantissa  
- The floating point numbers are represented using our special *normalized form* (0.1xxx…x), by which,  
- If the floating-point number is not zero, the most significant bit of the mantissa is 1 and the binary point is placed right before this leftmost bit.   
- If the floating-point number is zero, both the mantissa and the exponent fields should have a zero value. 

Notice that the above floating-point representation is not a standard one. Therefore, it may not be the most effective one (in terms of utilizing the available bits to achieve optimal accuracy and range of values). It is specifically designed to simplify your project implementation. 

***Examples*:** 

- The decimal number (13.25)10=(1101.01)2 is represented as follows: 
(1101.01)2= 0.110101 × 2+4  (normalized)  

	Therefore, the 16 bit **exponent** is 0000000000000100 (which is +4 in 2’s complement). The 16 bit **mantissa** is 1101010000000000. 

- The decimal number (0.3125)10=(0.0101)2 is represented as follows: 
	(0.0101)2= 0.101 × 2-1  (normalized)  
	
	Therefore, the 16 bit **exponent** is 1111111111111111 (which is -1 in 2’s complement). The 16 bit **mantissa** is 1010000000000000 

- The number zero is represented as 
**Exponent** = 0000000000000000 
**Mantissa**  = 0000000000000000 

Write assembly language programs to perform each of the following floating-point operations on two input floating point numbers A and B: 

1. Compute **C=A+B** and produce a normalized floating point result C 
1. Compute **D=A×B** and produce a normalized floating point result D (notice that in order to be able to perform this operation, you need to implement a subroutine that performs multiplication of two unsigned integers) 

You can make the following **assumptions**: 

1. The mantissa’s are unsigned (i.e., no negative values)  
1. A and B are non-zero values and A is greater than B 
1. The mantissa of input values A and B require no more than 8-bits (i.e., they are smaller than 256. Therefore, their multiplication will not result in a value that requires more than 16 bits. 
1. No overflow or underflow could occur. Therefore, you can ignore checking for these. 

***Add Algorithm*** 

1. Align the binary point of the two values by shifting the mantissa of the smaller value (i.e. B) right by a number of positions equal to the difference between exponents. With this you can imagine that both values have the same exponents and, therefore, the locations of their binary points are aligned. Make sure that for the first position shift, you should shift in a “1” value (the implicit most significant bit). 
1. Compute the result 
   1. The result mantissa of the result is the addition of both mantissa’s 
   1. The result exponent is the common exponent after aligning the binary point, which is the exponent of A. 
1. Normalize the result by shifting the result right by one position (if needed) and adjusting (incrementing) the exponent. Notice that considering the above assumptions, you only need to do shift the result by a maximum of one position if there is a carry when you add the mantissa’s.   

***Multiply Algorithm*** 

1. Shift both mantissa’s right by 8 positions (to make them occupy the least significant 8 bits) 
1. Multiply mantissa’s to generate the resulting mantissa 
1.  To get the result exponent, add the exponents together  
1.  Normalize the result by shifting the mantissa left and decrementing the exponent. Do this till the first bit of the exponent is non zero. Notice that since you started with normalized numbers, the number of positions to shift will be 0 or 1; either the most significant bit (bit 15) of the resulting mantissa is already 1 or it is zero but the next bit (bit 14) is 1. 

[Note: The above algorithm is designed with project simplicity in mind. Therefore, it may not have the best utilization of bits to achieve the best accuracy.] 

**Supplying input data** 

In all of your programs, store the input values starting at location 2048.  Clearly use labels to indicate your input variables. You should follow the format described in this section strictly as input will be supplied to your program using this format for testing. 

Your data should be organized as follows (in the given order): 

1. Pointers to input and output values 
1. Input values 
1. Output value 
1. Other variables if needed 

Figure 1 shows and example of data organization. Notice that the values of A and B provided in Figure 1 are (20)<sub>10</sub>=(0.1010000000000000)<sub>2</sub> × 2<sup>5</sup> and (3)<sub>10</sub>=(0.1100000000000000)<sub>2</sub> × 2<sup>2</sup> , respectively. 

![enter image description here](https://i.imgur.com/3Cf0hYD.png)
*Figure 1: Input Format*

**Submission and evaluation guidelines** 

- The project will be evaluated by running it on different input data provided by the instructor. Therefore, make sure that you strictly follow the required input format. A fully working program will get 100%, a partially working program will get 25%-75%, and a non-working program will get 0%.  
- Submit programs by the deadline as a single file on Blackboard.  
- With your final submission, you should submit a short report about your project on Blackboard. Use the provided report template. 
- Each team should have one and only one submission. No late submissions will be accepted. 
- Each team member should actively participate in developing the project and should fully understand the whole system. Individually, every team member should be able to demonstrate full understanding of the system details.   
- The teaching assistant or instructor may call individuals for a question and answer session. During this session *individuals* will be asked about the details of their program. Points will be deducted (typically zero will be given) if the individual is not able to demonstrate full understanding of the program. 

**Appendix: Mano’s Basic Computer**

**Registers and Bus** 

![](https://i.imgur.com/0VlTmew.png)

**Instruction Format** 

![](https://i.imgur.com/WA9WOWn.png)

**Instruction set** 

![](https://i.imgur.com/OpXNPre.png)
