---
date: 2018-08-05T04:32:25+02:00
title: Game Rules
---

## Gameplay

Your goal is to write a bot that controls a fleet of ships (units), conquer planets and battle with the opponent. 
The game starts with each side having `5` worker units and owning one planet.
With workers that are on a planet you can mine resources which you can use to build new units.
You can send your units to other planets to conquer them.
If a unit collides with an opponent unit or arrives at a planet owned by opponent units it engages in battle. 
The winner is the bot that manages to destroy all opponent units or that has more units than his opponent after the `200 s` mark.

In short, build more units and conquer more planets than your opponent!

* Game duration: 200 s or when a bot is eliminated

<br/><div style="text-align:center"><img src="/static/docs/gifs/example-gameplay.gif" alt="Example gameplay" width="60%"/></div>

## Power bar
Power bar represents a current balance of strength and shows ratio of the number of units each bot owns.
Power ratio of both bots is displayed during the mats as a green and red bar below the game UI.

<br/><div style="text-align:center"><img src="/static/docs/images/power-bar.png" alt="Power bar" width="70%"/></div>

## Map 
Map contains 22 planets that units can conquer. 
Units can move from one planet to the other (your bot can't change the destination of a unit while it is on its way!). 
If the unit can't go straight from one planet to another due to other planets being in between, it follows the path based on the graph shown in the image below.
Once it reaches a node in the graph (white circle) from where there is nothing in between itself and the planet it is traveling to, it goes directly to it.
In the image you can also see the ids of all the planets that are used in the game.

* Width: 96 map units
* Height: 54 map units
* Number of planets: 22

<br/><div style="text-align:center"><img src="/static/docs/images/map.png" alt="Map" width="50%"/></div>

## Planets
Each planet can host unlimited number of units.
Maximum of `5` worker units can mine resources simultaneously on a single planet.
When planet has `5` resources you can spawn a new unit on it where you can choose whether the unit will be worker or warrior.
If a unit arrives to a planet owned by the opponent it battles the opponent units that are on it.
When a unit attacks opponents planet it only does `80%` of normal damage to opponent units on that planet.
Let's call that home court advantage of the units that own the planet.

* Maximum number of workers mining simultaneously: 5
* Attacker damage reduced to: 80%
* Cost of a new unit: 5
* Size: 4 map units

 <div style="text-align:center"><img src="/static/docs/images/planets.png" alt="Planets" width="25%"/></div>

## Worker units
Worker units can mine resources but are bad at combat due to low health and attack.

* Resource generation speed: 1 resource / second
* Health: 50 HP
* Attack: 50 HP damage
* Size: 1.5 map units
* Price: 5 resources
* Speed: 6 map units / second
* Rotation speed: 60 degrees / second

 <div style="text-align:center"><img src="/static/docs/images/workers.png" alt="Workers" width="25%"/></div>

## Warrior units
Warrior units can't mine resources but they are strong at attack and defence and are thus great for combat.

* Health: 100 HP
* Attack: 100 HP damage
* Size: 1.5 map units
* Price: 5 resources
* Speed: 6 map units / second
* Rotation speed: 60 degrees / second

 <div style="text-align:center"><img src="/static/docs/images/warriors.png" alt="Warriors" width="25%"/></div>

## Battle 

Units can battle opponent units in two ways.

- **If two opponent units meet in space** they deal each other damage equal to the magnitude of their attack property. 
Note that warrior units have 2x attack and defence of worker units and are thus much better for fighting. 
- **If a unit lands on a planet owned by opponent units** it battles one opponent unit on that planet at a time, dealing damage according to: `attack property * 0.8` (opponent units have home court advantage) and receiving damage equal to the opponent unit's `attack` property. 
If it kills the opponent unit it starts battling another unit on the planet until it dies or no opponent units are left on the planet, in which case it takes over the planet. 
The unit first battles warrior opponent units on that planet and when there are no warrior units left it starts battling worker units.

## Bot restrictions

The following are bot limitations while the match is generating. 
Note that when running your bot locally in debug mode with the `-d` flag, no restrictions are set.
Head [here](/examples/debugging-your-code/) to see how to run your bot in debug mode.

* When the first update is called your bot has  **1 second to respond**
* For all other updates your bot has **0.2 seconds to respond**
* If your bot **fails to respond in time 8 or more times** in one match it is disqualified and the match will continue without it
* If your bot does **not connect within 15 seconds** when the match-generator has started it will be disqualified
* If the sum of the time that your bot took to respond to all requests combined is **greater than 45 seconds** it is disqualified

### Related:

* [Getting started](/getting-started/) - Get started with the game
* [API reference](/api/) - Check out how your bot can play the game