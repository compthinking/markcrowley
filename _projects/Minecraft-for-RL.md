---
layout: page
title: Minecraft for RL
name: Minecraft for RL
permalink: /minecraft/
domains: minecraft
bibkeyword: minecraft
methods: reinforcement-learning, ppo, dan, mdp
description: Exploring the use of Minecraft as an environment for Reinforcement Learning
status: active
people: nouhachatti, ankilpatel, markcrowley
toc: false
showtitle: true
bibkeyword: minecraft
showbib: false
publish: true
---

Minecraft is a video game that takes place in a virtual world where players need to obtain raw materials, build useful objects, grow and eat food, and defend themselves to survive. It's a simplified model of reality, with some additional physics(:)), that relates directly to planning in the real world. It's a perfect environment for exploring decision making, learning and maximizing utility.



## Tasks and Subtasks in Minecraft

It will help to operationalize the types of activities that need to happen in minecraft. These divisions aren't necessarily ones we'll define explicitly in any learning agent. Sometimes we'll want to try to learn as many of these as possible from fundamental interaction in the environment. Other times, we may want to explore the benefit of higher level algorithmic choices by define these subtasks explicitly for the agent to choose from. 

This is just one example of a task-subtasks hierarchy we'd expect to arise from learning an action. Given enough standard actions in the game we will see a pattern of the general subtask types and they can be defined globally. It is expected that learning on these individual subtasks will be applicable wherever they are encountered.

- Task(`obtain-wood`): Obtain wood in your inventory
	- subtask(`locate-blockOfType`): find a source block X of wood visually (tree or planks) (other available subtasks: `locate-entity`
	- what it involves: 
		- `scan-currentview-object` which analyzes the current view for the object
		- `turnto-direction` to look elsewhere and repeat scan 
	- subtask(`moveto-location`) : move to a square adjacent to X 
		- other avilable subtasks: 		
			- `moveto-direction-steps`
	- subtask(`turnto-object`) : face the block X
		  - other available subtasks:
			  - `turnto-direction`
	- subtask(`select-tool`) : choose the appropriate tool for obtaining the block 
		- relevant knowledge:
			- `tooleffectivness-obtain-material` : best tools for each material (axe for wood, shovel for sand/soil/gravel, pickaxe for most other things)
	- subtask(`obtain-block`): obtain the block you are facing
		- what it involves:
		  - holding the attack action for a duration of time
		  - judging length by the visual change in the block in front of you, or when the object is acquired in inventory
		- Hardcoded action in Malmo:
		  - Initiate `attack` action on block in front of the agent using the current tool in hand
		  - Maintain `attack` until one of the following conditions met:
		    - Inventory changes, new item appears
		    - Block in from of you disappears or changes (harder to determine in image environment)
		    - Time threshold is passed (default: 5 seconds)
		    - Design question: while the action is happening, can the agent still experience time? It can't move or do anything else since that would disrupt it. But technically it could cancel the action earlier, the problem is then we need to reason about time and duration, which makes it much more complicated. 
		      - Simple answer: no, the agent is blocked to keep performing attack until one of the conditions is met, if this is too long then the time threshold should be adjusted



## Interesting Ideas to Explore for Future

- NLP Mining for Minecraft:
  - There are a *vast number* of books and online materials on minecraft written for children and as a reference for players on how the universe of minecraft works. These documents are written in natural language with tables and descriptions meant for human consumption. 
  - Recently, researchers in chemistry, physics, medical images and other fields have used *Natural Language Processing* {% cite thatpaperonchmistrywiththeperiodic table %} algorithms to learning complex encodings of the relevant space. 
  - A *fascinating* project would be to do the same thing in the Minecraft space, to build a master conceptual encoding from websites and other documents and use these concepts for improving planning in Minecraft.
  - This is *important* because doing the same thing for material design and digital chemistry would be exactly the same process, just in a vastly more complex field.
