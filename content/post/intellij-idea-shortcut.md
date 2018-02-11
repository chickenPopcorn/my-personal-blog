---
title: "Intellij Idea Shortcut"
date: 2018-02-11T17:03:16-05:00
draft: true
---

**Creating Shortcut**

To create short cut in terminal for IDEA, simply download the [idea script](https://gist.github
.com/chickenPopcorn/f0377dd891a81b06aeb9c79f4cf3a6af) and install in 
your local user bin folder. 

You may have to update the script on where idea is installed.
`bash
IDEA= 'ls -1d ~/Library/Application\ Support/JetBrains/Toolbox/apps/IDEA-U/ch-0/173.4548.28/IntelliJ\ IDEA.app/ | 
tail -n1'`
`

Run the following command to download and add execution permission.
`bash
curl -L "https://gist.githubusercontent.com/chickenPopcorn/f0377dd891a81b06aeb9c79f4cf3a6af/raw/334bcdb0e38dcc7bb678e6a0c42074b517927d9d/idea" -o /usr/local/bin/idea
chmod +x /usr/local/bin/idea
`

Now you can use `idea .` in your terminal to fire up your IDE.


**Basic Cursor Operation** 

Shift + Alt + Right/Left: select on one word at a time.
Alt + Up/Down: increase/decrease selection
Command + A: select all
Shift+ Alt + Up/Down: move line/block by line
Command + Shift + Up/Down: move line/block by block

Command + /: Comment/De-comment line/block
 
Command + delete: Delete current line
Command + z: undo
Command + d: duplicate line/block

Command +/-: collapse current code block
Command+ Shift +/-: Collapse all code block
Control + G: Multi-select
Control + Shift + G Deselect multi-select


**Basic Completion**
