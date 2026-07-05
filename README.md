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
journal add some entry text                    	# add an unassigned entry
journal add +alias some entry text             	# add an entry to a project
journal add '+alias=Display Name' 	 	# name a project
journal ls                                     	# show the whole journal
journal ls +alias                              	# show one project
journal ls @context                            	# entries tagged @context, grouped
journal ls darude sandstorm			# entries containing "darude sandstorm"
journal -h                                     	# help
```

`a` aliases `add`, `list` aliases `ls`. Quote any argument containing spaces.
Entry text may carry `@context` tags todo.txt-style.
