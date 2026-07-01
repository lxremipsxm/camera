# Camera

## Component Connections and Layout

### Schematics

#### STM32 Power Requirements Schematic (power_conns.kicad_sch)
This schematic is based off of the power requirements detailed in the [STM32 F405xx/F407xx datasheet](https://www.st.com/content/ccc/resource/technical/document/datasheet/ef/92/76/6d/bb/c2/4f/f7/DM00037051.pdf/files/DM00037051.pdf/jcr:content/translations/en.DM00037051.pdf) and cross-checked with the [ST Application Note AN4488](https://www.alldatasheet.com/datasheet-pdf/view/701384/STMICROELECTRONICS/AN4488.html) for good measure.

![imgs/power_conns.png]

#### Power Supply and Charging Schematic (buck.kicad_sch)
This schematic contains all of the circuitry necessary to make charging possible and exposes pins to the battery. It includes connections for a USB-C socket that serves as the charging port for the camera, connections for the Dynamic Power Path Management IC (charging + power management), the buck converter circuitry to efficiently step down the battery's 3.7V to 3.3V, and the battery terminals, which will use an XH socket. (Initially I planned to have the buck converter on a separate schematic, hence the filename, but there wasn't enough detail to justify a separate schematic)

#### Components Schematic (components.kicad_sch)
This schematic contains the component connections that provide all the functionality of a camera. It contains the OV7670 Camera Module, the ILI9341 Display header, activity LEDs, and the MicroSD transflash breakout board.

![[imgs/comps.png]]

#### STM32F407 schematic (f407zgt6.kicad_sch)
Contains the STM32F407ZGT6 LPQF144 chip. In the near future I will put more circuits in this schematic, such as the bootloader switch. 


### Layout


## Use


## Personal Note
This is the continuation of my stmcam project that I had been working on for a long time, in [this repository](https://github.com/lxremipsxm/stmcam) if you are interested. The goal of that project was to have a completely naked approach to building this camera, using raw C, no Hardware Abstraction Layer and minimal library usage. It was a very code-centered project, and reasonably so, as I had no electrical knowledge or knowledge of using CAD to build (or at least prototype) PCBs. At the time, I was fully confident I could make this with a perfboard and some solder at home if I had the right components, which I did eventually purchase from Digikey. However, I had selected a board without Parallel Capture/DCMI and tried to work my way around it until the workload became utterly infeasible and would have led to me making a project of subpar quality even if I succeeded. It was incredibly frustrating, but I still haven't given up on this project. This repository is a fresh start, and I am changing my approach. I have a new board planned, I have the incredible resource of KiCAD 10.0, and I have developed the skills to build my own PCBs and print them. Additionally, this time I will not dive headfirst into baremetal programming as much. I will use HAL to make a functional project, and I do eventually have to create my own interface to facilitate the use of a OV7670 library I have found on GitHub, which means I still get to code a solid amount without leaving all of it to HAL. 

So here is my camera. I am so much more confident in this project's success.
