# journal

A todo.txt-style plain-text journal, grouped by project.

Entries are dated bullets, newest on top. Projects are sections headed
`YYYY-MM-DD Display Name +alias`; the `+alias` is the key you type. Entries
without an alias collect in an unassigned blob at the top of the file.

## Install

```sh
cp journal ~/bin/journal   # or anywhere on your $PATH
chmod +x ~/bin/journal
```

The journal lives at `~/journal.txt`, or `$JOURNAL_FILE` if set.

## Usage

```sh
journal add some entry text                    # add an unassigned entry
journal add '+alias=Display Name' some text    # create/name a project, add an entry
journal add +alias some entry text             # add an entry to a project
journal add '+alias=New Name'                   # rename a project (no entry text)
journal ls                                      # show the whole journal
journal ls +alias                               # show one project
journal ls @context                             # entries tagged @context, grouped
journal ls landing page                         # entries containing "landing page"
journal -h                                      # help
```

`a` aliases `add`, `list` aliases `ls`. Quote any argument containing spaces.
Entry text may carry `@context` tags todo.txt-style.

## Example

```
$ journal add '+web=Website Redesign' ship the new landing page
$ journal add +web fix @bug in nav
$ journal add grab milk

$ journal ls
- 2026-07-05 grab milk

2026-07-05 Website Redesign +web
- 2026-07-05 fix @bug in nav
- 2026-07-05 ship the new landing page
```
