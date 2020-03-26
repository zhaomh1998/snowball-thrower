# Automated buying item and consume for trust grinding in Xenoblade Chronicles 2 on Arduino

### How to use
Upload the compiled joystick.bin into Arduino from it's DFU mode, then plug in your Arduino to Nintendo Switch Type-C port through a Type-C to USB converter or plug into USB port on Nintendo Switch dock. In game, walk close enough to a store so that pressing "A" opens the store. Arduino will act as a automated joystick that buys max amount of the first item in the store, and consume that pouch item 20 times on the first character, then repeat.

### Uploading code to Arduino
#### Windows
Download and install FLIP https://www.microchip.com/developmenttools/productdetails.aspx?partno=flip, connect Arduino to computer, and install the USB driver from (flip installation folder)\usb.
Put Arduino in DFU mode, choose correct target device (ATmega16U2 for Arduino Uno and Mega), press ctrl+U and click "open" to connect to Arduino. Ctrl+L to load HEX file "joystick.bin". Check all four options on the left: Erase, Blank Check, Program and Verify, then hit "Run" to upload the code onto Arduino. When you see green circles, the uploading is done.
#### MacOSX
Check https://www.arduino.cc/en/Hacking/DFUProgramming8U2 under section `Download a DFU Programmer` for setting up the dfu-programmer.
Put Arduino in DFU mode as shown in the same link, and 

### Editing the code and compiling
If you only want to modify script logic flow, the only file you want to look at is joystick.c The scripe logic is in step[].
You will need to set up the following
#### LUFA Library
Clone https://github.com/abcminiuser/lufa, and set the `LUFA` folder's relative path at `LUFA_PATH` in Makefile.

#### AVR Toolchain
##### Windows and others
Follow http://www.fourwalledcubicle.com/files/LUFA/Doc/151115/html/_page__compiling_apps.html to setup environment for building for your specific environment
##### MacOSX
Follow https://github.com/osx-cross/homebrew-avr to use homebrew for installing AVR Toolchain
Then just run `make` to compile and obtain the updated `joystick.bin`


## Switch-Fightstick
Proof-of-Concept Fightstick for the Nintendo Switch. Uses the LUFA library and reverse-engineering of the Pokken Tournament Pro Pad for the Wii U to enable custom fightsticks on the Switch System v3.0.0.

### Wait, what?
On June 20, 2017, Nintendo released System Update v3.0.0 for the Nintendo Switch. Along with a number of additional features that were advertised or noted in the changelog, additional hidden features were added. One of those features allows for the use of compatible controllers, such as the Pokken Tournament Pro Pad, to be used on the Nintendo Switch.

Unlike the Wii U, which handles these controllers on a 'per-game' basis, the Switch treats the Pokken controller as if it was a Switch Pro Controller. Along with having the icon for the Pro Controller, it functions just like it in terms of using it in other games, apart from the lack of physical controls such as analog sticks, the buttons for the stick clicks, or other system buttons such as Home or Capture.

### But games like ARMS use the analog sticks!
The Pokken Tournament Pro Pad was made by HORI, who also makes controllers for other consoles; because of this, the descriptors provided to Nintendo for the Pokken controller are **very** similar to that of some third-party PS3 controllers. In fact, the Pokken Tournament Pro Pad -can- be used on the PS3 without anything special needing to be done. The original descriptors feature 13 buttons, two analog sticks, a HAT switch, and some vendor-specific items that we can safely ignore. Compare this to a PS3 controller, which has...13 buttons (4 Face, 4 Shoulders, 2 Sticks, Select/Start, and PS), two analog sticks, and a HAT switch (the D-Pad). 

### What do you mean by 'original descriptors?'
Turns out we can modify the descriptors to expose up to 16 buttons at **least**. The Switch Pro Controller has 14 buttons on it, and as it turns out, the modified set of descriptors does allow us to enable the use of the most important button:

### Is it the Captu-

# THE CAPTURE BUTTON

The Switch Pro Controller also exposes **additional** buttons within its descriptors; however, it's unknown as to what those do at this time. These come immediately after the HAT, so I'm under the assumption that they may be individual button presses instead of an angle. That being said, considering how flexible the Switch is with the Pokken controller descriptors, we may be able to mirror the Switch Pro Controller descriptors up to a certain point.
