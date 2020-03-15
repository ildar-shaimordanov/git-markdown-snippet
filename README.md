# git-markdown-link2code

translate markdown links to embedded codes

# NAME

`git-md-link2code` - translate markdown links to embedded codes

# SYNOPSIS

```
git-md-link2code < FILE1 > FILE2
```

# DESCRIPTION

Read an input and translate links to the files of the repository to the
code blocks and embed them replacing the links with codes.

# FORMAT

While parsing a file the script looks for the links formatted as follows:

```
[code=TITLE;url;lang=LANG;numbers;lines=LINES](path)
```

The `code` is mandatory as it marks the link specified to be replaced
with the content of the specified file.

* `code[=TITLE]`
  Marks the special link. The optional parameter `TITLE` is a text to
  be used as a text under link. If it is not specified, the original link
  will be used.
* `url`
  Outputs the link to the original file.
* `lang=LANG`
  Triggers the markdown system to colorize the embedded code accordingly
  the specified language.
* `numbers`
  Prints the line numbers in the beginning of each line.
* `lines=LINES`
  Specifies the lines to be printed. This parameter can be either a list
  separated by comma and/or a range of lines separated by dash.

# EXAMPLES

## Example 1

Assume the following two links:

```
[code;lang=perl;numbers;lines=3-9](git-md-link2code)
```

```
[code;lang=perl](git-md-link2code#L3-L9)
```

Both will be translated into the following code:

  ```perl
  3: =head1 NAME
  4:
  5: git-md-link2code - translate markdown links to embedded codes
  6:
  7: =head1 SYNOPSIS
  8:
  9:   git-md-link2code < FILE1 > FILE2
  
  ```
