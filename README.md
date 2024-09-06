# AssemblyX86-TASM-Project
Project AssemblyX86 sintax TASM 
This project is written in assembly language for the x86 architecture and uses DOS interrupt calls to interact with the user and display messages on the screen.

 Functionality description:
1. Reading a number from the user:
   - The program starts by displaying a message (`msg1`) asking the user to enter a number.
   - The input is read character by character until the `$` character is encountered, which marks the end of the input.

2. Displaying the number:
   - After the user enters the number, the program displays it on the screen using the message `msg2`.

3. Determining parity:
   - The program checks whether the entered number is even or odd by dividing it by 2.
   - Depending on the result, it displays the message `msg4` (if the number is even) or `msg5` (if the number is odd).

4. Number of digits:
   - The program calculates and displays how many digits the user entered, using the message `msg3`.

5. The `print_number` function:
   - This function is responsible for displaying a number on the screen, converting the numeric value into ASCII characters.

##Language used:
The project is written in **assembly language (assembly)** for the **x86** architecture and runs in **real mode**, using BIOS and DOS interrupts for input and output (e.g., `int 21h`).

.
