# briantist/ezenv
GitHub Action for easily setting persistent environment variables. Each variable is defined in order so variables can reference previous vars (to build paths for example). The assignments are done in `bash` so [shell parameter expansion](https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion.html) can be used.

## Inputs
### Required

- **env**: An (optionally) multi-line string containing environment variable definitions in the form `NAME=value`.

## Examples

### Simple values
```yml
- uses: briantist/ezenv@v1
  with:
    env: |
      SOME_FLAG=1
      THIS_GREETING=hello
      WITH_SPACES="a value with spaces"
```

### Referencing
```yml
- run: echo "ONE=one" >> "$GITHUB_ENV"

- uses: briantist/ezenv@v1
  with:
    env: |
      TWO=two
      ONETWOTHREE="$ONE $TWO three"
```

### Shell Expansion
```yml
- uses: briantist/ezenv@v1
  with:
    env: |
      THAT_VALUE="${THIS_GREETING:-hi} ${LOCATION:-world}"
      ABS_SUBDIR="$(pwd)/test"
```
