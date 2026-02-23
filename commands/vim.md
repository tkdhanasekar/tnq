## Modes
for normal mode ```Esc```

for insert mode ```i```

for command-line mode ```:```

## Navigation

### To navigate to start of a line
enter normal mode ```Esc```\
then type\
```0```

### To navigate to end of a line
enter normal mode ```Esc```\
then type\
```$```

### To navigate to bottom of a file
enter normal mode ```Esc```\
then type\
```G```

### To navigate to top of a file
enter normal mode ```Esc```\
then type\
```gg```

### To navigate to line n
enter command-line mode ```:```\
then type\
```:n```

### To jump to next word
enter normal mode ```Esc```\
then type\
```w```

### To jump to previous word
enter normal mode ```Esc```\
then type\
```b```

```dw```	Delete word\
```d$```	Delete to end of line\
```dd```	Delete current line\
```dG```	Delete to end of file\
```u```	        Undo\
```Ctrl+r```	Redo

##  Copy, Cut, and Paste
```yy```	Yank (copy) line
```yw```	Yank word
```y$```	Yank to end of line
```p``` 	Paste after cursor
```P``` 	Paste before cursor
```dd```	Cut (delete) line
```yap```       Copy a paragraph
```dap```       Delete a paragraph

## Searching
```/pattern```		Search forward
```?pattern```		Search backward
```:%s/old/new/g```	Replace all occurrences in file
```:n,m s/old/new/g```	Replace in lines n to m

To set line numbers
: set nu

To unset line numbers
: set nonu

To set highlight search
:set hlsearch

To set permanent parameters in vim 
```vim ~/.vimrc```
set hlsearch
set nu
```source ~/.vimrc```


