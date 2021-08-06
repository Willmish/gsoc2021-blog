---
layout: post
title: "Installing PowerVR SDK"
date: 2021-06-15
categories: Posts
---

This post will show you how to setup and test the PowerVR SDK from Imagination to be sure that everythings works fine.

## Download

First clone the repository:
```
git clone https://github.com/powervr-graphics/Native_SDK
```
Create the build directory:
```
cd Native_SDK
mkdir build
cd build
```

## Configure and Build
Now we can configure and build the SDK:
```
cmake ..
cmake --build .
```

You will also most likely need to specify the window system with a CMake define, like this `-DPVR_WINDOW_SYSTEM=X11` during the configuration phase, so the call looks like this:
```
cmake .. -DPVR_WINDOW_SYSTEM=X11
```

If you want to have a `compile_commands.json` file generated, you should run:
```
cmake -H. -BDebug -DCMAKE_BUILD_TYPE=Debug -DCMAKE_EXPORT_COMPILE_COMMANDS=YES
```
And then `cp`/`mv` the commands from the `Debug` directory to the root directory of the project you want develop. (`compile_commands.json` is a file used by Language servers for autocompletion and other magic. The more you know!).

## Testing if it works
Go to the `build/bin` directory and run the first example:
```
cd build/bin
./OpenGLESHelloAPI
```

It should display a nice triangle and close upon clicking on the window. This is all!

## Installing and testing on target (BBB)
First we should install our dependencies, such as EGL or GLES:
```
sudo apt install libegl1 libgles2
```
And create proper symlinks in the directory `/usr/lib/arm-linux-gnueabihf`:
```
sudo ln -s libEGL.so.1 libEGL.so
sudo ln -s libGLESv2.so.2 libGLESv2.so
```

Similarly as above, but with no window specified, we have to compile the SDK:
```
cmake .. -DPVR_WINDOW_SYSTEM=NullWS
```
Assuming you have the BBB image which can display something on a monitor, you can test any binary under `build/bin`.
