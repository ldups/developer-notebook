# C basics

## basic functions

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
		

## Programming Languages
	- Machine Languages
		- binary
		- each processor has different instruction set
	- Assembly Languages
		- assembler converts assembly language into machine code
	- High Level Languages		
		
## Basic elements of C
To print floats in string:
	- printf("The area is %f", radius)
		-d for integer, c for character 
