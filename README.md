<!-- md-toc-begin -->
# Table of Content
* [NAME](#name)
* [SYNOPSIS](#synopsis)
* [DESCRIPTION](#description)
* [FORMAT](#format)
* [EXAMPLES](#examples)
  * [Example 1](#example-1)
* [AUTHORS](#authors)
* [COPYRIGHT](#copyright)
<!-- md-toc-end -->

# NAME

git-md-snippet - translate markdown links to embedded code snippets

# SYNOPSIS


```
  git-md-snippet < FILE1 > FILE2
```
# DESCRIPTION

Read an input and translate links to the files of the repository to the code blocks and embed them replacing the links with codes.

# FORMAT

While parsing a file the script looks for the links formatted as follows:


```
  [code=TITLE;url;lang=LANG;numbers;lines=LINES;fence=FENCE](path)
```
The `code` is mandatory as it marks the link specified to be replaced with the content of the specified file.

The code link MUST be stick to the beginning of the line (no any white spaces are permitted).

* **code**[=_TITLE_]
  Marks the special link. The optional parameter _TITLE_ is a text to be used as a text under link. If it is not specified, the original link will be used.

* **url**
  Outputs the link to the original file.

* **lang**=_LANG_
  Triggers the markdown system to colorize the embedded code accordingly the specified language.

* **numbers**
  Prints the line numbers in the beginning of each line.

* **lines**=_LINES_
  Specifies the lines to be printed. This parameter can be either a list separated by comma and/or a range of lines separated by dash.

* **fence**=_backtick | tilde_
  Use backtick characters **\`** (ASCII 96) or tildes **~** (ASCII 126) for fencing code blocks. It can be useful, when for some reason you need to fence a code already containing fencing within. Defaults to backtick.


Another way to turn on the line range and numbering:


```
  [code...](path#LLINE1-LLINE2)
```
where `LINE1` and `LINE2` are define the range of line numbers to be extracted. This feature is compatible with GitHub's way for creating a permanent link to a code snippet. This format overrides inlined **numbers** and **lines** and turns on the line numbering implicitly.

# EXAMPLES

## Example 1

Assume the following two links:


```
  [code;lang=perl;numbers;lines=3-14;fence=tilde](git-md-snippet)
```
and


```
  [code;lang=perl;fence=tilde](git-md-snippet#L3-L14)
```
Both will be translated into the following code:


```
  ~~~perl
   3: =head1 NAME
   4:
   5: git-md-snippet - translate markdown links to embedded code snippets
   6:
   7: =head1 SYNOPSIS
   8:
   9:   git-md-snippet < FILE1 > FILE2
  10:
  11: =head1 DESCRIPTION
  12:
  13: Read an input and translate links to the files of the repository to the
  14: code blocks and embed them replacing the links with codes.

  ~~~
```
# AUTHORS

Ildar Shaimordanov <_ildar.shaimordanov@gmail.com_>

# COPYRIGHT

Copyright (c) 2019-2021 Ildar Shaimordanov. All rights reserved.


```
  MIT License
```
