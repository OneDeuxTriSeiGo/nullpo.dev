# Vim Tutorial: Command Composition <!--- Name in progress -->

<!---
Guide Starts with installing a plugin manager.
Provide useful plugins
explain text objects
-->

Vim is an extraordinarily powerful text editor despite its famously difficult
learning curve. Once you have an understanding of navigation, editing, and basic
regular expressions however, the editor begins to feel more natural and you can
perform many tasks with ease. To get the most out of Vim however, one must
master the concept of command composition. Once a user has mastered these
features they become capable of performing almost any task with the minimal amount
of motion necessary.

## Configuration and Plugins

Before beginning, the examples in this tutorial will use the plugins and options
below. These features are extraordinarily useful and are enabled in many
proficient Vim users .vimrc files in one variation or another. To install these
plugins, use a plugin manager such as
[Plug](https://github.com/junegunn/vim-plug),
[Pathogen](https://github.com/tpope/vim-pathogen), or
[Vundle](https://github.com/VundleVim/Vundle.vim).

### Enabled Options

```
" Show Line Numbers on the side 
set number 

" Show last command keystroke in the bottom right of the statusline.
set showcmd

" Highlight successful search matches
set hlsearch

" Update search matches as you type
set incsearch

" Bind a single spacebar keystroke to clear search highlighting in normal mode 
nnoremap <silent> <Space> :nohlsearch<Bar>:echo<CR>
```

### Plugins
- [christoomey/vim-sort-motion](https://github.com/christoomey/vim-sort-motion)
- [christoomey/vim-titlecase](https://github.com/christoomey/vim-titlecase)
- [tpope/vim-commentary](https://github.com/tpope/vim-commentary)
- [tpope/vim-repeat](https://github.com/tpope/vim-repeat)
- [tpope/vim-surround](https://github.com/tpope/vim-surround)


## Command Composition

In many text editors and IDEs, actions are discrete steps that are performed as
necessary by the user. Each action is well-defined and performs exactly one task
on the selected text. As a holdover from their experience with other editors,
many Vim users will attempt to manipulate text in this series of well-defined
steps (Select the text with visual mode and perform one action). This works well
for basic tasks however it becomes tedious for many complex ones. For these
tasks users will often either spend the time performing this tedious process or
they will abandon the text editor all together and spend time building scripts
to perform these specific tasks instead.

Much like how Vim uses the modal style instead of the traditional emacs style,
actions in Vim break away from traditional editing paradigms. In Vim, actions
are closer to sentences than discrete commands. This style takes a while to get
used to however it changes the way you think about manipulating text and greatly
reduces the amount of effort required to make substantial changes.

Actions in Vim can be divided like a sentence into pieces akin to verbs, nouns,
adjectives, and adverbs. The verb element of an action is just called a verb.
The equivalent to the adverb in Vim is often just referred to as a modifier and
changes the type or number of repetitions of the verb. Nouns and adjectives
together make what are referred to in Vim as a text object. A noun by itself is
instead referred to as a motion. Where text objects define a block the cursor
is within, motions select everything between the cursor and the next object
defined by the specified "noun". For more information on the specific details,
refer to the Vim documentation on motions and text objects with 
`:help cursor-motions` or in the 
[online documentation](vimdoc.sourceforge.net/htmldoc/motion.html).

Similarly to how sentences can be composed into paragraphs, actions in vim can
be composed together to form more complex actions. These complex actions can
then be recorded to a register and replayed over a large set of text with little
to no effort.

## Examples

Reflowing a text block to the set column width can be done with `gqip`. `gq` is
the verb and `ip` is the text object. 

![reflowp](https://jacoblambda.github.io/jacoblambda/ENGL3764/reflowp.svg)

```
[gq] Reflow
[i] Inner (not effecting surrounding whitespace)
[p] Paragraph
```

---

Reflowing the following 3 paragraphs can be done with a motion like `3gq}` where
`3` is the adverb, `gq` is the verb, and `}` is the motion.

![reflow3p](https://jacoblambda.github.io/jacoblambda/ENGL3764/reflow3p.svg)

```
[3] For 3 Times
[gq] Reflow
[}] until next paragraph
```

---

This deletes the current word without affecting whitespace and enters insert
mode to provide replacement text.

![changew](https://jacoblambda.github.io/jacoblambda/ENGL3764/changew.svg)

```
[c] Change
[i] Inner
[w] Word
```

---

This swaps the case of the entire sentence to title case.

![titles](https://jacoblambda.github.io/jacoblambda/ENGL3764/titles.svg)

```
[gt] Swap to title case for
[i] Inner
[s] Sentence
```

---

This creates a comment block around a bracketed block using the comment style of
the current file's language. This is a very useful when quickly enabling and
disabling debugging code.

![commentout](https://jacoblambda.github.io/jacoblambda/ENGL3764/commentout.svg)

```
[gc] Comment around
[a] a (including the delimiters)
[}] bracketed scope
```

---

This one is a little more complex. `gg` is technically its own action however
as there is no 'entire file' text object, a motion to the top followed by an
action that acts until the end is often used. In this case the action is
reformatting the indentation. Similarly, `ggVG` will select the
entire file in a Visual block.

![tab](https://jacoblambda.github.io/jacoblambda/ENGL3764/tab.svg)

```
[g] Go to
[g] top of file and
[=] Reformat indentation
[G] until the end of the file
```


## Breaking Down A Complex Action (Paragraphs)

This command looks complex and impossible to memorise however very rarely will
anyone recite a specific action like this. This would instead form naturally
like a person describing the action. This command converts a list of vim-plug
plugin entries into a Markdown list of links to the Github pages of each plugin.
I selected this example to show that with practice Vim command composition
becomes like a second language as this was a command that I performed while
creating this tutorial.  Look at the demonstration below and then see how
similar the description is to the command above.

```
qaciw-<Esc>wcs']wyi]A(https://github.com/<Esc>pA)<Esc>j^q6@a
```

![plugins](https://jacoblambda.github.io/jacoblambda/ENGL3764/plugins.svg)

```
[q] Record actions to
[a] register a.
[c] Change the
[i] inner
[w] word
[-] to "-"
[Esc] and return to normal mode.
[w] Go to the start of the next word.
[c] Change
[s] surrounding
['] single quotes to
[]] brackets (without padding).
[w] Go to the start of the next word.
[y] Yank (copy) everything within
[i] inner
[]] brackets.
[A] Append (to the end of the line with insert mode)
[(https://github.com/] "(https://github.com/"
[Esc] and return to normal mode.
[j] Go down one line.
[^] Go to the start of the line.
[q] End recording.
[6] For 6 times,
[@] run the recording in
[a] register a.
```
Without the line by line it looks like this. 

Record actions to register a. Change the inner word to "-" and return to normal
mode. Go to the start of the next word. Change surrounding single quotes to brackets
(without padding). Go to the start of the next word. Yank (copy) everything within inner
brackets. Append (to the end of the line with insert mode) "(https://github.com/" 
and return to normal mode. Go down one line. Go to the start of the line. End 
recording. For 6 times, run the recording in register a.

## From Here

Now that you have some familiarity with composing basic commands in Vim, either
in your head or out loud describe the steps to perform whatever task you need
to complete and translate each sentence into actions. Much like learning a new
language, at first you will be reaching to find what words to use but as you
build your vocabulary the ease with which you can express your thoughts will
continue to develop. In cases where you feel stuck, reach for a 
[cheat sheet](http://www.viemu.com/vi-vim-cheat-sheet.gif) 
or take advantage of the `:help` command to find the command/word you 
are looking for.
