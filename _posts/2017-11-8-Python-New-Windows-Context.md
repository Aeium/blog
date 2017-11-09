---
layout: post
title: Adding Python to Windows Explorer "New" Context
---

Python feels particularly at home on Linux. There are many reasons for this and that is not really the topic of this post.

Personally, the work that I do is split between Windows and Linux systems, so it's nice to streamline the Python experience in Windows where I can, so it's not so jarring for me dropping into a Windows system from a Linux one.

If you don't already have Python on your Windows computer, I recommend installing an Anaconda distribution. There is a good guide for that here: [link](https://medium.com/@GalarnykMichael/install-python-on-windows-anaconda-c63c7c3d1444)

So, now we have Python on the machine. But how do we make a script? What I wanted is a "New Python Script" option in the windows explorer context menu.

![_config.yml]({{ site.baseurl }}/images/17-11-8/0.png)

This will streamline things and help make Python seem more at home on Windows.

It will require a few additions to the registry. The easiest way to do this is to make a .reg file. I could fairly easily host the .reg file I used and offer it for download, but even if you trust me it is probably not good security practice to download and execute registry edits from the internet. Seems sort of sketchy.

Instead lets just make the registry file ourselves, this will give us an opportunity to at least give the .reg file a look and check for stuff that looks malicious.

This is the file that I used, in plain text:

```text
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\.py]
@="Python"
"Content Type"="text/x-python"
"Python"="Python"
"PerceivedType"="text"

[HKEY_CLASSES_ROOT\.py\ShellNew]
"NullFile"=""

[HKEY_CLASSES_ROOT\Python]
@="Python Script"
```

I got it from utapyngo's answer in this stackOverflow page: [link](https://stackoverflow.com/questions/19758455/how-do-i-add-a-new-python-script-option-to-the-context-menu)

Just copy that text into the clipboard and open Notepad.

Paste the text into Notepad.

Give it a look. To me this file looks pretty harmless, no weird URL, no ports opened, nothing like that. But it's your registry and I am not necessarily a security expert, so this part is up to you.

One we are ok with this registry change, we are ready to save and execute it. Go to File > Save As... Set the file type to "all files" and save as "myRegEdit.reg". Save it somewhere you can find it, it doesn't really matter where.

![_config.yml]({{ site.baseurl }}/images/17-11-8/1.png)

Execute the .reg file. You are almost done! Reboot the computer.

Important Note!! This require multiples reboots/shutdowns to take effect. For me this was the biggest obstacle and pain point getting this to work, because it made it seem like the working configuration still needed more tweaking, which made the entire process getting this to work much harder that it should have been. It doesn't need more changes! Those registry changes work! For some reason it just takes more than one reboot to take effect.

From my experience, it seems to require both a shut down and reboot. The second time I did this procedure, I did a complete shutdown first, and then a reboot next, and that was enough to see the new option appear in the context menu.

Maybe this sort of trouble is part of the reason Python feels more at home on Linux. But regardless, once you get it there, the "New Python Script" option in the explorer context menu is nice to have. Happy Hacking.
