# ColumbiaFscWled
Simple WLED lighting project for Columbia Figure Skating Club

# Background:
   Four LED control devices were assembled using a WiFi-equipped ESP32-based microcontroller dev boards.  These devices run the WLED firmware into project boxes.  Each box is similar, but may contain minor hardware differences with respect primarily to input voltages due to the use of differing buck/boost voltage converters.  Each box is labeled with a name, as well as its power input requirements.  

# Wireless Networking:
The controllers communicate using WiFi 802.11b at 2.4GHz.  When the controllers power-up, they will first seek out a pre-programmed wireless access point (WAP) with the SSID of CFSC-WLED-AP using a stored password.  If the WAP cannot be found, the WLED firmware will fallback to act itself as standalone access point using the same pre-defined password, but whose SSID is the name printed on the box (ie: CFSC-WLED-01).  This allows for the device to be re-programmed in the abscense of the expected WAP in the event that the expected WAP is lost or damaged.

In past shows, the WAP was located above the disused electic ice resurfacing machine (beneath the scoreboard).  It was taped onto the painted cinderblock walls using gaffer's tape, being careful not to fully block the air vents on the top surface of the device.  The two antennas should be pointed mostly upwards, but each with a slightly different angle.  It may not be totally necessary to mount it in this manner, but we thought it best to get it away from the metal of the resurfacing machine while also using a dedicated power outlet high up on the wall that would reduce the potential of the WAP being unplugged during the show.

In this location, all of the control boxes connected successfully from their positions on both the near and far side of the rink, and the operator was able to send commands to the controllers using a web-enabled tablet computer from anywhere in the near-half of the rink (farther distances were not attempted, but likely would have worked).

# Device Mounting



WiFi Access Point (WAP):
   Linksys WRT54G
   S/N: CDF003168204
   MAC: 00-06-25-BB-FA-85
   Power Input: 5VDC/2A
   SSDI: CFSC-WLED-AP
   WiFi Protocols: 802.11a + 802.11g
   Password: SkateShow
   Security: WPA2 Personal (PSK) + AES
   IP: 192.168.1.1
   Subnet Mask: 255.255.255.0
   DHCP Enabled: Yes
   Firmware: Tomato v1.28
   Web UI address: http://192.168.1.1
   Web UI username: admin 
   Web UI password: SkateShowAdmin

WLED-based Controllers:
- CFSC-WLED-01:
  - Hostname: CFSC-WLED-01.local
  - Firmware: WLED v0.13.1 (build 2203150)
- cfsc-wled-02.local
- cfsc-wled-02.local
- cfsc-wled-02.local


Standalone operation:
Router IP: 4.3.2.1
DHCP first device: 4.3.2.2
subnet 255.255.255.0


WLED v0.13.1 (build 2203150)
