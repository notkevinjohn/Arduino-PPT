# Arduino-PPT

This project is designed to simplify the development of Arduino code that follows the general pattern of a USB peripheral. This means that the computer will be connected via the hardware UART to the Arduino, and it will be sending commands to the Arduino and receiving data back from the Arduino over this interface. 

The tools in this package will allow an end user to mark any function in their sketch as being 'callable.' This means the Arduino-PPT package will generate the needed listener funtions such that the any function can be called via the serial interface and have its output returned. The Arduino-PPT will also create an executable binary in (written in C/C++) that will allow the end user to call these functions directly from the command line. This will provide a binding that allows the functionality offered by the Arduino to be easily integrated into applications written for the computer: hence, allowing it to serve as a USB peripheral. While the executable that controls the Arduino is written in C, it can easily be wrapped for other languages like Java or Python. 

