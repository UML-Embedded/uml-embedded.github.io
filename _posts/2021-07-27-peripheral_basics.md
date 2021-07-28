---
layout: post
title:  "Peripheral Basics"
post-title:  "Peripheral Basics"
date:   2021-07-27 21:41:46 -0500
permalink: /tutorials/peripheral_basics.html
permalink_name: /peripheral_basics
detail_image: /assets/images/posts/tutorials/peripheral_basics/tux_funny.png
category: tutorials
description: "Overview of some basic peripherals in embedded systems. GPIO, ADCs, DACs, I2C, SPI, etc."

categories: Tutorials
---

---

# What Are Peripherals
At a low level, peripherals are anything that interact with a computer to either give it information or send out information. This information can be pretty much anything.

A mouse is a peripheral that inputs the X and Y movement you make, and your computer uses that peripheral to determine where you want your cursor to appear on the screen. Another example would be a temperature sensor that communicates over I2C (pronounced I squared C).

Peripherals can be communicated with via numerous protocols, but we're only going to cover a few basic types of peripherals and protocols here.

---
# GPIO
This is the most basic type of peripheral you can attach to a processor. The pins either read the voltage on the line, or they write a voltage to the line. The voltage is digital, meaning it can only be on or off at the specific device's voltage.

Inputs can have numerous configurations such as high impedance, pull-up, pull-down, or floating. These dictate the standard state of the pin. Pull up means the pin is typically high, while pull down means the pin is typically low. High impedance effectively places an infinite resistor in series, while floating means the pin can do anything.

Outputs have numerous configurations as well, such as push-pull, open-drain, and open-collector.

