# C basics

## Basic functions

```
#include -> import library
stdio -> standard input output
# -> compiler directive
```

case matters, white space does not
comments go between /* and */
each statement is followed by a semicolon

main function:

```
int main(void) {
	/* action starts here */
	printf("This is a complete C program");
	return 0;
	/* and ends here */
}
```

Functions are regarded as integers
	- return statement at the end signifies if function has completed correctly
		- 0 == everything was fine
		- other numbers correspond to errors
		

## Programming languages

- Machine Languages
	- binary
	- each processor has different instruction set
- Assembly Languages
	- assembler converts assembly language into machine code
- High Level Languages		
		
## Basic elements of C

- To print floats in string:
	- printf("The area is %f", radius)
		-d for integer, c for character 
- Case matters, white space does not
- Variable names should start with letter

### C libraries

- C is lightweight language
- Examples:
	- stdio -> standard input/output library
	- math
- To use a library:
	- must include header file at top of the program
 ```
 #include <stdio.h>
 ```
 
 - in Microsoft, need to include the library on the link line

### Variable types

- char, int, float, double
- strings are arrays of characters
- must declare variable before using it

### Logical operators

- <, >, <=, >=, ==, &&, !, ||
- can compare any variable- compared based on ASCII values

### Statements

- If statements

```
if (expression) {
	statement;
}
```

- If/else statements
- For loops

```
for (initialization; test; increment) {
	statement;
}
```

### Debugging
#### Types of errors

- Syntax errors- caught at compile time
- Run-time errors- logic errors
	- in C, there is no protection against doing something unintended to a value stored in memory
	
