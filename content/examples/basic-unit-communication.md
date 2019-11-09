---
title: "Basic unit communication"
date: 2018-08-19T09:01:24+02:00
example: true
---

{{< headless-note title="Prerequisites" >}}
Before you can go through this example you need to first setup your environment. 
You can find out how to do that in our [Getting started](/getting-started) guide .
{{< /headless-note >}}

In this example you will learn how to make your units communicate with each other. 
When one unit will see an opponent near a teammate it will tell a warrior teammate to go towards the position of the opponent. 
This way the teammate will turn towards the opponent and start fighting it when it comes in to the range.

**NOTE**: In the code implementation below the unit is not "telling" directly it's teammate that there is an opponent near it.
We check for each warrior unit if any teammates sees an opponent near it and we then make it move towards the opponent (the ability to check if a teammate sees an opponent is the communication here). 

This method proves very effective. See for yourself below:

<br>
 <div style="text-align:center"><img src="/static/examples/gifs/basic-communication.gif" alt="Basic communication" width="60%"/></div>

## Code

Below is the code for this example. 

⚠️ To keep the example clean we didn't include the whole code for the bot. 
In order to use this code you need to paste it to an appropriate location in your bot implementation.

{{< multilang >}}

<div class="tab">
    <button class="tablinks tc1 active" onclick="changeLanguage(event, 'Java', 'tc1', 'cc1')">Java</button>
    <button class="tablinks tc1" onclick="changeLanguage(event, 'Python3', 'tc1', 'cc1')">Python3</button>
    <button class="tablinks tc1" onclick="changeLanguage(event, 'Kotlin', 'tc1', 'cc1')">Kotlin</button>
</div>

<div id="Java" class="tabcontent cc1" style="display: block;">
{{< highlight java "linenos=table,hl_lines=" >}}
// Paste this code in update(...) method. Note that you should not set 
// a new navigation path to your unit in the code after the one below,
// as it will override it. Thus it is good to place this code on the 
// bottom of your update(...) method.

// Iterate through all of your units.
for (UnitData unit : state.units) {

    // If the unit is a warrior and it currently does not see an opponent
    // (and fights it), check it's teammates vision ares for nearby opponents.
    if (unit.type == UnitType.WARRIOR && unit.opponentsInView.length == 0) {

        // Check if some teammate detected an opponent near the unit. If
        // it did then send the unit to the location of the opponent.
        for (UnitData teammate : state.units) {
            boolean found = false;

            for (OpponentInView opponent : teammate.opponentsInView) {
                // Calculate the distance between the unit and opponent.
                float dst = MathUtil.distance(unit.x, unit.y, opponent.x, opponent.y);

                if (dst < Constants.VIEWING_AREA_LENGTH) {
                    // We have detected an opponent that is very close!
                    api.navigationStart(unit.id, opponent.x, opponent.y);
                    found = true;
                    break;
                }
            }
            if (found) break;
        }
    }
}
{{< /highlight >}}
</div>

<div id="Python3" class="tabcontent cc1">
{{< highlight python3 "linenos=table,hl_lines=" >}}
# Paste this code in update(...) method. Note that you should not set 
# a new navigation path to your unit in the code after the one below,
# as it will override it. Thus it is good to place this code on the 
# bottom of your update(...) method.

# Iterate through all of your units.
for unit in state["units"]:

    # If the unit is a warrior and it currently does not see an opponent
    # (and fights it), check it's teammates vision ares for nearby opponents.
    if unit["type"] == UnitType.WARRIOR and len(unit["opponentsInView"]) is 0:

        # Check if some teammate detected an opponent near the unit. If
        # it did then send the unit to the location of the opponent.
        for teammate in state["units"]:
            found = False

            for opponent in teammate["opponentsInView"]:
                # Calculate the distance between the unit and opponent.
                dst = math_util.distance(unit["x"], unit["y"], opponent["x"], opponent["y"])

                if dst < constants.VIEWING_AREA_LENGTH:
                    # We have detected an opponent that is very close!
                    api.navigation_start(unit["id"], opponent["x"], opponent["y"])
                    found = True
                    break

            if found:
                break
{{< /highlight >}}
</div>


<div id="Kotlin" class="tabcontent cc1">
{{< highlight kotlin "linenos=table,hl_lines=" >}}
// Paste this code in update(...) method. Note that you should not set 
// a new navigation path to your unit in the code after the one below,
// as it will override it. Thus it is good to place this code on the 
// bottom of your update(...) method.

// Iterate through all of your units.
for (unit in state.units) {

    // Do this only when there is no opponent in viewing area. If there
    // is an opponent in viewing area it is better to fight it.
    if (unit.type == UnitType.WARRIOR && unit.opponentsInView.isEmpty()) {

        // Check if some teammate detected an opponent near the unit. If
        // it did then send the unit to the location of the opponent.
        for (teammate in state.units) {
            var found = false
            
            for (opponent in teammate.opponentsInView) {
                // Calculate the distance between the unit and opponent.
                val dst = MathUtil.distance(unit.x, unit.y, opponent.x, opponent.y)

                if (dst < Constants.VIEWING_AREA_LENGTH) {
                    // We have detected an opponent that is very close! 
                    api.navigationStart(unit.id, opponent.x, opponent.y)
                    found = true
                    break
                }
            }
            if (found) break
        }
    }
}
{{< /highlight >}}
</div>

## Explanation

To detect if there is an opponent near the unit we need to iterate through all of unit's teammates and check how far away from the unit are the opponents that the teammates see.
To calculate the distance between a unit and an opponent we use  [MathUtil](/api/#mathutil) library that comes together with all basic bot implementations. 
It has a ```distance``` function that calculates the distance between two points on the map.

Now we need to decide at what distance is it worth for the unit to engage with the opponent. 
Here we will use `VIEWING_AREA_LENGTH`, one of the constants that each basic bot implementation ships with by default (read more about game constants [here](/api/#constants)). 
If the distance is smaller than the `VIEWING_AREA_LENGTH` then we determine that the opponent is close enough to the unit and is worth engaging. 
In that case we send the unit to the location of the opponent. 

We have chosen this constant as our max distance value as it seems meaningful, but we didn't test if it is also optimal.
Try playing with the values a little  and see if you can make some improvements.


## &#9814; Extra tips

1. **Smartly pick your opponent** - If there are multiple opponents near you, try picking the one with the lowest health left and aim at it.

2. **Attack from behind** - Check if there is an opponent that is fairly close and is turning its back to your warrior unit. Send your unit to attack it from behind.

3. **All together!** - Send all of your units to attack one of the detected opponents regardless of the distance to it and see what happens. :smile:

## Next up

In the next example we will implement a simple tactic to make our units retreat back to safety.

Next: **[Retreat](/examples/retreat/)**

----

### Related:

* [Examples](/examples/overview/)
* [API reference](/api/)
* [Using an IDE](/examples/using-ide/)
* [Reference for Lia CLI](/lia-cli/)

