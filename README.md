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
journal                                        # show the whole journal
journal some entry text                        # add an unassigned entry
journal '+alias=Display Name' some entry text  # create/name a project, add an entry
journal +alias some entry text                 # add an entry to a project
journal '+alias=New Name'                       # rename a project
journal +alias                                  # show one project
journal @context                                # show entries tagged @context
journal -h                                      # help
```

Quote any argument containing spaces. Entry text may carry `@context` tags
todo.txt-style.

## Example

```
$ journal '+web=Website Redesign' ship the new landing page
$ journal +web fix @bug in nav
$ journal grab milk

$ journal
- 2026-07-05 grab milk

2026-07-05 Website Redesign +web
- 2026-07-05 fix @bug in nav
- 2026-07-05 ship the new landing page
```
