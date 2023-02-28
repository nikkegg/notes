# Tmux

## Quick reference

All commands below can be run on `tmux` prompt. You can invoke a the prompt with
`Bind-key :` shortcut and omit `tmux` prefix from the command.

### Sessions

Create new tmux session:
`$ tmux new -s mysession - new session`

Kill target session:
`$ tmux kill-session -t mysession`

Kill all sessions but the current:
`$ tmux kill-session -a`

Attach to a session with the name mysession:
`$ tmux a -t mysession`

### Windows

`Bind-key w` - window preview

`Bind-key ,` - rename window

`Bind-key c` - open new window

`Bind-key &` - kill window

`Bind-key v` - open vertical pane

`Bind-key x` - kill pane

`Bind-key ;` - jump to last active pane

`$ tmux swap-window -t 0` - to swap position of current window with window specified
after the t flag

### Commands

`Bind-key ?` - list bindings

`Bind-key :` - enter commands mode

`Bind-key [` - enter copy-mode

`/|?` - to search forwards|backwards in copy mode

### Scripting tmux

-F and -f options (format and filter) - super useful for scripting tmux and getting window/pane properties/flags. [Explanation](https://unix.stackexchange.com/questions/712407/how-does-tmux-list-panes-f-filter-work)
