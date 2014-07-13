Use an Arduino with an RFM69HW radio as a TNC for a Linux system.

For this I used a simple Arduino in a TNC-like setup.

Arduino:
The code from Arduino/radio_bridge.ino must be put in an Arduino.
I tested it with a Arduini Mini Pro, 3.3V, 8MHz, AtMega328.

Arduino                 RFM
- digital I/O pin 2     DI0 on the RFM
- 3,3V                  3,3V
- GND                   GND
- digital I/O pin 10    NSS
- digital I/O pin 11    MOSI
- digital I/O pin 12    MISO
- digital I/O pin 13    SCK

Then connect the Arduino to the Linux system.
Here's the pin layout for a Raspberry Pi but you can, of course,
use a serial-to-usb adapter to connect the Arduino to your linux
system as well.:
Arduino                 RPI
- 3,3V                  3,3V [1]
- GND                   GND  [6]
- TX                    RX   [10]
- RX                    TX   [8]

The code from Linux/ can be run on the Linux system.
Run "make" to build things.

	rgr_beacon /dev/ttyAMA0 "Hello, this is dog." 5

This will send a beacon (just the text given) every 5 seconds.
Any received messages will be shown. If you don't want that,
set "verbose = false" in the top of main().

	rgr_listen /dev/ttyAMA0

This will only listen and show what is received.

	rgr_kiss /dev/ttyAMA0 FH4GOU-1

This will start an AX25 network device with call sign "FH4GOU-1".
All traffic in and out will be routed over the radio.

If any program gives an error code, then this is what they mean:

210	unspecified
211	time out
212	escape out of range
213	unexpected start byte
214	end without start
215	buffer overflow

They're all related to communication between the Arduino and
the Linux system.
If you get them a lot, then check the cabling between the
arduino and the Linux box.


Any feedback can go to: mail@vanheusden.com

[![Flattr this git repo](http://api.flattr.com/button/flattr-badge-large.png)](https://flattr.com/submit/auto?user_id=flok&url=https://github.com/flok99/radio_gateway_rpi&title=radio_gateway_rpi&language=&tags=github&category=software)
