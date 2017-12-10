# bash

The most useful bash tips and tricks.

## Check if a folder exists

```bash
if [[ -d './some-folder' ]]; then
    echo './some-folder exists'
fi
```

## Check if a file exists

```bash
if [[ -e './some-file' ]]; then
    echo './some-file exists'
fi
```

## Loop over files

```bash
for file in Data/*.txt; do
    # If the glob expands to nothing then we get the goofy 'original glob' result
    [ -e "$file" ] || continue
    # ... rest of the loop body
done
```
