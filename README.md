# rvry

Mark time passing in the terminal.

By default prints one dot per second, and when stopped with `q` or `Ctrl-C` shows the time elapsed. Can be passed an optional tag to label the duration and a path for logging the whole, with the date and time, to a file.

## Why?

To track the durations of regular activities, see a measure of time taken on a task so far or zone out with a subtle visual beat.

## How?

The `rvry` command can be run alone to show the time elapsed as its final output.

A string to label the final output can be passed as the first argument:

```shell
rvry "task name"
```

The path to a log file can be passed as the second:

```shell
rvry "task name" path/to/log
```

Each log entry is a start datetime stamp, the duration and the tag.

## Script

The script can be run with the command `./rvry` while in the same directory, and from elsewhere using the pattern `path/to/rvry`, by first making it executable, if not already, with `chmod +x rvry`. Once executable, it can be run from any directory with the simpler `rvry` by placing it in the '/bin' or '/usr/bin' directory.

The hashbang at the top of the file assumes the presence of Bash.

### Defaults

The core default values are defined close to the top of the source file. The character(s) printed at each step are assigned to `mark` (currently '.'), the initial step count to `path` (0), the number of seconds between each step to `beat` (1) and the key pressed to end the script to `sign` ('q').

## Options

The following can be passed to `rvry` before the tag and log arguments:

- `--deep` / `-d`, to omit the printing of `mark`
- `--beat` / `-b`, to set `beat` to the value of the next argument, e.g. to 0.5 seconds with `-b 0.5`
- `--path` / `-p`, to set `path` to the value of the next argument, e.g. to 10 steps with `-p 10`
- `--mark` / `-m`, to set `mark` to the value of the next argument, e.g. to '+' with `-m +`
- `--help` / `-h`, to show usage then exit
- `--version` / `-v`, to show name and version number then exit

## Piping

If the output of `rvry` is piped to another process, the character(s) marking each step are not printed. The final output only is passed - and logged to file if applicable - as usual once the key to end the script has been pressed.
