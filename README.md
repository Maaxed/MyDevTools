# My Development Tools

This is the list of tools I use on Windows

## Tools

### Source control

- [Git for windows](https://gitforwindows.org/)
- [delta](https://github.com/dandavison/delta), a syntax-highlighting pager for git
- [git-graph](https://github.com/mlange-42/git-graph), an improved git log --graph

### IDE

- [VS Code](https://code.visualstudio.com/) for general programming
- [Eclipse IDE for Java Developers](https://www.eclipse.org/downloads/packages/)

### Compilation tools

- [rustup & cargo](https://www.rust-lang.org/fr/learn/get-started) for rust
- [MinGW-w64](https://www.mingw-w64.org/) for C/C++

### Graphics

- [Aseprite](https://www.aseprite.org/) for pixel art
- [paint.net](https://getpaint.net/) for image editing

### Game Development

- [Unity](https://unity.com)

### Programming font

- [JetBrains Mono](https://www.jetbrains.com/lp/mono/)

## Configuration

### Bash

``~/.bashrc``

```bash
# My aliases for commands I use all the time
# Ls with colors
alias ls="ls --color"
# Git log using git-graph
alias gitg="git-graph -s round"

# Set tab size
tabs 4

# Bash history config
# Ignore duplicates and lines starting with a white space
HISTCONTROL="ignoreboth"
# Ignore ls in history
HISTIGNORE="ls"
# Append history to the history file instead of overwriting the file
shopt -s histappend
# Save history after each command to avoid issues when using multiple terminals
PROMPT_COMMAND="history -a"

# Custom less style
export LESS_TERMCAP_mb="$(printf "\e[1;36m")"	# start blink
export LESS_TERMCAP_md="$(printf "\e[1;96m")"	# start bold
export LESS_TERMCAP_me="$(printf "\e[0m")"		# stop all
export LESS_TERMCAP_so="$(printf "\e[44m")"		# start standout
export LESS_TERMCAP_se="$(printf "\e[49m")"		# stop standout

export DISPLAY=:0
export TERM=cygwin
```

### Git

``~/.gitconfig``

```properties
# Use a specific .gitconfig file for all projets in my development folder
[includeIf "gitdir:C:/dev/some_folder/"]
	path = C:/dev/some_folder/.gitconfig
# My aliases for commands I use all the time
[alias]
	# git log as a graph
	glog = log --all --graph --oneline --decorate=short --branches="*"
	# glog but simplifies the graph to show the branch structure
	blog = log --all --graph --oneline --decorate=short --branches="*" --simplify-by-decoration
	# Make a commit with a message
	com = commit -m
	# Amend a commit
	amend = commit --amend
	# Pull rebase
	purr = pull --rebase
	# Diff but shows exactly what changed in each line
	wdiff = diff --word-diff --word-diff-regex=. -U0
	# Makes a quick backup branch (but deletes previous backup branch)
	backup = branch -f Backup
	# Discard local change
	discard = checkout HEAD -- 
	# Show a simmary of which files changed in a specific commit
	summary = show --summary --stat
	# Lists files known by git in a specific commit
	ls = ls-tree --name-only
	# Rebase merges
	rb = rebase --rebase-merges
[core]
	# Use VS Code as the default editor
	editor = code --wait
	# Use delta as the default pager
	pager = delta
	# Convert line ending to crlf when pulling and back to lf when pushing
	autocrlf = true
[init]
	# Use "main" as the default branch because it makes more sense
	defaultBranch = main
[pull]
	# Makes a the normal pull not accept conflicts
	ff = only
[rebase]
	# Automatically stash changed before rebase
	autoStash = true
[merge]
	# Automatically stash changed before merge
	autoStash = true
	# Show the original code when merging (used by delta)
	conflictstyle = diff3
[interactive]
	# Use delta for interactove diff
    diffFilter = delta --color-only

# My custom delta theme
[delta]
	dark = true
    navigate = true
	line-numbers = true
	file-style = yellow
	file-decoration-style = yellow ol ul
	hunk-label = >
	hunk-header-style = file syntax
	hunk-header-decoration-style = cyan box
	hunk-header-file-style = cyan
    line-numbers-left-style = cyan
    line-numbers-right-style = cyan
	true-color = always
```