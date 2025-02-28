---
description: PSReadLine provides an improved command-line editing experience in the PowerShell console.
Locale: en-US
ms.date: 10/14/2021
online version: https://docs.microsoft.com/powershell/module/psreadline/about/about_psreadline?view=powershell-7.3&WT.mc_id=ps-gethelp
schema: 2.0.0
title: about PSReadLine
---
# about_PSReadLine

## Short Description

PSReadLine provides an improved command-line editing experience in the
PowerShell console.

## Long Description

PSReadLine 2.1 provides a powerful command-line editing experience for the
PowerShell console. It provides:

- Syntax coloring of the command line
- A visual indication of syntax errors
- A better multi-line experience (both editing and history)
- Customizable key bindings
- Cmd and Emacs modes
- Many configuration options
- Bash style completion (optional in Cmd mode, default in Emacs mode)
- Emacs yank/kill-ring
- PowerShell token based "word" movement and deletion
- Predictive IntelliSense

PSReadLine requires PowerShell 3.0, or newer. PSReadLine works with default
console host, Visual Studio Code, and Window Terminal. It does not work in
PowerShell ISE.

PSReadLine 2.1.0 ships with PowerShell 7.2 and is supported in all supported
versions of PowerShell. It is available to install from the PowerShell Gallery.
To install PSReadLine 2.1.0 in a supported version of PowerShell run the
following command.

PSReadLine 2.2.0 (beta) added two new predictive IntelliSense features:

- Added the **PredictionViewStyle** parameter to allow for the selection of the
  new `ListView`.
- Connected PSReadLine to the `CommandPrediction` APIs introduced in PS 7.1 to
  allow a user can import a predictor module that can render the suggestions
  from a custom source.

```powershell
Install-Module -Name PSReadLine -AllowPrerelease
```

> [!NOTE]
> Beginning with PowerShell 7.0, PowerShell skips auto-loading PSReadLine on
> Windows if a screen reader program is detected. Currently, PSReadLine doesn't
> work well with the screen readers. The default rendering and formatting of
> PowerShell 7.0 on Windows works properly. You can manually load the module if
> necessary.

## Predictive IntelliSense

Predictive IntelliSense is an addition to the concept of tab completion that
assists the user in successfully completing commands. It enables users to
discover, edit, and execute full commands based on matching predictions from the
user's history and additional domain specific plugins.

### Enable Predictive IntelliSense

Predictive IntelliSense is disabled by default. To enable predictions, just run
the following command:

```powershell
Set-PSReadLineOption -PredictionSource History
```

The **PredictionSource** parameter can also accept plugins for domain specific
and custom requirements.

To disable Predictive IntelliSense, just run:

```powershell
Set-PSReadLineOption -PredictionSource None
```

The following functions are available in the class
**Microsoft.PowerShell.PSConsoleReadLine**.

## Basic editing functions

### Abort

Abort current action, for example: incremental history search.

- Emacs: `<Ctrl+g>`
- Vi insert mode: `<Ctrl+g>`
- Vi command mode: `<Ctrl+g>`

### AcceptAndGetNext

Attempt to execute the current input. If it can be executed (like AcceptLine),
then recall the next item from history the next time ReadLine is called.

- Emacs: `<Ctrl+o>`

### AcceptLine

Attempt to execute the current input. If the current input is incomplete (for
example there is a missing closing parenthesis, bracket, or quote) then the
continuation prompt is displayed on the next line and PSReadLine waits for
keys to edit the current input.

- Cmd: `<Enter>`
- Emacs: `<Enter>`
- Vi insert mode: `<Enter>`

### AddLine

The continuation prompt is displayed on the next line and PSReadLine waits for
keys to edit the current input. This is useful to enter multi-line input as a
single command even when a single line is complete input by itself.

- Cmd: `<Shift+Enter>`
- Emacs: `<Shift+Enter>`
- Vi insert mode: `<Shift+Enter>`
- Vi command mode: `<Shift+Enter>`

### BackwardDeleteChar

Delete the character before the cursor.

- Cmd: `<Backspace>`, `<Ctrl+h>`
- Emacs: `<Backspace>`, `<Ctrl+Backspace>`, `<Ctrl+h>`
- Vi insert mode: `<Backspace>`
- Vi command mode: `<X>`, `<d,h>`

### BackwardDeleteInput

Like BackwardKillInput - deletes text from the point to the start of the input,
but does not put the deleted text in the kill-ring.

- Cmd: `<Ctrl+Home>`
- Vi insert mode: `<Ctrl+u>`, `<Ctrl+Home>`
- Vi command mode: `<Ctrl+u>`, `<Ctrl+Home>`

### BackwardDeleteLine

Like BackwardKillLine - deletes text from the point to the start of the line,
but does not put the deleted text in the kill-ring.

- Vi command mode: `<d,0>`

### BackwardDeleteWord

Deletes the previous word.

- Vi command mode: `<Ctrl+w>`, `<d,b>`

### BackwardKillInput

Clear the text from the start of the input to the cursor. The cleared text is
placed in the kill-ring.

- Emacs: `<Ctrl+u>`, `<Ctrl+x,Backspace>`

### BackwardKillLine

Clear the text from the start of the current logical line to the cursor. The cleared text is
placed in the kill-ring.

- Function is unbound.

### BackwardKillWord

Clear the input from the start of the current word to the cursor. If the
cursor is between words, the input is cleared from the start of the previous
word to the cursor. The cleared text is placed in the kill-ring.

- Cmd: `<Ctrl+Backspace>`, `<Ctrl+w>`
- Emacs: `<Alt+Backspace>`, `<Escape,Backspace>`
- Vi insert mode: `<Ctrl+Backspace>`
- Vi command mode: `<Ctrl+Backspace>`

### CancelLine

Cancel the current input, leaving the input on the screen, but returns back to
the host so the prompt is evaluated again.

- Vi insert mode: `<Ctrl+c>`
- Vi command mode: `<Ctrl+c>`

### Copy

Copy selected region to the system clipboard. If no region is selected, copy
the whole line.

- Cmd: `<Ctrl+C>`

### CopyOrCancelLine

If text is selected, copy to the clipboard, otherwise cancel the line.

- Cmd: `<Ctrl+c>`
- Emacs: `<Ctrl+c>`

### Cut

Delete selected region placing deleted text in the system clipboard.

- Cmd: `<Ctrl+x>`

### DeleteChar

Delete the character under the cursor.

- Cmd: `<Delete>`
- Emacs: `<Delete>`
- Vi insert mode: `<Delete>`
- Vi command mode: `<Delete>`, `<x>`, `<d,l>`, `<d,Spacebar>`

### DeleteCharOrExit

Delete the character under the cursor, or if the line is empty, exit the
process.

- Emacs: `<Ctrl+d>`

### DeleteEndOfBuffer

Deletes to the end of the multiline buffer.

- Vi command mode: `<d,G>`

### DeleteEndOfWord

Delete to the end of the word.

- Vi command mode: `<d,e>`

### DeleteLine

Deletes the current logical line of a multiline buffer, enabling undo.

- Vi command mode: `<d,d>`, `<d,_>`

### DeletePreviousLines

Deletes the previous requested logical lines and the current logical line in a multiline buffer.

- Vi command mode: `<d,k>`

### DeleteRelativeLines

Deletes from the beginning of the buffer to the current logical line in a multiline buffer.

As most Vi commands, the `<d,g,g>` command can be prepended with a numeric argument that specifies an absolute line number,
which, together with the current line number, make up a range of lines to be deleted.
If not specified, the numeric argument defaults to 1, which refers to the first logical line in a multiline buffer.

The actual number of lines to be deleted from the multiline is computed as the difference between the current logical line number
and the specified numeric argument, which can thus be negative. Hence the _relative_ part of method name.

- Vi command mode: `<d,g,g>`

### DeleteNextLines

Deletes the current logical line and the next requested logical lines in a multiline buffer.

- Vi command mode: `<d,j>`

### DeleteLineToFirstChar

Deletes from the first non-blank character of the current logical line in a multiline buffer.

- Vi command mode: `<d,^>`

### DeleteToEnd

Delete to the end of the line.

- Vi command mode: `<D>`, `<d,$>`

### DeleteWord

Delete the next word.

- Vi command mode: `<d,w>`

### ForwardDeleteInput

Like KillLine - deletes text from the point to the end of the input, but
does not put the deleted text in the kill-ring.

- Cmd: `<Ctrl+End>`
- Vi insert mode: `<Ctrl+End>`
- Vi command mode: `<Ctrl+End>`

### ForwardDeleteLine

Deletes text from the point to the end of the current logical line, but
does not put the deleted text in the kill-ring.

- Function is unbound

### InsertLineAbove

A new empty line is created above the current line regardless of where the
cursor is on the current line. The cursor moves to the beginning of the new
line.

- Cmd: `<Ctrl+Enter>`

### InsertLineBelow

A new empty line is created below the current line regardless of where the
cursor is on the current line. The cursor moves to the beginning of the new
line.

- Cmd: `<Shift+Ctrl+Enter>`

### InvertCase

Invert the case of the current character and move to the next one.

- Vi command mode: `<~>`

### KillLine

Clear the input from the cursor to the end of the input. The cleared text is
placed in the kill-ring.

- Emacs: `<Ctrl+k>`

### KillRegion

Kill the text between the cursor and the mark.

- Function is unbound.

### KillWord

Clear the input from the cursor to the end of the current word. If the cursor
is between words, the input is cleared from the cursor to the end of the next
word. The cleared text is placed in the kill-ring.

- Cmd: `<Alt+d>`, `<Ctrl+Delete>`
- Emacs: `<Alt+d>`, `<Escape,d>`
- Vi insert mode: `<Ctrl+Delete>`
- Vi command mode: `<Ctrl+Delete>`

### Paste

Paste text from the system clipboard.

- Cmd: `<Ctrl+v>`, `<Shift+Insert>`
- Vi insert mode: `<Ctrl+v>`
- Vi command mode: `<Ctrl+v>`

> [!IMPORTANT]
> When using the **Paste** function, the entire contents of the clipboard
> buffer is pasted into the input buffer of PSReadLine. The input buffer is
> then passed to the PowerShell parser. Input pasted using the console
> application's **right-click** paste method is copied to the input buffer one
> character at a time. The input buffer is passed to the parser when a newline
> character is copied. Therefore, the input is parsed one line at a time. The
> difference between paste methods results in different execution behavior.

### PasteAfter

Paste the clipboard after the cursor, moving the cursor to the end of the
pasted text.

- Vi command mode: `<p>`

### PasteBefore

Paste the clipboard before the cursor, moving the cursor to the end of the
pasted text.

- Vi command mode: `<P>`

### PrependAndAccept

Prepend a '#' and accept the line.

- Vi command mode: `<#>`

### Redo

Undo an undo.

- Cmd: `<Ctrl+y>`
- Vi insert mode: `<Ctrl+y>`
- Vi command mode: `<Ctrl+y>`

### RepeatLastCommand

Repeat the last text modification.

- Vi command mode: `<.>`

### RevertLine

Reverts all input to the current input.

- Cmd: `<Escape>`
- Emacs: `<Alt+r>`, `<Escape,r>`

### ShellBackwardKillWord

Clear the input from the start of the current word to the cursor. If the
cursor is between words, the input is cleared from the start of the previous
word to the cursor. The cleared text is placed in the kill-ring.

Function is unbound.

### ShellKillWord

Clear the input from the cursor to the end of the current word. If the cursor
is between words, the input is cleared from the cursor to the end of the next
word. The cleared text is placed in the kill-ring.

Function is unbound.

### SwapCharacters

Swap the current character and the one before it.

- Emacs: `<Ctrl+t>`
- Vi insert mode: `<Ctrl+t>`
- Vi command mode: `<Ctrl+t>`

### Undo

Undo a previous edit.

- Cmd: `<Ctrl+z>`
- Emacs: `<Ctrl+_>`, `<Ctrl+x,Ctrl+u>`
- Vi insert mode: `<Ctrl+z>`
- Vi command mode: `<Ctrl+z>`, `<u>`

### UndoAll

Undo all previous edits for line.

- Vi command mode: `<U>`

### UnixWordRubout

Clear the input from the start of the current word to the cursor. If the
cursor is between words, the input is cleared from the start of the previous
word to the cursor. The cleared text is placed in the kill-ring.

- Emacs: `<Ctrl+w>`

### ValidateAndAcceptLine

Attempt to execute the current input. If the current input is incomplete (for
example there is a missing closing parenthesis, bracket, or quote) then the
continuation prompt is displayed on the next line and PSReadLine waits for
keys to edit the current input.

- Emacs: `<Ctrl+m>`

### ViAcceptLine

Accept the line and switch to Insert mode.

- Vi command mode: `<Enter>`

### ViAcceptLineOrExit

Like DeleteCharOrExit in Emacs mode, but accepts the line instead of deleting
a character.

- Vi insert mode: `<Ctrl+d>`
- Vi command mode: `<Ctrl+d>`

### ViAppendLine

A new line is inserted below the current line.

- Vi command mode: `<o>`

### ViBackwardDeleteGlob

Deletes the previous word, using only whitespace as the word delimiter.

- Vi command mode: `<d,B>`

### ViBackwardGlob

Moves the cursor back to the beginning of the previous word, using only
whitespace as delimiters.

- Vi command mode: `<B>`

### ViDeleteBrace

Find the matching brace, parenthesis, or square bracket and delete all contents
within, including the brace.

- Vi command mode: `<d,%>`

### ViDeleteEndOfGlob

Delete to the end of the word.

- Vi command mode: `<d,E>`

### ViDeleteGlob

Delete the next glob (whitespace delimited word).

- Vi command mode: `<d,W>`

### ViDeleteToBeforeChar

Deletes until given character.

- Vi command mode: `<d,t>`

### ViDeleteToBeforeCharBackward

Deletes until given character.

- Vi command mode: `<d,T>`

### ViDeleteToChar

Deletes until given character.

- Vi command mode: `<d,f>`

### ViDeleteToCharBackward

Deletes backwards until given character.

- Vi command mode: `<d,F>`

### ViInsertAtBegining

Switch to Insert mode and position the cursor at the beginning of the line.

- Vi command mode: `<I>`

### ViInsertAtEnd

Switch to Insert mode and position the cursor at the end of the line.

- Vi command mode: `<A>`

### ViInsertLine

A new line is inserted above the current line.

- Vi command mode: `<O>`

### ViInsertWithAppend

Append from the current line position.

- Vi command mode: `<a>`

### ViInsertWithDelete

Delete the current character and switch to Insert mode.

- Vi command mode: `<s>`

### ViJoinLines

Joins the current line and the next line.

- Vi command mode: `<J>`

### ViReplaceLine

Erase the entire command line.

- Vi command mode: `<S>`, `<c,c>`

### ViReplaceToBeforeChar

Replaces until given character.

- Vi command mode: `<c,t>`

### ViReplaceToBeforeCharBackward

Replaces until given character.

- Vi command mode: `<c,T>`

### ViReplaceToChar

Deletes until given character.

- Vi command mode: `<c,f>`

### ViReplaceToCharBackward

Replaces until given character.

- Vi command mode: `<c,F>`

### ViYankBeginningOfLine

Yank from the beginning of the buffer to the cursor.

- Vi command mode: `<y,0>`

### ViYankEndOfGlob

Yank from the cursor to the end of the WORD(s).

- Vi command mode: `<y,E>`

### ViYankEndOfWord

Yank from the cursor to the end of the word(s).

- Vi command mode: `<y,e>`

### ViYankLeft

Yank character(s) to the left of the cursor.

- Vi command mode: `<y,h>`

### ViYankLine

Yank the entire buffer.

- Vi command mode: `<y,y>`

### ViYankNextGlob

Yank from cursor to the start of the next WORD(s).

- Vi command mode: `<y,W>`

### ViYankNextWord

Yank the word(s) after the cursor.

- Vi command mode: `<y,w>`

### ViYankPercent

Yank to/from matching brace.

- Vi command mode: `<y,%>`

### ViYankPreviousGlob

Yank from beginning of the WORD(s) to cursor.

- Vi command mode: `<y,B>`

### ViYankPreviousWord

Yank the word(s) before the cursor.

- Vi command mode: `<y,b>`

### ViYankRight

Yank character(s) under and to the right of the cursor.

- Vi command mode: `<y,l>`, `<y,Spacebar>`

### ViYankToEndOfLine

Yank from the cursor to the end of the buffer.

- Vi command mode: `<y,$>`

### ViYankToFirstChar

Yank from the first non-whitespace character to the cursor.

- Vi command mode: `<y,^>`

### Yank

Add the most recently killed text to the input.

- Emacs: `<Ctrl+y>`

### YankLastArg

Yank the last argument from the previous history line. With an argument, the
first time it is invoked, behaves just like YankNthArg. If invoked multiple
times, instead it iterates through history and arg sets the direction
(negative reverses the direction.)

- Cmd: `<Alt+.>`
- Emacs: `<Alt+.>`, `<Alt+_>`, `<Escape,.>`, `<Escape,_>`

### YankNthArg

Yank the first argument (after the command) from the previous history line.
With an argument, yank the nth argument (starting from 0), if the argument is
negative, start from the last argument.

- Emacs: `<Ctrl+Alt+y>`, `<Escape,Ctrl+y>`

### YankPop

If the previous operation was Yank or YankPop, replace the previously yanked
text with the next killed text from the kill-ring.

- Emacs: `<Alt+y>`, `<Escape,y>`

## Cursor movement functions

### BackwardChar

Move the cursor one character to the left. This may move the cursor to the
previous line of multi-line input.

- Cmd: `<LeftArrow>`
- Emacs: `<LeftArrow>`, `<Ctrl+b>`

### BackwardWord

Move the cursor back to the start of the current word, or if between words,
the start of the previous word. Word boundaries are defined by a configurable
set of characters.

- Cmd: `<Ctrl+LeftArrow>`
- Emacs: `<Alt+b>`, `<Escape,b>`
- Vi insert mode: `<Ctrl+LeftArrow>`
- Vi command mode: `<Ctrl+LeftArrow>`

### BeginningOfLine

If the input has multiple lines, move to the start of the current line, or if
already at the start of the line, move to the start of the input. If the input
has a single line, move to the start of the input.

- Cmd: `<Home>`
- Emacs: `<Home>`, `<Ctrl+a>`
- Vi insert mode: `<Home>`
- Vi command mode: `<Home>`

### EndOfLine

If the input has multiple lines, move to the end of the current line, or if
already at the end of the line, move to the end of the input. If the input has
a single line, move to the end of the input.

- Cmd: `<End>`
- Emacs: `<End>`, `<Ctrl+e>`
- Vi insert mode: `<End>`

### ForwardChar

Move the cursor one character to the right. This may move the cursor to the
next line of multi-line input.

- Cmd: `<RightArrow>`
- Emacs: `<RightArrow>`, `<Ctrl+f>`

### ForwardWord

Move the cursor forward to the end of the current word, or if between words,
to the end of the next word. Word boundaries are defined by a configurable set
of characters.

- Emacs: `<Alt+f>`, `<Escape,f>`

### GotoBrace

Go to the matching brace, parenthesis, or square bracket.

- Cmd: `<Ctrl+]>`
- Vi insert mode: `<Ctrl+]>`
- Vi command mode: `<Ctrl+]>`

### GotoColumn

Move to the column indicated by arg.

- Vi command mode: `<|>`

### GotoFirstNonBlankOfLine

Move the cursor to the first non-blank character in the line.

- Vi command mode: `<^>`, `<_>`

### MoveToEndOfLine

Move the cursor to the end of the input.

- Vi command mode: `<End>`, `<$>`

### NextLine

Move the cursor to the next line.

- Function is unbound.

### NextWord

Move the cursor forward to the start of the next word. Word boundaries are
defined by a configurable set of characters.

- Cmd: `<Ctrl+RightArrow>`
- Vi insert mode: `<Ctrl+RightArrow>`
- Vi command mode: `<Ctrl+RightArrow>`

### NextWordEnd

Move the cursor forward to the end of the current word, or if between words,
to the end of the next word. Word boundaries are defined by a configurable set
of characters.

- Vi command mode: `<e>`

### PreviousLine

Move the cursor to the previous line.

- Function is unbound.

### ShellBackwardWord

Move the cursor back to the start of the current word, or if between words,
the start of the previous word. Word boundaries are defined by PowerShell
tokens.

- Function is unbound.

### ShellForwardWord

Move the cursor forward to the start of the next word. Word boundaries are
defined by PowerShell tokens.

- Function is unbound.

### ShellNextWord

Move the cursor forward to the end of the current word, or if between words,
to the end of the next word. Word boundaries are defined by PowerShell tokens.

- Function is unbound.

### ViBackwardChar

Move the cursor one character to the left in the Vi edit mode. This may move
the cursor to the previous line of multi-line input.

- Vi insert mode: `<LeftArrow>`
- Vi command mode: `<LeftArrow>`, `<Backspace>`, `<h>`

### ViBackwardWord

Move the cursor back to the start of the current word, or if between words,
the start of the previous word. Word boundaries are defined by a configurable
set of characters.

- Vi command mode: `<b>`

### ViForwardChar

Move the cursor one character to the right in the Vi edit mode. This may move
the cursor to the next line of multi-line input.

- Vi insert mode: `<RightArrow>`
- Vi command mode: `<RightArrow>`, `<Spacebar>`, `<l>`

### ViEndOfGlob

Moves the cursor to the end of the word, using only whitespace as delimiters.

- Vi command mode: `<E>`

### ViEndOfPreviousGlob

Moves to the end of the previous word, using only whitespace as a word
delimiter.

- Function is unbound.

### ViGotoBrace

Similar to GotoBrace, but is character based instead of token based.

- Vi command mode: `<%>`

### ViNextGlob

Moves to the next word, using only whitespace as a word delimiter.

- Vi command mode: `<W>`

### ViNextWord

Move the cursor forward to the start of the next word. Word boundaries are
defined by a configurable set of characters.

- Vi command mode: `<w>`

## History functions

### BeginningOfHistory

Move to the first item in the history.

- Emacs: `<Alt+<>`

### ClearHistory

Clears history in PSReadLine. This does not affect PowerShell history.

- Cmd: `<Alt+F7>`

### EndOfHistory

Move to the last item (the current input) in the history.

- Emacs: `<Alt+>>`

### ForwardSearchHistory

Perform an incremental forward search through history.

- Cmd: `<Ctrl+s>`
- Emacs: `<Ctrl+s>`
- Vi insert mode: `<Ctrl+s>`
- Vi command mode: `<Ctrl+s>`

### HistorySearchBackward

Replace the current input with the 'previous' item from PSReadLine history
that matches the characters between the start and the input and the cursor.

- Cmd: `<F8>`

### HistorySearchForward

Replace the current input with the 'next' item from PSReadLine history that
matches the characters between the start and the input and the cursor.

- Cmd: `<Shift+F8>`

### NextHistory

Replace the current input with the 'next' item from PSReadLine history.

- Cmd: `<DownArrow>`
- Emacs: `<DownArrow>`, `<Ctrl+n>`
- Vi insert mode: `<DownArrow>`
- Vi command mode: `<DownArrow>`, `<j>`, `<+>`

### PreviousHistory

Replace the current input with the 'previous' item from PSReadLine history.

- Cmd: `<UpArrow>`
- Emacs: `<UpArrow>`, `<Ctrl+p>`
- Vi insert mode: `<UpArrow>`
- Vi command mode: `<UpArrow>`, `<k>`, `<->`

### ReverseSearchHistory

Perform an incremental backward search through history.

- Cmd: `<Ctrl+r>`
- Emacs: `<Ctrl+r>`
- Vi insert mode: `<Ctrl+r>`
- Vi command mode: `<Ctrl+r>`

### ViSearchHistoryBackward

Prompts for a search string and initiates search upon AcceptLine.

- Vi command mode: `</>`

## Completion functions

### Complete

Attempt to perform completion on the text surrounding the cursor. If there are
multiple possible completions, the longest unambiguous prefix is used for
completion. If trying to complete the longest unambiguous completion, a list
of possible completions is displayed.

- Emacs: `<Tab>`

### MenuComplete

Attempt to perform completion on the text surrounding the cursor. If there are
multiple possible completions, the longest unambiguous prefix is used for
completion. If trying to complete the longest unambiguous completion, a list
of possible completions is displayed.

- Cmd: `<Ctrl+@>`, `<Ctrl+Spacebar>`
- Emacs: `<Ctrl+Spacebar>`

### PossibleCompletions

Display the list of possible completions.

- Emacs: `<Alt+=>`
- Vi insert mode: `<Ctrl+Spacebar>`
- Vi command mode: `<Ctrl+Spacebar>`

### TabCompleteNext

Attempt to complete the text surrounding the cursor with the next available
completion.

- Cmd: `<Tab>`
- Vi command mode: `<Tab>`

### TabCompletePrevious

Attempt to complete the text surrounding the cursor with the previous
available completion.

- Cmd: `<Shift+Tab>`
- Vi command mode: `<Shift+Tab>`

### ViTabCompleteNext

Ends the current edit group, if needed, and invokes TabCompleteNext.

- Vi insert mode: `<Tab>`

### ViTabCompletePrevious

Ends the current edit group, if needed, and invokes TabCompletePrevious.

- Vi insert mode: `<Shift+Tab>`

## Prediction functions

### AcceptNextSuggestionWord

When using `InlineView` as the view style for prediction, accept the next word of the inline suggestion.

- Function is unbound.

### AcceptSuggestion

When using `InlineView` as the view style for prediction, accept the current inline suggestion.

- Function is unbound.

### NextSuggestion

When using `ListView` as the view style for prediction, navigate to the next suggestion in the list.

- Function is unbound.

### PreviousSuggestion

When using `ListView` as the view style for prediction, navigate to the previous suggestion in the list.

- Function is unbound.

### SwitchPredictionView

Switch the view style for prediction between `InlineView` and `ListView`.

- Cmd: `<F2>`

## Miscellaneous functions

### CaptureScreen

Start interactive screen capture - up/down arrows select lines, enter copies
selected text to clipboard as text and HTML.

- Function is unbound.

### ClearScreen

Clear the screen and draw the current line at the top of the screen.

- Cmd: `<Ctrl+l>`
- Emacs: `<Ctrl+l>`
- Vi insert mode: `<Ctrl+l>`
- Vi command mode: `<Ctrl+l>`

### DigitArgument

Start a new digit argument to pass to other functions.

- Cmd: `<Alt+0>`, `<Alt+1>`, `<Alt+2>`, `<Alt+3>`, `<Alt+4>`, `<Alt+5>`,
  `<Alt+6>`, `<Alt+7>`, `<Alt+8>`, `<Alt+9>`, `<Alt+->`
- Emacs: `<Alt+0>`, `<Alt+1>`, `<Alt+2>`, `<Alt+3>`, `<Alt+4>`, `<Alt+5>`,
  `<Alt+6>`, `<Alt+7>`, `<Alt+8>`, `<Alt+9>`, `<Alt+->`
- Vi command mode: `<0>`, `<1>`, `<2>`, `<3>`, `<4>`, `<5>`, `<6>`, `<7>`,
  `<8>`, `<9>`

### InvokePrompt

Erases the current prompt and calls the prompt function to redisplay the
prompt. Useful for custom key handlers that change state. For example, change
the current directory.

- Function is unbound.

### ScrollDisplayDown

Scroll the display down one screen.

- Cmd: `<PageDown>`
- Emacs: `<PageDown>`

### ScrollDisplayDownLine

Scroll the display down one line.

- Cmd: `<Ctrl+PageDown>`
- Emacs: `<Ctrl+PageDown>`

### ScrollDisplayToCursor

Scroll the display to the cursor.

- Emacs: `<Ctrl+End>`

### ScrollDisplayTop

Scroll the display to the top.

- Emacs: `<Ctrl+Home>`

### ScrollDisplayUp

Scroll the display up one screen.

- Cmd: `<PageUp>`
- Emacs: `<PageUp>`

### ScrollDisplayUpLine

Scroll the display up one line.

- Cmd: `<Ctrl+PageUp>`
- Emacs: `<Ctrl+PageUp>`

### SelfInsert

Insert the key.

- Function is unbound.

### ShowCommandHelp

Provides a view of full cmdlet help. When the cursor is at the end of a
fully-expanded parameter, hitting the `<F1>` key positions the display of help
at the location of that parameter.

The help is displayed on an alternate screen buffer using a Pager from
**Microsoft.PowerShell.Pager**. When you exit the pager you are returned to the
original cursor position on the original screen. This pager only works in
modern terminal applications such as
[Windows Terminal](https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701).

- Cmd: `<F1>`
- Emacs: `<F1>`
- Vi insert mode: `<F1>`
- Vi command mode: `<F1>`

### ShowKeyBindings

Show all bound keys.

- Cmd: `<Ctrl+Alt+?>`
- Emacs: `<Ctrl+Alt+?>`
- Vi insert mode: `<Ctrl+Alt+?>`

### ShowParameterHelp

Provides dynamic help for parameters by showing it below the current command
line like `MenuComplete`. The cursor must be at the end of the fully-expanded
parameter name when you press the `<Alt+h>` key.

- Cmd: `<Alt+h>`
- Emacs: `<Alt+h>`
- Vi insert mode: `<Alt+h>`
- Vi command mode: `<Alt+h>`

### ViCommandMode

Switch the current operating mode from Vi-Insert to Vi-Command.

- Vi insert mode: `<Escape>`

### ViDigitArgumentInChord

Start a new digit argument to pass to other functions while in one of vi's
chords.

- Function is unbound.

### ViEditVisually

Edit the command line in a text editor specified by $env:EDITOR or
$env:VISUAL.

- Emacs: `<Ctrl+x,Ctrl+e>`
- Vi command mode: `<v>`

### ViExit

Exits the shell.

- Function is unbound.

### ViInsertMode

Switch to Insert mode.

- Vi command mode: `<i>`

### WhatIsKey

Read a key and tell me what the key is bound to.

- Cmd: `<Alt+?>`
- Emacs: `<Alt+?>`

## Selection functions

### ExchangePointAndMark

The cursor is placed at the location of the mark and the mark is moved to the
location of the cursor.

- Emacs: `<Ctrl+x,Ctrl+x>`

### SelectAll

Select the entire line.

- Cmd: `<Ctrl+a>`

### SelectBackwardChar

Adjust the current selection to include the previous character.

- Cmd: `<Shift+LeftArrow>`
- Emacs: `<Shift+LeftArrow>`

### SelectBackwardsLine

Adjust the current selection to include from the cursor to the start of the
line.

- Cmd: `<Shift+Home>`
- Emacs: `<Shift+Home>`

### SelectBackwardWord

Adjust the current selection to include the previous word.

- Cmd: `<Shift+Ctrl+LeftArrow>`
- Emacs: `<Alt+B>`

### SelectCommandArgument

Make visual selection of the command arguments. Selection of arguments is scoped
within a script block. Based on the cursor position, it searches from the innermost
script block to the outmost script block, and stops when it finds any arguments
in a script block scope.

This function honors DigitArgument. It treats the positive or negative argument
values as the forward or backward offsets from the currently selected argument,
or from the current cursor position when no argument is selected.

- Cmd: `<Alt+a>`
- Emacs: `<Alt+a>`

### SelectForwardChar

Adjust the current selection to include the next character.

- Cmd: `<Shift+RightArrow>`
- Emacs: `<Shift+RightArrow>`

### SelectForwardWord

Adjust the current selection to include the next word using ForwardWord.

- Emacs: `<Alt+F>`

### SelectLine

Adjust the current selection to include from the cursor to the end of the line.

- Cmd: `<Shift+End>`
- Emacs: `<Shift+End>`

### SelectNextWord

Adjust the current selection to include the next word.

- Cmd: `<Shift+Ctrl+RightArrow>`

### SelectShellBackwardWord

Adjust the current selection to include the previous word using
ShellBackwardWord.

- Function is unbound.

### SelectShellForwardWord

Adjust the current selection to include the next word using ShellForwardWord.

- Function is unbound.

### SelectShellNextWord

Adjust the current selection to include the next word using ShellNextWord.

- Function is unbound.

### SetMark

Mark the current location of the cursor for use in a subsequent editing
command.

- Emacs: `<Ctrl+@>`

## Predictive IntelliSense functions

> [!NOTE]
> Predictive IntelliSense needs to be enabled to use these functions.

### AcceptNextWordSuggestion

Accepts the next word of the inline suggestion from Predictive IntelliSense.
This function can be bound with <kbd>Ctrl</kbd>+<kbd>F</kbd> by running the
following command.

```powershell
Set-PSReadLineKeyHandler -Chord "Ctrl+f" -Function ForwardWord
```

### AcceptSuggestion

Accepts the current inline suggestion from Predictive IntelliSense by pressing
<kbd>RightArrow</kbd> when the cursor is at the end of the current line.

## Search functions

### CharacterSearch

Read a character and search forward for the next occurrence of that character.
If an argument is specified, search forward (or backward if negative) for the
nth occurrence.

- Cmd: `<F3>`
- Emacs: `<Ctrl+]>`
- Vi insert mode: `<F3>`
- Vi command mode: `<F3>`

### CharacterSearchBackward

Read a character and search backward for the next occurrence of that character. If an
argument is specified, search backward (or forward if negative) for the nth
occurrence.

- Cmd: `<Shift+F3>`
- Emacs: `<Ctrl+Alt+]>`
- Vi insert mode: `<Shift+F3>`
- Vi command mode: `<Shift+F3>`

### RepeatLastCharSearch

Repeat the last recorded character search.

- Vi command mode: `<;>`

### RepeatLastCharSearchBackwards

Repeat the last recorded character search, but in the opposite direction.

- Vi command mode: `<,>`

### RepeatSearch

Repeat the last search in the same direction as before.

- Vi command mode: `<n>`

### RepeatSearchBackward

Repeat the last search in the same direction as before.

- Vi command mode: `<N>`

### SearchChar

Read the next character and then find it, going forward, and then back off a
character. This is for 't' functionality.

- Vi command mode: `<f>`

### SearchCharBackward

Read the next character and then find it, going backward, and then back off a
character. This is for 'T' functionality.

- Vi command mode: `<F>`

### SearchCharBackwardWithBackoff

Read the next character and then find it, going backward, and then back off a
character. This is for 'T' functionality.

- Vi command mode: `<T>`

### SearchCharWithBackoff

Read the next character and then find it, going forward, and then back off a
character. This is for 't' functionality.

- Vi command mode: `<t>`

### SearchForward

Prompts for a search string and initiates search upon AcceptLine.

- Vi command mode: `<?>`

## Custom Key Bindings

PSReadLine supports custom key bindings using the cmdlet
`Set-PSReadLineKeyHandler`. Most custom key bindings call one of the above
functions, for example

```powershell
Set-PSReadLineKeyHandler -Key UpArrow -Function HistorySearchBackward
```

You can bind a ScriptBlock to a key. The ScriptBlock can do pretty much
anything you want. Some useful examples include

- edit the command line
- opening a new window (for example, help)
- change directories without changing the command line

The ScriptBlock receives two arguments:

- `$key` - A **[ConsoleKeyInfo]** object that is the key that triggered the
  custom binding. If you bind the same ScriptBlock to multiple keys and need
  to perform different actions depending on the key, you can check $key. Many
  custom bindings ignore this argument.

- `$arg` - An arbitrary argument. Most often, this would be an integer
  argument that the user passes from the key bindings DigitArgument. If your
  binding doesn't accept arguments, it's reasonable to ignore this argument.

Let's take a look at an example that adds a command line to history without
executing it. This is useful when you realize you forgot to do something, but
don't want to re-enter the command line you've already entered.

```powershell
$parameters = @{
    Key = 'Alt+w'
    BriefDescription = 'SaveInHistory'
    LongDescription = 'Save current line in history but do not execute'
    ScriptBlock = {
      param($key, $arg)   # The arguments are ignored in this example

      # GetBufferState gives us the command line (with the cursor position)
      $line = $null
      $cursor = $null
      [Microsoft.PowerShell.PSConsoleReadLine]::GetBufferState([ref]$line,
        [ref]$cursor)

      # AddToHistory saves the line in history, but does not execute it.
      [Microsoft.PowerShell.PSConsoleReadLine]::AddToHistory($line)

      # RevertLine is like pressing Escape.
      [Microsoft.PowerShell.PSConsoleReadLine]::RevertLine()
  }
}
Set-PSReadLineKeyHandler @parameters
```

You can see many more examples in the file `SamplePSReadLineProfile.ps1` which
is installed in the PSReadLine module folder.

Most key bindings use some helper functions for editing the command line.
Those APIs are documented in the next section.

## Custom Key Binding Support APIs

The following functions are public in Microsoft.PowerShell.PSConsoleReadLine,
but cannot be directly bound to a key. Most are useful in custom key bindings.

```csharp
void AddToHistory(string command)
```

Add a command line to history without executing it.

```csharp
void ClearKillRing()
```

Clear the kill-ring.  This is mostly used for testing.

```csharp
void Delete(int start, int length)
```

Delete length characters from start.  This operation supports undo/redo.

```csharp
void Ding()
```

Perform the Ding action based on the users preference.

```csharp
void GetBufferState([ref] string input, [ref] int cursor)
void GetBufferState([ref] Ast ast, [ref] Token[] tokens,
  [ref] ParseError[] parseErrors, [ref] int cursor)
```

These two functions retrieve useful information about the current state of
the input buffer.  The first is more commonly used for simple cases.  The
second is used if your binding is doing something more advanced with the Ast.

```csharp
IEnumerable[Microsoft.PowerShell.KeyHandler]
  GetKeyHandlers(bool includeBound, bool includeUnbound)

IEnumerable[Microsoft.PowerShell.KeyHandler]
  GetKeyHandlers(string[] Chord)
```

These two functions are used by `Get-PSReadLineKeyHandler`. The first is used to get all key
bindings. The second is used to get specific key bindings.

```csharp
Microsoft.PowerShell.PSConsoleReadLineOptions GetOptions()
```

This function is used by Get-PSReadLineOption and probably isn't too useful in
a custom key binding.

```csharp
void GetSelectionState([ref] int start, [ref] int length)
```

If there is no selection on the command line, the function returns -1 in both
start and length. If there is a selection on the command line, the start and
length of the selection are returned.

```csharp
void Insert(char c)
void Insert(string s)
```

Insert a character or string at the cursor.  This operation supports undo/redo.

```csharp
string ReadLine(runspace remoteRunspace,
  System.Management.Automation.EngineIntrinsics engineIntrinsics)
```

This is the main entry point to PSReadLine. It does not support recursion, so
is not useful in a custom key binding.

```csharp
void RemoveKeyHandler(string[] key)
```

This function is used by Remove-PSReadLineKeyHandler and probably isn't too
useful in a custom key binding.

```csharp
void Replace(int start, int length, string replacement)
```

Replace some of the input. This operation supports undo/redo. This is
preferred over Delete followed by Insert because it is treated as a single
action for undo.

```csharp
void SetCursorPosition(int cursor)
```

Move the cursor to the given offset. Cursor movement is not tracked for undo.

```csharp
void SetOptions(Microsoft.PowerShell.SetPSReadLineOption options)
```

This function is a helper method used by the cmdlet Set-PSReadLineOption, but
might be useful to a custom key binding that wants to temporarily change a
setting.

```csharp
bool TryGetArgAsInt(System.Object arg, [ref] int numericArg,
  int defaultNumericArg)
```

This helper method is used for custom bindings that honor DigitArgument. A
typical call looks like

```powershell
[int]$numericArg = 0
[Microsoft.PowerShell.PSConsoleReadLine]::TryGetArgAsInt($arg,
  [ref]$numericArg, 1)
```

## Notes

### Command History

PSReadLine maintains a history file containing all the commands and data you
have entered from the command line. The history files is a file named
`$($host.Name)_history.txt`. On Windows systems the history file is stored at
`$env:APPDATA\Microsoft\Windows\PowerShell\PSReadLine`. On non-Windows systems,
the history files is stored at `$env:XDG_DATA_HOME/powershell/PSReadLine` or
`$env:HOME/.local/share/powershell/PSReadLine`.

The history can contain sensitive data including passwords. PSReadLine attempts
to filter out sensitive information. Any command lines containing the following
strings are not written to the history file.

- password
- asplaintext
- token
- apikey
- secret

PSReadLine 2.2.0 improves the filtering of sensitive data in the following ways:

- Uses the PowerShell Abstract Syntax Tree (AST) of the parsed command line to
  look for sensitive data.
- Uses an allowlist of safe cmdlets from the **SecretManagement** module to
  allow those commands to be added to the history. The allowlist contains:
  - `Get-Secret`
  - `Get-SecretInfo`
  - `Get-SecretVault`
  - `Register-SecretVault`
  - `Remove-Secret`
  - `Set-SecretInfo`
  - `Set-SecretVaultDefault`
  - `Test-SecretVault`
  - `Unlock-SecretVault`
  - `Unregister-SecretVault`

For example, the following commands are allowed to be written to the history
file:

```powershell
Get-Secret PSGalleryApiKey -AsPlainText # Get-Secret is in the allowlist
$token = Get-Secret -Name github-token -Vault MySecret
[MyType]::CallRestAPI($token, $url, $args)
$template -f $token
```

The following command will not be written to the history file:

```powershell
$token = 'abcd' # Assign expr-value to sensitive variable name.
Set-Secret abc $mySecret # Set-Secret is not in the allowlist.
ConvertTo-SecureString stringValue -AsPlainText # '-AsPlainText' is an alert.
Invoke-WebRequest -Token xxx # Expr-value as argument to '-Token'.
Get-ResultFromTwo -Secret1 (Get-Secret -Name blah -AsPlainText) -Secret2 sdv87ysdfayf798hfasd8f7ha # '-Secret2' has expr-value argument.
```

### Behavior of the OnIdle event

When PSReadLine is in use, the **OnIdle** event is fired when `ReadKey()` times out (no typing in
300ms). The event could be signaled while the user is in the middle of editing a command line, for
example, the user is reading help to decide which parameter to use.

Beginning in PSReadLine 2.2.0-beta4, **OnIdle** behavior changed to signal the event only if there
is a `ReadKey()` timeout and the current editing buffer is empty.

### Feedback & Contributing To PSReadLine

[PSReadLine on GitHub](https://github.com/PowerShell/PSReadLine)

Feel free to submit a pull request or submit feedback on the GitHub page.

## See Also

PSReadLine is heavily influenced by the GNU
[readline](https://tiswww.case.edu/php/chet/readline/rltop.html) library.
