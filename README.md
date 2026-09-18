# quad

`quad` turns a directory into a 2x2 tmux grid of four `ollama` panes — one
tmux session per project.

Companion to [`try`](https://github.com/tobi/try): from the try selector
straight into a four-panel workspace.

## Usage

```
quad            # 2x2 grid for the current directory
quad name       # fresh date-stamped dir ($QUAD_HOME/YYYY-MM-DD-name) + grid
quad /path      # 2x2 grid for that directory (created if missing)
quad new [name] # run the try selector, create/pick a try dir, then grid it
quad -l         # list running quad sessions
```

Each pane runs `ollama`, which brings up the interactive Ollama menu where you
pick an integration (Claude Code, OpenCode, Codex, …) and model.

Sessions are named after the directory and reused: running `quad` again for the
same directory reattaches, while a different directory rebuilds the session.

## Install

```sh
git clone git@github.com:razodin137/quad-code.git
ln -s "$PWD/quad-code/quad" ~/.local/bin/quad
```

## Configuration

| Variable     | Default            | Purpose                                  |
| ------------ | ------------------ | ---------------------------------------- |
| `QUAD_HOME`  | `$HOME/Projects`   | Where bare-name date-stamped dirs live   |
| `TRY_PATH`   | `$HOME/Work/tries` | Where `try` creates/selects try dirs     |

To run something other than bare `ollama` per pane, edit the `PANE1`–`PANE4`
variables near the bottom of the script, e.g.:

```sh
CLAUDE_CMD='ollama launch claude -- --dangerously-skip-permissions'
PANE1="$CLAUDE_CMD"
```
