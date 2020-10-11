# docs

Useful guides, documents, snippets for working with tech.


<!-- vim-markdown-toc GFM -->

* [Introduction](#introduction)
    * [Vim](#vim)
        * [Quick Replace](#quick-replace)
    * [Programming Languages](#programming-languages)
        * [TypeScript](#typescript)

<!-- vim-markdown-toc -->

# Introduction

This is a set of assorted documents, snippets and links I've found useful and often refer to.

## Vim

### Quick Replace

Go to the word you want to replace, then in command mode just use `Ctrl+R` `Ctrl+W` to paste the word into the command editor, e.g.

```
:%s/<now type Ctrl+R Ctrl+W>
```

This works because `CTRL-R` is used to insert a register in either command or insert mode. In command mode `CTRL-W` is the word under the cursor. Other related tricks

- `CTRL-R` + `\` - Insert the last search term
- `CTRL-R` + `a` - Insert a register named `a`
- `CTRL-R` + `=` - Insert the result of an expression (e.g. `3*78`)

More info: `:help i_CTRL-R` and `:help c_CTRL-R`.

## Programming Languages

### TypeScript

Beginner friendly and to-the-point overview of TypeScript, assuming the reader already knows JavaScript:

https://github.com/rmolinamir/typescript-cheatsheet

Other links:

- [TypeScript for JavaScript Programmers](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html)
