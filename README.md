# RFID
RFID with old wiegand reader and modern ones

## This work is from: https://www.pagemac.com/projects/rfid/arduino_wiegand  Written by Daniel Smith

# Arduino Wiegand Decoder for HID RFID Reader
I wrote this Arduino sketch as a follow-up to my PIC Wiegand decoder. That article goes into a lot more detail about the Wiegand protocol and how it works. However, it was one of my first microcontroller projects. The code wasn't great and the hardware was a custom PIC18 development board. If you're starting from scratch, it wouldn't be particularly easy to re-implement that code. So, I made a Wiegand decoder using the Arduino, since it's a very popular development platform.

# Hardware and Connections
The only hardware required is an Arduino Uno (sub for your preferred board) and an HID reader. Pictured is a smaller ProxPoint Plus, but any 125 kHz HID proximity reader should work. You may need to provide power externally.

* Connect the red wire (power) to 5V
* Connect the black wire to ground
* Connect the green wire (DATA0) to Digital Pin 2 (INT0)
* Connect the white wire (DATA1) to Digital Pin 3 (INT1)

# Operation
This program will decode the wiegand data from a HID RFID Reader (or, theoretically, any other device that outputs Wiegand data). The Wiegand interface has two data lines, DATA0 and DATA1. These lines are normally held high at 5V. When a 0 is sent, DATA0 drops to 0V for a few microseconds. When a 1 is sent, DATA1 drops to 0V for a few microseconds. There is usually a few milliseconds between the pulses.

Each of the data lines are connected to hardware interrupt lines. When one drops low, an interrupt routine is called and adds the bits to a buffer. Since the number of bits on a card is variable, the Arduino must wait until it hasn't received any bits for some time. After this time of not receiving any bits, the Arduino will decode the data and output it over serial. I've only added the 26 bit and 35 bit formats, but you can easily add more. For more information about data formats, check out this page.

This was my second Arduino project, and I'm always amazed at how simple it is to get things up and running. It only took me an hour! I especially like having easy functions such as attachInterrupt, as it's much easier than hunting down registers on a PIC or boot.tpl files on a PSoC.
