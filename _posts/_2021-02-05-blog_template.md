---
layout: post
title:  "Blog Template"
post-title:  "Blog Template"
date:   2021-04-23 21:41:46 -0500
permalink: /blogs/blog_template.html
permalink_name: /blog_template
detail_image: /assets/images/posts/blog/blog_template/soft_robotics_repo.jpg
category: blogs
description: "Basic Template for writing a blog. Make a pull request when you finish writing one up :)"

categories: Blogs
---

---
# Here's a basic template

You can write plane text just like this. If you want a return character to appear before reaching the end of the screen
you need to put two spaces after the end of the line.  
So after that period there are two spaces!

If you don't include detail_image it will generate without it

Here's an example of centering an image (I use the html version cause markdown always breaks for me lol)
<center>
<img src="/assets/images/posts/tutorials/tutorial_template/sr_gripper_fsm.png" alt="Soft Robotic Gripper State Machine">
</center>


## Subheadings are like this :)
* And You
* Can do a dotted list like this

- Or this
- again, this

1. Or you can number it
2. Test
4. It's funny cause if you label this row 4. in the markdown it still says 3 on the site
5. Remember, everything is white space sensitive. The space after the number or bullet list symbols are required.


---
## Communicating with the UR Computer via TCP/IP
### Here's some random example code I have. This is a python TCP/IP Client
#### You Just need to specify the language after the backticks
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