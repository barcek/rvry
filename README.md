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

The script can be run with the command `./rvry` while in the same directory, and from elsewhere using the pattern `path/to/rvry`. It can be run from any directory with `rvry` by a) placing it in the '/bin' or '/usr/bin' directory and b) making it executable, if not already, with `chmod+x rvry`.

The hashbang at the top of the file assumes the presence of Bash.

## Options

The following can be passed to `rvry` in place of the tag and log arguments:

- `--help` / `-h`, for usage
