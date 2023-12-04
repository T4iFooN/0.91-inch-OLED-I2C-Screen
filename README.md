# 0.91-inch-OLED-I2C-Screen examples and setup
This is the example provided by AZ-Delivery for the 0.91 inch OLED I2C Screen

# Disclaimer: 
This repository is just to provide the exact documentation of AZ-Delivery. It is not maintained nor give I any guarantee on things of this documentation or the code of it.
I am in no way affiliated or partnered with AZ-Delivery! This repository is just for reference only.
All linked repositories are maintained and owned by there respective owners and I am not involved in any of them, therefore I am not responsible to damages to your hardware if you use their code wrong or the code is falsy.

## Table of Contents
1. [Introduction](#introduction)
2. [Specifications](#specifications)
3. [The pinout](#pinout)
4. [How to set-up Arduino IDE](#setuparduino)
5. [How to set-up Raspberry Pi and the Python](#setupraspi)
6. [Connecting the screen with Atmega328P Board](#atmega328p)
7. [Library for Arduino IDE](#arduinolib)
   1. [Sketch example](#sketch)
8. [Connecting the screen with Raspberry Pi](#connectionraspi)
   1. [Enabling the I2C interface](#i2cconnection)
   2. [Finding I2C adresses](#i2cadresses)
   3. [Python library](#pythonlib)
   4. [Python script](#pythnscript)


## Introduction <a name="introduction"></a>
OLED stands for Organic Light Emitting Diodes. OLED screens are arrays
of LEDs stacked together in a matrix. The 0.91 OLED screen has a 128x32
pixels (LEDs). To control these LEDs we need a driver circuit or a chip. The
screen has a driver chip called *SSD1306*. The driver chip has an I2C
interface for communication with the main microcontroller. The I2C address
of a driver chip is predefined with value *0x3C*. 

The OLED screen and SSD1306 driver chip operate in the *3.3V* range. But
there is an on-board *3.3V* voltage regulator, which means that these
screens can operate in the *5V* range.

The performance of these screens is much better than traditional LCDs.
Simple I2C communication and a low power consumption make them more
suited for a variety of applications.

## Specifications <a name="specifications"></a>
| Operating voltage range: | from 3.3V to 5V DC                  |
| Communication interface: | I2C                                 |
| Pixel color:             | White                               |
| Operating temperature:   | from -20 to 70 ℃                   |
| Low power consumption:   | less then 8mA                       |
| Dimensions:              | 30 x 12 x 2mm [1.2 x 0.5 x 0.1in    |

To extend the lifetime of the screen, it is common to use a "Screen saver". It
is recommended not to use fixed information over a long time period,
because that shortens the lifespan of the screen and increase so called
"Screen burn" effect.

## The pinout <a name="pinout"></a>
The 0.91 inch OLED screen has four pins. The pinout is shown on the
following image:

**Insert image**

The screen has an on-board *3.3V* voltage regulator. The pins of the 0.91
inch OLED screen can be connected to both *3.3V* or *5V* logic and power
supply without danger to the screen itself.

**NOTE:** When using Raspberry Pi, the power supply should be drawn from
3.3V pin only.

## How to set-up Arduino IDE <a name="setuparduino"></a>
If the [Arduino IDE](https://www.arduino.cc/en/Main/Software) is not installed, follow the link and download the
installation file for the operating system of choice.

**Insert image**

For *Windows* users, double click on the downloaded *.exe* file and follow
the instructions in the installation window.

For *Linux* users, download a file with the extension *.tar.xz*, which has to
be extracted. When it is extracted, go to the extracted directory and open
the terminal in that directory. Two *.sh* scripts have to be executed, the first
called *arduino-linux-setup.sh* and the second called *install.sh*.

To run the first script in the terminal, open the terminal in the extracted
directory and run the following command:
`sh arduino-linux-setup.sh user_name`
**user_name** - is the name of a superuser in the Linux operating system. A
password for the superuser has to be entered when the command is
started. Wait for a few minutes for the script to complete everything.

The second script called *install.sh* script has to be used after
installation of the first script. Run the following command in the terminal
(extracted directory): `sh install.sh`

After the installation of these scripts, go to the *All Apps*, where the
*Arduino IDE* is installed.

**Insert image**

Almost all operating systems come with a text editor preinstalled (for
example, *Windows* comes with *Notepad*, *Linux Ubuntu* comes with
*Gedit*, *Linux Raspbian* comes with *Leafpad*, etc.). All of these text
editors are perfectly fine for the purpose of the ~~eBook~~ repository.

Next thing is to check if your PC can detect an ATmega328P board. Open
freshly installed Arduino IDE, and go to: 
*Tools > Board > {your board name here}*
*{your board name here}* should be the *Arduino/Genuino Uno*, as it
can be seen on the following image:

**Insert image**

The port to which the microcontroller board is connected has to be selected.
Go to: *Tools > Port > {port name goes here}*
and when the microcontroller board is connected to the USB port, the port
name can be seen in the drop-down menu on the previous image. 

If the Arduino IDE is used on Windows, port names are as follows:

**Insert image**

For *Linux* users, for example port name is */dev/ttyUSBx*, where *x*
represents integer number between *0* and *9*.

## How to set-up Raspberry Pi and the Python <a name="setupraspi"></a>
For the Raspberry Pi, first the operating system has to be installed, then
everything has to be set-up so that it can be used in the *Headless* mode.
The *Headless* mode enables remote connection to the Raspberry Pi,
without the need for a *PC* screen Monitor, mouse or keyboard. The only
things that are used in this mode are the Raspberry Pi itself, power supply
and internet connection. ~~All of this is explained minutely in the free eBook:
[Raspberry Pi Quick Startup Guide](https://www.az-delivery.de/products/raspberry-pi-kostenfreies-e-book?ls=en)~~

The *Raspbian* operating system comes with *Python* preinstalled.

## Connecting the screen with Atmega328P Board <a name="atmega328p"></a>
Connect the 0.91 inch OLED screen with the Atmega328P Board as shown
on the following connection diagram:

**Insert image**

| Screen pin | Board pin | Wire color |
|------------|-----------|------------|
| SDA        | A4        | <span style="color:blue;">**Blue**</span>       |
| SCK        | A5        | <span style="color:green;">**Green**</span>      |
| VCC        | 5V        | <span style="color:red;">**Red**</span>        |
| GND        | GND       | **Black**     |

## Library for Arduino IDE <a name="arduinolib"></a>
To use the screen with Atmega328P Board, it is recommended to download
an external library for it. The library that is used in this ~~eBook~~ repository is called the
*U8g2*. To download and install it, open Arduino IDE and go to: 
*Tools > Manage Libraries*. 
When a new window opens, type *u8g2* in the search box and install the
library [*U8g2* made by *oliver*](https://github.com/olikraus/u8g2/), as shown in the following image:

**Insert image**

Several sketch examples come with the library, to open one, go to:
*File > Examples > U8g2 > full_buffer > GraphicsTest*
The screen can be tested with this sketch. In this ~~eBook~~ repository, the sketch code is
modified in oreder to create more beginner friendly version of code.

### Sketch example <a name="sketch"></a>
The example script written in C can be found [within this repository](https://raw.githubusercontent.com/T4iFooN/0.91-inch-OLED-I2C-Screen/main/arduino_sketch_example.c).

At the beginning of the sketch two libraries are imported the *U8g2lib* and
*Wire*. 

Next, object called *u8g2* is created, with the following line of code:
`U8G2_SSD1306_128X32_UNIVISION_F_HW_I2C u8g2(U8G2_R0, U8X8_PIN_NONE);`

The created object represents the screen itself and it is used to control the
screen. The *U8g2* library can be used for many other OLED screens, thus
there are many constructors in the sketch examples from the library.

After that, the function called `u8g2_prepare()` is created, which has no
arguments and returns no value. Inside this function, five *u8g2* library
functions are used.

The first function is called `setFont()` which has one argument and returns
no value. The argument represents the *u8g2* font. The list of available fonts
can be found on the following [link](https://github.com/olikraus/u8g2/wiki/fntlist8x8).

The second function is called `setFontRefHeightExtendedText()`
which has no arguments and returns no value. It is used for drawing
characters on the screen. More detailed explanation of this function can be
found on the following [link](https://github.com/olikraus/u8g2/wiki/u8g2reference#setfontrefheightextendedtext).

The third function is called `setDrawColor()` which has one argument and
returns no value. The argument value is an integer number which
represents a color index for all drawing functions. Font drawing procedures
use this argument to set the foreground color. The default value is *1*. If it is
set to *0*, then the space around the character is lit up, and the character is
not. Argument value *2* can also be used, but there is no differense from *0*.

The fourth function is called `setFontPosTop()` which has no argument
and returns no value. This function controls the character position in one
line of the text. The function has a couple of versions. The first is
`setFontPosBaseLine()` second is `setFontPosCenter()`. The third is
`setFontPosBottom()` and their purpose is to change the position of the
characters in the one line.

The fifth function is called `setFontDirection()`, which has one
argument and returns no value. The argument is an integer number which
represents direction of the text. The value is an integer number in the range
of *0* to *3*, where *0* = *0°*, *1* = *90°*, *2* = *180°* and *3* = *270°*.

The function called `drawStr()` has three arguments and returns no value.
It is used to display a constant string on the screen. The first two arguments
represent the *X* and *Y* position of the cursor, where the text is displayed.
The third argument represents the text itself, a constant string value. The
functions that set text layout before using `drawStr()` function should be
used, otherwise the `drawStr()` function uses default settings for the font,
size and overall layout of the text.

To display shapes, specific functions for each shape are used:

The function called `drawFrame()`, has four arguments and returns no
value. It is used to display a frame, an empty rectangle. The first two
arguments represent the *X* and *Y* position of the top left corner of the frame.
The third argument represents the width of the frame and the fourth
argument represents the height of the frame.

The function called `drawRFrame()` has five arguments and returns no
value. It is used to display a frame with rounded corners. The first two
arguments represent the *X* and *Y* position of the top left corner of the frame.
The second two arguments represent the width and height of the frame and
the fifth argument represents the corner radius.

The function called `drawBox()` has four arguments and returns no value. It
is used to display a filled rectangle. The first two arguments represent the *X*
and *Y* position of the top left corner of the rectangle. The second two
arguments represent the width and height of the rectangle,respectively.

The function called `drawRBox()` has five arguments and returns no value.
It is used to display a filled rectangle with rounded edges. The first two
arguments represent the *X* and *Y* position of the top left corner of the
rectangle. The second two arguments represent the width and height of the
rectangle, respectively. The fifth argument represents the corner radius.

The function called `drawCircle()` has three arguments and returns no
value. It is used to display a circle. The first two arguments represent the *X*
and *Y* positions of the circle center point. The third argument represents the
circle radius.

The function called `drawDisc()` has three arguments and returns no
value. It is used to display a disc. The first two arguments represent *X* and
*Y* position of the disc center point. The third argument represents the disc
radius.

The function called `drawTriangle()` has six arguments and returns no
value. It is used to display a filled triangle. The first two arguments represent
the *X* and *Y* position of the first corner point of the triangle. The second two
arguments represent the *X* and *Y* positions of the second corner point of the
triangle. The last two arguments represent the *X* and *Y* positions of the last
corner point of the triangle.

The function called `drawLine()` has four arguments and returns no value.
It is used to display a line. The first two arguments represent the *X* and *Y*
position of the starting point of the line. The second two arguments
represent *X* and *Y* position of the end point of the line.

The function called `drawUTF8()` has three arguments and returns а value.
It is used to display a text, the string value which may contain a character
encoded as a Unicode character. The first two arguments represent the *X*
and *Y* position of the cursor and the third represents the text itself. The
Unicode characters can be displayed in a couple of ways. The first is to
copy and paste the existing character into the sketch, like in the following
line of the code: `u8g2.drawUTF8(50, 20, "☂")`
The second is to create a char array, which has two values: the first value
is a hexadecimal number of the Unicode character, and the second value
is a null character *("\0")*. This can be done by using the char array called
*COPYRIGHT_SYMBOL*, like in the following lines of the code:
```
const char COPYRIGHT_SYMBOL[] = {0xa9, '\0'}
u8g2.drawUTF8(95, 20, COPYRIGHT_SYMBOL); //COPYRIGHT SYMBOL
```

The third way of using the function is to use a hexadecimal number for the
character itself, like in the following line of code:
`u8g2.drawUTF8(115, 15, "\xb0"); // DEGREE SYMBOL`

The function returns a value, an integer number which represents the width
of the text *(string)*.

To display something on the screen, the screen data buffer has to be
cleared first, then a new value is set (an image) for data buffer, then a new
value of data buffer is send to the screen. This way, a new image is
displayed on the screen. In order to see this change, `delay()` function has
to be used to shift the next change of the data buffer, like in the following
lines of code:
```
u8g2.clearBuffer();
u8g2_bitmap(); // setting the data buffer
u8g2.sendBuffer();
delay(time_delay);
```

## Connecting the screen with Raspberry Pi <a name="connectionraspi"></a>
Connect the screen with the Raspberry Pi as shown on the following
connection diagram:

**Insert image**

| Screen pin | Raspberry Pi ping | Physical pin No. | Wire color |
|------------|-------------------|------------------|------------|
| SDA        | GPIO2             | 3                | <span style="color:blue;">**Blue**</span>       |
| SCK        | GPIO3             | 5                | <span style="color:green;">**Green**</span>      |
| VCC        | 3V3               | 1                | <span style="color:red;">**Red**</span>        |
| GND        | GND               | 9                | **Black**      |

### Enabling the I2C interface <a name="i2cconnection"></a>
In order to use the screen with Raspberry Pi, I2C interface has to be
enabled. Open following menu: 
*Application Menu > Preferences > Raspberry Pi Configuration*

**Insert image**

In the new window, under the tab *Interfaces*, enable the I2C radio
button, as on the following image:

**Insert image**

> TODO: Add description for raspi-config

### Finding I2C adresses <a name="i2cadresses"></a>
If it is enabled, we will use the command i2detect to find the module on the 
I2C bus: `i2cdetect -y 1`
The result should look like the one shown below:

**Insert image**

Our device was recognised with the address "0x3c". This is the standard 
address for this type of device.

#### Troubleshooting
If you connected the screen correctly but don't get any output on `i2cdetect -y 1` the baudrate of the I2C is propably wrong.
To correct this you must edit the boot config file:
`sudo nano /boot/config.txt`
Here you must add `dtparam=i2c1_baudrate=50000`, save the file with *Ctrl+O* and exit it with *Ctrl+X*. Afterwards you need to reboot you Pi `sudo reboot now`.

### Python library <a name="pythonlib"></a>
For the display of shapes, text and images we will use a Python library. On 
the current Raspberry Pi OS, Python3, pip3 and git are already preinstalled, but if this is not the case, you can install the whole thing with the 
following commands: 

```
sudo apt-get install -y \
   python3-dev \
   libffi-dev \
   libssl-dev \
   python3-pil \
   libjpeg-dev \
   zlib1g-dev \
   libfreetype6-dev \
   liblcms2-dev \
   libopenjp2-7 \
   libtiff5
```

```
sudo apt-get install -y \
   python3-rpi.gpio \
   python3-pip
```

`sudo apt-get install git -y`

We use the "luma.oled" library, which can be installed with the following 
command:
`sudo -H pip3 install luma.oled`

### Python script <a name="pythnscript"></a>
In the folder "pi" (or your respective user) we now create a folder called "oled" and go to this folder
```
sudo mkdir oled
cd oled
```

luma.oled offers many examples and we can download them with the 
following command:
`sudo git clone https://github.com/rm-hull/luma.examples`
with:
`cd luma.examples/examples/`
we change to the folder in which the examples are located.
and with:
`python3 demo.py`
we can start one of the examples. If there is a white noise on the display,
the correct controller must be passed. this can be done with:
`python3 demo.py --device [controller]`
luma.oled uses the SSD1306 by default, if you have SH1106 for example,
starting the script would look like this:
`python3 demo.py --device ssh1106`

There are more examples in the folder. 
With the command:
`ls -a`
you can see them.
Try out more examples.
And with:
`sudo nano [examplescript]`
the scripts can be edited.

Now is the time to learn and make projects on your own. You can do that
with the help of many example scripts and other tutorials, which can be
found on the Internet.
