---
title: "Globbing_with_sudo"
date: 2024-01-12T16:46:20-05:00
tags: [TIL,shell] 
---

Ran across an issue I’ve encountered many times before and finally decided it was irritating enough to research. Something I’ve occasionally wanted to do is apply an operation as `sudo` to a number of files in a directory or group of directories. The easiest example is listing all the files of a given type from a group of directories. 

If elevated privileges aren’t required, `ls **/*.py` will list all the python files in every subdirectory of a given location. However, `sudo ls **/*.py` will fail with the error that `File *.py not found.`. A bit of reading revealed that this happens because the action of globbing occurs _before_ the call to `sudo` happens, so calling `sudo` doesn’t help to reveal any of the files in inaccessible folders. The way to correct this is to call the `ls **/*.py` file in a subshell and use `sudo` to launch the subshell, like so: `sudo zsh -c ‘ls **/*.py’`. This will run the command as `sudo` and let the shell do the globbing with the correct privileges. Lesson learned, need to remember to run more commands as subshells!