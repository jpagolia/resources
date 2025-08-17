# Cheatsheet for tmux

## Start a new named tmux session
```
tmux new -s <session_name>
```

## Detach from your session
Ctrl-B, then D

## Find the list of ongoing sessions (make sure you are logged into the correct node that is running your tmux sessions)
```
tmux ls
```
If server not found, there are no tmux sessions, or you are not ssh'ed into the correct login node.

## Attach to an ongoing session
```
tmux attach-session -t <session_name>
```

## Kill an ongoing session
```
tmux kill-session -t <session_name>
```

## Scroll up in the tmux output
Ctrl-B, then [
