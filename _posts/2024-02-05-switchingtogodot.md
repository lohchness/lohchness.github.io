---
title: Switching game engines to Godot
date: 2024-02-05 19:20:10 +0800
categories: [Projects]
tags: [code, gamedev]
---

We've all heard it countless times - *this* game engine will solve all my problems and it'll be the one I'm looking for!!

But THIS time it's the one for me. Godot is made by gamedevs for gamedevs, and its editor and language is super super nifty and intuitive and more handy than I thought. I'm not going into professional game development but just doing this as a solo side dev, so Godot was perfect - better at 2D than Unity, unbelievably fast code adjusting and running, intuitive game structuring with nodes, no engine bloat, incredibly good UX, the language GDScript is a nice blend of Lua and Python... it just *clicks*.

So I banged together Pong in a few days, added power ups, some skill, and named it Pongo, with an option to play against another local human opponent, or against the computer.

Here's a demo of me playing against the computer (the computer *can* be beaten with ball speed - like the player, it has a maximum paddle move speed):



https://github.com/lohchness/lohchness.github.io/assets/50405970/9c1a5d4e-1bdb-4265-91f5-d6621a29044d



Godot's unique features really made it extremely easy to get around roadblocks I had (which may not be the best practice, but for this scale it's no problem) - namely signals, and nodes.

Instead of Unity's GameObjects where you attach components (RigidBody, Sprite, etc) to it, in Godot you would have a Node component as the parent, then attach more Nodes to it to make up an object called a Scene. Also unlike Unity, each of Godot's Nodes inherit their parent's functionality. So a RigidBody2D inherits functionality of PhysicsBody2D, which in turn inherits from CollisionObjects2D, Node2D, and so on. As a result I didn't have to reuse scripts or functionality between GameObjects in Unity.

![](/assets/images/node.png)

Godot signals are extremely useful when you want to broadcast some sign to any and all connected Scenes listening to the signal, similar to the Observer pattern from OOP concepts. The Inspector tab in the editor makes this really easy, but if you want to connect two unrelated Scenes you'd have to use code to connect the signal to the function that would be called when the signal is broadcast. 

```js
var size_up = size_ups.instantiate()
// Connect its body_entered signal with ball's function
size_up.connect("body_entered", ball._on_size_up_body_entered)
```

Signals are consistent across all objects, and you can create your own signals to be broadcast. 

![](/assets/images/signals.png)

```js
func _on_p2_score():
	p2_pts += 1
	ui_p2_score.text = str(p2_pts)
	reset_game_state()
```

```js
// My own signal
signal point_scored

func _on_body_entered(body):
	if (body.get_name() == "ball"):
		point_scored.emit()
```

This signal system is similar to JavaScript's signals, and are superior to Unity's event handling.

Download Pongo here, and view the source code here.

I have some ideas for a couple upcoming games to show off what this can do (so I guess that's that for RoRxDestiny), but I'll build a couple more small games like this before embarking on the many-month-to-years-long journey.

The first idea is a game called Colorphyll (a play on the words Colorfull and Chlorophyll). It'll be a zen game about filling in colors or something. Maybe a mobile game. The theme will be green and/or something to do with leaves and nature.

The second idea is one where I want to show off my made up written languages and bring a bit of my worldbuilding to the small screen. It's a game called Tech Witch/Tek Witch (?) and it's a roguelike set in the future where you play as a sci-fi witch armed with a 90s power glove that can hack reality. There has been a plague that melded man with machine but you can handle the plague at bay for now. You use TAROS (haha tarot and OS) cards to upgrade your abilities, and speak the ancient arcane language of Python. Yes, the programming language. I'm working on the specifics but that's all I have right now. Purple and neon green color scheme.
