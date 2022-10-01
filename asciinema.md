# Install

```bash
brew install asciinema
```

## Authenticate

```bash
asciinema auth
```

## Record

```
asciinema rec
# Then ^D to stop recording
```

## Record a Tmux Session

Make sure you are not already attached to the target session.

```bash
asciinema rec --command "tmux attach -t dwmkerr_com"
```

## Create SVG (for GitHub README files)

```bash
cast_id=523641
npx svg-term-cli --in ${cast_id}.cast --out ${cast_id}.svg --window
```


