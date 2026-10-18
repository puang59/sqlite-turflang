# sqlite

A TurfLang package, created with `turf new`.

## Everyday commands

| Command | What it does |
|---|---|
| `turf run` | build and run `src/main.tr` |
| `turf build` | build without running; the program is `build/sqlite` |
| `turf check` | report every error and warning, without building |
| `turf add <dep> --path ../<dep>` | depend on a package on disk |
| `turf add <dep> --git <url> --tag <tag>` | depend on a package in a git repository |
| `turf remove <dep>` | stop depending on it |
| `turf update` | move git dependencies to the newest commit their tag or branch names |
| `turf clean` | delete `build/` |
| `turf fmt --write src/main.tr` | format a file in place |
| `turf explain E090` | explain an error code |
| `turf help` | every command |

## Layout

- `turf.toml`: the package's name, version and dependencies
- `turf.lock`: pins every dependency; written by the first build, commit it
- `src/main.tr`: the entry point, what `turf run` runs
- `build/`: build output, ignored by git
