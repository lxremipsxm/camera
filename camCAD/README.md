## Component Connections and Layout

### Schematics

#### STM32 Power Requirements Schematic (power_conns.kicad_sch)
This schematic is based off of the power requirements detailed in the [STM32 F405xx/F407xx datasheet](https://www.st.com/content/ccc/resource/technical/document/datasheet/ef/92/76/6d/bb/c2/4f/f7/DM00037051.pdf/files/DM00037051.pdf/jcr:content/translations/en.DM00037051.pdf) and cross-checked with the [ST Application Note AN4488](https://www.alldatasheet.com/datasheet-pdf/view/701384/STMICROELECTRONICS/AN4488.html) for good measure.

![Power Connections Schematic](../imgs/stmpwr.png)

#### Power Supply and Charging Schematic (buck.kicad_sch)
This schematic contains all of the circuitry necessary to make charging possible and exposes pins to the battery. It includes connections for a USB-C socket that serves as the charging port for the camera, connections for the Dynamic Power Path Management IC (charging + power management), the buck converter circuitry to efficiently step down the battery's 3.7V to 3.3V, and the battery terminals, which will use an XH socket. (Initially I planned to have the buck converter on a separate schematic, hence the filename, but there wasn't enough detail to justify a separate schematic)

![Power Supply and Charging Schematic](../imgs/pwr&charge.png)

#### Components Schematic (components.kicad_sch)
This schematic contains the component connections that provide all the functionality of a camera. It contains the OV7670 Camera Module, the ILI9341 Display header, activity LEDs, and the MicroSD transflash breakout board.

![Components Schematic](../imgs/comps.png)

#### STM32F407 schematic (f407zgt6.kicad_sch)
Contains the STM32F407ZGT6 LPQF144 chip. ~~In the near future I will put more circuits in this schematic, such as the bootloader switch.~~
![STM32 Schematic](../imgs/stm.png)

#### User Interface (user_interface.kicad_sch)
This schematic contains the buttons that will aid the user in communicating with the camera, such as taking pictures, toggling flash, deleting pictures, and navigating saved pictures via a picture menu.

![User Interface Schematic](../imgs/ui.png)

### PCB Layout (Two Layer)
I was recommended to use four layers to separate the ground and VCC Planes better, but this is what I got routing with a two-layer PCB, with the back CU layer housing a ground fill zone. 

#### Front Layout
All dimensions are in mm.
| Layout | 3D Model |
| ------- | -------- |
| ![Front Layout CU only](../imgs/twoLayer_FCu.png) | ![Front 3D Model](../imgs/twoLayer_3DF.png) |



#### Back Layout
All dimensions are in mm.
| Layout | 3D Model |
| ------- | -------- |
| ![Back Layout Cu](../imgs/twoLayer_BCu.png) | ![Back 3D Model](../imgs/twoLayer_3DB(1).png) |



### PCB Layout (Four Layer)
This PCB will be printed once I reverify the schematics and layout

| Front CU | Back CU |
|-------- | -------- | 
| ![Front Layout CU ](../imgs/fourLayer_FCu.png) | ![Back Layout CU only](../imgs/fourLayer_BCu.png) |
| ![Front 3D ](../imgs/fourLayer_3DF.png) | ![Back 3D ](../imgs/fourLayer_3DB.png) |


| VCC CU | GND CU |
| ------- | ------- |
| ![VCC Layout CU](../imgs/fourLayer_3VCu.png) | ![GND Layout CU](../imgs/fourLayer_GNDCu.png) |

