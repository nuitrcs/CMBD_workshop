# The Very Basics

### Different Modes in Vim

One of the most important concepts in Vim is modes. This is the major
difference between Vim and other text editors like Notepad in Windows
and gedit in Linux. Here is a short overview of each mode available
in vim:

- Normal mode: For navigation and manipulation of text. This is the
default mode when you start Vim. Press `ESC` to exit back to normal
mode from other modes.
- Insert mode: For inserting new text. Insert mode can be reached in
several ways, e.g., pressing `i` when in normal mode.
- Command-line mode: For entering editor commands, such as help, search,
 save, quit. Press `:` when in normal mode to enter command-line mode.
- Visual mode: For navigation and manipulation of text selections.
This mode allows you to perform most normal mode commands, and a few extra
others, on selected (i.e. highlighted) text. Press `v` when in normal
mode to enter visual mode.

**Example I:** Navigation in Vim with `h, j, k, l` or arrow keys.

In Vim normal mode, commands `h`, `j`, `k`, `l` are used to move cursor
left, down, up or right. Arrow keys can also be used for the same purpose.

- Open *introduction.txt* using vim from the terminal
```bash
vim introduction.txt
```
- Make sure you are in normal mode by hitting `ESC`.
- Press `h`, `j`, `k`, `l` or arrows to move your cursor around until
you feel comfortable with that.

\
**Example II:** Insert text in Line 2 of *introduction.txt*.

- Open *introduction.txt* and make sure you are in normal mode by
hitting `ESC`.
- Navigate to Line 2 (empty) with movement or arrow keys.
- Press `i`, and you should notice the bottom left shows "-- INSERT --",
which indicates you have switched to insert mode. Now you can type new
text as you like.
- Exit back to normal mode by hitting `ESC`. Leave it open for next
example.

\
**Example III:** Quit with/without saving in Vim

- In the opened *introduction.txt*, type `:q!` and hit `ENTER/RETURN` to exit
WITHOUT saving the changes.
- Reopen *introduction.txt*, insert some text with command `i`.
Type `:wq` and hit `ENTER/RETURN` to exit WITH saving the changes. `w`
is short for "write" and `q` is short for "quit".
- There are two other save and quit methods while a file is open: (i) When in
normal mode type `ZZ` (i.e. `SHIFT+z+z`). (ii) Type `:` to switch to
command-line mode from normal mode then type `x` and hit `ENTER/RETURN`.

**Example IV:** Save as another file

- Reopen *introduction.txt*, insert some text with command `i`. Type
`:w introduction_bckp.txt` and hit `ENTER/RETURN`.
- The change you have made has been saved as *introduction_bckp.txt*
but you continue to edit *introduction.txt*
- Quit *introduction.txt* without saving by typing `:q!` and hitting
`ENTER/RETURN`
- Investigate both *introduction.txt* and *introduction_bckp.txt* using
VIM

--------------

# More on Text Editing

Let's discuss about Vim text edit techniques in details. For these
exercises we will use *editing.txt*.

### 1. Deletion Command

Command `x` is used to delete the character under the cursor.

**Example I:** Correct the text lines marked by -->.

- Open *editing.txt* and navigate to Example I. Make sure you are in
normal mode by hitting `ESC`.
- Move your cursor to the character you want to delete, hit `x`
- Repeat until all lines marked by --> are corrected.

A **count** can be inserted before the motion to delete more. E.g., `2x`
is used to delete two characters at one time.

Command `d` is also for deletion. It can be combined with a motion
command. E.g. `dw` is used to delete a word, and `d$` is used to delete
to the end of the line.

\
**Example II:** Correct the text lines marked by -->.

- Open *editing.txt* and navigate to Example II. Make sure you are in
normal mode by hitting `ESC`.
- Move your cursor to the beginning of the word you want to delete,
hit `dw`.
- Repeat until all lines marked by --> are corrected.

\
**Example III:** Delete all UPPERCASE words marked by -->.

- Open *editing.txt* and navigate to Example III. Make sure you are in
normal mode by hitting `ESC`.
- Move your the first "MEOW", hit `d3w` to delete "MEOW MEOW MEOW".
- Repeat until all lines marked by --> are corrected.

In addition to those mentioned above, command `dd` can be used to delete
a whole line. Note here to delete multiple lines with count, use `3dd`,
rather than `d3d`.

\
**Example IV:** Delete all lines marked by -->

- Open *editing.txt* and navigate to Example IV. Make sure you are in
normal mode by hitting `ESC`.
- Move your the cursor to anywhere of a line marked by -->, and hit `dd`
- Repeat until all lines marked by --> are deleted. You can also try
use `3dd` to delete three lines together.

### 2. Undo Command

To undo your last command, use command `u`.

**Example V:** Correct the text lines marked by -->, then undo the
correction.

- Open *editing.txt* and navigate to Example V. Make sure you are in
normal mode by hitting `ESC`.
- Use command `x` to correct the line marked by -->.
- Now hit `u`, it will undo your last deletion. Hit `u` again, it will
redo your second last deletion.

### 3. Put Command

The text deleted last time is stored and can be put back with command
`p`. This works just like cut & paste in other editors like notepad.

**Example VI:** Correct the text lines marked by -->.

- Open *editing.txt* and navigate to Example VI. Make sure you are in
normal mode by hitting `ESC`.
- Move your the cursor to the beginning of word "some", and hit `dw`.
- Move your the cursor to the space after "are", and hit `p`. You
should have moved word some to the correct position.
- Repeat until all lines marked by --> are corrected.

### 4. Replace Command

Command `r` is to replace one character at the cursor with new character
you input. The command capital `R` is used to replace more than one
character.

**Example VII:** Correct the text lines marked by -->.

- Open *editing.txt* and navigate to Example VII. Make sure you are in
normal mode by hitting `ESC`.
- Move the cursor to the character "u" in word "sume", and hit
`ro`. You should have corrected character "u" by "o". It also
automatically switches back to normal mode.
- Move your the cursor to the character "q" in word "misqhdsi", and hit
`Rtakes`. You should have corrected the word "misqhdsi" by "mistakes". Hit
`ESC` to switch back to normal mode.

### 5. Copying

Command `y` is used for yanking (copying). It can be used in combination
with motion like `yw` (copy single word) and `y3w` (copy 3 words)
You can also use `yy` to copy an entire line. Copied text can be pasted
with command `p`.

**Example VIII:** Complete the text line marked by -->.

- Open *editing.txt* and navigate to Example VIII. Make sure you are in
normal mode by hitting `ESC`.
- Move your the cursor to the beginning of the word "are" in the first sentence.
- Hit `y6w` to copy the following six words
- Navigate to the position you want to paste in the second sentence and
hit `p`.


--------------

# More on Navigation and Search
Let's discuss some fast navigation techniques between lines and pattern
search methods in Vim. For these exercises we will use *animals.txt*.

#### 1. Moving to Start and End of the File

**Example I:** Move to start/end of the file in normal mode
- Switch to normal mode by hitting `ESC`. Type `G` (i.e. SHIFT+g) to move
to the last line of the file
- Switch to normal mode by hitting `ESC`. Type `gg` to move to the first
line of the file

\
**Example II:** Move to start/end of the file in command-line mode
- Switch to command-line mode by hitting `ESC` and then typing `:`. Type
`$` and hit `ENTER/RETURN` to move to the last line of the file
- Hit `ESC` then type `:` to switch to command-line mode. Type `0` and hit
`ENTER/RETURN` to move to the beginning of the file

#### 2. Moving to an Arbitrary Line

**Example III:** Move to a line using the line number in normal mode
- Hit `ESC`, type the number of the line, say 14, and then type `G` (i.e.
`SHIFT+g`)

\
**Example IV:** Move to a line using the line number in command-line mode
- Hit `ESC`, type `:`, then type the number of the line, say 23, hit
`ENTER/RETURN`

\
**Example V:** Let's make sure we moved to 23<sup>rd</sup> line by showing
the line numbers before each line.
- Hit `ESC`, type `:set nu` (or equally `:set number`), hit `ENTER/RETURN`
- Type `:set nonu` (or equally `:set nonumber`) and hit `ENTER/RETURN` to
hide the line numbers

#### 3. Pattern Search
Another strong suite of Vim lies in its pattern search functionality. It
is possible to search for single pattern, multiple patterns,
whole words, patterns that are in specific order, duplicate words etc.

**Example VI:** Find the first *bear* pattern in *animals.txt* file
from the normal mode.
- Hit `ESC` to switch to normal mode then type `/bear` and hit `ENTER/RETURN`

Forward slash, `/`, is used to search the trailing pattern, in this case
"bear". Consequently, `/bear` will find the first matching pattern after
the cursor's current location and move the cursor to the beginning of
the pattern.

\
**Example VII:** Find the next *bear* pattern in *animals.txt*
file from the normal mode.
- Hit `ESC` to switch to normal mode then hit `n`

Each time you hit `n` the next matching pattern will be found and the
cursor will move to that location.

\
**Example VIII:** Find the previous *bear* pattern in *animals.txt*
file from the normal mode.
- Hit `ESC` to switch to normal mode then hit `N` (i.e. `SHIFT+n`)

Each time you hit `N` the previous matching pattern will be found and
the cursor will move to that location.

#### 5. Text Substitution
Many modern document and text editors provide functionality for finding
and replacing strings. Vim is no exception and it offers many additional
features.

The substitute operation can be done in command-line mode using `s` (short
for substitute). The general format of a substitute is `:s/foo/bar` where
*foo* is the pattern to be substituted by *bar*.

\
**Example IX:** Replace the first instance of "rabbit" with "squirrel"
in the 2<sup>nd</sup> line of *animals.txt* using substitute. Save and exit.
- First let's create a backup file i.e. *animals_bckp.txt*
for *animals.txt*, then open *animals.txt* using vim from the terminal.
```bash
cp animals.txt animals_bckp.txt
vim animals.txt
```
- Hit `ESC` and go to command-line mode with typing ":"
- Type `2` to go to the second line
- Type `:` to start the command-line mode and write `s/rabbit/squirrel`
and hit `ENTER/RETURN`
- Type `:` to start the command-line then type `wq` and hit `ENTER/RETURN`

\
**Example X:** Replace the first instance of "rabbit" with "squirrel"
in all the lines of *animals.txt* using substitute. Save and exit.

- Open *animals.txt* using vim from the terminal
```bash
vim animals.txt
```
- Hit `ESC` and type `:` go to command-line mode
- Write `%s/rabbit/squirrel/` and hit `ENTER/RETURN`
- Type `:` to start the command-line then type `x` and hit `ENTER/RETURN`

`%` indicates that whole buffer (practically whole document) will be
considered for substitution.

\
**Example XI:** Replace all instances of "fox" with "wolf"
in all the lines of *animals.txt* using substitute. Save and exit.

- Open *animals.txt* using vim from the terminal
```bash
vim animals.txt
```
- Hit `ESC` and type `:` go to command-line mode
- Write `%s/fox/wolf/g` and hit `ENTER/RETURN`
- Hit `ESC` to switch to normal mode and `ZZ`

Here `g` is short for global and it is used to replace all instances of
the pattern in a line.

--------------

# Split Windows for Opening Multiple Files
It is possible to open multiple files spreading horizontally or
vertically in a single window. This can be achieved while you are starting
the user interface (UI) or from within the UI.

**Example I:** Open the two files *animals.txt* and *editing.txt* in a
split windows oriented vertically, switch between panes and then quit
all without saving.
- Issue the following command on your terminal:

```bash
vim -O animals.txt editing.txt
```

- Once the split windows are opened, switch to normal mode by hitting
`ESC`
- While holding `CTRL` hit `w` twice (i.e. `CTRL+w+w`) which will move the
cursor to the next pane
- Type `qall!` and hit `ENTER/RETURN`

**Example II** Open the *animals.txt* first then open *editing.txt* by
splitting the window vertically from the user interface. Switch between
panes and then quit all without saving.
- Issue the following command on your terminal
```bash
vim animals.txt
```
- Switch to command-line mode by typing `:`
- Type `vsplit editing.txt`
- Switch to normal mode by hitting `ESC`
- While holding CTRL hit `w` twice (i.e. `CTRL+w+w`) which will move the
cursor to the next pane
- Type `:qall!` to quit all windows


--------------

# Need More Help?
Any moment during your Vim session hit `ESC`, type `:help` and hit `ENTER/RETURN`.
To quit from help page type `:q!`.

You can also specify the help topic by identifying the command that you
want to learn. During your Vim session, hit `ESC`, type `:help :<command>`
and hit `ENTER/RETURN`. For instance, if you would like to see more
information about `substitute` you should write `:help :s` and hit
`ENTER/RETURN`.

--------------

# Additional Resources

Cheat sheets:

1. [Vim Cheat Sheet](https://vim.rtorr.com/)
2. [Graphical Cheat Sheet](http://www.viemu.com/vi-vim-cheat-sheet.gif)
3. [A Great Vim Cheat Sheet](http://vimsheet.com/)
4. [Advanced Vim Cheat Sheet](http://vimsheet.com/advanced.html)

Interactive Online Learning:

1. [VIM Adventures](https://vim-adventures.com/)
2. [Interactive Vim tutorial](http://www.openvim.com/)

--------------

# VIM Text Editor Exercises

**IV.01)** Open "ilikemyname.txt" using VIM editor.
<details><summary>Click me</summary>
<p>

#### Answer
```bash
vim ilikemyname.txt
```
</p>
</details>

**IV.02)** While you are viewing the file, set VIM to
show line numbers.
<details><summary>Click me</summary>
<p>

#### Answer
```bash
#-- Go to the command-line mode (hit "esc" then ":") and write set nu, hit enter/return
```
</p>
</details>

**IV.03)** Delete 783219th line.
<details><summary>Click me</summary>
<p>

#### Answer
```bash
#-- Go to the command-line mode (hit "esc" then ":")
#1- write 783219 and hit enter/return OR write ?783219 and hit enter/return.
#2- Hit d two times when the cursor is on line 783219
```
</p>
</details>

**IV.04)** Undo your deletion.
<details><summary>Click me</summary>
<p>

#### Answer
```bash
#-- Hit "esc" to go to the normal mode and hit "u"
```
</p>
</details>

**IV.05)** Only erase the number before YourName on line 783219.
<details><summary>Click me</summary>
<p>

#### Answer
```bash
#-- Two possible option to accomp:

#1- Hit "esc" to switch to the normal mode, move the cursor to the beginning of the
#number and hit "x" 6 times to erase the number on that line one character at a time

#or

#1- Hit "esc" and "6" and then "x" to erase 6 characters. There are several more ways.
```
</p>
</details>

**IV.06)** Go to the last line of the file and enter the text "Last"
before YourName. Then go to the first line of the file and enter the
text "First" after YourName.
<details><summary>Click me</summary>
<p>

#### Answer
```bash
#-- Follow the steps below

#1- Hit "esc" and ":" to go to the command-line mode
#2- Write "$", hit enter/return
#3- Hit "i" to enter insert mode and type "Last" before YourName
#4- Hit "esc" and ":" to go to the command-line mode
#5- Write "0", hit enter/return
#6- Hit "i" to enter insert mode, move the cursor after YourName and type "First"
```
</p>
</details>

**IV.07)** Save the file as *ilikemyname_bkcp.txt*
<details><summary>Click me</summary>
<p>

#### Answer
```bash
#1- Hit "esc" and type ":w ilikemyname_bkcp.txt"
```
</p>
</details>

**IV.08)** Replace all YourName pattern with your first name. Save the file
and quit.
<details><summary>Click me</summary>
<p>

#### Answer
```bash
#1- Hit `ESC` and type `:` go to command-line mode
#2- Write `%s/YourName/yourfirstname/` and hit `ENTER/RETURN`
```
</p>
</details>

**IV.09)** Save the file and quit.
<details><summary>Click me</summary>
<p>

#### Answer
```bash
#1- Type `:` to start the command-line then type `x` and hit `ENTER/RETURN`
```
</p>
</details>

**IV.10)** Compare *ilikemyname.txt* and *ilikemyname_bckp.txt* side by
side in one VIM window

<details><summary>Click me</summary>
<p>

#### Answer
```bash
vim -O ilikemyname.txt ilikemyname_bckp.txt
```
</p>
</details>

**IV.11)** Exit from VIM without saving files
<details><summary>Click me</summary>
<p>

#### Answer

```bash
#1- Type `:qall` and hit `ENTER/RETURN` to close both files and quit VIM
```
</p>
</details>
