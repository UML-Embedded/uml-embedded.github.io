---
layout: post
title:  "Altium Layout Tutorial"
post-title:  "Altium Layout Tutorial"
date:   2021-02-28 02:41:46 -0500
permalink: /tutorials/altium_layout_tutorial.html
permalink_name: /altium_layout_tutorial
detail_image: /assets/images/altium_logo.png
category: tutorials
description: "This guide is a basic overview of how to layout a board in Altium, primarily created for Umass Lowell's Embedded Club but it's useful for anyone trying to learn Altium"

categories: Personal Engineering Tutorials
---

---
## Creating the board
---
**ProjectName.PrjPcb >> Right Click >> Add New to Project >> PCB  
PCB1.PcbDoc >> Right Click >> Rename(as desired)**


---
## Configuring the Board
---
### Set the Origin  
**Edit >> Origin >> Set**  

### Set Units
**View >> Toggle Units	(Hotkey: Q)**  

### Set Snapgrid  
**Hotkey: G  
Hotkey: Ctrl+Shift+G**  
(Opens snapgrid settings rather than swap between predefined snapgrids)  

---
## Edit the Board Shape
---
**Ctrl+PgDown: Zoom Fit  
View >> Board Planning Mode	(Hotkey: 1)  
Design >> Edit Board Shape**  
Adjust Board corners until desired board shape is achieved  

You can also redraw with  
**Design >> Redefine Board Shape**  
Draw the polygon fill to create board  

---
## Transfer the Design
---
### from schematic  
**Design >> Update PCB Document Name.PcbDoc**  

### from PCB
Design >> Import Changes from Name.PrjPcb  
**Validate Changes  
Execute Changes**  

If you're missing any footprints you'll get an error when you try to import

---
## Setup Layer View
---
Panels >> View Configuration (Hotkey: L)

---
## Setting Up the Stackup
---
**Design >> Layer Stack Manager (Make sure to save!)  
Panels >> Properties  
Properties >> Enable Stack Symmetry**  

Set up Planes and Signal layers (Standard is 1 oz. copper, if it's a high power board 2 oz. may be neccassary but for hobby projects realize 2 oz. is expensive!)  

**Via Types >> Ensure through hole via is present(If you need partial/embedded vias you'll be able to figure it out here on your own)**  

Remember to save the stackup!

## Before you Place Set Up Your Snap Grid!

---
## Basic Electrical Rule Configuration
---
Here's some basics to get you started, ICs tend to have metric based packages so probably best to use mm here.  
* **Route Width:** 0.25 mm	Where: Routing Grid Design Rule (Can also do whatever 50 ohm impedance is for your dielectric/stackup)  
* **Clearance:** 0.25 mm		Where: Electrical Clearance Design Rule	(High speed signals need special care!)  
* **Board Definition Grid:** 5 mm		Where: Cartesian Grid Editor  
* **Component Placement Grid:** 1 mm	Where: Cartesian Grid Editor  
* **Routing Grid:** 1 mm		Where: Cartesian Grid editor  
* **Via size:** 1 mm			Where: Routing Via style design rule	(High current traces may need larger/multiple vias)  
* **Via hole:** 0.6 mm		Where: Routing Via Style Design Rule  

Altium Support Polar Grids if you're doing a curved board but I'm not going into that  

Cartesian Grid Editor (Hotkey:Ctrl+G)
Set the grid definition here as well so you can see it well

---
## PCB Rules
---
**Design >> Rules**  
Set up everything according to what your manufacturer supports. Some manufactures will provide an altium rule file to import, and if they do love them eternally because so much less busy work  

---
## Basic setup
---
* **clearance:** 0.25mm for all  
* **signal:** 0.25mm standard  
* **power:** thick traces, minimum can still be low for small offshoots to pins, etc  
* **routing vias:** 1mm diameter, 0.6mm hole size

Yes, you can be more specific, and if the boards high density please do look in depth at your manufacturers capabilities. If it's a hobby project, who cares :)

---
## Placement
---
My first boss taught me that 90% of the battle is placement, and I recommend you take his advice.  

* Spend time making the rat's nest of traces as short as possible. Rotate parts around, make sure there is as short of a distance as possible for you to route wires.  
* Place Connectors and any mechanical requirements First, then place components as fits.  
* Make sure you place the bypass caps as close as physically possible to the VCC and GND pins of your components!  
* If you need to use vias use them, there's different theories on what's best here. Some people prefer routing all on the top layer, some believe hiding the signals in your stack up is more beneficial.  

I'll point you to Henry Ott (hottconsultants.com) if you want to read up on the different stack ups and routing techniques
I also hear good things about Howard Johnson, and John Howie(totally different names, not clones or anything) has some stuff on EMC, but it's a bit harder to find  

---
## Planes
---
**Place your planes now!**  

You need to have a small keepout area on the edge of the board to make manufacturers happy  

**Polygon Pour >> Draw >> Click Polygon >> Properties >> Assign Net >> Repour**  
(If you mess with things be sure to repour, it'll fix some weird issues)  

If you think yourself a genius feel free to attempt to split your ground planes, if your like the rest of us mortals do the best to ensure your board has as solid of a ground plane as possible.  

A solid plane rather than a split one is almost always better.

---
## Basic Routing
---
**Route Mode (Hotkey: Ctrl+W)**  

* Connect everything with the shortest trace possible! Highest priority signals get routed first, remember some lines need controlled impedance/differential pair routing  
* Route slow speed traces last  
* Make sure to put vias to prevent any dead copper!  
* There are fancy methods of making high speed transmission lines with vias along fancy traces but that's application specific  
* In general spread some via stitch out around the board after to help with return paths. The person who taught me taught me to do it pseudo randomly to prevent "resonance of something". I can't quite remember everything ¯\_(ツ)_/¯ , but he's a pretty bright guy so I'd assume he was right.

Autorouting is a privilege you earn after you learn when to use it. If you're starting out you don't know how to and shouldn't. It can save time in some cases but I avoid it 95% of the time  

---
## Boards Done -> Design Rule Check
---
**Tools >> Design Rule Check**  

Fix or approve any errors  

---
## Check your board out!
---
* Press 3 to view the board in 3D, make sure everything looks alright
* Press 2 to go back to routing mode

---
## Fabrication Outputs(Getting your board made!)
---
You can either output individual files from  

**File >> Fabrication Output  
File >> Assembly Output**  

You can also export to other tools such as HyperLynx (super fancy sim software for EMI that you'll only get to play with if your company has a license) from the file tab.  

You can print PDFs from here as well, Altium can output 3D pdf files that allow rotation and zoom in Adobe Acrobat almost as if you were looking at the assembly in Solidworks.

---
## Setting Up Output Job Files
---
This will output everything you want, think of it like the CMake of Altium  

**Right Click Project >> Add New to Project >> Output Job File**  

Save file as desired name  

### Basic set of outputs to set up in the .OutJob file
**Fabrication >> Gerber >> PCB Document  
Fabrication >> NC Drill Files >> PCB Document  
Assembly >> Generate pick and place files >> PCB Document  
Documentation Output >> Schematic Prints >> (single page for basic setup)  
Documentation Output >> PCB Prints >> PCB Document**  

### Configuring the outputs
To Configure each output right click and hit configure  
**Gerber Config**  - (Format, 4:4, Units:mm, layers >> plot layers >> used on, advanced >> position on filme >> reference to relative origin)  

### Set up the output container
Click the folder structure in output containers.  

Now check the enable box for every file you want in that folder.  
Set the top file path to manually managed.  

I recommend you store everything in a folder call outputs because it looks better.  

You may want to go into advanced and enable auto load of gerber and NC drill outputs so you can check to see if they're accurate after being created 

Click the PDF Container and add your PDF's to it, adjust this output structure as well.
Name it as you'd like and configure auto open if you want

ODB++ is a new format that contains pick and place info alongside board info. Fancy board houses like it. If you're getting high quality boards or a large number of boards made
please just communicate with your board house/assembly house. They'll tell you what they prefer, and if you give them what they prefer it'll save you a bit of money hopefully

We're going to add our BOM to the output as well, but we need to set it up first

---
## Active BOM
---
**Right Click Project Name >> Add new to project >> Active Bom  
Properties >> Set Production Quantity to see best prices**  

Now go through each type of component and select the manufacture you want to buy from, Once you select the manufacturer give it a user rank by making a star rating.  

Once you do this the status message on the far right side of the BOM should become a green check box for the items that were in stock.  
Add vendors links for any products that still need them by clicking the part and doing add solution.

If you replace a part with a new solution note that whatever option has the most stars will be used if available.  
(ie: if you have 2 different types of amps you can use but the preferred one is usually out of stock set the preffered to 5 stars and option 2 to 4)  

If you entered the production amount the tool will help you pick from the different distributors and ensure stocks.  

Save the bom and the project!

Now go back to your output job file and add the bom, I recommend you customize it and add either the single supplier or double supplier template.  

Add it to your output folder container!  

---
## Wrap Up
---
Save everything! You can reuse things like rules setups and your output job file for most cases!  

Now go into your output job file and click your output containers.
Click generate content for each and ensure it's correct.

Now you have the pdfs of your schematic and board to share with everyone, and your manufacturing files! You're all set to have it made :)

---
### Now you have to write the firmware you've been avoiding :)