---
layout: page
title: Movement System
---

# The Movement System



## Section Overview

The Dynamix Modular Movement System handles network-replicated character movement that also supports custom multiplayer frameworks. This framework consists of pluggable movement ‘modules’ that can implement different ‘modes’ of movement. The framework will also come with built-in modules, such as walking, running, jumping, climbing, and wall-running.

## The State System

The movement system operates by switching between states when certain conditions are met. Each state is assigned a number, and each module specifies the number of states it requires. The module then receives a mapping of states to modules, and can use that to register and call state values. Modifiers can also be applied to the state system, which can change the behavior of states and modules.

## Default Modules

The movement system comes with several different default modules.

### Idle

This module is the basic module. By default, it occupies state number 0. It is triggered when the condition of no other state is met.

### Walking

This state is the basic movement state. It is triggered when ‘forward_input > 0’ and no other modifiers are applied. It sets the character’s speed to a configured ‘walk_speed’ value.

### Sprinting

A character is considered to be sprinting when ‘forward_input > 0’ and the sprint modifier is applied. It sets the character’s speed to a configured ‘run_speed’ value.

### Crouching

A character is considered crouching when ‘input == *’ and only the crouch modifier is applied. This module sets the character’s speed to a configured ‘crouch_speed’ value.

### Falling

This state is triggered when the player is falling.

### Jumping

This state is triggered when the jump modifier is applied and the character is not falling. It makes the character ‘jump’ in the air at ‘i’ velocity where ‘i’ is a configured value.

### Climbing

This state is triggered when the character is ‘falling’ and a wall is within climbable reach, which is defined by a configured value. This state moves the character upwards at a configured rate until a configured time is exhausted, the speed of climb has been reduced to zero by an on-tick scalar, or the top of the wall it reached, at which point the state transitions to ledge grabbing.

### Ledge Grabbing

This state is triggered if the character has just been falling or climbing and is facing the inverse edge of a precipice at a configured z-offset from the top of the ledge. If the jump modifier is applied during this state, or ‘forward-input > 0’ during this state, the state transitions to mantle.

### Mantle

This state is manually triggered after a wall hang or the jump modifier is applied when facing the inverse edge of a precipice and the character is over a configured z-offset from the edge of the precipice (for example, vaulting a fence). This state launches the character over the edge at a configured speed, and transitions to the crouching state, which then clears because the crouching modifier is not applied.

### Sliding

This state is applied when both crouching and sprinting modifiers are applied. This module reduces ground friction by a configured amount and transitions to crouching after a configured time or speed is reached.

### Wall Run

This comes in two states 'wall-run-left’ and ‘wall-run-right’ which are triggered when the character is in the air parallel to a wall that is at a minimum and maximum configured angle relative to the ground. This state locks the player on the wall and allows them to ‘run’ on the wall at a configured speed in an arcing pattern until either a timer is elapsed or the speed equals zero. If the jumping modifier is applied, the character will jump off of the wall at a configured angle.