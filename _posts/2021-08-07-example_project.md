---
layout: post
title:  " Example C Project"
post-title:  "Example C Project"
date:   2021-08-07 21:41:46 -0500
permalink: /projects/example_c_project.html
permalink_name: /example_c_project
category: projects
description: "Example C Project showing how to use CMake, CTest (with Unity Framework), and Doxygen to build documents"

categories: Projects
---

---
# Overview
I created an [example project](https://github.com/PatrickCPE/c_example) so you guys can have a basic idea of how to structure your code. There are a few pieces of advice for your projects that will make your life much better in the long run.

---
* Use Version Control (Always!!!)
* Use a Build System (Always!)
* Test Your Code (For any sizeable project that you intend to create, test from the start!)
* Document Your Code (Always document the basics! If you intend to get help on it use an autodoc tool and document it properly!)

---
For Version control the industry standard is Git. Learn it at a basic level, the rest will come with time.

For our build system we will be using CMake. It supports pretty much everything out there, but its main focus is C and C++.

For testing, we will be using CTest. This is a simple testing interface that is incorporated with CMake. It merely runs the tests.

For the test themselves you can either write a bare-bones wrapper by hand, or use a library like Unity (What I use) to test your code.

For Documentation there is your good ole README file, and that's always a requirement. F auto-documentation we'll use Doxygen. 

Doxygen can also output to Sphinx which is the tool I used to make my python doc sites, but for now we'll make a bare-bones site with Doxygen itself.

---
# Version Control - Git

Git pretty much keeps track of changes in your project, and it allows you to revert changes if you screw up. It also allows other people to work on the project with you, and to merge your code without causing as many problems.

Here's the basic rundown of how to use [Git](https://www.atlassian.com/git)

My basic workflow goes like this. Create a git directory with
```shell
cd directory
git init
```
Then I create a .gitignore file and add any files I don't want tracked to it.

From there on out my workflow is very simple.
```shell
# Add everything in this directory recursively to be added with this commit
git add .
git commit -m "Message detailing what I did, what I changed, or what I absolutely just broke :)"
# And if I need to push remotely I do
git push -u origin main
```
That's it. If I screw up I can always fix it later. I don't bother showing you how to merge or anything because for now I just want you to have a backups of your changes, and keep everything tracked properly.

---
# Build System - CMake
[CMake](https://cmake.org/) is a cross-platform build tool for blah blah blah.

It allows you to compile your libraries and your code easily. It also has testing incorporated, and it's a necessity for C or C++ projects. There are other tools, but CMake is the industry standard.

At the top level of your project you will have a CMakeList.txt file

This is pretty much the master control file for the project. In your sub folders you'll have files under the same name with more CMake commands. You pretty much do this recursively till the build tool has your entire project mapped out.

Here's the top level CMakeList.txt for this project commented up for you.
```
#Set min version
cmake_minimum_required(VERSION 3.20)

#Set project name, version, and support languages
project(c_example VERSION 0.1 LANGUAGES C)
#For example to support C and C++
#project(c_example C C++)

#Use C 11 and disable compiler extensions
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS OFF)

#Or set the standard for a particular library
#set_target_properties(lib_a PROPERTIES
#        C_STANDARD          11
#        C_STANDARD_REQUIRED ON
#        C_EXTENSIONS        OFF
#)

#Set compiler flags for all versions
set(CMAKE_C_FLAGS "-Wall -Wextra")

#include(Ctest)
enable_testing()
add_subdirectory(src/libs)
add_subdirectory(src)
add_subdirectory(tests)

#Example setup for GNU Make for the release directory
#cmake -G "Unix Makefiles" -S . -B ../build/release/
#cd ../build/release
#make

#Example setup for Ninja for the debug directory
#cmake -G Ninja -S . -B ../build/debug/
#cd ../build/debug
#ninja

#Or just use CMake to avoid the low level build tools for either
#cmake --build ../build/debug/ --config Release --target tes
```

This file doesn't do much for you in my case, all my building is handled inside the subdirectories that I add.

It's important to set an up-to-date CMake required version, and to set the proper C standard.Compiler flags can be changed as needed.

---
Let's take a look at the src directories CMakeList.txt file
```
#Set compiler flags
set(CMAKE_C_FLAGS "-Wall -Wextra")

add_executable(main main.c)
target_link_libraries(main PRIVATE lib_b)

add_subdirectory(libs/Unity
```

This sets flags for this scope, creates an executable main that depends on main.c, and creates a link telling the compiler main depends on lib_b.

I add the Unity Subdirectory, and it builds and installs the Unity test framework.


lib_b is added in the subdirectory below that I added in the top level file. Here is that file.
```
add_library(lib_a example_lib_a.c)
add_library(lib_b example_lib_b.c)

target_link_libraries(lib_b PRIVATE lib_a
```

You can see here that I create 2 libraries called lib_a, and lib_b from their respective source files. I tell the build tool that lib_b depends on lib_a, and the build tool handles the rest for me.

---
When this is all said and done you can run the configuration commands shown in the top level CMake to set up the build system, and then to build your code.

---
# Testing - CTest
The only CMakeList.txt file I failed to mention is in tests. We'll go over that here.

```

#Create executables for tests
enable_testing()
#Basic testing without a framework
add_executable(test_pass test_pass.c)
add_test(test_pass test_pass)

add_executable(test_fail test_fail.c)
add_test(test_fail test_fail)

#Testing using the Unity Framework
add_executable(test_example_lib_b test_example_lib_b.c)
target_link_libraries(test_example_lib_b PRIVATE unity)
target_link_libraries(test_example_lib_b PRIVATE lib_b)

add_test(test_example_lib_b test_example_lib_b
```

When it comes to testing you need to enable at the top level, and at the sub-level that you'll be running the test.

At a basic level all you need to do is add executables for your test, and list the executable as a test. 

If you do this as shown, CTest will run them all for you.

CTest is very simple, if the program returns 0, it passes. If it doesn't, it fails. The first two examples show how simple tests really are, and the third example shows testing using a framework.

---
Unity is the framework that we'll be using in this case.

Unity pretty much just allows you to assert some condition, and it will return zero if true, or false if not. It also has a lot of niceties like error messaging and comparing in certain bases like hex comparison, etc.

You can learn how to use their framework [here](http://www.throwtheswitch.org/unity).

---
In the end, as long as your code is built all you need to do is move into the build directory and run 
```shell
ctest
```

You'll get output like this
```
patrick@patrick-desktop:~/ws/club/projects/c_example/build/debug$ ctest
Test project /home/patrick/ws/club/projects/c_example/build/debug
    Start 1: test_pass
1/3 Test #1: test_pass ........................   Passed    0.00 sec
    Start 2: test_fail
2/3 Test #2: test_fail ........................***Failed    0.00 sec
    Start 3: test_example_lib_b
3/3 Test #3: test_example_lib_b ...............***Failed    0.00 sec

33% tests passed, 2 tests failed out of 3

Total Test time (real) =   0.00 sec

The following tests FAILED:
          2 - test_fail (Failed)
          3 - test_example_lib_b (Failed)
Errors while running CTest
Output from these tests are in: /home/patrick/ws/club/projects/c_example/build/debug/Testing/Temp...
Use "--rerun-failed --output-on-failure" to re-run the failed cases verbosely.
```
Don't worry, those fails are meant to occur. Those are just to show you how fails work.

---
# Documentation - Doxygen
There are two levels of documentation. A simple README showing what your code does, and how to use it is always required. This is the first thing people see when it comes to your project.

When it comes to working on a large project though it's often useful to have an autodocumentation tool. For this, we'll use Doxygen. Doxygen is an autoparser that will read through your code, document the functions, classes, structs, pretty much anything in there and build a website to show you all the information.

To install it run
```shell
sudo apt install doxygen
sudo apt install doxygen-gui
```
Simply go into your docs directory and run doxygui, it's pretty self explanatory when your in the application. Make sure to save the config to a Doxyfile, and when your ready to build do
```shell
cd docs
doxygui
doxygen Doxyfile
```
Inside the documents folder you will now have a build folder that contains a html site documentation your project. Open the index.html to see the homepage.

You can either select to document all code automatically, or only things commented in Doxygen style when you're in the GUI.

To learn how to use Doxygen style comments check [this out](https://www.doxygen.nl/manual/docblocks.html).

---

# Wrapping Up
This write-up by no means goes into depth on any of these things. This is a high-level overview and you're meant to download the repo and look at it yourself to get a better understanding.

What I do want you to understand is that you need a build system, you need some level of documentation, and if you're making a substantial project, you need testing.

The more you invest at startup, the less painful it will be to have to implement this stuff down the road. Best of luck with your projects :)