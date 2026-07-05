# journal.txt

A todo.txt-style plain-text journal, grouped by project.

## Install

```sh
cp journal ~/bin/journal
chmod +x ~/bin/journal
```

## Usage

```sh
journal a[dd] some entry text         # add an unassigned entry
journal a[dd] +alias some entry text  # add an entry to a project
journal a[dd] '+alias=Display Name'   # name a project
journal ls                            # show the whole journal
journal ls +alias                     # show one project
journal ls @context                   # entries tagged @context, grouped
journal ls darude sandstorm           # entries containing "darude sandstorm"
journal import [done.txt]             # import completed todo.txt tasks
journal e[dit]                        # open the journal in $EDITOR
journal -h                            # help
```

`ls` and `list` are synonyms. Quote any argument containing spaces. Entry text
may carry `@context` tags todo.txt-style.

`ls` colorizes when writing to a terminal and prints plain when piped or
redirected.

## Importing from todo.txt

`journal import` reads a todo.txt `done.txt` and files each completed task into
the journal. A done line `x <completed> [<created>] [+project] text` becomes a
bullet dated by its **completion** date, filed under its `+project` (or the top
blob), with the creation date kept as a `created:<date>` tag:

```
x 2026-07-02 2026-06-22 +1T ship the thing
  ->  under +1T:  - 2026-07-02 ship the thing created:2026-06-22
```

The source defaults to `$DONE_FILE`, then `~/done.txt`, and is **left
untouched**. Imported lines are logged to `<journal>.imported`, so re-running
only picks up newly completed tasks.

## Config

`~/.journal.txt.cfg` (or `$JOURNAL_CONFIG`) is plain shell. Defaults:

```sh
JOURNAL_FILE="$HOME/journal.txt"
DONE_FILE="$HOME/done.txt"
JOURNAL_PLAIN=      # set to 1 to disable color
C_HEAD=$'\033[1m'   # heading   (bold)
C_DATE=$'\033[34m'  # date      (blue)
C_PROJ=$'\033[32m'  # +project  (green)
C_CTX=$'\033[33m'   # @context  (yellow)
C_META=$'\033[2m'   # key:value (dim)
C_RESET=$'\033[0m'
```
