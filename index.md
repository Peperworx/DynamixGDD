---
layout: page
title: Dynamix GDD
---

# Project Dynamix

## Overview

Dynamix is an experimental FPS concept for controlling the positioning of players in a large ‘open’ world with the purpose of enabling contact with other players. Dynamix will do this by scaling a ring, similar to the ring or ‘storm’ found in battle royale games. However, Dynamix differs from battle royale games as the ring is not scaled by an elapsed time, but by the number of players currently in the world.

## About this document

This document provides the absolute specification for the architecture of "Dynamix."

Dynamix development has been through two stages already: The first stage which was initially a first person game, but ended up third person had some issues with, not only poor design, but not actually being designed at all. The second stage of Dynamix, while still being poor in design, actually had some thought put into it. It was predetermined that Dynamix would be a first person game. The only issue with the second stage of Dynamix was that proper design patterns were not being followed. Components that were supposed to be independent started depending on each other, and the code turned into a mess. What was worse was that this was not "Code" but was written in Unreal Engine's blueprints, which removed most of the chances for future maintainability and collaboration. This document serves to provide the specification, architecture, and design patterns to be used in the development in the third stage of Dynamix, the one that is expected to eventually release.

## C++ vs Blueprints

In Unreal Engine, there are two ways to develop your game. C++ and Blueprints. Blueprints allow you to write code in a flow chart like manner, and thus allow much faster development time to "just throw a few things together" while C++ allows much more control and easier collaboration through systems like Git.

In this third stage of Dynamix, we will be using a blend of C++ and Blueprints. Blueprints to connect everything together, and C++ to implement the actual logic. This is how it is recommended to use Unreal Engine, and this is how we will use Unreal Engine.

## Modularity

Using the latest technology provided with Unreal Engine 5, we can create modular components that "attach" to other components and systems. This is how almost every system will be implemented in Dynamix. This also means that modules can be plugged into other games with minimal modifications. Here is a list of the modules that will be used:

### PeperworxCoreModule

This module will contain several classes that provide extended support for other classes. For example, there will be a Character class that supports running events between other modules, a Gamemode class that does the same whilst also being able to control what modules are loaded on all characters, etc.
All modules require this module to also be used.

### PeperworxGlobalConfiguration

Some modules may require this module for global configuration requirements, including registering input actions and such.

### PeperworxMovementCore

This module provides core functionalities for movement systems. These core functionalities include different states for each mode of movement, pluggable movement modes, etc. All movement related modules rely on this one.

### PeperworxBasicMovement

This module provides basic movement components built on PeperworxMovementCore. This includes walking, jumping, running, and crouching.

### PeperworxSlidingMovement

This module provides a sliding movement type for PeperworxMovementCore

### PeperworxWallrunMovement

This module provides a wallrun movement type for PeperworxMovementCore.

### PeperworxProneMovement

This module provides a prone movement type for PeperworxMovementCore.

### PeperworxClimbMovement

This module provides climbing, ledge hanging, and mantling for PeperworxMovementCore.

### PeperworxInteractionCore

This module provides core functionality for interacting with objects in the world. It send messages through the character provided by PeperworxCoreModule to trigger systems such as inventory, weaponry, etc.

### PeperworxInventory

This module provides a slot-based inventory system. This system may be replaced with a jig-saw system in the future.

### PeperworxWeaponryComponent

This module is closely tied to the character and to the next component. This component implements systems for managing weaponry and the states of weapons. While this system is simple, it connects a lot of systems together, even though those systems do not actually need each other to function.

### PeperworxAnimationComponent

This module handles animation and meshes for the character. This module also allows the Weaponry component to play and modify animations, although it does not rely on it.


## Module pluggability

All of these modules can be disabled, enabled, replaced or updated without modifications or impact on the other modules.