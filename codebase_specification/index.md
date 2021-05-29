---
layout: page
title: Codebase Specification
---

# Codebase Specification

The detailed specification for the formatting of code and use of engine features.

## Section Overview

Dynamix is a large and complex piece of software that requires individual components to closely integrate with each other. This means that code must be easily readable, and dependencies easily traced between files.

## The Use of Blueprints

Unreal Engine provides an extremely useful feature for quickly prototyping applications in the form of blueprints. Sadly, blueprints are stored in a binary format and do not synchronize well with version control systems such as git. This means that we must keep the use of blueprints to a minimum, and write as much code in C++ as possible. If something can be implemented in C++, we must implement it in C++. This is especially true for components that will meet milestones, such as the Movement System.

## The Architecture of Dynamix

Dynamix will be developed using Unreal Engine 4 and migrated to Unreal Engine 5 upon the latter’s release. As Dynamix is ultimately an Unreal Engine project, there will be several key components that `glue` other components together.

### The Character

A Character is a single object that encapsulates all of the logic relating to the player. Movement, Inventory, Weaponry, etc. will all be components that the character glues together. The character can be dropped into any game mode or world and still continue to operate with the same mechanics. The character is completely decoupled from the rest of the game, excepting required files such as animations, components, and multiplayer services.

### The Game Mode

The game mode is where particular mechanics of the game are implemented. This is the class where mechanics such as the ring/’storm’ will be implemented. The game mode is independent of the world or the character, meaning that the game mode may take place in any world, with any characters playing it.

### The World

The world consists of multiple ‘levels’ that are stitched together at runtime to form one, seemingly singular world. The world contains the content of any ‘maps’ that players would play on, and also contains all of the logic specific to that world (Day/night cycle, weather, random events, etc).

## Code Formatting

What follows is the general style guidelines for any C++ code which will be written in the development of this project.
The only strict rule is that braces must be used. For example, this is not allowed:
```c
for(int i = 0; i < 20; i ++)
    cout << i << endl;
```


This is not allowed in any cases.

Other rules include:
Function and Class names must be descriptive
No platform-specific system calls or libraries.
No large external dependencies.
Use custom libraries for web requests.
Languages other than C++ are cool, except for when wrapper code is required.
