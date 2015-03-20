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
I'll try to explain some of the modifications done and my results.

##Modifying board-rk3168-ds1006h-camera.c
A few modifications were done on this file. The majority of them are showed below:

{% gist 350578c7a02d1d269080 %}

In the code above we added a new camera device with the specifications of the OV7740 sensor. We also modified the camera sensor configuration macro the represent an OV7740 sensor for all the back cameras.

The last modification done in this file was to change the value of the ldo7 variable to 3.3 volts, since that is the voltage required by the OV7740 sensor to operate. This change for the ldo7 variable have to also be reflected in the board file, which sets the minimum and maximum values for ldo7. 

##Modifying rk_camera.h
The file rk_camera.h required a number of modifications. All of these were for the inclusion of configuration parameters about the OV7740 sensor in the file. Modifications are shown below.

<script src="https://gist.github.com/pedro1713/89d68a80ce4b163129d8.js"></script>

##Modifying v4l2-chip-ident.h
This file required a single modification. I added one line within the range of chip identifier numbers reserved for Omnivision sensors.
{% gist 81a388659feae8a11940 %}

##Still a work in progress
After the modifications shown above the camera is detected by the Radxa Rock Pro. I can boot from Android and open the camera via the camera app. However, I don't get a proper image. What I get is a green image alternating with a gray image, at a very low refresh rate. This may be related to the configuration of some of the camera registers. I'm currently looking into them.


