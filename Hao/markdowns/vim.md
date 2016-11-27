# Vim

****

I've been using vim for a long time but keep staying at the entry level. The best way to master a skill for me is to write it down. Of course, other ways like teaching may be even better. However, it may not be a choice for me now. Thus now I start to show my summary about how to use vim. Below is my configuration of .vimrc which allows me to change the interface of vim.



```

" Configuration file for vim
set modelines=0         " CVE-2007-2438

" Normally we use vim-extensions. If you want true vi-compatibility
" remove change the following statements
set nocompatible        " Use Vim defaults instead of 100% vi compatibility
set backspace=2         " more powerful backspacing

" -> lines from this quote to next quote are added to the original file by me   

set nu                  " set line number 
set ai                  " auto indenting
set history=100         " keep 100 lines of history
set ruler               " show the cursor position
syntax on               " syntax highlighting
set hlsearch            " highlight the last searched term
filetype plugin on      " use the file type plugins

" When editing a file, always jump to the last cursor position
autocmd BufReadPost *
\ if ! exists("g:leave_my_cursor_position_alone") |
\ if line("'\"") > 0 && line ("'\"") <= line("$") |
\ exe "normal g'\"" |
\ endif |
\ endif

" -> till this quote

" Don't write backup file if vim is being called by "crontab -e"
au BufWrite /private/tmp/crontab.* set nowritebackup
" Don't write backup file if vim is being called by "chpass"
au BufWrite /private/etc/pw.* set nowritebackup

```

****

After adding new options, now the vim works with showing line numbers, syntax highlighting and so on. I got this first from this [blog](http://geekology.co.za/article/2009/03/how-to-enable-syntax-highlighting-and-other-options-in-vim) and then checked with official vim documents.

After introduing how to set some basic options in .vimrc, going through vim commands should be the next step. However, there are already too many documents about how to use vim. Thus, I just attached the best I found blow. **Read it, check it, google it.**

> [English](http://yannesposito.com/Scratch/en/blog/Learn-Vim-Progressively/)
> 
> [Chinese](http://blogread.cn/it/article/4542?f=wb) [CoolShell](http://coolshell.cn/articles/5426.html)

Enjoy it!

Below I modified the *Learn Vim Progressively* a little to make it a reference for myself.

## 1st Level

> * `i` → *Insert* mode. Type `ESC` to return to Normal mode.
> * `x` → Delete the char under the cursor
> * `:wq` → Save and Quit (`:w` save, `:q` quit)
> * `dd` → Delete (and copy) the current line
> * `p` → Paste
> 
> Recommended:
> 
> * `hjkl` (highly recommended but not mandatory) → basic cursor move (←↓↑→). Hint: `j` looks like a down arrow.
> * `:help <command>` → Show help about `<command>`. You can use `:help` without a `<command>` to get general help.

## 2nd Level

1. Insert mode variations:

    > * `a` → insert after the cursor
    > * `o` → insert a new line after the current one
    > * `O` → insert a new line before the current one
    > * `cw` → replace from the cursor to the end of the word

2. Basic moves

    > * `0` → go to the first column
    > * `^` → go to the first non-blank character of the line
    > * ` * `g_` → go to the last non-blank character of line
    > * `/pattern` → search for `pattern`

3. Copy/Paste

    > * `P` → paste before, remember `p` is paste after current position.
    > * `yy` → copy the current line, easier but equivalent to `ddP`

4. Undo/Redo

    > * `u` → undo
    > * `<C-r>` → redo

5. Load/Save/Quit/Change File (Buffer)

    > * `:e <path/to/file>` → open
    > * `:w` → save
    > * `:saveas <path/to/file>` → save to `<path/to/file>`
    > * `:x`, `ZZ` or `:wq` → save and quit (`:x` only save if necessary)
    > * `:q!` → quit without saving, also: `:qa!` to quit even if there are modified hidden buffers.
    > * `:bn` (resp. `:bp`) → show next (resp. previous) file (buffer)

## 3rd Level

### Better

Let's look at how vim could help you to repeat yourself:

1. `.` → (dot) will repeat the last command,
2. N → will repeat the command N times.

Some examples, open a file and type:

> * `2dd` → will delete 2 lines
> * `3p` → will paste the text 3 times
> * `100idesu [ESC]` → will write "desu" 100 times
> * `.` → Just after the last command will write again the 100 "desu ".
> * `3.` → Will write 3 "desu" (and not 300, how clever).

### Stronger

Knowing how to move efficiently with vim is *very* important.

1. N`G` → Go to line N
2. `gg` → shortcut for `1G` - go to the start of the file
3. `G` → Go to last line
4. Word moves:

    > 1. `w` → go to the start of the following word,
    > 2. `e` → go to the end of this word.
    > 3. `W` → go to the start of the following WORD,
    > 4. `E` → go to the end of this WORD.

Now let's talk about very efficient moves:

> * `%` : Go to the corresponding `(`, `{`, `[`.
> * `*` (resp. `#`) : go to next (resp. previous) occurrence of the word under the cursor

### Faster

Remember about the importance of vi moves? Here is the reason. Most commands can be used using the following general format:

`<start position><command><end position>`

For example : `0y * `0` → go to column 0
> * `^` → go to first character on the line
> * ` * `g_` → go to the last character on the line
> * `fa` → go to next occurrence of the letter `a` on the line. `,` (resp. `;`) will find the next (resp. previous) occurrence.
> * `t,` → go to just before the character `,`.
> * `3fa` → find the 3rd occurrence of `a` on this line.
> * `F` and `T` → like `f` and `t` but backward.

A useful tip is: `dt"` → remove everything until the `"`.

### Zone selection `<action>a<object>` or `<action>i<object>`

These command can only be used after an operator in visual mode. But they are very powerful. Their main pattern is:

`<action>a<object>` and `<action>i<object>`

Where action can be any action, for example, `d` (delete), `y` (yank), `v` (select in visual mode). The object can be: `w` a word, `W` a WORD (extended word), `s` a sentence, `p` a paragraph. But also, natural character such as `"`, `'`, `)`, `}`, `]`.

Suppose the cursor is on the first `o` of `(map (+) ("foo"))`.

> * `vi"` → will select `foo`.
> * `va"` → will select `"foo"`.
> * `vi)` → will select `"foo"`.
> * `va)` → will select `("foo")`.
> * `v2i)` → will select `map (+) ("foo")`
> * `v2a)` → will select `(map (+) ("foo"))`

### Select rectangular blocks: `<C-v>`.

Rectangular blocks are very useful for commenting many lines of code. Typically: `0<C-v><C-d>I-- [ESC]`

* `^` → go to the first non-blank character of the line
* `<C-v>` → Start block selection
* `<C-d>` → move down (could also be `jjj` or `%`, etc...)
* `I-- [ESC]` → write `--` to comment each line

Note: in Windows you might have to use `<C-q>` instead of `<C-v>` if your clipboard is not empty.

### Completion: `<C-n>` and `<C-p>`.

In Insert mode, just type the start of a word, then type `<C-p>`, magic...

### Macros : `qa` do something `q`, `@a`, `@@`

`qa` record your actions in the *register* `a`. Then `@a` will replay the macro saved into the register `a` as if you typed it. `@@` is a shortcut to replay the last executed macro.

> *Example*
> 
> On a line containing only the number 1, type this:
> 
> * `qaYp<C-a>q` →
>     
>     
>     * `qa` start recording.
>     * `Yp` duplicate this line.
>     * `<C-a>` increment the number.
>     * `q` stop recording.
> * `@a` → write 2 under the 1
>     
>     
> * `@@` → write 3 under the 2
>     
>     
> * Now do `100@@` will create a list of increasing numbers until 103.

### Visual selection: `v`,`V`,`<C-v>`

We saw an example with `<C-v>`. There is also `v` and `V`. Once the selection has been made, you can:

* `J` → join all the lines together.
* `<` (resp. `>`) → indent to the left (resp. to the right).
* `=` → auto indent

blogimage("autoindent.gif","Autoindent")

Add something at the end of all visually selected lines:

* `<C-v>`
* go to desired line (`jjj` or `<C-d>` or `/pattern` or `%` etc...)
* ` * `:split` → create a split (`:vsplit` create a vertical split)
> * `<C-w><dir>` : where dir is any of `hjkl` or ←↓↑→ to change the split.
> * `<C-w>_` (resp. `<C-w>|`) : maximise the size of the split (resp. vertical split)
> * `<C-w>+` (resp. `<C-w>-`) : Grow (resp. shrink) split



