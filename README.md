# journal.txt

A todo.txt-style plain-text journal, grouped by project.

## Install

Download into a directory on your `$PATH` and make it executable:

```sh
curl -fsSL https://raw.githubusercontent.com/mxschll/journal.txt/refs/heads/main/journal -o ~/bin/journal
chmod +x ~/bin/journal
```

## Usage

```sh
journal a[dd] some entry text         # add an unassigned entry
journal a[dd] +alias some entry text  # add an entry to a project
journal a[dd] '+alias=Display Name'   # name a project
journal n[ote] +alias '*Scope:* ...'  # add an undated note below the title
journal ls                            # show the whole journal
journal ls +alias                     # show one project
journal ls @context                   # entries tagged @context, grouped
journal ls darude sandstorm           # entries containing "darude sandstorm"
journal import [done.txt]             # import completed todo.txt tasks
journal e[dit]                        # open the journal in $EDITOR
journal -h                            # help
```

## Project notes

`journal note` adds an **undated** bullet to a project. These sit right below the
title and above the dated entries, so you can keep a short description or
structured summary at the top of a section:

```
2026-07-08 Test Improvements +TestImprovements
- *Scope:* CI reliability and cache correctness
- *Outcome:* flaky rate down, cache-busting shipped
- 2026-07-07 Merged [PR](https://.../pull/55)
- 2026-07-05 Merged [CR](https://.../CR-286541997) enabling Cloudfront caching
```

Notes stay pinned above the dated entries no matter when you add them, and new
notes stack below existing ones. It's just plain text, so you can also add or
edit them directly with `journal edit`.

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
JOURNAL_NO_LINKS=   # set to 1 to keep raw markdown links (no OSC 8 hyperlinks)
C_HEAD=$'\033[1m'   # heading   (bold)
C_DATE=$'\033[34m'  # date      (blue)
C_PROJ=$'\033[32m'  # +project  (green)
C_CTX=$'\033[33m'   # @context  (yellow)
C_META=$'\033[2m'   # key:value (dim)
C_LINK=$'\033[4m'   # link text (underline)
C_RESET=$'\033[0m'
```

On a terminal, `ls` renders `[text](url)` markdown links as clickable
[OSC 8 hyperlinks](https://gist.github.com/egmontkob/eb114294efbcd5adb1944c9f3cb5feda):
only the link text shows (underlined), the URL is hidden but still clickable.
Terminals without OSC 8 support show the text with no way to reach the URL; set
`JOURNAL_NO_LINKS=1` there to keep the raw markdown. The journal file itself
always stays plain todo.txt.

Inside tmux, add `set -ga terminal-features ",*:hyperlinks"` to `~/.tmux.conf` so
links are passed through to the outer terminal.
