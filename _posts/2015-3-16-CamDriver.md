---
layout: post
title: My OV7740 driver for the Radxa Rock Pro
---

It's been about two months since I started working on this driver.
It was quite the learning experience.
I didn't know much of writing Linux drivers when I started, I still don't know much but I think now I at least understand the basics.
The driver code can be found [here](https://github.com/pedro1713/7740driver).
It is still a work in progress.
I need to fine tune some register values to make it work.
But I think it is getting there.

## Some required explanation of my code
The Rock Pro by default expects an OV5640 on its camera interface.
One important difference between the OV5640 and the OV7740 is that the OV7740 requires a higher voltage to power up, 3.3 V are required for the 7740 and 2.8 V for the 5640.
I needed to go into the board file to change the value assigned to the regulators that provide power the the camera interface.

