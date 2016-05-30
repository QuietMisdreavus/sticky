# sticky

Tiny shell scripts to show tiny text notes-to-self

This was written to fulfill a very specific need: make a way to display quick notes without
polluting my monitor and stand with sticky notes. Throwing these notes in text files like this also
allows me to easily swap out lines when certain reminders are no longer necessary. I personally
wanted this for learning keyboard shortcuts for various programs like vim or spectrwm. But things
like terminal commands or other reminders could also be useful here.

The scripts will store notes as text files in the folder `$XDG_DATA_HOME/sticky`
(`$HOME/.local/share/sticky` if `$XDG_DATA_HOME` isn't set) and call the program defined in
`$VISUAL` or `$EDITOR` to edit them. (They'll call `nano` in the absence of either of those
variables.)

## Basic Usage

* Call `sticky` by itself to show a list of notes.
* Call `sticky` with the name of a note to display the contents of that note.
* Call `visticky` with the name of a note to edit a note.
* Clearing a note with `visticky` (i.e. leaving it empty) will delete the note.

## Installation

Essentially, all you'll need to do is just copy/symlink the scripts to somewhere in your `$PATH`. I
personally use a `~/bin` folder as a personal scripts folder, so the following will work:

```sh
ln -s ./sticky ./visticky ~/bin
```

If, like me, you use bash as your shell and you'd like to have the list of available notes as a
tab-completion for these scripts, you can copy the following into your `.bashrc` or similar:

```bash
_sticky() {
	local arg;
	arg=${COMP_WORDS[$COMP_CWORD]}
	COMPREPLY=( $(compgen -W "$(ls ${XDG_DATA_HOME:-$HOME/.local/share}/sticky)" -- $arg) )
}
complete -F _sticky sticky visticky
```
