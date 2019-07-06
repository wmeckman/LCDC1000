# LCDC1000
An ESP32 based controller that can drive any kind of LED strip, or motor. Includes microSD, USB-UART, and large voltage range input.

![alt text](https://github.com/wmeckman/LCDC1000/blob/master/LCDC1000_title.jpeg)

This project started as a Wifi and bluetooth controller that could drive any type of LED strip. LED strip controllers are everywhere, but I wanted a controller that I could customize without using a breadboard. As the project progressed, I wanted this board to be able to drive motors as well. I added a microSD card for file storage, and a USB-UART for debug. Here are the main features:

ESP32 based using MicroPython
Drives Any type of LED strip - RGB, RGBW, WS2812, APA102, Neopixel, etc
Wide input power range: 4.5V to 30V DC.
Input power via Barrel Jack 2.10mm ID (0.083"), 5.50mm OD or Terminal Block.
Reverse polarity input power protection.
Drives 1 stepper motor in full H-bridge configuration.
Drives 2 bipolar DC motors in half H-bridge configuration.
Drives 4 Unipolar DC Motors.
Additional outputs for servo motors available.
Current sense for motor/LED drivers.
Outputs on terminal blocks.

Power: 4.5V-30V DC power can be applied either through the barrel jack or the terminal block (not both). An on-board regulator is used to create the 3.3V necessary for the ESP32, MicroUSB, and USB-UART.  The power input on J6 and J5 is equal to the power output on J7.  Use a power supply that is designed to drive what is connected on the output.  For example, if driving a 12V RGB LED strip, use a 12V power supply.  

To use the board, connect whatever you're controlling (LED, motor, etc) to the terminal blocks (J3, J4, J7), then apply power to J5 or J6.  The 'connection notes' section provides more in depth instruction by device.

Pinouts

J6 Barrel Jack Input Power

    Pin:  +Vin 4.5V to 30V
    Shield:  Ground

J5 Input Power Terminal Block

    1:  +Vin 4.5V to 30V
    2:  +Vin 4.5V to 30V
    3:  Ground
    4:  Ground

J7 Output Power Terminal Block

    1:  +Vout
    2:  +Vout
    3:  Ground
    4:  Ground

J3, J4, J8 High Current Motor and RGB, RGBW LED Drive Terminal Block

    J3-1:  Power Out
    J3-8:  Drive1Out1
    J4-1:  Drive1Out2
    J4-2:  Drive2Out1
    J8-1:  Drive2Out2
    J8-2:  Ground

J9 and J10:  SPI, and PWM Drive Signals for Servo Motor, individually addressable LED's Terminal Block

    J9-1:  GPIO_2 (ESP32 IO2)
    J9-2:  GPIO_5 (ESP32 IO5) 
    J10-1:  LED_DATA (ESP IO19)
    J10-2:  LED_CLK (ESP IO18)

Test Point Header Pins

    TP1:  TDI_SD_MISO - Primarily used to SD card, but can be used for JTAG
    TP2:  TDO_SD_CD - Primarily used to SD card, but can be used for JTAG
    TP3:  TMS_SD_CLK - Primarily used to SD card, but can be used for JTAG
    TP4:  TCK_SD_MOSI - Primarily used to SD card, but can be used for JTAG
    TP5:  ESP32 Enable
    TP7:  IO17
    TP8:  GPIO_0 - ESP32 IO0
    TP9:  ESP32 IO35
    TP10:  ESP32 SENSOR_VP
    TP11:  ESP32 SENSOR_VN
    TP12:  +Vout
    TP13:  +Vout
    TP14:  +Vout
    TP17:  GND
    TP18:  GND
    TP19:  GND
    USBPWR_TP:  USB Power 

Note:  TP2, TP7, TP8 are arranged on the PCB with TP12-TP14, and TP17-TP19 to be compatible with servo motor connections.

---------------------------------------------------------------------------------------------------

Connection Notes:  Overview of connections for various devices

Individually addressable LED's - WS2812, NeoPixel, etc.

    J7-1:  LED Power
    J7-4:  LED Ground
    J9-1:  LED Data

Individually Addressable LED's - APA102, SK9822, DotStar, etc.

    J7-1:  LED Power
    J7-4:  LED Ground
    J10-1:  LED Data
    J10-2:  LED Clock

J10-1, and J10-2 are connected to the ESP32 SPI bus.  This provides the highest speed possible.  Additional LED strips can be connected using lower speed GPIO pins.  

Low speed GPIO connection example:

    J7-2:  LED Power
    J7-3:  LED Ground
    J9-1:  LED Data
    J9-2:  LED Clock

RGB Strips

    J7-1: LED Power
    J3-1: R
    J3-2: G
    J3-3: B

RGBW Strips

    J3-1: LED Power
    J3-2: R
    J4-1: G
    J4-2: B
    J8-1: W

Bipolar DC Stepper Motor

    J3-2:  Coil1+
    J4-1:  Coil1-
    J4-2:  Coil2+
    J8-1:  Coil2-

Unipolar DC Stepper Motor 5 Wire

    J3-2:  Coil 1
    J4-1:  Coil 2
    J4-2:  Coil 3
    J8-1:  Coil 4
    J7-3:  Ground

Unipolar DC Stepper Motor 6 Wire

    J3-2:  Coil 1
    J4-1:  Coil 2
    J4-2:  Coil 3
    J8-1:  Coil 4
    J7-3:  Ground
    J7-4:  Ground

DC Motor Unidirectional  :  Connect up to 4

    Use J3-2 or J4-1 or J4-2 or J8-1 for (+) wire
    Use J7-3 or J7-4 for (-) wire

DC Bidirectional Motor  :  Connect up to 2

    J3-2: Motor 1 (+) 
    J4-1: Motor 1 (-)
    J4-2: Motor 2 (+) 
    J8-1: Motor 2 (-)

Servo Motors

    J7-1 Servo 1 Power +
    J7-3 Servo 1 Power -
    J9-1 Servo 1 Control

    J7-2 Servo 2 Power +
    J7-4 Servo 2 Power -
    J9-2 Servo 2 Control

Additional Servos can be connected on the header pins.
