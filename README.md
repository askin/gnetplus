# gnetplus.py
-------------

## Python module for interfacing with the Mifare RFID card reader

- The reader is the PCR310U Promag contact-less card reader made by 
GIGA-TMS Inc gigatms.com.tw.

- The module gnetplus.py can be invoked on the command line or 
be a module in a python program.

- On a Linux machine, no additional drivers or libraries are needed
as the PCR 310U is detected as "Prolific Technology, Inc. PL2303 Serial Port"
which is a USB-serial device.

## Communicating with the reader:
---------------------------------

When the reader is plugged into a Linux machine such as a Raspberry Pi,
Fedora etc, a new serial USB port is assigned.  Check the command "dmesg" 
for the actual assignment of the port.  It would look something like 

                  /dev/ttyUSBNNN where N is a number.  

/dev/ttyUSB0 is an example.  You MUST know what the port assignment 
is before invoking the gnetplus.py program or it will throw up an 
exception/error.

The syntax to invoke the script is:

                 % python gnetplus.py /dev/ttyUSB0

replace the 0 with the right number assigned.

## The card to use:
-------------------

The cards that work with this reader are the ISO14443A Card Type, 
MIFARE(r) Ultra-Light/1K/PRO Cart Types.

## Example output:
------------------

- when the reader is inserted into a USB port, the following is a snippet
  of the dmesg output indicating the port assigned:

  usb 6-1: new full-speed USB device number 6 using uhci_hcd
  usb 6-1: New USB device found, idVendor=067b, idProduct=2303
  usb 6-1: New USB device strings: Mfr=1, Product=2, SerialNumber=0
  usb 6-1: Product: USB-Serial Controller D
  usb 6-1: Manufacturer: Prolific Technology Inc. 
  pl2303 6-1:1.0: pl2303 converter detected
  usb 6-1: pl2303 converter now attached to ttyUSB3

The key info is the ttyUSB3 as seen above. The full path to the port is
/dev/ttyUSB3 for the example above.

- invoke the python module as:

       python gnetplus.py /dev/ttyUSB3

- bring a compliant card close to the reader and reader will beep as well as 
  light up the left LED on the reader.

- on the screen, you will see messages like the following:

   $ python gnetplus.py /dev/ttyUSB3

    Tap card again.
    Found card: 0x19593d65
    Tap card again.
    Found card: 0x19593d65
    Tap card again.
    Tap card again.
    Tap card again.
    Tap card again.
    Found card: 0x19593d65

- the script returns either the "Tap card again." message or a message
"Found card: 0xNNNNNNNN" where NNNNNNNN is the serial number of the card
that it was able to detect. 

- the script shows how you can communicate with the reader and does not
  provide any writing to the smart card functions. 


