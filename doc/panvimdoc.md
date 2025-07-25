```{.include}
README.md
```

# Specification

See [./panvimdoc.txt](./panvimdoc.txt) for generated output of this file.

## External includes

Use the following in your markdown file to include any other markdown file:

````markdown
```{.include}
README.md
```
````

The path of the file is with respect to the working directory where `pandoc` is executed.

## Codeblocks

```
Multi line Code blocks are indented 4 spaces and

are formatted

appropriately with > and <.
```

Alternatively, you can use `vimdoc` as the language for the code block to write raw text that will be inserted into the final document.

For example, the following:

````
```vimdoc
You can use codeblocks that have language as `vimdoc` to write raw vimdoc.
```
````

will be rendered verbatim in the generated documentation.

<!-- panvimdoc-ignore-start -->

e.g.:

```vimdoc
You can use codeblocks that have language as `vimdoc` to write raw vimdoc.
```

<!-- panvimdoc-ignore-end -->

This can be used to write any custom whitespace formatted documentation in the generated vimdoc (for mappings, options etc).

# Title

The first line of the documentation that is generated will look something like this:

```
*panvimdoc.txt*    For VIM - Vi IMproved 8.1       Last change: 2021 August 11
```

# Heading

Main headings are numbered.

<!-- panvimdoc-ignore-start -->

e.g.:

```
==============================================================================
2. Heading                                                 *panvimdoc-heading*

Main headings are numbered.
```

<!-- panvimdoc-ignore-end -->

## Sub Heading 2

Sub headings are upper cased heading.

<!-- panvimdoc-ignore-start -->

e.g.:

```
SUB HEADING 2                                        *panvimdoc-sub-heading-2*

Sub headings are upper cased heading.
```

<!-- panvimdoc-ignore-end -->

Notice that both headings and subheadings have tags.

### Sub Heading 3

Sub headings are upper cased, but do not have tags. They are also not included in the TOC.
They are suffixed with ` ~` which highlights as **bold** text when the file is viewed on GitHub.

## Markdown Links

You can use markdown links in vimdoc.

<!-- panvimdoc-ignore-start -->

The following markdown:

<!-- panvimdoc-ignore-end -->

```markdown
You can link to the tags by using [sub heading 2](#sub-heading-2).
```

<!-- panvimdoc-ignore-start -->

is converted to the following vimdoc:

```
You can link to the tags by using |projectName-sub-heading-2|.
```

<!-- panvimdoc-ignore-end -->

This way, any links will work in markdown README on GitHub or on the web using anchors AND will work as tags and links in vimdoc.
The anchors are simply dropped in vimdoc inline.
The onus is on the documentation writer to choose the correct anchor for the appropriate Markdown link.

In vimdoc tags are created when anchors to the internal document are used.
If the target is an external link, the link is inlined.

If the external link is to the neovim documentation, an internal vim link is generated. For example:

- [cursorcolumn](https://neovim.io/doc/user/options.html#'cursorcolumn')
- [`completeopt`](https://neovim.io/doc/user/options.html#'completeopt')
- [vim](https://github.com/vim/vim)
- [neovim](https://github.com/neovim/neovim)

<!-- panvimdoc-ignore-start -->

The following is generated in vimdoc:

```
- |cursorcolumn|
- |`completeopt`|
- vim <https://github.com/vim/vim>
- neovim <https://github.com/neovim/neovim>
```

<!-- panvimdoc-ignore-end -->

This is excluded from the links section.

Lastly, if the markdown text is a url, the link is not added to the links section and instead is placed inline.

## Linking to help tags

Markdown documents may suggest help tags via `:h help-tag`, which are converted to `|help-tag|` "hot links" in vimdoc.

## Mappings

While you can use codeblocks with the language `vimdoc` to insert text in the generated vimdoc, it can be useful to have a markdown friendly way to write documentation for mappings.

Pandoc supports definition lists: <https://pandoc.org/MANUAL.html#definition-lists>.
This can be used to generate documentation of mappings.
All of the content in curly braces `{...}` that is part of the header is dropped and a tag is created.

For example, the following in a markdown file:

````markdown
:FnlCompileBuffer

: Compiles current active fennel buffer

:FnlCompile[!]

: Diff compiles all indexed fennel files
If bang! is present then forcefully compiles all `source` files

:Fnl {expr}

: Executes and Evalutate {expr} of fennel

     ```fennel
     :Fnl (print "Hello World")

     :Fnl (values some_var)
     ```

     Testing
````

becomes the following vimdoc:

```

                                             *projectName-:FnlCompileBuffer*


:FnlCompileBuffer                      Compiles current active fennel buffer


                                                   *projectName-:FnlCompile*


:FnlCompile[!]                         Diff compiles all indexed fennel files
                                       If bang! is present then forcefully compiles all `source` files


                                                          *projectName-:Fnl*


:Fnl {expr}                            Executes and Evalutate {expr} of fennel
                                       >fennel
                                           :Fnl (print "Hello World")

                                           :Fnl (values some_var)
                                       <
                                       Testing
```

Notice that the tag `*projectName-:Command*` is generated for you. Additionally, content in square brackets `[...]` or curly brackets `{...}` is also dropped for creating the tag name.

i.e. the term `### :[range]Command` becomes the tag `*projectName-:Command*`.

See following mappings as examples:

<!-- prettier-ignore-start -->

pv{motion}

:    Command that operates over {motion} moved.

<!-- panvimdoc-ignore-start -->

The following vimdoc mapping is generated:

```
                                                              *panvimdoc-pv*


pv{motion}                             Command that operates over {motion} moved.
```

<!-- panvimdoc-ignore-end -->

pvd

:    Command that takes [count] lines.

<!-- panvimdoc-ignore-start -->

The following vimdoc mapping is generated:

```
                                                             *panvimdoc-pvd*


pvd                                    Command that takes [count] lines.
```

<!-- panvimdoc-ignore-end -->

:[range]CommandName {doc=CommandName}

:     Command that operates over [range].

<!-- panvimdoc-ignore-start -->

The following vimdoc mapping is generated:

```
                                                    *panvimdoc-:CommandName*


:[range]CommandName {doc=CommandName}  Command that operates over [range].
```

<!-- panvimdoc-ignore-end -->

{Visual}pv

:     Command that operates over highlighted lines.

<!-- panvimdoc-ignore-start -->

The following vimdoc mapping is generated:

```
                                                              *panvimdoc-pv*


{Visual}pv                             Command that operates over highlighted lines.
```

<!-- panvimdoc-ignore-end -->

<!-- prettier-ignore-end -->

## Table

Support for markdown tables is also available:

<!-- prettier-ignore-start -->

| Option                             | Background | Default | Description                                                               |
| ---------------------------------- | ---------- | ------- | ------------------------------------------------------------------------- |
| lightness                          | light      | `nil`   | Change background colors lightness. Options: `'bright'`, `'dim'`.         |
| darkness                           | dark       | `nil`   | Change background colors darkness. Options: `'stark'`, `'warm'`.          |
| solid_vert_split                   | both       | `false` | Solid \|hl-VertSplit\| background.                                        |
| solid_line_nr                      | both       | `false` | Solid \|hl-LineNr\| background.                                           |
| solid_float_border                 | both       | `false` | Make \|hl-FloatBorder\| have a more distinguishable background highlight. |
| darken_noncurrent_window           | light      | `false` | Make non-current window background darker than _Normal_.                  |
| lighten_noncurrent_window          | dark       | `false` | Make non-current window background lighter than _Normal_.                 |
| italic_comments                    | both       | `true`  | Make comments italicize.                                                  |
| darken_comments                    | light      | `38`    | Percentage to darken comments relative to Normal bg.                      |
| lighten_comments                   | dark       | `38`    | Percentage to lighten comments relative to Normal bg.                     |
| darken_non_text                    | light      | `25`    | Percentage to darken \|hl-NonText\| relative to Normal bg.                |
| lighten_non_text                   | dark       | `30`    | Percentage to lighten \|hl-NonText\| relative to Normal bg.               |
| darken_line_nr                     | light      | `33`    | Percentage to darken \|hl-LineNr\| relative to Normal bg.                 |
| lighten_line_nr                    | dark       | `35`    | Percentage to lighten \|hl-LineNr\| relative to Normal bg.                |
| darken_cursor_line                 | light      | `3`     | Percentage to darken \|hl-CursorLine\| relative to Normal bg.             |
| lighten_cursor_line                | dark       | `4`     | Percentage to lighten \|hl-CursorLine\| relative to Normal bg.            |
| colorize_diagnostic_underline_text | both       | `false` | Colorize the fg of `DiagnosticUnderline*`.                                |
| transparent_background             | both       | `false` | Make background transparent.                                              |

<!-- prettier-ignore-end -->

<!-- panvimdoc-ignore-start -->

The following gets generated:

```
  -----------------------------------------------------------------------------------------------------
  Option                               Background   Default   Description
  ------------------------------------ ------------ --------- -----------------------------------------
  lightness                            light        nil       Change background colors lightness.
                                                              Options: 'bright', 'dim'.

  darkness                             dark         nil       Change background colors darkness.
                                                              Options: 'stark', 'warm'.

  solid_vert_split                     both         false     Solid |hl-VertSplit| background.

  solid_line_nr                        both         false     Solid |hl-LineNr| background.

  solid_float_border                   both         false     Make |hl-FloatBorder| have a more
                                                              distinguishable background highlight.

  darken_noncurrent_window             light        false     Make non-current window background darker
                                                              than Normal.

  lighten_noncurrent_window            dark         false     Make non-current window background
                                                              lighter than Normal.

  italic_comments                      both         true      Make comments italicize.

  darken_comments                      light        38        Percentage to darken comments relative to
                                                              Normal bg.

  lighten_comments                     dark         38        Percentage to lighten comments relative
                                                              to Normal bg.

  darken_non_text                      light        25        Percentage to darken |hl-NonText|
                                                              relative to Normal bg.

  lighten_non_text                     dark         30        Percentage to lighten |hl-NonText|
                                                              relative to Normal bg.

  darken_line_nr                       light        33        Percentage to darken |hl-LineNr| relative
                                                              to Normal bg.

  lighten_line_nr                      dark         35        Percentage to lighten |hl-LineNr|
                                                              relative to Normal bg.

  darken_cursor_line                   light        3         Percentage to darken |hl-CursorLine|
                                                              relative to Normal bg.

  lighten_cursor_line                  dark         4         Percentage to lighten |hl-CursorLine|
                                                              relative to Normal bg.

  colorize_diagnostic_underline_text   both         false     Colorize the fg of DiagnosticUnderline*.

  transparent_background               both         false     Make background transparent.
  -----------------------------------------------------------------------------------------------------
```

<!-- panvimdoc-ignore-end -->

## Markdown only content

Sometimes you want to show content that is to be present in Markdown and on the rendered view on GitHub but ignored in the generated vimdoc.
This can be placed inside `panvimdoc-ignore-{start/end}` blocks:

```
<!-- panvimdoc-ignore-start -->

<details>
    <summary>Vimdoc Ignored Section</summary>

This section will ignored when generating the vimdoc file.
This will only show up in the Markdown file.

</details>

<!-- panvimdoc-ignore-end -->
```

The following will only be present in the Markdown document.

<!-- panvimdoc-ignore-start -->

<details>
    <summary>Vimdoc Ignored Section</summary>

This section will ignored when generating the vimdoc file.
This will only show up in the Markdown file.
See the raw markdown of this file for examples.

</details>

<!-- panvimdoc-ignore-end -->

The convenient advantage of using `<!-- panvimdoc-ignore-{start/end} -->` blocks in a HTML comment syntax is that the comment will not rendered in HTML or on GitHub, giving the documentation writers control to present the information differently on GitHub and in vimdoc.
If you want to see examples of this, see the raw markdown version of this file.

The only thing to keep in mind is that you must leave new line spaces before and after a comment tag. For example, **do not** do this:

```
<!-- panvimdoc-ignore-start -->
![screenshot](./gif.gif)
<!-- panvimdoc-ignore-end -->
```

because it may cause the rest of your document to be ignored. Do this instead:

```
<!-- panvimdoc-ignore-start -->

![screenshot](./gif.gif)

<!-- panvimdoc-ignore-end -->
```

## Vimdoc only content

Inversely to [markdown only content](#markdown-only-content), sometimes you want to show content only present in Vimdoc and hidden when viewed on Github.

This can be placed inside `panvimdoc-include-comment` comments.

As with markdown only content, you must include a blank link before and after the comment.

```markdown

<!-- panvimdoc-include-comment You can include single lines  -->

<!-- panvimdoc-include-comment

Or multiple lines

- with other
- content
- types

# And vimdoc only headings

## That can include subheadings

Infact you can include any kind of content in the comment.

-->

```

<!-- panvimdoc-include-comment Neovim is a great text editor. -->

<!-- panvimdoc-include-comment

Neovim supports `:h lua` plugins and is also:

- Multiplatform
- Open source

-->

## Details and summary

You can even use `<details>` and `<summary>` tags for your README.md.

<details>

<summary><b>Summary</b></summary>

This section is the details.

</details>

<!-- panvimdoc-ignore-start -->

This gets rendered as:

```
Summary ~

This section is the details.
```

<!-- panvimdoc-ignore-end -->

The `html` tags are dropped and the following output is generated in the vimdoc file.

If you are using html `<b> ... </b>` tags, use them on new lines. <b>Inline bold tags</b> will have
a ` ~` appended to the text and that may not be what you want.

## Keyboard HTML tag

Use `<kbd>CMD + o</kbd>` in markdown, for example <kbd>CMD + o</kbd>.

<!-- panvimdoc-ignore-start -->

This gets rendered as:

```
Use `<kbd>CMD + o</kbd>` in markdown, for example CMD + o.
```

<!-- panvimdoc-ignore-end -->

## Examples

First example

## Examples

Second example

## Remove emojis

### :sparkles: Features

### :zap: Requirements

### :package: Installation

<!-- panvimdoc-ignore-start -->

This gets rendered as:

`demoji: false`:

```
:SPARKLES: FEATURES ~


:ZAP: REQUIREMENTS ~


:PACKAGE: INSTALLATION ~
```

OR

`demoji: true`:

```
FEATURES ~


REQUIREMENTS ~


INSTALLATION ~
```

<!-- panvimdoc-ignore-end -->
