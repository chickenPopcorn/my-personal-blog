---
title: "Intellij Idea Shortcut"
date: 2018-02-11T17:03:16-05:00
tags: ["IDE", "tooling", "Intellij"]
draft: false
---
### **Overview**
I recently moved to Intellij Idea as my IDE for development. It's simple to use and feature packed. The only 
downsides are it's expensive, and it may take a little bit of time to start up. That's said, there is a learning 
curve as with migrating to any new IDE. There post goes through some of th basics on how to use Intellij Idea more 
effective to boost your daily productivity. 


### **Create Shortcut**

To create short cut in terminal for IDEA, simply download the [idea script](https://gist.github.com/chickenPopcorn/f0377dd891a81b06aeb9c79f4cf3a6af) and install in your local user bin folder. You can simply run the following command to download and add execution permission.
```bash
curl -L "https://gist.githubusercontent.com/chickenPopcorn/f0377dd891a81b06aeb9c79f4cf3a6af/raw/334bcdb0e38dcc7bb678e6a0c42074b517927d9d/idea" -o /usr/local/bin/idea
chmod +x /usr/local/bin/idea
```

You may have to update the script on where idea is installed on your machine.
```bash
IDEA= 'ls -1d ~/Library/Application\ Support/JetBrains/Toolbox/apps/IDEA-U/ch-0/173.4548.28/IntelliJ\ IDEA.app/ | tail -n1'`
```



Now you can use `idea .` in your terminal to fire up your IDE.


### **Basic Cursor Operation** 

#### **Selection** 

> - <kbd>Shift</kbd> + <kbd>Alt</kbd> + <kbd>Right/Left</kbd>: Select on one word at a time.
- <kbd>Alt</kbd> + <kbd>Up/Down</kbd>: Increase/decrease selection
- <kbd>Command</kbd> + <kbd>A</kbd>: Select all
- <kbd>Shift</kbd>+ <kbd>Alt</kbd> + <kbd>Up/Down</kbd>: Move line/block by line
- <kbd>Command</kbd> + <kbd>Shift</kbd> + <kbd>Up/Down</kbd>: Move line/block by block

#### **Comment/Deletion** 
> - <kbd>Command</kbd> + <kbd>/</kbd>: Comment/De-comment line/block
- <kbd>Command</kbd> + <kbd>Delete</kbd>: Delete current line
- <kbd>Command</kbd> + <kbd>Z</kbd>: Undo
- <kbd>Command</kbd> + <kbd>D</kbd>: Duplicate line/block

#### **Others** 
> - <kbd>Command</kbd> <kbd>+/-</kbd>: Collapse current code block
- <kbd>Command</kbd>+ <kbd>Shift</kbd> <kbd>+/-</kbd>: Collapse all code block
- <kbd>Control</kbd> + <kbd>G</kbd>: Multi-select
- <kbd>Control</kbd> + <kbd>Shift</kbd> + <kbd>G</kbd>: Deselect multi-select

### **Basic Completion**
TODO