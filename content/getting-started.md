---
date: 2018-08-05T04:32:25+02:00
title: Getting started
---

Let's setup your Planet Lia environment for Planetization game.

## 1. Download

* **Download Planet Lia CLI** for your operating system and unzip it into a folder of your liking. The tool is portable so you don't need to install it.
    * <a href="https://files.production.cloud.planetlia.com/games/planetization/1.0/windows/planet-lia.zip" target="_blank">Windows <i class="fas fa-download"></i></a>
    * <a href="https://files.production.cloud.planetlia.com/games/planetization/1.0/linux/planet-lia.zip">Linux <i class="fas fa-download"></i></a>
    * <a href="https://files.production.cloud.planetlia.com/games/planetization/1.0/macos/planet-lia.zip" target="_blank">macOS <i class="fas fa-download"></i></a>
* <a href="https://java.com/en/" target="_blank">Install Java</a> on your system. Planetization game is written in Java and it needs it in order to run. On most system it is already installed.
* <a href="/setup-programming-language/" target="_blank">Setup programming language</a> that you will use for writing your bot. 
If you have used the language before, you most likely already have everything that you need.

## 2. Play a game

Open up a **Cmd.exe** or **PowerShell.exe** on Windows or a **Terminal** on Linux or macOS, **move to the unzipped Planet Lia CLI** directory and run the commands below. 
First we will download a Planetization game and set it as our default game.
Then we will create a new starting bot `john` using programming language Java and will battle it against itself. 
To choose a different language for your bot simply replace the ```java``` part of the first command with ```python3``` or ```kotlin```.
The first time you play a match with your bot it may take some time as a couple of libraries need to be downloaded, later runs will be much faster.

{{< multilang >}}

<div class="tab">
    <button class="tablinks tc1 active" onclick="changeLanguage(event, 'Cmd', 'tc1', 'cc1')">Windows cmd</button>
    <button class="tablinks tc1" onclick="changeLanguage(event, 'PowerShell', 'tc1', 'cc1')">Windows PowerShell</button>
    <button class="tablinks tc1" onclick="changeLanguage(event, 'Terminal', 'tc1', 'cc1')">Linux/macOS</button>
</div>

<div id="Cmd" class="tabcontent cc1" style="display: block;">
{{< highlight cmd >}}
lia.exe game download planetization
lia.exe game set planetization
lia.exe bot new java john
lia.exe play john john
{{< /highlight >}}
</div>

<div id="PowerShell" class="tabcontent cc1">
{{< highlight powershell >}}
.\lia.exe game download planetization
.\lia.exe game set planetization
.\lia.exe bot new java john
.\lia.exe play john john
{{< /highlight >}}
</div>

<div id="Terminal" class="tabcontent cc1">
{{< highlight bash >}}
./lia game download planetization
./lia game set planetization
./lia bot new java john
./lia play john john
{{< /highlight >}}
</div>

<!-- ##### *Commands:* [*bot*](/lia-cli/#bot), [*play*](/lia-cli/#play) -->

After running the commands above, wait until the match is generated and voila, a browser window is opened displaying a replay of the generated match! 
Also a new directory named `john` is created in your current working directory. 
This directory contains all the code for your bot. We will dig into it in the next section.

<br/><div style="text-align:center"><img src="/static/docs/images/game-example.png" alt="Example gameplay" width="80%"/></div>

**Pro tip**: To speed up match generation, use `--skip-build` flag with `play` command. 
This will avoid building both bots before a match and it can be used when you will want to generate many matches one after another.

## 3. Understand your bot

With your favorite text editor open up your bot's main file. If you have created `Java` bot then open up `john/src/MyBot.java`, if `Python3` then `john/my_bot.py` and if `Kotlin` then `john/src/MyBot.kt`. 
You can also open the whole bot directory (eg. `john`) in an IDE. Check <a href="/examples/using-ide/">Using an IDE</a> example to learn more.

Starting bot implementation is very simple. Its now your goal to improve it.

**Read through the code to see how it works! If you need help, check out our <a href="/api">API</a>.**

Note that during the development you can structure your bot directory as you like, as long as the `MyBot` file acts as your "main" file.
This means that you can create additional files which you then import into `MyBot`.

 To delete a bot, simply delete it's directory, in our case the directory named `john`.

## 4. Debug your bot

A more detail guide on how to debug your bot using a step debugger integrated into your favourite IDE, is available [here](/examples/debugging-your-code).

Now we will only note that if you use `-d` flag with `play` command (eg. `lia.exe play -d john john`), you can **get a very useful debug view** while the match is generating, as shown below. 
It will let you to pause the match generation, step through it, view details of game entities, API calls and more. 

<br/><div style="text-align:center"><img src="/static/docs/images/debug-viewer.png" alt="Debug viewer" width="80%"/></div>


## Next up

Check out the game rules.

Next: **[Game rules](/game-rules)**

----

### Related:

* [Game rules](/game-rules)
* [API reference](/api/)
