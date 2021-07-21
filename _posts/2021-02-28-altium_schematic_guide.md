---
layout: post
title:  "Altium Schematic Tutorial"
post-title:  "Altium Schematic Tutorial"
date:   2021-02-28 01:41:46 -0500
permalink: /tutorials/altium_schematic_tutorial.html
permalink_name: /altium_schematic_tutorial
detail_image: /assets/images/altium_logo.png
category: tutorials
description: "This guide is a basic overview of how to do draw up schematics in Altium, primarily created for Umass Lowell's Embedded Club but it's useful for anyone trying to learn Altium"

categories: Personal Engineering Tutorials
---

---
I lost my old hard drive that had my Altium workflow guide and hotkeys guide on it. I figured I'll write up this guide for
anyone who's interested in learning/switching to Altium. I suppose this will save me a lot of questions when I get around 
to starting the embedded club in person. If you have any questions or suggestions to add to this guide reach out!

Note: Thou is the same as Mill for anyone who doesn't know, 1/1000 of an inch!

# Altium Schematic Design Guide

---
### Creating the project
---
**File >> New >> Project**  

Default PCB will work for your basic project.  
I recommend you use Git, or SVN if you prefer that. I believe Altium actually incorporates SVN but I'm a Git guy myself, and it does have some Git support (although I still use a terminal).  

---
### Adding a Schematic
---
**Right Click Project >> Add New to Project >> Schematic  
Right Click Schematic >> Rename**  

Rename as you find appropriate  

---
### Configuring Properties
---
Property Configuration **(Panels >> Property)**  
Set Visible Snap Grid (I go with 100 mil)  
Set Layout Snap Grid (Again, 100 mil)  
Set Page Color (Slightly Gray is Better on my Eyes, Choice is yours!)  
Set Sheet Size (Whatever you prefer, it's rare to actually print schematics nowadays, but I recommend it when you check traces!)  

---
### Selecting Components
---
There are two options in Altium, the Altium Vault and personal Libraries  

If your in a large company they'll probably have their own library to ensuring manufacturing tolerances, but I like the Altium Vault Library cause it saves time and shows part availability. The standard component library does have your standard passives/connectors that you can use as well. I might make a tutorial on component generation later, but school's killing me right now.  

---
### Selecting Parts Via Manufacturer Part Search
---
Using Manufacturer Part Search **(Panels >> Manufacturer Part Search)**  
It has built in filter systems if you click the funnel shaped symbol on the top left, querying works rather well, and then you can filter down to desired packaged size/stock/etc. after the fact.  

**example search: "smd led 0603 red"**  

This will yield plenty of suitable parts, and it integrates with Octopart (part availability from distributors) to tell you pricing and availability. Some components will have the footprint designed by Altium (typically there's a small, medium, and large footprint). When designing for manufacture part availability and price is huge!  

when you picked out a part you want to use  

**right click >> place >> left click to place on schematic  
right click >> add supplier link and parameter to part(if you want to) >> left click part on schematic**  

---
### Selecting Parts Via Local Libraries
---
Using Local/Content Server Libraries  

**Panels >> Components**

I'll be honest I don't have a content server so I can't really speak for it, but here's how to use the local libraries  

---
#### Installing Libraries  

---
**Components >> The 3 Bar Icon >> File Based Library Preferences >> Installed >> Installed**  

You can also just store the component in the local project directory if you'd like to use it within just the project. Querying and Parameterized search is the same for local components as Manufacturer Part Search. Placing the component is the same as well  

---
### Wiring the Schematic
---
* Ctrl+W >> Draw Wires  
* Left click to place  
* Left Click Hold and drag to move wire and component  
* Left Click+Ctrl Hold and drag to move just components  
* Right Click to exit wire mode**  

If you prefer the arch to show where connections don't exist it's in the general page of preferences for the schematic  

---
### Net Labels
---
Right Click the Quickbar in the wire slot and select net label   
Use **Tab >> Preferences** to declare the labels  
Place on a net to label it  

---
### General Rules for Drawing Schematics
---
* High voltage at the top, Ground at the bottom
* Signals move form left to right
* Don't connect more than 2 signals at a single dot if possible, this ensures you can see what is and what isn't a connection.
* Ensure Reference Designators are done properly
* Put relevant calculations right on the schematic with a text comment
* Fill out your name, project name, and revision number on the schematic

---
## Schematic Hotkeys
---
**Spacebar: Rotate Part 90 degrees  
X: Flip along X-axis  
Y: Flip along Y-axis  
Tab: Display Properties for a placed part, any properties filled out are kept for subsequent places of the same component(good to label reference designators)  
Ctrl+Wheel: Zoom in or Out  
Right Click+Drag: Move schematic  
Ctrl+PgDwn: Fit Sheet to page  
G: Cycle snap grids  
Ctrl+W: Draw Wires**

## With all of this in mind, go ahead and draw up your schematic. Then we'll move onto ERC checks.

---
### Configure Error Reporting
---
**Project >> Project Options >> Error Reporting**  
Chose the severity level of each warning if you'd like to alter the defaults, as a beginner I'd leave it alone  

**Project >> Project Options >> Set up as desired**  
If you want certain types of pins connecting to other pins configure it here. I recommend you atleast have warnings for unconnected pins  

---
### Running Design Rule Check
---
**Panels >> Messages  
Project >> Validate Projectname.PrjPcb**  

You will see errors outputted in the message box, double click the message to zoom on the error. if you consider the error to be acceptable (for example leaving one end of a potentiometer unconnected).  

Right click the message and place no erc for the connection if it's a false error. If there's an actual error fix it, then rerun the Validation  

---
## You're now done with the schematic! Check out the PCB tutorial if you're responsible for the layout as well, hope this helped :)