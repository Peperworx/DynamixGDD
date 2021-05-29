---
layout: page
title: Dynamix GDD
---

# Project Dynamix

## Overview

Dynamix is an experimental FPS concept for controlling the positioning of players in a large ‘open’ world with the purpose of enabling contact with other players. Dynamix will do this by scaling a ring, similar to the ring or ‘storm’ found in battle royale games. However, Dynamix differs from battle royale games as the ring is not scaled by an elapsed time, but by the number of players currently in the world.

## About this document

Because Dynamix is a concept for a game mode and not a full game, an actual game will need to be built first. This is being developed, but progress has slowed and the codebase has become hard to maintain. Hence, this document is being written to provide the full and absolute specification for a rewrite of the core Dynamix game, also called the Peperworx Game Architecture (Or codebase). This type of document is known as a Game Design Document, or GDD.

## Milestones

This section details specific milestones that must be accomplished *in the specified order*.

### Movement System

The first operational system of the core game is the movement system. The Movement System consists of the core movement mechanics that the game is based on. This is detailed in the Movement System chapter of this document.

### Status System

This system handles player status, such as health, stamina, etc. This is detailed in the status system chapter.

### Inventory System

The inventory system is the second operational game mechanics system. The inventory may be achieved using an Unreal Engine plugin. This system is detailed in the chapter 'Inventory System' of this document.

### Weaponry System

The weaponry system is the system that handles the dynamic equipping and use of weaponry in First and Third Person views. This system is detailed further in the 'Weaponry System' section of this document.