# rvry

Mark time passing in the terminal.

By default prints one dot per second, and when stopped with `q` or `Ctrl-C` shows the time elapsed. Can be passed a tag to label the duration and a path to log the whole with date and time to a file, plus a Bash command to be run on completion.

## Why?

To track the durations of regular activities, see a measure of time taken on a task so far, or delay one, or zone out with a subtle visual beat.

## How?

The `rvry` command can be run alone to show the time elapsed as its final output.

A string to label the final output can be passed as the first argument:

```shell
rvry "label 1"
```

The path to a log file can be passed as the second:

```shell
rvry "label 1" path/to/log
```

Each log entry is a start datetime stamp, the duration and the tag.

Several options are available (see [Options](#options) below), including the use of a Bash command on completion. Any such command can receive the available log entry elements, i.e. start datetime stamp and duration plus any tag, via the output cue - `:RVRY` by default - each use of which is replaced by the elements before the command is run.

## Script

The script can be run with the command `./rvry` while in the same directory, and from elsewhere using the pattern `path/to/rvry`, by first making it executable, if not already, with `chmod +x rvry`. Once executable, it can be run from any directory with the simpler `rvry` by placing it in the '/bin' or '/usr/bin' directory.

The hashbang at the top of the file assumes the presence of Bash.

### Defaults

The following core default values are defined close to the top of the source file:

- `mark` - the character(s) printed at each step (currently '.')
- `path` - the initial step count (0)
- `beat` - the number of seconds between each step (1)
- `edge` - the number of steps at which to end automatically, if greater than zero only (0, i.e. no automatic end)
- `sign` - the key pressed to end the script manually ('q')
- `word` - the output cue for commands run via the `task` option (':RVRY').

## Options

The following can be passed to `rvry` before the tag and log arguments:

- `--deep` / `-d`, to omit the printing of `mark`
- `--mark` / `-m`, to set `mark` to the value of the next argument, e.g. to '+' with `-m +`
- `--path` / `-p`, to set `path` to the value of the next argument, e.g. to 10 steps with `-p 10`
- `--beat` / `-b`, to set `beat` to the value of the next argument, e.g. to 0.5 seconds with `-b 0.5`
- `--edge` / `-e`, to set `edge` to the value of the next argument, e.g. to 15 steps with `-e 15`
- `--task` / `-t`, to show and run on completion the Bash command being the value of the next argument, e.g. `echo done` with `-t "echo done"`, or, if a file path, e.g. `-t path/to/script.sh`, the content of the file; the command may include the substring `:RVRY`, replaced before the command is run with the start datetime stamp, duration and any tag
- `--help` / `-h`, to show usage then exit
- `--version` / `-v`, to show name and version number then exit

## Piping

If the output of `rvry` is piped to another process, the character(s) marking each step are not printed. The final output only is passed - and logged to file if applicable - as usual once the key to end the script has been pressed.
