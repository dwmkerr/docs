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
* [BASH Regex](#bash-regex)
    * [Extract with Regex in Bash](#extract-with-regex-in-bash)
* [Sed](#sed)
    * [Append a line](#append-a-line)
    * [Extract a capture group](#extract-a-capture-group)

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

## BASH Regex

```sh
# osx/bsd
man re_format

# GNU
man grep
```

### Extract with Regex in Bash

```
image_tag="<img src="/wp-content/uploads/2012/imported/CDSF-CodePlex-Banner-Logo.png" alt="" />"
regex='.*alt="([^"]+)"'
if [[ $image_tag =~ $regex ]]; then echo $BASH_REMATCH[1]; fi
```

## Sed

### Append a line

```bash
sed 's//\n/g'
```

### Extract a capture group

In the below example, we extract the value of the `src` attribute by matching the whole line, and capturing `src` only.

```bash
image_tag="<img src="/wp-content/uploads/2012/imported/CDSF-CodePlex-Banner-Logo.png" alt="" />"
image_tag_src=$(echo $image_tag | sed -E 's/.*src="([^"]*).*/\1/')
```
