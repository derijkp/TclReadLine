TclReadLine
===========

This is a pure Tcl readline extension, providing in-line editing, history capabilities, and completion in tcl shells.


It started from code from http://wiki.tcl.tk/20215 and
http://wiki.tcl.tk/16139 by HCG, and modified by rjmcmahon

It was further modified by Peter De Rijk, adding the following functionality:
- signal handling
  - ctrl-C (sigint) will interrupt running code while keeping shell alive (instead of ignoring with Tclx or killing entire program without)
  - default signal handling using Expect (not TclX as it interferes with some code)
- completion
  - completion using Shift-Tab (so we can still enter/copy-paste actual tabs)
  - completion using TAB is by default off, but can be turned on (and off again) using Control-t
  - TAB completion is not attempted for tabs at the start of a line (allows copy-paste for code indented with tabs, but not tabs in the code)
  - catch errors in tab completion code
- cursor control in editing mode
  - ctrl-up (or shift-up) and ctrl-down (or shift-down) to move up and down one line in editing mode
  - shift-left and shift-right to move to begin and end of the current line in editing mode
  - ctrl-left and ctrl-right to move left and right by word
- (optionally) limit the number of characters displayed of return/result (default 1000 characters), can e.g. be set to max 200 characters with
    printlimit 200
        or unset with 
    printlimit ""
- turn off auto glob substitution (with option var CMDLINE_GLOB, default 0) (gave strange errors sometimes)

Installation
------------
Put the TclReadLine directory somewhere Tcl looks for extensions.

Usage
-----
```
package require TclReadLine
# you can set the prompt string, this string is substituted each time, so you can use e.g. [pwd] to display the current wd in the prompt
set ::TclReadLine::PROMPT {tclsh[info patchlevel] \[[pwd]\]% }
# start interactive use with TclReadLine
TclReadLine::interact
```

example usage in .tclshrc:
```
package require TclReadLine
tailcall ::TclReadLine::interact
```
