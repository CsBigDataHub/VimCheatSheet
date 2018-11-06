# Vim Cheatsheet
### Entering and leaving vi
- vi file edits existing or new file
- [Shift] + ZZ writes file and quits (or :wq[Return] )
- :q![Return] quits without saving changes (or [Shift] + ZQ)

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:black;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:black;}
.tg .tg-0pky{border-color:inherit;text-align:left;vertical-align:top}
</style>
<table class="tg">
  <tr>
    <th class="tg-0pky">Verbs</th>
    <th class="tg-0pky">d - delete <br>c - change <br>y - yank (copy) <br>v - visually select</th>
  </tr>
  <tr>
    <td class="tg-0pky">Modifiers</td>
    <td class="tg-0pky">i - inside<br>a - around<br>NUM - number (1,2,10)<br>t - searches for something and stops before it<br>f - searches for that thing and lands on it</td>
  </tr>
  <tr>
    <td class="tg-0pky">Nouns</td>
    <td class="tg-0pky">w - word<br>s - sentence<br>p - paragraph<br>t - tag (think HTML/XML)<br>b - block (think programming)</td>
  </tr>
</table>

### Buffer Management
```vim
:buffers "list open buffers
:ls "list open buffers
:list buffers "list open buffers
:b [TAB] "to cycle through buffers
:bp "previous buffer
:bn "next buffer
:bd "to delete contents in current buffer
:b<number> "number of buffer from ls
```

### File management

- need to be in normal mode
  
```vim
:w "Write without quitting 
:q "Quit without writing
:q! "Abandon changes 
:vi "Edit another file
:e "Edit another file
:n "Go to next file 
:N "Go to previous file
:rew "Rewind to first file
:r "Read file into this one
:-1r <file name> "Read file to line before
:e "to open a file
:e . " ls of the current directory
:e! " back to last saved
```

### Movement commands

- need to be in normal/command mode
  
```vim
w "forward a word
3w "to move forward 3 words, you use numeric prefix in almost all vi commands
b "back a word
e "forward to end of the current or next word
) "forward a sentance
( "backward a sentance
} "forward a paragraph
{ "backward a paragraph
^ "move the cursor to the beginning of a line
0(zero) "will move to beginning of the line
$ "move the cursor to the end of the line
:$ "end of the file
GA "end of thr file
3j6w "this will move 3 lines down and 6 words to left
- (minus) "goes to the beginning of the previous line
1G or gg(lower case) "i.e 1+shift+g # first line of the file
G "i.e shift+g # last line of the file
% " % All lines (same as 1,$)
ctrl+f " page down
ctrl+b "page up
'. "(single quote period i.e dot) to go to last change
```

### Scrolling
```shell
• [Control] + e   #Scroll down one line (“expose”)
• [Control] + y   #Scroll up one line
• [Control] + d   #Scroll down half a screen
• [Control] + u   #Scroll up half a screen
• [Control] + f   #Scroll down one screen (“forward”)
• [Control] + b   #Scroll up one screen (“back”)
```
### insert

- All of these commands enter insert mode
  
```vim
i "to insert text at the cursor
a "to append text 
I "to insert at the beginning of the line
A "to insert at the end of the line
o "to open a new line below the cursor
O "to open a new line above the cursor 
vi <filename> +<line number> " to start editor on a line - eg: vi test.txt +8 will open file test.txt on line 8
ctrl+p "auto complete option
```

### delete

- Can use dx, where x is any movement command
- Can use a number before any deletion command

```vim
x "deletes the current character at the cursor
dd "deletes current line
d2w "delete two words
dw "deletes current word, also deletes white space after the word
de "deletes the current word to end of the word with out deleting the white space after the word
d^ "deletes to beginning of line
d$ or D "deletes to end of line
d() "deletes current sentence 
```

 ### change text
```vim
r "changes the current character # r leaves in command mode
s "changes the current character # s leaves in command mode
cc "changes the current line, deletes the contents in current line and leaves you in insert mode
cw (also ce) "changes the current word and leaves you in insert mode
c^ "changes to beginning of line
c$ (also C) "changes to end of line
```

### replace mode
```vim
R "enters overwrite mode
~ "changes the case of the character at the cursor
J "joins the next line to the current line
```

### undo,redo and repeat
```vim
u "undo last changes
ctrl+r "redoes last change(undoes undo)
U "undoes all changes to current line
. "(dot or period)repeats last change
```

#copy and paste
```vim
dd "delete(cut) line
yy "yanks (copy) a line
yw "yanks a word
y( "yanks a sentance
p " put the text after cursor
P "or shift+p put the text before cursor
1vp "pasting over text
```

#Searching
```vim
/text "Searches forward for text
?text "Searches backward for text
n "repeats previous Search
N "repeats previous Search in opposite direction
```

#### wild card or meta character while searching
```vim
. "is a wild card # example '/a.c' matches 'abc' or 'axc'
\ "removes special meaning # '/a\.c' matches 'a.c' or '/a\\c' matches 'a\c' or '/a\/c' matches 'a/c'
^ , $ "match line start and end # '/^abc' matches lines beginning with 'abcd' or '/abc$' matches lines ending with 'abcd'
/a[xyz]c "matches 'axc' but does not match 'axyzc' #matches any single character in set
/a[a-z]c "matches 'abc'
/a[A-Z]c "matches 'aBc'
/a[^a-z]c " does not match 'abc'
* "is a repeat operator
/ab*c  "matches 'abc' or 'abbc' or 'abbbbc' or 'ac'
/\(ab\)*c "matches 'abababababc'
```

#### Search and replace
```vim
* "* on a word will give you next occurence of the word
?<word> "to search backwords
/\c{word} "search with out case sensitivity
:set ic "is shorthand for ignorecase
:set noic "is shorthand for ignorecase
:set ignorecase
:s/old/new/
:s/old/new/g "replace on current line
:%s/old/new/ "replace on every line first occurrence
:%s/old/new/g "global replace
:%s/the[ym]/(&)/g "this replaces every occurrence of they or them with (they) or (them)
:%s/\(they\) \(were\)/\2 \1/g "replaces every occurrence of they [space] were with were [space] they
:%s/[pattern]//gn "Count and highlight number of occurences in File
```

### indent , auto-indent, word wrap
```vim
>> "indent current line
<< "outdent current line
:se ai "enables auto-indent
:se noai "disables auto-indent
:se wm=8 "enables wrap margin, 8 is the length of the line which can be changed
:se wm=0 "disables wrap margin
```

### Filtering through shell commands
```vim
!! "filters current line through shell command
n!! "filters n lines
!% "filters to matching parentheses
!} "filters next paragraph 
!{ "filters previous paragraph
```
- Useful commands include fmt, tr, grep, sed, and awk
- example, changing line from lower case to upper case
  ```vim
  !!tr a-z A-Z
  ```
### Modes

```vim
v "visual mode from normal mode
[shift]+v "visual line mode
[ctrl]+v "visual block mode
c "change mode
```

### Marks
- marks are like bookmarks in your file
- You can use all the lower and upper case letter as marks. Lowercase marks are local to the current buffer, while uppercase marks are across 

```vim
m<character>
mx "set a mark called x 
```

### Jump through history
```vim
ctrl+o "to jump backwords
ctrl+i "to move forward
t" ""jump to right before the next quotes
f" ""jump and land on the next quotes
:jumps "to get jump list
```

### Windows
```vim
:split " to split the window
ctrl+ww " will move to windows in split
ctrl+wc " to close the window
```

### abbreviations
```vim
:abb <abbreviation> <what does it stand for>
:abb _imp import "in this instance _imp will populate import
```

### Command
```vim
:com! Py ! python %  "Py is the name of the command and then exclamation mark to run an external command python, which is a command to run and give it the parameter percent.
```
### Diff
```vim
vim -d <file> <file> 
"while in diff
do "diff obtain
dp "diff putt
:diffsplit <filename>  "diff from one buffer to another in horizontal
:vert diffsplit <filename> 
```
### Settings
```vim
:set ic "set case insensitive
:set hls "set highlight search
:noh "turn off highlight
:set incsearch
:set dip "get diff option
:set dip+=vertical "set diff vertical
:set clipboard=unnamedplus "Vim uses its own clipboard. To integrate with the system clipboard, use set clipboard equal unnamedplus, and now, you can copy from other programs and paste in Vim, and the other way around.
:syntax on 
:set list "to see line-endings.
:set nolist "to go back to normal.

" Search & display
set ignorecase
set incsearch
set nohls
set number
set showmatch
set smartcase

" Enable vim: ... directives
set modeline

" Tab stuff
set tabstop=8
set softtabstop=4
set shiftwidth=4

" Make no noise
set visualbell t_vb=
set noerrorbells

" Vertical diff
set diffopt=filler,vertical
```