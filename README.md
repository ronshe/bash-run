# bash-run
**Easy and comfortable way to keep long command lines as short and memorable.**

## Explanations and examples

For example, if you have a long command to remove all old backups except for the first of each month:
```bash
find /backup -name '????-??-01.*' -prune -o -mtime +7 -exec rm {} \;
```
You can save it (and immediately run the command):
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

## Advanced topics
Backslash (**\\**) is your best friend.

### Piping
If you will try to save the following command,
```bash
runsave dirs-only ls -l | grep '^dr'
```
The immediate result will be good, but if you will try to rerun it using `run dirs-only`, you'll see a wrong result.  
The reason is that `bash` runs `runsave dirs-only ls -l` and pipes the result to `grep '^dr'`.

If you want to save it all (including the pipe), than you have to tell it to ignore the pipe and look at it as a text character. It will be saved and than ran, but this time it will be treated as a pipe.

The correct line should be (notice the added **\\**):
```bash
runsave dirs-only ls -l \| grep '^dr'
```
### Ifs, loops and multi multi-commands
Example:
```bash
for f in *
do
    if [ -d $f ]
    then
        echo $f
    fi
done
```
Should be one liner:
```bash
for f in *; do if [ -d $f ]; then echo $f ; fi ; done
```
And backslashed in order to be run-saved:
```bash
runsave list-dirs for f in *\; do if [ -d \$f ]\; then echo \$f \; fi \; done
```
