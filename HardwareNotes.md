# Notes about Hardware

---

## Component List (Digikey)
1. STM32F407: 497-11766-ND
2. OV7670: 1188-CAMERA-OV7670-ND
3. MicroSD Breakout: 1568-00544-ND
4. FPC Socket for ILI9341: WM12371CT-ND
5. ILI9341: 1987-DT024ETFT-IPS-SHB-ND
6. RGB LED: CLMVC-FKA-CL1D1L71BB7C3C3CT-ND
7. Charge-Pump: 31-AP3602AKTR-G1CT-ND
8. Flash LED: 1516-QBLP677AD-IWD-2897CT-ND
9. Buck Converter: SC189ZSKCT-ND
10. Battery: 1471-MIKROE-4474-ND
11. Battery Connector: 455-B2B-XH-A-ND
12. Charging IC: 
13. USB-C for Charging: 

## STM32F407 + Recommendations from manufacturer
1. PCB should be a multilayer one with separate layers for VSS and VDD
2. Don't have one singular GND return plane, try and ground components individually
3. Recommended to put buck converter far from other components to avoid noise 
4. Unused counters or I/O should not be left free, either set to 1/0 or peripheral disabled.
5. Draws <= 150mA



## OV7670
1. Draws ~18 mA, maximum not provided by documentation, USE 25-50mA just in case


## MicroSD
1. Draws ~100mA worst case scenario


## SWD Header
1. Exposes the SWD peripheral that can be used to debug with a STLink


## ILI9341

### Header
1. 

### Actual device
1. Backlight draws <= 60mA
2. Functional part draws <= 15mA


## AP3602A Regulated Charge-Pump
1. Outputs up to 250mA current after charging
2. SHDN cannot be floating, tie to GPIO pin HIGH (enable) or LOW, never leave floating
3. Bypass VOUT with a 1uF to 22uF low ESR *ceramic* cap to GND
4. Bypass VIN with another 1uf-22uF low ESR ceramic cap to GND
5. Flying capacitor is separate from these two capacitors
6. Draws ~75mA while firing flash


## Flash LED
1. Current draw see Charge Pump^
2. V_LED = 3.2V
3. V_Out (Charge-Pump) = 5V
4. Required LED Current ~= 50mA
5. R (resistor) >= V/I <= (5-3.2V)/(50*10^-3) >= 36 Ohms


## SC189Z 3.6V->3.3V Buck Converter
1. EN pin should be tied to VIN on itself
2. LX is a switching node, connect inductor between here and output cap
3. Place components as closely as possible to the SC189Z.
4. For SOT-23 package at Vin = 4.0V, Vout = 3.3V and I_load ~= 560 mA, efficiency is roughly 93%


## Power + Activity RGBLED
1. Common Anode (3.3V)
2. PWM-controlled, using Advanced timer TIM4
3. B CH1, G CH2, R CH3
4. Draws ~(25 + 13 + 13) mA = ~51 mA

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


# Power Considerations for Battery

## Current Needs of Components
1. STM32 = 150mA
2. OV7670 = 50 mA
3. MicroSD Breakout = 100mA
4. ILI9341 = 75mA
5. Charge-pump + Flash = 75mA
6. LEDs ~= 51 + 3(20) = 111mA

Total = 150 + 50 + 100 + 75 + 75 + 111 = 350 + 75 + 111 = 561 mA


## Safety Margin and Buck Converter Efficiency
~~Once I choose a buck converter, I will include the efficiency of that to decide the battery configuration.~~
With the selected buck converter, the SC189Z, and a 4.0V input with 3.3V output configuration, the efficiency is ~93%.

Using this and a safety margin of 20% to account for battery aging:
Estimated needs (safety margin of 20%, 4 hour usage) = (561 * 4)/0.93 * 1.2 = 2895.5 mAh, which we can round up to 3000mAh.


Battery selected (Items 10 and 11 in **Component List**).


# Charging method

## MLP805660 Battery pack
1. 3.7V, 3000mAh
2. Discharges 0.2 C-rate
3. Standard charging 0.5C (C-rate, NOT coulombs like I initially thought), takes about 5.5-6.5 hours to charge fully 
4. Current needed for standard charging, therefore, is 0.5C * 3000mAh = 1.5A
5. 

## BQ24072 Charging IC
1. 
2. 
