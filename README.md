# journal.txt

A todo.txt-style plain-text journal, grouped by project.

Entries are dated bullets, newest on top. Projects are sections headed
`YYYY-MM-DD Display Name +alias`; the `+alias` is the key you type. Entries
without an alias collect in an unassigned blob at the top of the file.

## Install

```sh
cp journal ~/bin/journal   # or anywhere on your $PATH
chmod +x ~/bin/journal
```

The journal lives at `$JOURNAL_FILE`, defaulting to `~/journal.txt` (here,
`/Volumes/workplace/github/journal.txt/journal.txt`).

## Usage

```sh
journal add some entry text                    	# add an unassigned entry
journal add +alias some entry text             	# add an entry to a project
journal add '+alias=Display Name' 	 	# name a project
journal ls                                     	# show the whole journal
journal ls +alias                              	# show one project
journal ls @context                            	# entries tagged @context, grouped
journal ls darude sandstorm			# entries containing "darude sandstorm"
journal import [done.txt]			# import completed todo.txt tasks
journal edit					# open the journal in $EDITOR
journal -h                                     	# help
```

`a` aliases `add`, `list` aliases `ls`, `e` aliases `edit`. Quote any argument
containing spaces. Entry text may carry `@context` tags todo.txt-style.

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
