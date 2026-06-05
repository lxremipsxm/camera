# Notes about Hardware

--- 

## OV7670
NA so far


## MicroSD
NA so far


## SWD Header
1.  Exposes the SWD peripheral that can be used to debug with a STLink


## ILI9341 Display **HEADER**
NA so far


## AP3602A Regulated Charge-Pump
1. Outputs up to 250mA current after charging
2. SHDN cannot be floating, tie to GPIO pin HIGH (enable) or LOW, never leave floating
3. Bypass VOUT with a 1uF to 22uF low ESR *ceramic* cap to GND
4. Bypass VIN with another 1uf-22uF low ESR ceramic cap to GND
5. Flying capacitor is separate from these two capacitors


## Flash LED
1. Takes 50mA maximum, need a series resistor
2. V_LED = 3.2V
3. V_Out (Charge-Pump) = 5V
4. Required LED Current ~= 50mA
5. R (resistor) >= V/I <= (5-3.2V)/(50*10^-3) >= 36 Ohms


## Power + Activity RGBLED
1. Common Anode (3.3V)
2. PWM-controlled, using Advanced timer TIM4
3. B CH1, G CH2, R CH3

### Resistor and control details
V_GPIO <= 3.3V

#### Red
V_red = 1.9 V
I_avg = 25*10^-3 A

R_red >= (3.3-1.9)/(2.5*10^-3) = 53.85 Ohm


#### Green
V_green = 2.9 V
I_avg = 13*10^-3 A

R_green = (3.3-2.9)/(13*10^-3) >= 30.77 Ohm


#### Blue
V_blue = 3.0 V
I_avg = 13*10^-3 A

R_blue = (3.3-3.0)/(13*10^-3) >= 23.08 Ohm