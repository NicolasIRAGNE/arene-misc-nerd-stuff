# Random rambling

## Software i use

* IDE: VSCode
* Git client: SmartGit
* Term: kitty w/ zsh (oh-my-zsh)

## General VSCode stuff

### Ctrl+Shift+P

your best friend

use it

every day

opens up a command palette, just type in what you want to do and it will probably be there, along with a shortcut

### Other random shortcuts

* vscode shortcuts are your friends here are some nice ones
  * key modifiers: ctrl, shift
    * shift: select
    * ctrl: move one word at a time
  * use home / end to go to the beginning / end of a line
  * use page up / page down to go up / down a page
  * ctrl+d: select the next occurrence of the current selection, repeat to select more occurrences
  * use keyboard as much as you can
  * ctrl+r: browser through recent workspaces
  * ctrl+shift+t: reopen closed tab
  * ctrl+,: open settings
  * ctrl+o: open file
  * ctrl+k ctrl+o: open folder

### Font

I use [Fira Code](https://github.com/tonsky/FiraCode) with ligatures enabled.

```json
"editor.fontFamily": "Fira Code",
"editor.fontLigatures": true,
"editor.fontWeight": "300",
```

### Settings

sticky scroll: makes it so it displays wherever you are when editing some big text:

```json
"editor.stickyScroll.enabled": true
```

makes the cursor nicer:

```json
"editor.cursorBlinking": "smooth",
"editor.cursorSurroundingLines": 10,
```

### Extensions

Included in this repo are a list of common useful extensions [.vscode\extensions.json](.vscode\extensions.json).

## Git

### Random stuff

```bash
git config --global pull.rebase true
```

this option makes it not stupid and prevent you from completely messing up your work when you pull

```bash
git config --add oh-my-zsh.hide-dirty 1
```

this can be useful if you notice that your terminal is very slow in bigger repos

### Client

https://www.syntevo.com/smartgit/

i use this as my git client

it's nice, no extra bullshit

but you can use anything (except GitKraken (has some VERY error-prone behavior))

### These terms you need to get a grasp of

* rebase (very important later when you work with other people)
* reset (technically this is still a rebase but yeah)
* fast-forward (in git). try to keep your history linear so that your pulls are fast-forward
* DONT PANIC. most of the time, you can fix your mistakes. git remembers most of your actions, as long as they were committed at some point. most important: DONT DELETE .git FOLDERS. when in doubt, ask someone who looks like they are homeless, they can probably fix it.
* (a bit more advanced and subject to debate) pick a workflow. i use a semi-linear git history (merge commits only)
* use SSH authentification (google ssh-keygen if things are not working)
* try to use branches, never commit directly to master
  * so branch, code, whenever your feature is ready to be implemented, FIRST REBASE then merge
  * this will make it easier to integrate new code and avoid conflicts
* use gitignore (use gitignore.io)
* (advanced) use unit tests and integration tests along with a CI/CD pipeline
  * (advanced) these tests should be integrated to your IDE so you can run them easily without having to run the whole pipeline
* squash commits when necessary. try to keep your history clean and readable.

## Other random unorganized rambling

* use SPACES not tabs (should change literally nothing in your life but some software breaks with tabs)
* **use a linter (eslint, prettier, sonarlint, etc)**
  * this is very important and one of the first things you should setup. It will pick up on a lot of stupid mistakes and enforce a common style.
  * *always* use sonarlint, along with another language-specific linter (e.g. eslint for JS)
* if something is frustrating, STOP WHAT YOU ARE DOING AND FIX IT ON THE SPOT EVEN IF IT TAKES YOU 3 HOURS
  * brain power is more expensive than computer power. your energy / wellbeing is your most important resource. unhappy programmers are bad programmers.
* **document WHAT your code does and WHY, not HOW**
  * try to document all your APIs / interfaces, in JSDoc or whatever your language uses
  * DO NOT WRITE DOCUMENTATION YOURSELF. OUTDATED / WRONG DOCUMENTATION IS WORSE THAN NO DOCUMENTATION
* (advanced) **SSOT** (google it, extremely important)
* use a password manager (KeePassXC)
* everytime you use a tool, try to understand its philosophy and how it works
* try to use standard / cross-platform tools (or understand how they interact)
* SSH again, important
* if you plan to work in cybersecurity, learn how to use a terminal (especially UNIX-like systems)
  * get a playground of some sort. use a VM, a raspberry pi, a docker container, whatever. just get used to it.
  * try to use it as your main OS for a while. try to understand the philosophy behind it. it will probably break at some point. fix it and learn from it.
  * start with mint or ubuntu. they are easy to get up and running. use the terminal as much as you can.
  * (very advanced) try to use an arch-based distro. you will cry. you will learn. but you will cry. but it's the best way to understand how a system works as a whole.
* (opinionated) use headers in your files. indicate their purpose, author, date, etc (automated, of course) (i use [psioniq file header](https://marketplace.visualstudio.com/items?itemName=psioniq.psi-header))
* if working together, enforce a code style and common practices using shared config files
* try to integrate as much stuff as you can into your IDE. context switching is bad for performance (both computer and human)
* review your code and your teammates' code. be harsh but not stupid. reject PRs that are not up to standards. enforce quality.
* readability is more important than performance in the vast majority of cases. if you are not sure, benchmark.
* assume that most of your time will be spent READING code, not writing it. make sure it's readable and don't cut corners.
* assume that 90% of your problems have already been solved by someone else who devoted their life to it. use their work.
* the only time you should reinvent the wheel is when you are learning how to make a wheel. and realize you're really bad at making wheels. people have been making wheels for thousands of years. use their wheels. or use your own wheel, that will randomly break and wiggle around and just make your life miserable. (e.g. your sorting algorithm is probably worse than the one in your language's standard library. use theirs.)

### Logging

Logging is the process of spewing relevant information about your program to the console / a file / whatever.

It is *very* important, and also *very* easy to get wrong.

#### What to log

Knowing what to log might not be obvious at first, but you will get a feel for it.

As a rule of thumb, you should log:

* user actions
* i/o operations (e.g. file read / write / open)
* errors and warnings
* important events (e.g. server start / stop, etc)
* anything that might be useful to debug a problem

It can be hard to find the right balance between too much and too little logging, adjust accordingly.

Your logs **should** contain, at the very least:

* a timestamp
* the severity of the message (e.g. info, warning, error, etc)
* the source of the message (e.g. the name of the function that logged it)
* the message itself
* if in a debugging context, source code location (e.g. file, line, column) in a way that's parseable by your IDE so you can click on it and go to the source code

This ensures that your logs are 1. readable, 2. searchable, 3. cooperative when running in another program's context.

Use a logging library, they do most of this correctly for you.

#### Allow filtering

You should allow filtering of your logs, at least by severity.

If you're in a debugging context, you probably want trace-level logs. If you're in production, you probably just want info-level logs.

### Error handling

* DO NOT JUST CATCH ERRORS AND IGNORE THEM. handle them. an error going off silently is the worst thing that can happen. it is better to crash than to ignore an error.
* sometimes, crashing is the behavior you want. if you are in a context where you can't recover from an error, end the program. it's better than continuing in an unknown state. the responsibility of the caller is to handle the error.
