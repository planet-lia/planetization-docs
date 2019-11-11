---
date: 2018-08-05T04:32:25+02:00
title: Planet Lia CLI
---

Planet Lia CLI is a <a href="https://en.wikipedia.org/wiki/Command-line_interface" target="_blank">command line interface</a> that helps you play Planet Lia games as effortlessly as possible.
It can setup your bots, generate matches, help you with debugging and much more.
To set it up check our [Getting started](/getting-started) guide.

To see what Planet Lia CLI can do, open up a **Cmd.exe** or **PowerShell.exe** on Windows or a **Terminal** on Linux or macOS, **move to the unzipped Planet Lia directory** and run the command below:

{{< multilang >}}

<div class="tab">
    <button class="tablinks tc1 active" onclick="changeLanguage(event, 'Cmd', 'tc1', 'cc1')">Windows cmd</button>
    <button class="tablinks tc1" onclick="changeLanguage(event, 'PowerShell', 'tc1', 'cc1')">Windows PowerShell</button>
    <button class="tablinks tc1" onclick="changeLanguage(event, 'Terminal', 'tc1', 'cc1')">Linux/macOS</button>
</div>

<div id="Cmd" class="tabcontent cc1" style="display: block;">
{{< highlight cmd >}}
lia.exe --help
lia.exe bot --help
lia.exe play --help
...
{{< /highlight >}}
</div>

<div id="PowerShell" class="tabcontent cc1">
{{< highlight powershell >}}
.\lia.exe --help
.\lia.exe bot --help
.\lia.exe play --help
...
{{< /highlight >}}
</div>

<div id="Terminal" class="tabcontent cc1">
{{< highlight bash >}}
./lia --help
./lia bot --help
./lia play --help
...
{{< /highlight >}}
</div>
