# tasmota_safepower
Using Tasmota rules as a safe shutdown for linux sbc.

I use rules so it can be run in either ESP8266 or ESP32. For ESP32, it also create a serial bridge using 2nd serial channal, so you can monitor a serial console. 

The rule basically does the following:

- Detect a button press
- Turn a relay on or off and pulse an output call shutdown
- Depending on the number of times and the duration of the press, it does the following:
  1. First press when the system powers up will turn the relay on and change shutdown to low
  2. Second press will pulse the shutdown output
  3. Third press will change shtdown to low and turn relay off for 3 second, then turn it back on
  4. The sequence will repeat from 1.
  5. At anytime, when the button is press and hold for longer than 3 second, shutdown wil be pulsed and relay turn off after 30 second.
 
There is also a companion c program on the linux side which detect the shutdown signal on a GPIO, triggering a falling edge, which issue a system poweroff.

I have tested this on a LC Technology DC5-60V 1 Channel Relay Board, which is a ESP32 based board and a Nanopi Neo 2. 
