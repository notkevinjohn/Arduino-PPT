# Arduino-PPT

This project is designed to simplify the development of Arduino code that follows the general pattern of a USB peripheral. This means that the computer will be connected via the hardware UART to the Arduino, and it will be sending commands to the Arduino and receiving data back from the Arduino over this interface. 

The tools in this package will allow an end user to mark any function in their sketch as being 'callable.' This means the Arduino-PPT package will generate the needed listener funtions such that the any function can be called via the serial interface and have its output returned. The Arduino-PPT will also create an executable binary in (written in C/C++) that will allow the end user to call these functions directly from the command line. This will provide a binding that allows the functionality offered by the Arduino to be easily integrated into applications written for the computer: hence, allowing it to serve as a USB peripheral. While the executable that controls the Arduino is written in C, it can easily be wrapped for other languages like Java or Python. 

## Functional Example
Imagine you had an Arduino that drove an LED, and you wanted to be able to control that LED as if it was a USB peripheral. Using Arduino-PPT, you would write the sketch to drive the LED like normal, and after running the Arduino-PPT script, that sketch would include function callbacks that would led you execute your functions via the serial port. 

You might write the following function into a myLED.ino sketch:

`void LED_On(){
  digital_write(ledPin, HIGH)
 }`

This would

## Work Process Flow
When a new sketch is created, it is generated from an Arduion-PPT template that does things like instiate an instance of the Arduino-PPT class in the setup() function and then call it each time through the loop() function so that it can continuously poll the serial buffer for data. 

When it's time to compile, the Arduino-PPT precompile script is run first (this can be done in a single step using the Arduino CLI). This parses through the sketch.ino file and finds all instances of functions that have been marked as callable. When it finds these, it creates a new entry in the list of functions it knows how to call by dynamically extending the Arduino-PPT library file. This creates the needed code such that when we want to call myFunction() from the Arduino, we can write some byte code like '0A' to the buffer to indicate this. If this function extpects an argument, we can write that to the serial buffer as well. This gives us a callable/testable serial interface into our Arduino sketch. 

Aside from generating the needed code to give serial commands that the Arduino can parse into function calls, we also dynamically generate and make a C/C++ program that maps all these serial communications in a way that can be bound to our application. This program could also be called directly from the command line. 

<img src='https://github.com/notkevinjohn/Arduino-PPT/blob/master/Arduino-PPT.png' />

