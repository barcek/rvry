# rvry

Mark time passing in the terminal.

Highly configurable by flag, with a flow description option and self-test. Can be passed a tag to label the duration and a path to log the whole with date and time to a file, plus a Bash command to be run at each step or on completion.

Available over an Alpine base image via the Dockerfile in [shipping](https://github.com/barcek/shipping).

## Why?

To track the durations of regular activities, see a measure of time taken on a task so far, or delay one, or zone out with a subtle visual beat.

Useful also for jobs needing immediate setup, sub-minute spacing or display.

## How?

The `rvry` command can be run alone to show the time elapsed as its final output. By default it prints one dot per second, and when stopped with `q` or `Ctrl-C` shows the time elapsed.

A string to label the final output can be passed as the first argument:

```shell
rvry "label 1"
```

The path to a log file can be passed as the second:

```shell
rvry "label 1" path/to/log
```

Each log entry is a start datetime stamp, the duration and the tag.

Several options are available (see [Options](#options) below). These include the use of a Bash command run either on completion or at each step, specifically:

- on completion with the base option (i.e. `--task` / `-t`)
- at each step with one additional option applied (i.e. also `--lift` / `-l`)

The command is passed to `bash -c` by default, to `exec` unquoted if the `--flux` / `-x` option is applied.

Any such command can receive the available log entry elements, i.e. start datetime stamp and duration plus any tag, via the output cue - `:RVRY` by default - each use of which is replaced with the log entry elements before the command is run.

## Source

The script can be run with the command `./rvry` while in the same directory, and from elsewhere using the pattern `path/to/rvry`, by first making it executable, if not already, with `chmod +x rvry`. Once executable, it can be run from any directory with the simpler `rvry` by placing it in a directory listed on the `$PATH` environment variable, e.g. '/bin' or '/usr/bin'.

The hashbang at the top of the file assumes the presence of Bash in '/bin', the source code that several utils are installed. A list can be found close to the top of the file, and is printed also in the help text. In the event of any absence, the script will print the fact then exit.

### Defaults

The following core default values are defined close to the top of the source file:

- `mark` - the character(s) printed at each step (currently '.')
- `path` - the initial step count (0)
- `beat` - the number of seconds between each step (1)
- `edge` - the number of steps at which to end automatically, if greater than zero only (0, i.e. no automatic end)
- `sign` - the key pressed to end the script manually ('q')
- `word` - the output cue for commands run via the `task` option (':RVRY').

### Making changes

Running the self-test after making changes plus extending or adding test cases to cover new behaviour is recommended. The self-test is run with the `--test` or `-T` flag (see [Options](#options) below). The test cases are set in the `push` function close to the top of the source file.

## Options

The following can be passed to `rvry` before the tag and log arguments:

- `--mark` / `-m`, to set `mark` to the value of the next argument, e.g. to '+' with `-m +`
- `--path` / `-p`, to set `path` to the value of the next argument, e.g. to 10 steps with `-p 10`
- `--beat` / `-b`, to set `beat` to the value of the next argument, e.g. to 0.5 seconds with `-b 0.5`
- `--edge` / `-e`, to set `edge` to the value of the next argument, e.g. to 15 steps with `-e 15`
- `--sign` / `-s`, to set `sign` to the value of the next argument, e.g. to space with `-s " "`
- `--word` / `-w`, to set `word` to the value of the next argument, e.g. to '<LINE>' with `-w "<LINE>"`
- `--task` / `-t`, to show and run on completion the Bash command being the value of the next argument, e.g. `echo done` with `-t "echo done"`, or, if a file path, e.g. `-t path/to/script.sh`, the content of the file; the command may include the `word` substring - `:RVRY` by default - replaced before the command is run with the start datetime stamp, duration and any tag
- `--flux` / `-x`, to perform the action for `--task` / `-t` by passing its Bash command to `exec` unquoted rather than to `bash -c`
- `--lift` / `-l`, to perform the action for `--task` / `-t` at each step, in place of printing `mark`, rather than on completion
- `--deep` / `-d`, to omit the printing of `mark`, or the printing of the command itself if both `--task` / `-t`  and `--lift` / `-l` are passed
- `--full` / `-f`, to print escaped characters in `mark`
- `--near` / `-N`, to retain all printed characters and show those ordinarily hidden, overriding `--full` / `-f`
- `--glimpse` / `-g`, to show the flow with current values then exit
- `--version` / `-v`, to show name and version number then exit
- `--help` / `-h`, to show help text then exit
- `--test` / `-T`, to perform the self-test then exit, returning an exit code of 1 on failure

## Streams

If the output of `rvry` is piped to another process, only the final output is passed, without the character(s) marking each step, unless the `--near` or `-N` flag is used. Use of `Ctrl-C` to end the script will interrupt the entire pipeline.

## Development plan

The following are the expected next steps in the development of the code base. The general medium-term aim is a more portable, robust and visual implementation. Pull requests are welcome for these and other potential improvements.

- provide sample uses
- extend argument handling for short flag clustering
- allow for:
  - greater variation in visual output
  - alternative timestamp formats
- revise for full POSIX compatibility
