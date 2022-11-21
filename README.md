# InverterOfThings Logger
ESP8266 based WiFi interface for Voltronic Axpert MppSolar PIP inverters

**Note that this project is incomplete, It doesn't do anything useful yet!**

# Overview
Based around an ESP8266 WiFi microcontroller.
Software is built using [Arduino for ESP8266](https://github.com/esp8266/Arduino). It's the simplest way to get the toolchain.

**UART0:** Used for programming and debugging

**UART1:** Hardware TX only, I've implemented a software receiver. Talks to the inverter at 2400 baud

**I2C:** Kept open for optional accessories

**GPIO:** Button on GPIO0, changes wifi mode, also used for programming when DTR pin isn't available.

**GPIO:** LEDs on GPIO 15 and 16 provide status.

**POWER:** Inverter has +12V on pin 4 or 7 depending on the model. I used a cheapo DC-DC converter module to bring this down to ~5V, then a 1117-3.3V linear regulator to provide 3.3V. It draws about half a watt while the WiFi is connected.

**LOGGING:** The voltages, currents etc are uploaded to thingspeak.com. 4 different channels are used, you'll have to create an account and make the channels:
- Battery: Write only
- Load: Write only
- Charger: Write only
- Settings: Read/Write

Each thingspeak channel provides a read and write API key. These keys will be set on the logger using a served webpage (it's not implemented yet)

**WIFI:** The logger defaults to AP mode with the ssid 'Setup'. Connect to 192.168.4.1/wifi to setup the access point to connect to. You'll be given a list of APs in range to connect to. Select the AP, enter the password, then click submit to connect. The AP will be stored and the logger will connect automatically on next boot.

Press the button on GPIO0 to go back to AP mode if you need to change the AP to connect to. (It might not respond if it's busy uploading, keep trying...)

# Parts required to build one

Most of the parts can be bought as modules, it's usually cheaper that way.

Approximate prices found on aliexpress
- ESP-07 or ESP-13 module with breakout adapter board ($3.00)
- MAX3232 module ($0.50) - it's just a max3232 with 5 capacitors on a tiny little board
- DC-DC buck module ($1.00) - 12v down to 5v
- AMS1117-3.3V ($1.00) - Or any 3.3V regulator
- USB-TTL serial module ($1.50) - Make sure it has RTS and DTR outputs
- RJ45 socket with LEDs ($0.50) - The leds are for status etc.
- Tact switch ($0.00) - I'm sure you have an old button lying around.

Total cost: $7.50

