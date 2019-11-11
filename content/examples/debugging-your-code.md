---
title: "Debugging your code"
date: 2018-08-19T09:01:24+02:00
example: true
---


Planet Lia CLI can help you with debugging your code. 
Usually when you run the [```play```](/lia-cli/#play) command through terminal, Cmd or PowerShell, Planet Lia CLI automatically runs the match generator and two bots that you have specified in the command.
This is great because you can see the resulting match within seconds.
Sometimes though, yo want to connect your bot manually to match generator and stop the match in between, step through your code with a debugger and check what is going on.

### Generating game in debug mode

Fortunately `play` and `generate` commands have a flag with which you say which bots you will run manually. 
It is also useful to include the `-d` flag that will display the debug view of the match.
The command below will generate a match between bots `jon` and `bob`. Planet Lia CLI will take care of running `bob`, while `john` will have to be run manually.

```bash
# Flag -m stands for manual mode and 0 defines that a bot at 0 index 
# (in this case john) will be run manually.
#
# If you would type -m 1 then bob would have to be run manually and 
# if you would set -m 0,1 then both bots would have to be run manually
./lia play -d -m 0 john bob 
```

After you press ENTER, you should see something like this: 
```text
...
Running match generator.
Bot server started on port 8887
Waiting for bots to connect
Running bot bob
Bot 'bob' has connected
```

Match generator will then wait until you manually connect your bot.

### Manually connecting your bot

Now you can manually run your bot using your IDE.
Let's see how this can be done with IntelliJ IDEA (We are by no means affiliated with JetBrains, the creators of IntelliJ IDEA, this IDE is used here just to showcase the point).

### Connecting your bot with IntelliJ IDEA

Make sure you have [IntelliJ IDEA](https://www.jetbrains.com/idea/) installed. You can then open your bot with it the following way.

1. Launch IDEA and click Open on the welcome screen. <br/> &nbsp;
    <div style="text-align:center"><img src="/static/examples/images/intellij-open.png" alt="Open IntelliJ IDEA" width="30%" vspace="20"/></div>
2. Locate your bot (eg. `john`), mark it and then choose OK. <br/> &nbsp;
    <div style="text-align:center"><img src="/static/examples/images/intellij-path-to-john.png" alt="Path to John" width="30%"/></div>
3. On the next screen tick *Use auto-import* checkbox and click OK. 
4. Editor will open up and you will see Gradle installing dependencies. Wait until it is finished.
5. Open up *MyBot* (arrow 1) then click on the empty space in the line where you want your debugger to stop (shown by arrow 2) and then click the play icon (arrow 3) and choose *Debug 'MyBot.main()'* option. Note that the match generator should be running and waiting for `john` to connect as shown above. <br/> &nbsp;

    <div style="text-align:center"><img src="/static/examples/images/intellij-opened.png" alt="Opened IntelliJ IDEA" width="90%"/></div>

If all went well, you should be able to see the match generator successfully connecting your bot and starting to generate the match but stopping at the beginning. If you look in your IDEA editor you can see that the IDEA has paused the game generation and you can now analyse the state of your bot.
Because the match generator is in debug mode, your bot won't timeout and you will be able to take as much time as you need before continuing with the match generation.

 <div style="text-align:center"><img src="/static/examples/images/intellij-debug.png" alt="Debug IntelliJ IDEA" width="90%"/></div>

That is it. Happy debugging!

----

### Related:

* [Using an IDE](/examples/using-ide/)
* [Reference for Lia CLI](/lia-cli/)
* [API reference](/api/)

