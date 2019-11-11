---
title: "API"
date: 2018-08-09T17:29:46+02:00
---

This is the collection of all the data that your bot has access to during the generation of a mach as well as all the methods that it can
use in order to control game entities.

On this page you can find references for:

* [InitialData](#initialdata) - Gives you match state and all the constants when the match starts
* [MatchState](#matchstate) - Gives you access to match state during the match generation
* [Response object](#response-object) - With it you can control your game units, make them move, spawn new ones, etc.

---

## InitialData

Bot receives InitialData object only once at the beginning of the match. It holds the following data:

- *... same values as in [MatchState](#matchstate) except for the `time` value which is `0` in InitialData...*
- **`mapWidth`**`: int` - *In world units*
- **`mapHeight`**`: int` - *In world units*
- **`unitSize`**`: float` - *In world units*
- **`planetDiameter`**`: float` - *In world units*
- **`unitSpeed`**`: float` - *In world units / second*
- **`unitRotationSpeed`**`: float` - *In degrees / second*
- **`numberOfWorkersOnStart`**`: int`
- **`unitCost`**`: int` - *How much resources a new unit costs*
- **`resourceGenerationSpeed`**`: float` - *resources / second*
- **`maxActiveWorkersPerPlanet`**`: int` - *How many workers can be simultaneously mining resources on the same planet*
- **`maxNumberOfUnitsPerTeam`**`: int` - *If reached your bot won't be able to spawn new units*
- **`maxMatchDuration`**`: float`
- **`workerHealth`**`: float`
- **`workerAttack`**`: float`
- **`warriorHealth`**`: float`
- **`warriorAttack`**`: float`
- **`damageReductionRatioOnDefence`**`: float` - *How much the attack of a unit is reduced when it is attacking opponent units at opponent planet*
- **`__matchDetails`**`: MatchDetails` - *A few details about the match and participating bots*
    - **`yourBotIndex`**`: int` - *Index of the bot in botsDetails to which this instance of MatchDetails was sent to*
    - **`botsDetails`**`: list` - *List of all bots that participate in this match with their details*
        - **`botName`**`: string`
        - **`teamIndex`**`: int`

---

## MatchState

Bot receives MatchState every 0.2 match second (5 times per match second). 
It holds the data about what is going on with match entities at a current time during the match.

- **```time```**```: float``` - *Current match time in seconds*
- **`yourPlanets`**`: list` - *List of planets that your bot currently owns*
    - **`id`**`: float` - *Id of the planet*
    - **`owner`**`: Owner` - *Enum - can be `RED`, `GREEN`, `NONE`*
    - **`x`**`: float` - *x location of the planet*
    - **`y`**`: float` - *y location of the planet*
    - **`resources`**`: float` - *How many resources are currently mined on the planet*
    - **`canSpawnNewUnit`**`: boolean` - *If there are enough resources on the planet to spawn a new unit*
    - **`idsOfUnitsOnPlanet`**`: list of int` - *List of ids of the units that are currently on the planet*
- **`freePlanets`**`: list` - *List of planets that are still free, same object types as `yourPlanets`*
- **`opponentPlanets`**`: list` - *List of planets that are owned by the opponent, same object types as `yourPlanets`*
- **`yourWorkers`**`: list` - *List of your workers*
    - **`id`**`: float` - *Id of the unit*
    - **`type`**`: UnitType` - *Enum - can be `WORKER`, `WARRIOR`*
    - **`x`**`: float` - *x location of the unit*
    - **`y`**`: float` - *y location of the unit*
    - **`rotation`**`: float` - *In degrees*
    - **`health`**`: float`
    - **`currentPlanetId`**`: int` - *Id of the current planet, if the unit is not on a planet the it is `-1`*
    - **`destinationPlanetId`**`: int` - *Id of the destination planet, if the unit is not traveling then it is `-1`*
- **`opponentWorkers`**`: list` - *List of opponent workers, same object types as `yourWorkers`*
- **`yourWarriors`**`: list` - *List of your warriors, same object types as `yourWorkers`*
- **`opponentWarriors`**`: list` - *List of opponent warriors, same object types as `yourWorkers`*

---

## Response object

Using Response object you can communicate with the match generator and tell it what you want your units to do. You can use the following methods:

* **```spawnUnit(int planetId, UnitType type)```**
    * *Tells match generator to spawn new unit on a planet with id `planetId` and of type `type` that can be `WORKER` or `WARRIOR`*
* **```sendUnit(int unitId, int destinationPlanetId)```**
    * *Tells match generator to send a unit with `unitId` to the planet with id `destinationPlanetId`. 
    Note that you can only send away units that are not already traveling somewhere.*

---