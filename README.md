# bash-run

## Explanations and examples
**Easy and comfortable way to keep long command lines as short and memorable.**

For example, if you have a long command to remove all old backups except for the first of each month:
```bash
find /backup -name '????-??-01.*' -prune -o -mtime +7 -exec rm {} \;
```
You can save it:
```bash
runsave rm-backups find /backup -name '????-??-01.*' -prune -o -mtime +7 -exec ls {} \\\;
```
And run it later:
```bash
run rm-backups
```
**It has auto completions** - You can write `run` and pound the TAB key to get run commands completions.

To see the content of a command, use `runshow` (has auto completions).
```bash
runshow rm-backups
```

To see a list of all commands, use `runlist`

To remove an existin command, use `rundel` (has auto completions).
```bash
rundel rm-backups
```

To edit a command using your favorite editor, use `rundel` (has auto completions).
```bash
runedit rm-backups
```
To determine your favorite editor, set `EDITOR` environment variable in your `.bashrc`:
```bash
export EDITOR=emacs
```
The default editor is `vi`.

Finally to see help on the commands, use `runhelp`.

## Cons and pros over scripts and aliases
**Cons:**
* It is quick and easy to manage.
* It runs in your current shell (script creates a new shell and runs in it). The meaning is that you can move to other locations using cd and you can set environment variables.
**Pros:**
* you cannt use parameters.

## Installation
1. Save file `.bash_run` in your home folder.
2. Add the following line to your `.bashrc`:
   ```bash
   [ ! -f ~/.bash_aliases ] || (source ~/.bash_aliases)
   ```
3. To set the editor, add also the following line to your `.bashrc`:
   ```bash
   export EDITOR=vim
   ```
