# turfdb

A toy SQLite clone written in [TurfLang](https://github.com/), following the
["Let's Build a Simple Database"](https://cstack.github.io/db_tutorial/) tutorial.

## Features

- REPL with a `db > ` prompt
- Meta-commands (start with a dot): `.exit`
- Two SQL statements on one hard-coded table `users(id, username, email)`:
  - `insert <id> <username> <email>`
  - `select`
- In-memory only: rows live in pages (14 rows per page, up to 1400 rows) and are lost on exit

## Example

```
db > insert 1 cstack foo@bar.com
Executed.
db > insert 2 bob bob@example.com
Executed.
db > select
(1, cstack, foo@bar.com)
(2, bob, bob@example.com)
Executed.
db > insert foo bar 1
Syntax error. Could not parse statement.
db > delete foo
Unrecognized keyword at start of 'delete foo'.
db > .tables
Unrecognized command '.tables'
db > .exit
```

## How it works

1. **REPL** (`main`) reads a line into an `InputBuffer`.
2. Lines starting with `.` go to `do_meta_command`.
3. Other lines go to `prepare_statement` (the "SQL compiler"), which fills in a `Statement`.
4. `execute_statement` (the "virtual machine") runs it against the `Table`.

## Everyday commands

| Command | What it does |
|---|---|
| `turf run` | build and run `src/main.tr` |
| `turf build` | build without running; the program is `build/sqlite` |
| `turf check` | report every error and warning, without building |
| `turf fmt --write src/main.tr` | format a file in place |
| `turf clean` | delete `build/` |
| `turf explain E090` | explain an error code |
| `turf help` | every command |

## Layout

- `turf.toml`: the package's name, version and dependencies
- `turf.lock`: pins every dependency; written by the first build, commit it
- `src/main.tr`: the whole database (REPL, parser, table)
- `build/`: build output, ignored by git
