# Vim

Most of `vim` commands/bindings I use often are burnt into my fingers, so this file is
mostly for things I don use frequently but which come very handy when I need
them. It also contains interesting facts about `vim` I did know and all kinds of
`vim` recipes and explanations.

## Regex

Lots of useful stuff [here](https://dev.to/iggredible/learning-vim-regex-26ep)
I am migrating to to this section when I have a
use-case/brainspace.

`^\(\(pattern\)\@!.\)*$` - will grep for all lines
not containing `pattern`.

`\%Vpattern` - will search in visual selection. Select text first, then enter
normal mode and run the command.

`g/^$/d` - remove all blank lines. In general `g` (for global) command will apply normal mode
command after the last slash (e.g `d` for delete in this case, `p` for paste, `y` for yank
and so on) to all the lines containing matching pattern in the entire file.

## Sorting

`:sort u` - will perform alphabetical sort and deduplicate entries.
`!sort -k 2 -t ,` - sorts csv columns. -k flag is to specify which column to
sort by, -t flag is to specify delimiter. !sort is unix sorting command so needs
a bang.
