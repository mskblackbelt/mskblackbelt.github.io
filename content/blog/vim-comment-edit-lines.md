---
title: "How to make edits on multiple lines in Vim"
date: 2023-03-09T20:46:20-05:00
tags: [TIL, vim]
---

While my preferred (current) editor is [Nova](https://nova.app/), occasionally I have reason to edit in Vim, particularly when I'm working on files on a remote server. Recently, I found myself wanting to comment multiple lines in a Python file. On my personal machines, I've installed [NerdCommenter][nerdcomment], but that isn't always available.[^fn1] 

[^fn1]: Using NerdCommenter, selected (or current) line can be commented/uncommented with the toggle `<Leader>c<space>` (or commented with `<Leader>cc` and uncommented with `<Leader>cu`)
[nerdcomment]: https://github.com/preservim/nerdcommenter

For those occasions, basic Vim line editing skills come in to play. First, you can toggle "Visual Line mode" by hitting <kbd>Shift</kbd> + <kbd>V</kbd>, then highlighting the relevant lines. From there, doing a simple replacement (`:'<'>s/^/#/`,[^fn2] or whatever your comment replacement should be) comments out the selected lines. 

[^fn2]: The `'<'>` gets inserted as soon as you type <kbd>:</kbd>.

Alternately, you can do a block selection (enter that mode with <kbd>Ctrl</kbd>+<kbd>V</kbd>), select the start of each line, then press <kbd>Shift</kbd>+<kbd>I</kbd>. Type out the pattern (it will only show up on a single line for the moment), press <kbd>Esc</kbd>, then press <kbd>Enter</kbd> and the changes will be applied to the whole block selection. 

These methods are outlined in [a post on ostechnix.com][ost-post] in methods 1 and 4. 

[ost-post]: https://ostechnix.com/comment-multiple-lines-vim-editor/