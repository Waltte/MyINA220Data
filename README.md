# MyINA220Data
Short INA220 I2C programming guide


## Registers

#### Device Addresses 80h ... 8Fh
Depending on the A0 and A1 pins, you can have address between hex 80 and 8F <br>
Typical GND GND will give the address <b> 80 </b>

#### Configuration register 00h
The configuration register <b> 0x00 </b> default value is: <br>
<b> 00111001 10011111 </b> <br>
or 39 9F <br>

| 15  |  14  |  13 |12 ... 11|10 ... 7|6 ... 3|2 ... 0|
|--------|---|---|---|---|---|---|
|Reset||Bus V range|Shunt V gain|Bus ADC res & avg|Shunt ADC res & avg |  MODE  |

<br>

<b>Bus V range</b> 16 V (0) , or 32 V (1) <br>
<b>Shunt V gain</b> (divider) between 1 and 8 (default) <br>
<b>ADC resolution & averaging</b> will get a larger res and averaging with increasing value <br>
1101 will give averaging of 32 samples. <br>
1000 wille give a single 12-bit value. <br>
<b>Mode</b> has 000 as power-down mode and 111 as continous measuring.<br> 
You can also enable triggering and disable ADC with mode.

#### Shunt voltage register 01h
  The shunt voltage can be read from this 16 bit register <br>
  LSB is always 10 uV. Read straight into an int16_t variable.<br>
#### Bus voltage register 02h
  <b> Register value must be shifted 3 bits right </b>.<br>
  The last 3 bits are for "conversion ready" and overflow -flags.<br>
  Bus voltage register LSB is 4 mV.<br>
  To get actual voltage, multiply the integer value with 0.004 to get V, or 4 to get result in mV.
#### Power register 03h
  To use power register, the calibration register must be filled.
#### Current register 04h
  To use current register, the calibration register must be filled.
#### Calibration register 05h
  Calibration does not seem to increase the accuracy, however it will leviate the MCU from making the conversions.<br>
  <b> usage of calibration register might be updated at a later time </b>
