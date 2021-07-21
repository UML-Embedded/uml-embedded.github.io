---
layout: post
title:  "UR Offline Simulator Install"
date:   2021-02-16 16:52:46 -0500
permalink: /tutorials/UR_Simulator
permalink_name: /UR_Simulator
detail_image: /assets/images/ur5.png
category: tutorials
description: "How to install UR Offline Simulator on Ubuntu and communicate over TCP/IP, because UR's install scripts are woefully outdated and broken :)"

categories: tutorial robotics
---

---
## Downloading and Setting Up
* Go to universal-robots.com/download  
* navigate to software -> offline for non linux (guess what their linux version relies on libcurl3 which hasn't been supported in ages)
* download the latest version
* download virtualbox
* unrar the download from ur with unrar x <filename>
  

open virtual box
* New
* name -> Whatever, Type Linux, Version: Ubuntu
* Memory 768 MB
* Use existing hard drive file
* Navigate to where you unRARed the .rar package and select the top module
* Create
* Start

On the virtual machine settings make network bridged to allow two way networking between
host and the virtual machine, reboot machine to have it take affect

This is likely just a virtual machine issue, in real life it's an ethernet connection

---
## Communicating with the UR Computer via TCP/IP
```python
import socket

HOST = "10.0.0.65"   #UR5 IP Address found in about panel on the robot's tablet
PORT = 30002 #UR5 TCP IP port found in the same location

sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
sock.connect((HOST, PORT))


text = "set_digital_out(0,False)" + "\n"  #Newline termination required on all payload messages
msg = text.encode("utf8")

sock.send(msg)
data = sock.recv(1024)
sock.close()

print("Received: ", repr(data))
```

This code shows a simple example of how you'd communicate with the robot and set a digital output pin.  
  
  
The UR Computer has multiple ports, the one we wrote to allows you to send commands or listen to the state of the system.  

There are additional ports that only allow you to listen to the system state. My next goal is going to be to listen to this port, and create a wrapper for you to read
any state updates from in Python. This requires you to deserialize a custom message, and will be hosted on my github soon.
