---
title: "Z-shell completions"
date: 2024-01-29T11:15:42-05:00
tags: [TIL, shell_scripting, zsh, zsh_completions]
draft: false
---

I just spent far too long toying with creating a shell completion for my Zsh setup… On the surface, all I wanted was a simple function to take a graded assignment and return it to a student. Last fall, I put together a script using the `install` function to do precisely this (wanted to copy a file owned by my user over to a students folder with the appropriate permissions). The script itself looks like this:

```shell
return_graded () {
		sudo install -g "$1" -o "$1" -m 0755 -t "/home/$1/Graded" -D $2
}
```

For completions, I wanted Zsh to prompt me with a list of users on the system for the first argument and a list of files for the second argument. Unfortunately, finding a simple example of a completion function (along with directions on how to name it and where to place it) was quite difficult. After much searching and reading through many posts that gave small pieces of the answer (along with the `man` page for `zshcompsys`, which showed all the necessary tags), I managed to put together the following simple file, located at `~/.local/zsh-completions`, a folder I made sure to add to my `$fpath` variable in `.zshrc`. 

```shell
#compdef _return_graded return_graded
_return_graded() {
	_arguments ': :_users' ': :_files'
}
```

The first line tells Zsh this is a completion definition file (and I'm not sure whether just one or both function names are required afterward). The next lines define the completion function. From what I can tell, preceding the completion function with an underscore is an agreed-upon standard to keep the completion functions out of the normal function namespace. The zshcompsys man page gives some details about using the `_arguments` function to set completions for specific arguments. The `_users` and `_files` tags are built into zshcompsys, so I just had to look up their names. While it's possible to set keyword arguments with specific completions, I'm fine with my arguments being unnamed and strictly ordered (there's only two…). So long as the arguments are in order, there's no need to add numbers, but `'1: :_users' '2: :_files'` would let you explicitly (or out-of-order) label the arguments. The space (or a descriptive title for the completion) between the two colons is required. The long form of the above completion would be `_arguments '1:Username:_users' '2:Filename:_files:'`. Both versions have the same effect on the final product. 

## Further steps

Someday, I may decide that returning assignments one at a time is too slow and figure out how to let `return_graded` take multiple files at the end (should be simple). At that point, I'll have to modify the `_files` completion to take all remaining arguments, but until then, this gets the job done. 