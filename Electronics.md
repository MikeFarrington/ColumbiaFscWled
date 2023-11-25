# Disclaimer
This documentation is being written approximately 2.5 years after initial development and may not be entirely accurate.

# WIRING WARNING
Power should only every flow outward from the light connectors coming out of the control box. Light strips do not need termination, and SHOULD NEVER RETURN TO THE CONTROL BOX!  This will likely destroy the electronics within the control box, and may cause a dangerous "thermal runaway" condition within the batteries which can lead to fire (unlikely, but can't be ruled out).

# DESIGN WARNING
This hardware was designed and assembled by a hobbyist and not a professional electroncis engineer.  As such, there is no design documentation (no drawings or 3D designs).

# Hardware Design Overview
The lighting control boxes utilize a WiFi-enabled ESP32-based microcontroller development board, along with power circuitry to accept a wide range of input voltages.  The electronics are enclosed within a project box that appears waterproof, but is not fully waterproof and should not be used outdoors.

A buck/boost conervters is used to accept input power between 12-36V DC, and multiple buck converters are used to provide 5V to the microcontroller and 12V to the lights. Differing models of the input buck/boost converter were used, and certain boxes may accept a wider input range, but 12-36 is the lowest common denominator and should be adhered to.  The power supply should be able to accomidate up to 10A.  A fast-blow glass fuse is included for overcurrent protection.

The microcontroller boards utilize the [Aircookie WLED firmware](https://github.com/Aircoookie/WLED), at version [0.13.1](https://github.com/Aircoookie/WLED/releases/tag/v0.13.1) at the time of initial development and was not updated to a newer version as of the writing of this document.  Many bug fixes and feature improvements have been made to the project since this version was released.

# Ideas for Future Improvements
- Indicator button, as seen on Box #4, to change modes locally by the skaters.  The button on Box #4 was never wired to anything.
- Adding a microphone to enable sound-reactive lighting.  It would allow the lighting to appear to be synchronized to the music being played during the show.
- Device synchronization.  This is a feature within the firmware that can be used to change the lighting all at once.
  - This was never needed as the first use was for a Harry Potter show where each staircase was their own "house colors", or a twinkling candlelight.  The changes would be made manually via the Web UI and took just a couple of seconds to change all four staircases.  When used in its first nutcracker show, a twinkling red and green Christmas pattern was chosen, then never changed throughout the show.
 
# Light Addressing
Each control box has 4 channel outputs.  These outputs can be individually programmed, but this has not been necessary thus far and they all currently work in a duplicating fashion.  The GPIO pin / channel arrangements can be found in the README.md document.  Each channel is currently configured to have 45 segments (two light strips of 22 segments chained onto the included first segment).  The first segment is the one that comes out of the control box and generally remains blank (but can be activated for debugging purposes).  The "Skip 1st LED" option is used to blank out this first segment and prevent lights from shining within the staircase (which may bleed out).  However, this option can be disabled if there is no concern of light bleed.  This can act as a power indicator as there is no such indicator on the control box.

# Light Strips
In the initial design, when used on the staircases designed for the Harry Potter show and subsequently used for The Nutcracker holiday shows, two strips (each strip containing 22 segments) are wired to each channel.  This means that each channel would handle the lighting for two consecutive landings on the staircase.  If an alternating pattern is to be used, as it was in the Harry Potter show, then care should be made to keep the same back-and-forth A/B pattern on the stairs.  For example:
- Ch 1: Tread 1 -> Tread 2
- Ch 2: Tread 3 -> Tread 4
- CH 3: Tread 5 -> Tread 6
- CH 4: Tread 7 -> Tread 8

# Notes on Extending Channels
Please see the WLED documentation with regards to how many segments per channel can be reliably controlled with this level of microprocessor.  While WLED can likely control many more light segments per channel, the power draw may overwhelm the hardware design and cause "voltage sag" where light intensity fades over longer distances.  "Brownouts" may also occur where the devices randomly reboots.  Brownouts experienced during development caused the channel configuration to be lost, requiring those settings to need to be re-entered into the WLED WebUI.  Luckily, other settings such as WiFi configuration are not lost.  This may be a bug that was rectified in newer version of the firmware.
