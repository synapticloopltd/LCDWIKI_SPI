# LCDWIKI_SPI Library

This is a library for the SPI LCD display, which supports the following LCD Controllers.  Before using any of the functions in this library, you will need to `#define` the model number from the list below, and set the pins, and possibly set the `MISO` and `MOSI` pins as well.

 - **`ILI9325`**
 - **`ILI9328`**
 - **`ILI9341`**
 - **`HX8357D`**
 - **`HX8347G`**
 - **`HX8347I`**
 - **`ILI9486`**
 - **`ST7735S`**
 - **`SSD1283A`**
 - **`SH1106`**
 - **`ST7735S128`**
 - **`ILI9488`**
 - **`ILI9488_18`**
 - **`ILI9225`**
 - **`ST7796S`**

# The most notable additions

1. `Push_Compressed_Image()` function - if you want to know the format and details of the compression see [Image Compression Algorithm for the 4" TFT SPI ST7796S on an Arduino](https://medium.com/@synapticloop/image-compression-algorithm-for-the-4-tft-spi-st7796s-on-an-arduino-50d64021cf5d).
2. `Read_GRAM()` fix so that it is reset to write mode after reading it, rather than trying to remember to pass the opaque sounding `flag` set to `first`.
3. General code cleanup and method documentation

## Download And Installation

Click on the `<> Code` button (top right of the screen), and then select `Download ZIP`

![Downloading the code](/Document/images/arduino-download-library.png)

Unzip the library and move the newly unzipped folder folder into your `Arduino/libraries/` directory

Restart the Arduino IDE

## Usage
You will need to include the library in your sketch project, at the top of the file:

```
#include <LCDWIKI_SPI.h>    //Hardware-specific library
```

You may also want to include the `LCDWIKI_GUI` library as well:

```
#include <LCDWIKI_GUI.h>    //Core graphics library
```

## Quickstart Code

### Arduino UNO
```c++
//paramters define
#define MODEL ST7796S // this is the model number of the chipset that you are using
#define CS A5
#define CD A3
#define RST A4
#define LED A0  //if you don't need to control the LED pin,you should set it to -1 and set it to 3.3V

// If you need to use Software SPI - which is not recommended as it is much slower - you will need to set the MOSI and SCK pins as well
#define MOSI  11
#define SCK   13
```

### Arduino mega2560

```c++
//paramters define
#define MODEL ST7796S // this is the model number of the chipset that you are using
#define CS A5
#define CD A3
#define RST A4
#define LED A0  // if you don't need to control the LED pin,you should set it to -1 and set it to 3.3V

// If you need to use Software SPI - which is not recommended as it is much slower - you will 
// need to set the MISO, MOSI, and SCK pins as well


#define MISO  50
#define MOSI  51
#define SCK   52

```

### Common Setup Code

Once the pins are set, then you need to initialise the LCD, which is the same for either Arduino device depending on whether you are using software or hardware SPI.

```c++

// NOTE: Initialise only __ONE__ of the following

LCDWIKI_SPI mylcd(MODEL, CS, CD, RST, LED); // this is for the hardware SPI
LCDWIKI_SPI mylcd(MODEL, CS, CD, MISO, MOSI, RST, SCK, LED); // this is for the software SPI


void setup() {
  mylcd.Init_LCD();
  // mylcd.Do_Your_Code_Here();
}

```

---

### Previous Library License README.txt

--- 

This is a library for the SPI lcd display.

This library support these lcd controller:

- ILI9325 
- ILI9328 
- ILI9341 
- HX8357D 
- HX8347G 
- HX8347I 
- ILI9486 
- ST7735S 
- SSD1283A

Check out the file of LCDWIKI SPI lib Requirements for our tutorials and wiring diagrams.

These displays use spi bus to communicate, 5 pins are required to interface (MISO is no need).

Basic functionally of this library was origianlly based on the demo-code of Adafruit GFX lib and Adafruit SPITFT lib.  

MIT license, all text above must be included in any redistribution

To download. click the DOWNLOADS button in the top right corner, rename the uncompressed folder `LCDWIKI_SPI`. Check that the `LCDWIKI_SPI` folder contains `LCDWIKI_SPI.cpp` and `LCDWIKI_SPI.h`

Place the `LCDWIKI_SPI` library folder your `<arduinosketchfolder>/libraries/` folder. You may need to create the libraries subfolder if its your first library. Restart the IDE

Also requires the LCDWIKI_GUI library for Arduino. 
[https://github.com/lcdwiki/LCDWIKI_gui]()
