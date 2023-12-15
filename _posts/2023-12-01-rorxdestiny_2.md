---
title: RoRxDestiny 2 - Basics
date: 2023-12-01 21:01:39 +0800
categories: [RoRxDestiny]
tags: [gamedev]
image:
    path: /assets/images/huntress_select.png
---

So finally with Devlog 1 out of the way, I can finally get on with showing the basic stuff done for the game. This is going to be animations, movements, actions, and plans.

Firstly, I'd like to mention about the iterative process of game design - which is to repeatedly propose, prototype, and playtest again and again. Each time with new ideas learned from each cycle. Instead of focusing on getting things perfect, the game will be iterated upon, and everything here will be replaced some time down the line. I just need to get the base mechanics working before adding personal touches.

Although this is far from my first gamedev project, using Unity and C# is completely new to me.

Not using Java sped up this process significantly. Otherwise, I would have to draw up had models and designs for all the classes required ([da heck is this???](https://github.com/lohchness/pac-man-extended/blob/f41a2aed39e8522755c1c112bedc5d9450f9ca5a/documentation/DesignModel%20-%20Full.pdf)). I shudder to think about what I could have done.

## Character Animation

In the interest of time, I repurposed the Huntress spritesheet to use in my character animations. I decided to only use one character (for now) to get the wheels on the ground and get the base game running.

![](/assets/images/MergedImages.png)

## Basic Movement

Here's some basic movement so far, implemented with the PlayerInput component. Walls/Objects that have the BoxCollider2D component will block the player's movement going into its hitbox, but will still allow perpendicular movement. 

![](/assets/images/movement.gif)

So far, the animator:

![](/assets/images/player_animator.png)

## File Structure

## Object/Enemy Interaction
