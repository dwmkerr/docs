# bash

The most useful bash tips and tricks.


<!-- vim-markdown-toc GFM -->

* [Variables](#variables)
    * [Check if a variable is set](#check-if-a-variable-is-set)
* [Files and Folders](#files-and-folders)
    * [Check if a folder exists](#check-if-a-folder-exists)
    * [Check if a file exists](#check-if-a-file-exists)
    * [Loop over files / folders](#loop-over-files--folders)
    * [Loop over each value in a multiline string](#loop-over-each-value-in-a-multiline-string)
    * [Loop over each line in a file](#loop-over-each-line-in-a-file)
* [Sed](#sed)
    * [Append a line](#append-a-line)

<!-- vim-markdown-toc -->

## Variables

### Check if a variable is set

Some combinations of set, not set, empty, not empty.

```bash
# Is x a non-empty string?
if [ -n "$x" ]; then
    echo "x is not empty"
elif [ "$x" ]; then
    echo "x is not empty"
fi
```


## Files and Folders

- [Cheatsheet for Bash Conditional Operators](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_07_01.html)

### Check if a folder exists

```bash
if [[ -d './some-folder' ]]; then
    echo './some-folder exists'
fi
```

### Check if a file exists

```bash
if [[ -e './some-file' ]]; then
    echo './some-file exists'
fi
```

### Loop over files / folders

```bash
for file in Data/*.txt; do
    # If the glob expands to nothing then we get the goofy 'original glob' result
    [ -e "$file" ] || continue
    # ... rest of the loop body
done
```

```bash
for folder in Data/*/; do
    # If the glob expands to nothing then we get the goofy 'original glob' result
    [ -e "$folder" ] || continue
    # ... rest of the loop body
done
```

### Loop over each value in a multiline string

```bash
while read -r line; do
    echo "... $line ..."
done <<< "$variable"
```

### Loop over each line in a file

```bash
while read -r line; do
    echo "... $line ..."
done <file.txt
```

## Sed

### Append a line

- TODO!

