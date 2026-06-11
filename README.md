# Camera

## Personal Note
This is the continuation of my stmcam project that I had been working on for a long time, at [this link](https://github.com/lxremipsxm/stmcam) if you are interested. The goal of that project was to have a completely naked approach to building this camera, using raw C, no Hardware Abstraction Layer and minimal library usage. It was a very code-centered project, and reasonably so, as I had no electrical knowledge or knowledge of using CAD to build (or at least prototype) PCBs. At the time, I was fully confident I could make this with a perfboard and some solder at home if I had the right components, which I did eventually purchase from Digikey. However, I had selected a board without Parallel Capture/DCMI and tried to work my way around it until the workload became utterly infeasible and would have led to me making a project of subpar quality. It was incredibly frustrating, but I still haven't given up on this project. This repository is a fresh start, and I am changing my approach. I have a new board planned, I have the incredible resource of KiCAD 10.0, and I have developed the skills to build my own PCBs and print them. Additionally, this time I will not dive headfirst into baremetal programming as much. I will use HAL to make a functional project, and I do eventually have to create my own interface to facilitate the use of a OV7670 library I have found on GitHub, which means I still get to code a solid amount without leaving all of it to HAL. 

So here is my camera. I am so much more confident in this project's success.


## Use
