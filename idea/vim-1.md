On [Unix-like](https://www.computerhope.com/jargon/u/unix-like.htm) operating systems, **vim**, which stands for "[Vi](https://www.computerhope.com/unix/uvi.htm) Improved", is a [text](https://www.computerhope.com/jargon/t/text.htm) [editor](https://www.computerhope.com/jargon/e/editor.htm). It can be used for editing any kind of text and is especially suited for editing computer [programs](https://www.computerhope.com/jargon/p/program.htm).

## Description

**vim** is a text editor that is upwards compatible to **Vi**. There are a lot of enhancements above **Vi**: multi level [undo](https://www.computerhope.com/jargon/u/undo.htm), multiple windows and buffers, [syntax](https://www.computerhope.com/jargon/s/syntax.htm) highlighting, [command line](https://www.computerhope.com/jargon/c/commandi.htm) editing, [file name](https://www.computerhope.com/jargon/f/filename.htm) completion, a complete help system, visual selection, and others.

## Starting vim

Most often, **vim** is started to edit a single file using the following command.

```
vim file
```

More generally, the syntax for starting **vim** is as follows:

```
vim [options] [filelist]
```

If the *filelist* is missing, the editor will start with an empty [buffer](https://www.computerhope.com/jargon/b/buffer.htm). Otherwise, one out of the following four options may be used to choose one or more files to be edited.

## Main Options

| *file*...            | A list of one or more file names. The first one will be the current file and read into the buffer. The [cursor](https://www.computerhope.com/jargon/c/cursor.htm) will be positioned on the first line of the buffer. You can get to the other files with the "**:next**" command. To edit a file that starts with a dash, precede the filelist with a double dash ("**--**"). |
| -------------------- | ------------------------------------------------------------ |
| **-**                | A single dash specifies that the file to edit is to be read from [standard input](https://www.computerhope.com/jargon/s/stdin.htm). |
| **-t** {*tag*}       | The file to edit and the initial cursor position depends on a "tag", a sort of [goto](https://www.computerhope.com/jargon/g/goto.htm) label. The {*tag*} is looked up in the tags file, the associated file becomes the current file and the associated command is executed. Mostly this is used for [C](https://www.computerhope.com/jargon/c/c.htm) programs, in which case {*tag*} could be a [function](https://www.computerhope.com/jargon/f/function.htm) name. The effect is that the file containing that function becomes the current file and the cursor is positioned on the start of the function. For more information within **vim**, use the command "**:help tag-commands**". |
| **-q** [*errorfile*] | Start in quickFix mode. The file *errorfile* is read and the first error is displayed. If *errorfile* is omitted, the file name is obtained from the '**errorfile**' option (defaults to "**errors.err**" on most systems). Further errors can be jumped to with the "**:cn**" command. For more information within **vim**, use the command "**:help quickfix**". |

## Invoking vim

**vim** behaves differently depending on the name of the command used to invoke it. For example, if you create a [symbolic link](https://www.computerhope.com/jargon/s/symblink.htm) to the **vim** [executable](https://www.computerhope.com/jargon/e/execfile.htm) with one of the following names, it will behave in the following fashion:

**command name****behavior**

|                                            |                                                              |
| ------------------------------------------ | ------------------------------------------------------------ |
| **vim**                                    | "Normal" execution. Everything is default.                   |
| **ex**                                     | Start in [Ex](https://www.computerhope.com/unix/uex.htm) mode. Go to Normal mode with the "**:vi**" command. Can also be done with the "**-e**" [argument](https://www.computerhope.com/jargon/a/argument.htm). |
| **view**                                   | Start in read-only mode. You will be protected from writing the files. Can also be done with the "**-R**" argument. |
| **gvim**, **gview**                        | The [GUI](https://www.computerhope.com/jargon/g/gui.htm) version (if installed). Starts a new window. Can also be done with the "**-g**" argument. |
| **evim**, **eview**                        | Runs GUI vim in "easy mode". This command is a simplified mode of **vim** operation, which is a lot like a normal text editor. This is the same as running **vim** with the "**-y**" argument. |
| **rvim**, **rview**, **rgvim**, **rgview** | Like the above, but running in "restricted" mode. It will not be possible to start [shell](https://www.computerhope.com/jargon/s/shell.htm) commands from within **vim**, or to suspend **vim**. This is the same as specifying the "**-Z**" argument. |

## Syntax

```
vim [options] [file ..]
vim [options] -
vim [options] -t tag
vim [options] -q [errorfile]
```

## Additional Options

The options may be given in any order, before or after file names. Options without an argument can be combined after a single dash.

| **+**[*num*]                         | For the first file the cursor will be positioned on line *num*. If *num* is missing, the cursor will be positioned on the last line. |
| ------------------------------------ | ------------------------------------------------------------ |
| **+**/{*pat*}                        | For the first file the cursor will be positioned on the first occurrence of {*pat*}. From within <v> vim, use the "**:help search-pattern**" command for the available search patterns. |
| **+**{*command*}, **-c** {*command*} | {*command*} will be executed after the first file has been read. {*command*} is interpreted as an [ex](https://www.computerhope.com/unix/uex.htm) command. If the {*command*} contains spaces it must be enclosed in double quotes (this depends on the [shell](https://www.computerhope.com/jargon/s/shell.htm) that is used). For example:  `vim "+set si" main.c`You can use up to 10 "**+**" or "**-c**" commands. |
| **-S** {*file*}                      | {*file*} will be sourced after the first file has been read. This is equivalent to **-c "source {file}"**. {*file*} cannot start with '**-**'. If {*file*} is omitted, **"Session.vim"** is used (only works when **-S** is the last argument). |
| **--cmd** {*command*}                | Like using "**-c**", but the command is executed just before processing any **vimrc** file. You can use up to 10 of these commands, independently from "**-c**" commands. |
| **-A**                               | If **vim** has been compiled with Arabic support for editing right-to-left oriented files and Arabic keyboard mapping, this option starts **vim** in Arabic mode, i.e. '**arabic**' is set. Otherwise, an error message is given and **vim** aborts. |
| **-b**                               | [Binary](https://www.computerhope.com/jargon/b/binary.htm) mode. A few options will be set that makes it possible to edit a binary or executable file. |
| **-C**                               | Compatible mode. Sets the '**compatible**' option. This will make **vim** behave mostly like [Vi](https://www.computerhope.com/unix/uvi.htm), even though a **.vimrc** file exists. |
| **-d**                               | Start in [diff](https://www.computerhope.com/jargon/d/diff.htm) mode. There should be two, three or four file name arguments. **vim** will open all the files and show differences between them. Works like **vimdiff**. |
| **-d** {*device*}                    | Open {*device*} for use as a [terminal](https://www.computerhope.com/jargon/t/terminal.htm) (only on the [Amiga](https://www.computerhope.com/jargon/a/amiga.htm)). |
| **-D**                               | [Debugging](https://www.computerhope.com/jargon/d/debug.htm) mode. Go to debugging mode when executing the first command from a [script](https://www.computerhope.com/jargon/s/script.htm). |
| **-e**                               | Start **vim** in **ex** mode, just like if the executable is called "**ex**". |
| **-E**                               | Start **vim** in improved **ex** mode, just like if the executable was called "**exim**". |
| **-f**                               | Foreground mode. For the GUI version, **vim** will not [fork](https://www.computerhope.com/jargon/f/fork.htm) and detach from the shell it was started in. On the Amiga, **vim** is not restarted to open a new window. This option should be used when **vim** is executed by a program that will wait for the edit session to finish (e.g., [mail](https://www.computerhope.com/unix/umail.htm)). On the Amiga the "**:sh**" and "**:!**" commands will not work. |
| **--nofork**                         | Foreground mode. For the GUI version, **vim** will not fork and detach from the shell it was started in. |
| **-F**                               | If **vim** has been compiled with FKMAP support for editing right-to-left oriented files and Farsi keyboard mapping, this option starts **vim** in Farsi mode, i.e. '**fkmap**' and '**rightleft**' are set. Otherwise, an error message is given and **vim** aborts. |
| **-g**                               | If **vim** has been compiled with GUI support, this option enables the GUI. If no GUI support was compiled in, an error message is given and vim aborts. |
| **-h**                               | Give a bit of help about the command line arguments and options. After this **vim** exits. |
| **-H**                               | If **vim** has been compiled with **RIGHTLEFT** support for editing right-to-left oriented files and Hebrew keyboard mapping, this option starts **vim** in Hebrew mode, i.e. '**hkmap**' and '**rightleft**' are set. Otherwise, an error message is given and **vim** aborts. |
| **-i** {*viminfo*}                   | When using the *viminfo* file is enabled, this option sets the file name to use, instead of the default "**~/.viminfo**". This can also be used to skip the use of the **.viminfo** file, by giving the name "**NONE**". |
| **-L**                               | Same as **-r**.                                              |
| **-l**                               | [Lisp](https://www.computerhope.com/jargon/l/lisp.htm) mode. Sets the '**lisp**' and '**showmatch**' options on. |
| **-m**                               | Modifying files is disabled. Resets the '**write**' option. You can still modify the buffer, but writing a file is not possible. |
| **-M**                               | Modifications not allowed. The '**modifiable**' and '**write**' options will be unset, so that changes are not allowed and files can not be written. Note that these options can be set to enable making modifications. |
| **-N**                               | No-compatible mode. Reset the '**compatible**' option. This will make **vim** behave a bit better, but less **Vi** compatible, even though a **.vimrc** file does not exist. |
| **-n**                               | No swap file will be used. Recovery after a crash will be impossible. Handy if you want to edit a file on a very slow medium (e.g., floppy). Can also be done with "**:set uc=0**". Can be undone with "**:set uc=200**". |
| **-nb**                              | Become an editor server for NetBeans.                        |
| **-o**[*N*]                          | Open *N* windows stacked. When *N* is omitted, open one window for each file. |
| **-O**[*N*]                          | Open *N* windows side by side. When *N* is omitted, open one window for each file. |
| **-p**[*N*]                          | Open *N* tab pages. When *N* is omitted, open one tab page for each file. |
| **-R**                               | Read-only mode. The '**readonly**' option will be set. You can still edit the buffer, but will be prevented from accidently overwriting a file. If you do want to overwrite a file, add an [exclamation mark](https://www.computerhope.com/jargon/e/exclamation-mark.htm) to the **Ex** command, as in "**:w!**". The **-R** option also implies the **-n** option (see below). The '**readonly**' option can be reset with "**:set noro**". See "**:help 'readonly'**". |
| **-r**                               | List swap files, with information about using them for recovery. |
| **-r** {*file*}                      | Recovery mode. The swap file is used to recover a crashed editing session. The swap file is a file with the same file name as the text file with "**.swp**" appended. See "**:help recovery**". |
| **-s**                               | Silent mode. Only when started as "**Ex**" or when the "**-e**" option was given before the "**-s**" option. |
| **-s** {*scriptin*}                  | The script file {*scriptin*} is read. The [characters](https://www.computerhope.com/jargon/c/charact.htm) in the file are interpreted as if you had typed them. The same can be done with the command "**:source! {scriptin}**". If the end of the file is reached before the editor exits, further characters are read from the keyboard. |
| **-T** {*terminal*}                  | Tells **vim** the name of the terminal you are using. Only required when the automatic way doesn't work. Should be a terminal known to **vim** (builtin) or defined in the **termcap** or **terminfo** file. |
| **-u** {*vimrc*}                     | Use the commands in the file {*vimrc*} for initializations. All the other initializations are skipped. Use this to edit a special kind of files. It can also be used to skip all initializations by giving the name "**NONE**". See "**:help initialization**" within vim for more details. |
| **-U** {*gvimrc*}                    | Use the commands in the file {*gvimrc*} for GUI initializations. All the other GUI initializations are skipped. It can also be used to skip all GUI initializations by giving the name "**NONE**". See "**:help gui-init**" within **vim** for more details. |
| **-V**[*N*]                          | [Verbose](https://www.computerhope.com/jargon/v/verbose.htm). Give messages about which files are sourced and for reading and writing a **viminfo** file. The optional number *N* is the value for '**verbose**'. Default is **10**. |
| **-v**                               | Start **vim** in **Vi** mode, just like the executable was called "**vi**". This only has effect when the executable is called "**ex**". |
| **-w** {*scriptout*}                 | All the characters that you type are recorded in the file {*scriptout*}, until you exit **vim**. This is useful if you want to create a script file to be used with "**vim -s**" or "**:source!**". If the {*scriptout*} file exists, characters are appended. |
| **-W** {*scriptout*}                 | Like **-w**, but an existing file is overwritten.            |
| **-x**                               | Use [encryption](https://www.computerhope.com/jargon/e/encrypt.htm) when writing files. Will prompt for a crypt key. |
| **-X**                               | Don't connect to the [X](https://www.computerhope.com/jargon/x/xwin.htm) server. Shortens startup time in a terminal, but the window title and clipboard will not be used. |
| **-y**                               | Start **vim** in easy mode, just like the executable was called "**evim**" or "**eview**". Makes **vim** behave like a click-and-type editor. |
| **-Z**                               | Restricted mode. Works like the executable starts with "**r**". |
| **--**                               | Denotes the end of the options. Arguments after this will be handled as a file name. This can be used to edit a file name that starts with a '**-**'. |
| **--echo-wid**                       | GTK GUI only: Echo the Window ID on standard output.         |
| **--help**                           | Give a help message and exit, just like "**-h**".            |
| **--literal**                        | Take file name arguments literally, do not expand [wildcards](https://www.computerhope.com/jargon/w/wildcard.htm). This has no effect on [Unix](https://www.computerhope.com/jargon/u/unix.htm) where the shell expands wildcards. |
| **--noplugin**                       | Skip loading plugins. Implied by **-u NONE**.                |
| **--remote**                         | Connect to a **vim** server and make it edit the files given in the rest of the arguments. If no server is found a warning is given and the files are edited in the current **vim**. |
| **--remote-expr** {*expr*}           | Connect to a **vim** server, evaluate {*expr*} in it and print the result on stdout. |
| **--remote-send** {*keys*}           | Connect to a **vim** server and send {*keys*} to it.         |
| **--remote-silent**                  | As **--remote**, but without the warning when no server is found. |
| **--remote-wait**                    | As **--remote**, but **vim** does not exit until the files have been edited. |
| **--remote-wait-silent**             | As **--remote-wait**, but without the warning when no [server](https://www.computerhope.com/jargon/s/server.htm) is found. |
| **--serverlist**                     | List the names of all **vim** servers that can be found.     |
| **--servername** {*name*}            | Use {*name*} as the server name. Used for the current **vim**, unless used with a **--remote** argument, then it's the name of the server to connect to. |
| **--socketid** {*id*}                | GTK GUI only: Use the **GtkPlug** mechanism to run **gvim** in another window. |
| **--version**                        | Print version information, and exit.                         |

## Accessing Help From Within vim

Type "**:help**" in **vim** to get started. Type "**:help subject**" to get help on a specific subject. For example: "**:help ZZ**" to get help for the "**ZZ**" command. Use **** and **Ctrl-D** to complete subjects ("**:help cmdline-completion**"). Tags are present to jump from one place to another (sort of hypertext links, see "**:help**"). All documentation files can be viewed in this way, for example "**:help syntax.txt**".

## Learning vim With The vim Tutor

**vim** installs with a built-in tutorial system called the **vimtutor** to help you learn vim commands. It is a 30 minute tutorial that teaches the most basic **vim** functionality hands-on. On [Unix](https://www.computerhope.com/jargon/u/unix.htm) and [Linux](https://www.computerhope.com/jargon/l/linux.htm), if **vim** has been properly installed, you can start it from the command line by running the command:

```
vimtutor
```

On [Microsoft](https://www.computerhope.com/comp/msoft.htm) [Windows](https://www.computerhope.com/jargon/w/windows.htm) you can find it in the **Programs/vim** menu, or you can run **vimtutor.bat** in the directory where **vim** was installed.

## Editing In vim: Inserting Text

The **vim** editor is a "modal" editor. That means that the editor behaves differently depending on which mode you are in. The two basic modes are called **Normal mode** and **Insert mode**. In Normal mode the characters you type are commands. In Insert mode the characters are inserted as text.

Since you have just started **vim** it will be in Normal mode. To start Insert mode you type the "**i**" command (**i** for Insert). Then you can enter the text. It will be inserted into the file. For example, you can start a new **vim** session by running the following command from the command line:

```
vim
```

This will place you in a new **vim** editing window, which will show a [tilde](https://www.computerhope.com/jargon/t/tilde.htm) ("**~**") on any line that is empty of text. The window will resemble the following:

```
┌────────────────────────────────────────────────────────┐
│~                                                       │
│~                                                       │
│~                                                       │
│~                                                       │
│                                                        │
└────────────────────────────────────────────────────────┘
```

You will start in **normal mode**, so to insert text you will need to enter **insert mode**. You will type **i**, and then the text you want to insert into the document. So, you can type the following:

```
iThis is a line of text.
This is line number two!
```

(Press **** after the word **text** to start the new line). Finally you press the **** key to stop Insert mode and go back to Normal mode. You now have two lines of text in your **vim** window:

```
┌────────────────────────────────────────────────────────┐
│This is a line of text.                                 │
│This is line number two!                                │
│~                                                       │
│~                                                       │
│                                                        │
└────────────────────────────────────────────────────────┘
```

## Getting Out Of Trouble

When first learning **vim**, it is common to get confused by typing the wrong command, or typing it in the wrong mode. At all times, to get back to Normal mode (no matter what mode you are in), press the **** key. Sometimes you have to press it twice. If **vim** beeps at you, you already are in Normal mode.

## Moving Around

After you return to Normal mode, you can move around by using these keys:

| **h** | left  |
| ----- | ----- |
| **j** | down  |
| **k** | up    |
| **l** | right |

These keys may seem like odd choices for moving the cursor, but there is a very good reason for these: Moving the cursor is the most common thing you do in an editor, and these keys are on the home row of your right hand. In other words, these commands are placed where you can type them the fastest (especially when you type with ten fingers).

You can also move the cursor by using the arrow keys. If you do, however, you greatly slow down your editing because to press the arrow keys, you must move your hand from the text keys to the arrow keys. Considering that you might be doing it hundreds of times an hour, this can take a significant amount of time. Also, there are keyboards which do not have arrow keys, or which locate them in unusual places; therefore, knowing the use of the **hjkl** keys helps in those situations.

The best way to learn these commands is by using them. Use the "**i**" command to insert some more lines of text. Then use the **hjkl** keys to move around and insert a word somewhere. Don't forget to press **** to go back to Normal mode. The **vimtutor** is also an easy way to learn by doing.

## Deleting Characters

To delete a character, move the cursor over it and type "**x**". Move the cursor to the beginning of the first line, for example, and type xxxxxxx (seven **x**'s) to delete "**This is**". The result should look like this:

```
┌────────────────────────────────────────────────────────┐
│ a line of text.                                        │
│This is line number two!                                │
│~                                                       │
│~                                                       │
│                                                        │
└────────────────────────────────────────────────────────┘
```

Now you can insert new text, for example by typing:

```
iHere is
```

<Esc>

This begins an insert (the **i**), inserts the words "**Here is**", and then exits insert mode (****). The result:

```
┌────────────────────────────────────────────────────────┐
│Here is a line of text.                                 │
│This is line number two!                                │
│~                                                       │
│~                                                       │
│                                                        │
└────────────────────────────────────────────────────────┘
```

## Deleting A Line

To delete a whole line, move the cursor to that line and type "**dd**". The next line will then move up to fill the gap. For instance, if you move the cursor to the first line and type "**dd**", our example will look like:

```
┌────────────────────────────────────────────────────────┐
│This is line number two!                                │
│~                                                       │
│~                                                       │
│~                                                       │
│                                                        │
└────────────────────────────────────────────────────────┘
```

## Deleting A Line Break

In **vim** you can join two lines together, which means that the line break between them is deleted. The "**J**" command does this. Take these two lines:

```
This is line 
   number two
```

Move the cursor to the first line and press "**J**":

```
This is line number two
```

## Undo

The "**u**" command [undoes](https://www.computerhope.com/jargon/u/undo.htm) the last edit. In **vim**, pressing **u** multiple times continues to undo previous edits. This is one of the ways **vim** is different than **vi**; in **vi**, pressing **u** twice undoes the undo itself.

## Redo

Pressing **Ctrl-R** (redo) reverses the preceding command. So, after performing an undo with "**u**", pressing **Ctrl-R** will undo the undo.

## Appending

The "**i**" command inserts a character before the character under the cursor. That works fine; but what happens if you want to add stuff to the end of the line? For that you need to insert text after the cursor. This is done with the "**a**" (append) command. For example, to change the line

```
I am very excited about using vim.
```

to

```
I am very excited about using vim!!!
```

move the cursor over to the dot (period) at the end of the line. Then type "**x**" to delete the period. The cursor is now positioned at the end of the line. Now type

```
a!!!
```

And then press **** to return to normal mode.

So, any time you want to insert text right where the cursor is, press "**i**". But if you want to start adding text after the cursor position, press "**a**".

## Opening Up A New Line

The "**o**" command creates a new, empty line below the cursor and puts **vim** in Insert mode. Then you can type the text for the new line. Suppose the cursor is somewhere in the first of these two lines:

```
I am very excited about using vim. 
Amaze.
```

If you now use the "**o**" command and type new text:

```
oWow. Such useful. Many time saving.
```

Then type **** to return to normal mode. The result is:

```
I am very excited about using vim.
Wow. Such useful. Many time saving.
Amaze.
```

The "**O**" command (uppercase) is similar, but opens a line above the cursor instead of below it.

## Repeating A Command Using A Count

Suppose you want to move up nine lines. You can type "**kkkkkkkkk**" or you can enter the command "**9k**". In fact, you can precede many commands with a number. For instance, earlier we added three exclamation points to the end of a line by typing "**a!!!**". Another way to do this is to use the command "**3a!**". The count of **3** tells the command that follows to triple its effect. Similarly, to delete three characters, use the command "**3x**". The count always comes before the command it applies to.

## Quitting vim

To exit, use the "**ZZ**" command. This command writes the file and exits.

Unlike other editors, **vim** does not automatically make a backup file. If you type "**ZZ**", your changes are committed and there's no turning back. You can configure **vim** to produce backup files (see "[Backup Files](https://www.computerhope.com/unix/vim.htm#Backup-Files)", below), but it will not do so by default.

## Discarding Changes

To exit without saving your changes, use the command

```
:q!
```

For those of you interested in the details, the three parts of this command are the colon (**:**), which enters Command-line mode; the **q** command, which tells the editor to quit; and the override command modifier (**!**). The override command modifier is needed because **vim** is reluctant to throw away changes. If you were to just type "**:q**", **vim** would display an error message and refuse to exit:

```
E37: No write since last change (use ! to override)
```

If you merely want to revert to the saved version of the file, the "**:e!**" command reloads the original version of the file.

## Moving From Word To Word

To move the cursor forward one word, use the "**w**" command. Like most **vim** commands, you can use a numeric prefix to move past multiple words. For example, "**3w**" moves three words. This example shows how it works: For the following line of text, if you press "**w**" where indicated, the cursor moves to the place indicated by the arrow.

```
This is a line with example text 
w--->_
 w->_
 w>_
```

Or, using the numeric prefix:

```
This is a line with example text
3w------->_
```

The "**b**" command moves backward to the start of the previous word:

```
This is a line with example text 
                    _<---b
          _<--------2b 
        _<b 
     _<-b 
_<---b 
```

There is also the "**e**" command that moves to the next end of a word and "**ge**", which moves to the previous end of a word:

```
This is a line with example text 
   <-   <--- ----->   ---->
   ge    ge     e       e
```

If you are at the last word of a line, the "**w**" command will take you to the first word in the next line. Thus you can use this to move through a paragraph, much faster than using "**l**". "**b**" does the same in the other direction.

A word ends at a non-word character, such as a "**.**", "**-**" or "**)**". To change what **vim** considers to be a word, use the "**:help iskeyword**" command. It is also possible to move by [white space](https://www.computerhope.com/jargon/w/whitspac.htm)-separated words. This is not a "word" in the normal sense, that's why the uppercase is used. The commands for moving this way are in uppercase, as shown here:

```
 ge b w e
       _<     _<         -->_                          -->_
This is-a line, with special/separated/words (and some more). 
   _<---- _<--- 	 ------------------->_         ---->_
 gE B W E
```

With this mix of lowercase and uppercase commands, you can quickly move forward and backward through a paragraph.

## Moving To The Start Or End Of A Line

The "**$**" command moves the cursor to the end of a line. If your keyboard has an **** key it will do the same thing.

The "**^**" command moves to the first non-blank character of the line. The "**0**" command (zero) moves to the very first character of the line (the **** key does the same thing):

```
 ^
     _<----------
     This is a line with example text 
_<---------------     -------------->_
 0 $
```

The "**$**" command takes a count, like most movement commands. But moving to the end of the line several times doesn't make sense. Therefore it causes the editor to move to the end of another line. For example, "**1$**" moves you to the end of the first line (the one you're on), "**2$**" to the end of the next line, and so on.

The "**0**" command doesn't take a count argument, because the "**0**" would be part of the count.

Using a count with "**^**" doesn't have any effect.

## Moving To A Character

One of the most useful movement commands is the single-character search command. The command "**fx**" searches forward in the line for the single character "x". The "f" stands for "Find".

For example, you are at the beginning of the following line. Suppose you want to go to the "h" in "human". Just execute the command "**fh**" and the cursor will be positioned over the **h**:

```
To err is human. To forgive is divine. 
--------->_
fh	
```

You can specify a count; so, from the beginning of the line, you can go to the "o" of "forgive" with "**3fo**":

```
To err is human. To forgive is divine. 
-------------------->_
3fo
```

The "**F**" (uppercase F) command searches to the left:

```
To err is human. To forgive is divine.
          _<----------
 Fh
```

The "**tx**" command works like the "**fx**" command, except it stops one character before the searched character. The "t" stands for "To". The backward version of this command is "**Tx**".

```
To err is human. To forgive is divine. 
          _<---------    --------->_
 Th tn
```

These four commands can be repeated with "**;**".

"**,**" repeats in the other direction.

The cursor is never moved to another line. Not even when the sentence continues.

Sometimes you will start a search, only to realize that you have typed the wrong command. You type "**f**" to search backward, for example, only to realize that you really meant "**F**". To abort a search, press ****. So "**f**" is an aborted forward search and doesn't do anything. **** cancels most operations, not just searches.

## Matching A Parenthesis

When writing a program you often end up with nested <v>()</v> constructs. Then the "**%**" command is very handy: It moves to the matching parenthesis. If the cursor is on a "**(**" it moves to the matching "**)**". If it's on a "**)**" it moves to the matching "**(**".

```
 %
         _<----
if (a == (b * c) / d) 
    --------------->_
 %
```

This also works for **[]** and **{}** pairs. This can be defined with the '**matchpairs**' option. Use the "**:help matchpairs**" command within **vim** for more information.

When the cursor is not on a useful character, "**%**" will search forward to find one. Thus if the cursor is at the start of the line of the previous example, "**%**" will search forward and find the first "**(**". Then it moves to its match:

```
if (a == (b * c) / d) 
 --+--------------->_
%
```

## Moving To A Specific Line

To move to a specific line, use the "**G**" command.

With no argument, "**G**" positions you at the end of the file. A quick way to go to the start of a file use "**gg**". "**1G**" will do the same.

```
	    |	first line of a file   ^
	    |	text text text text    |
	    |	text text text text    | gg
	7G |	text text text text    |
	    |	text text text text
	    |	text text text text
	    V	text text text text    |
		text text text text    | G
		text text text text    |
		last line of a file    V
```

Another way to move to a line is using the "**%**" command with a count, which moves you that percent through the file. For example "**50%**" moves you to halfway the file. "**90%**" goes to near the end.

The previous assumes that you want to move to a line in the file, no matter if it's currently visible or not. What if you want to move to one of the lines you can see? This figure shows the three commands you can use, **H**, **M**, and **L**.

**H** moves you to the top of the visible screen, **M** to the middle, and **L** to the end. For example:

```
        ┌───────────────────────────┐	
H -->	| sample text               |
        | sample text               |
        | sample text               |
        | sample text               |
M -->	| sample text	            |
        | sample text		    |
        | sample text               |
        | sample text               |
L -->	| sample text               |
        └───────────────────────────┘
```

"H" stands for Home, "M" stands for Middle and "L" stands for Last.

## Determining Where You Are

To see where you are in a file, there are three ways:

Use the **Ctrl-G** command. You get a message like this:

```
"usr_03.txt" line 233 of 650 --35%-- col 45-52
```

This shows the name of the file you are editing, the line number where the cursor is, the total number of lines, the percentage of the way through the file and the column of the cursor.

Sometimes you will see a split column number. For example, "**col 2-9**". This indicates that the cursor is positioned on the second character, but because character one is a tab, occupying eight spaces worth of columns, the screen column is **9**.

Set the '**number**' option. This displays a line number in front of every line:

```
:set number
```

To switch this off again:

```
:set nonumber
```

Since 'number' is a [boolean](https://www.computerhope.com/jargon/b/boolean.htm) option, prepending "**no**" to its name has the effect of switching it off. A boolean option has only these two values, it is either on or off.

**vim** has many options. Besides the boolean ones there are options with a numerical value and string options. You will see examples of this where they are used.

Set the '**ruler**' option. This displays the cursor position in the lower right corner of the **vim** window:

```
:set ruler
```

## Scrolling

The **Ctrl-U** command scrolls down half a screen of text. Think of looking through a viewing window at the text and moving this window up by half the height of the window. Thus the window moves up over the text, which is backward in the file. Don't worry if you have a little trouble remembering which end is up. Most users have the same problem.

The **Ctrl-D** command moves the viewing window down half a screen in the file, thus scrolls the text up half a screen.

```
                               ┌────────────────┐
                               | some text      |
                               | some text      |
                               | some text      |
┌───────────────┐              | some text      |
| some text     | Ctrl-U -->  |                |
|               |              | 123456         |
| 123456        |              └────────────────┘
| 7890          |
|               |              ┌────────────────┐
| example       | Ctrl-D -->  | 7890           |
└───────────────┘              |                |
                               | example        |
                               | example        |
                               | example        |
                               | example        |
                               └────────────────┘
```

To scroll one line at a time use **Ctrl-E** (scroll up) and **Ctrl-Y** (scroll down). Think of **Ctrl-E** to give you one line Extra. If you use MSWindows-compatible key mappings **Ctrl-Y** will redo a change instead of scroll.

To scroll forward by a whole screen (except for two lines) use **Ctrl-F**. The other way is backward, **Ctrl-B** is the command to use. Fortunately **Ctrl-F** is Forward and **Ctrl-B** is Backward, that's easy to remember.

A common issue is that after moving down many lines with "**j**" your cursor is at the bottom of the screen. You would like to see the context of the line with the cursor. That's done with the "**zz**" command.

```
┌──────────────────┐             ┌──────────────────┐
| some text        |             | some text        |
| some text        |             | some text        |
| some text        |             | some text        |
| some text        | zz -->   | line with cursor |
| some text        |             | some text        |
| some text        |             | some text        |
| line with cursor |             | some text        |
└──────────────────┘             └──────────────────┘
```

The "**zt**" command puts the cursor line at the top, "**zb**" at the bottom. To always keep a few lines of context around the cursor, use the '**scrolloff**' option ("**:set scrolloff**").

## Simple Searches

To search for a [string](https://www.computerhope.com/jargon/s/string.htm), use the "**/***string*" command. To find the word "include", for example, use the command:

```
/include
```

You will notice that when you type the "**/**" the cursor jumps to the last line of the **vim** window, like with colon commands. That is where you type the word. You can press the backspace key (backarrow or ****) to make corrections. Use the **** and **** cursor keys when necessary. Pressing **** executes the command.

Note: The characters **.\*[]^%/\?~$** have special meanings. If you want to use them in a search you must put a **\** in front of them; see below.

To find the next occurrence of the same string use the "**n**" command. Use this to find the first "#include" after the cursor:

```
/#include
```

And then type "**n**" several times. You move to each "#include" in the text. You can also use a count if you know which match you want. Thus "**3n**" finds the third match. Using a count with "**/**" doesn't work.

The "**?**" command works like "**/**" but searches backwards:

```
?word
```

The "**N**" command repeats the last search the opposite direction. Thus using "**N**" after a "**/**" command search backwards, using "**N**" after "**?**" searches forward.

## Ignoring Case

Normally you have to type exactly what you want to find. If you don't care about upper or lowercase in a word, set the '**ignorecase**' option:

```
:set ignorecase
```

If you now search for "word", it will also match "Word" and "WORD". To match case again:

```
:set noignorecase
```

## History

Suppose you do three searches:

```
/one
/two
/three
```

Now let's start searching by typing a simple "**/**" without pressing ****. If you press **** (the cursor key), **vim** puts "**/three**" on the command line. Pressing **** at this point searches for three. If you do not press ****, but press **** instead, **vim** changes the prompt to "**/two**". Another press of **** moves you to "**/one**".

You can also use the **** cursor key to move through the history of search commands in the other direction.

If you know what a previously used pattern starts with, and you want to use it again, type that character before pressing ****. With the previous example, you can type "**/o**" and **vim** will put "**/one**" on the command line.

The commands starting with "**:**" also have a history. That allows you to recall a previous command and execute it again. These two histories are separate.

## Searching For A Word In The Text

Suppose you see the word "TheLongFunctionName" in the text and you want to find the next occurrence of it. You could type "**/TheLongFunctionName**", but that's a lot of typing.

There is an easier way: Position the cursor on the word and use the "*****" command. **vim** will grab the word under the cursor and use it as the search string.

The "**#**" command does the same in the other direction. You can prepend a count: "**3\***" searches for the third occurrence of the word under the cursor.

## Searching For Whole Words

If you type "**/the**" it will also match "there". To only find words that end in "the" use:

```
/the\>
```

The "**\>**" notation is a special marker that only matches at the end of a word. Similarly "**\<**" only matches at the begin of a word. Thus to search for the word "the" only:

```
/\<the\>
```

This does not match "there" or "soothe". Notice that the "*****" and "**#**" commands use these start-of-word and end-of-word markers to only find whole words (you can use "**g\***" and "**g#**" to match partial words).

## Highlighting Matches

While editing a program you see a variable called "nr". You want to check where it's used. You could move the cursor to "nr" and use the "*****" command and press "**n**" to go along all the matches.

There is another way. Type this command:

```
:set hlsearch
```

If you now search for "**nr**", **vim** will highlight all matches. That is a very good way to see where the variable is used, without the need to type commands.

To switch this off:

```
:set nohlsearch
```

Then you need to switch it on again if you want to use it for the next search command. If you only want to remove the highlighting, use this command:

```
:nohlsearch
```

This doesn't reset the option. Instead, it disables the highlighting. As soon as you execute a search command, the highlighting will be used again. Also, for the "**n**" and "**N**" commands.

## Tuning Searches

There are a few options that change how searching works. These are the essential ones:

```
:set incsearch
```

This makes **vim** display the match for the string while you are still typing it. Use this to check if the right match will be found. Then press **** to really jump to that location. Or type more to change the search string.

```
:set nowrapscan
```

This stops the search at the end of the file. Or, when you are searching backwards, at the start of the file. The '**wrapscan**' option is on by default, thus searching wraps around the end of the file.

## Intermezzo

If you like one of the options mentioned before, and set it each time you use **vim**, you can put the command in your **vim** startup file.

If you need to learn where the startup file is, use this command:

```
:scriptnames
```

Edit the file, for example with:

```
:edit ~/.vimrc
```

Then add a line with the command to set the option, just like you typed it in **vim**. Example:

```
Go:set hlsearch<Esc>
```

"**G**" moves to the end of the file. "**o**" starts a new line, where you type the "**:set**" command. You end insert mode with ****. Then write the file:

```
ZZ
```

If you now start **vim** again, the '**hlsearch**' option will already be set.

## Simple Search Patterns

The **vim** editor uses [regular expressions](https://www.computerhope.com/jargon/r/regex.htm) ("Regex") to specify what to search for. Regular expressions are an extremely powerful and compact way to specify a search pattern.

## Regex: Beginning And End Of A Line

The **^** ([caret](https://www.computerhope.com/jargon/c/caret.htm)) character matches the beginning of a line. The pattern "include" matches the word include anywhere on the line. But the pattern "**^include**" matches the word include only if it is at the beginning of a line.

The **$** character matches the end of a line. Therefore, "**was$**" matches the word "was" only if it is at the end of a line.

You can try searching with "**/^the$**", it will only match a single line consisting soley of the word "the". White space matters; therefore if a line contains a space after the word, like "the ", the pattern will not match.

## Regex: Matching Any Single Character

The **.** (dot, or period) character matches any existing character. For example, the pattern "**c.m**" matches a string whose first character is a "c", whose second character is anything, and whose the third character is "m".

## Regex: Matching Special Characters

If you really want to match a dot, you must avoid its special meaning by putting a backslash before it, like this: "**\.**". The same goes for any special character (**.\*[]^%/\?~$**).

## Using Marks

When you make a jump to a position with the "**G**" command, **vim** remembers the position from before this jump. This position is called a mark. To go back where you came from, use this command:

```
``
```

This **`** is a backtick or open single-quote character.

If you use the same command a second time you will jump back again. That's because the **`** command is a jump itself, and the position from before this jump is remembered.

Generally, every time you do a command that can move the cursor further than within the same line, this is called a jump. This includes the search commands "**/**" and "**n**" (it doesn't matter how far away the match is). But not the character searches with "**fx**" and "**tx**" or the word movements "**w**" and "**e**".

Also, "**j**" and "**k**" are not considered to be a jump. Even when you use a count to make them move the cursor quite a long way away.

The **``** command jumps back and forth, between two points. The **Ctrl-O** command jumps to older positions ("O" stands for "older"). **Ctrl-I** then jumps back to newer positions. Consider this sequence of commands:

```
33G
/^The
Ctrl-O
```

You first jump to line 33, then search for a line that starts with "The". Then with **Ctrl-O** you jump back to line 33. Another **Ctrl-O** takes you back to where you started. If you now use **Ctrl-I** you jump to line 33 again. And to the match for "The" with another **Ctrl-I**.

Note: **Ctrl-I** is the same as ****.

The "**:jumps**" command gives a list of positions you jumped to. The entry which you used last is marked with a "**>**".

## Named Marks

**vim** enables you to place marks in the text. The command "**ma**" marks the place under the cursor as mark "a". You can place 26 marks (**a** through **z**) in your text. You can't see them, it's just a position that vim remembers.

To go to a mark, use the command **`**{*mark*}, where {*mark*} is the mark letter. Thus to move to the a mark:

```
`a
```

The command **'***mark* (single quotation mark, or apostrophe) moves you to the beginning of the line containing the mark. This differs from the **`***mark* command, which moves you to marked column.

The marks can be very useful when working on two related parts in a file. Suppose you have some text near the start of the file you need to look at, while working on some text near the end of the file.

Move to the text at the start and place the "s" (start) mark there:

```
ms
```

Then move to the text you want to work on and put the "e" (end) mark there:

```
me
```

Now you can move around, and when you want to look at the start of the file, you use this to jump there:

```
's
```

Then you can use **''** to jump back to where you were, or **'e** to jump to the text you were working on at the end.

There is nothing special about using "s" for start and "e" for end, they are just easy to remember.

You can use this command to get a list of marks:

```
:marks
```

You will notice a few special marks. These include:

| **''** | The cursor position before doing a jump.        |
| ------ | ----------------------------------------------- |
| **"**  | The cursor position when last editing the file. |
| **[**  | Start of the last change.                       |
| **]**  | End of the last change.                         |

## Operators And Motions

The "**dw**" command deletes a word. You may recognize the "**w**" command as the move word command. In fact, the "**d**" command may be followed by any motion command, and it deletes from the current location to the place where the cursor winds up. The "**4w**" command, for example, moves the cursor over four words. The **d4w** command deletes four words.

```
To err is human. To forgive is divine. To breathe is required. 
                 --------------------->
 d4w
To err is human. To breathe is required.
```

**vim** only deletes up to the position where the motion takes the cursor. That's because **vim** knows that you probably don't want to delete the first character of a word. If you use the "**e**" command to move to the end of a word, **vim** guesses that you do want to include that last character:

```
To err is human. To breathe is required. 
                ---------->
 d2e
To err is human. is required.
```

Whether the character under the cursor is included depends on the command you used to move to that character. This is called "exclusive" when the character isn't included and "inclusive" when it is.

The "**$**" command moves to the end of a line. The "**d$**" command deletes from the cursor to the end of the line, which is an inclusive motion, thus the last character of the line is included in the delete operation:

```
To err is human. is divine. 
                 -------->
 d$
To err is human.
```

There is a pattern here: operator-motion. You first type an operator command. For example, "**d**" is the delete operator. Then you type a motion command like "**4l**" or "**w**". This way you can operate on any text you can move over.

## Changing Text

Another operator is "**c**", change. It acts just like the "**d**" operator, except it leaves you in Insert mode. For example, "**cw**" changes a word. Or more specifically, it deletes a word and then puts you in Insert mode.

```
To err is human 
   ------->
 c2wbe<Esc>
To be human
```

This "**c2wbe**" contains these bits:

| **c**  | The change operator.                                       |
| ------ | ---------------------------------------------------------- |
| **2w** | Move two words (they are deleted and Insert mode started). |
| **be** | Insert this text.                                          |
| ****   | Back to Normal mode.                                       |

The space before "human" isn't deleted. The **c** operator works just like the **d** operator, with one exception: "**cw**". It actually works like "**ce**", change to end of word. Thus the space after the word isn't included, which is an exception that dates back to the old **Vi**. Since many people are used to it now, the inconsistency has remained in **vim**.

## More Changes

Like "**dd**" deletes a whole line, "**cc**" changes a whole line. It keeps the existing indent (leading white space) though.

Just like "**d$**" deletes until the end of the line, "**c$**" changes until the end of the line. It's like doing "**d$**" to delete the text and then "**a**" to start Insert mode and append new text.

## Shortcuts

Some operator-motion commands are used so often that they have been given a single letter command:

| **Command:** | **Stands For:** | **Description:**                     |
| ------------ | --------------- | ------------------------------------ |
| **x**        | **d1**          | Delete character under the cursor.   |
| **X**        | **dh**          | Delete character left of the cursor. |
| **D**        | **d$**          | Delete to end of the line.           |
| **C**        | **c$**          | Change to end of the line.           |
| **s**        | **c1**          | Change one character.                |
| **S**        | **cc**          | Change a whole line.                 |

## Where To Put The Count

The commands "**3dw**" and "**d3w**" delete three words. If you want to get really picky about things, the first command, "**3dw**", deletes one word three times; the command "**d3w**" deletes three words once, which is a difference without a distinction. You can actually put in two counts, however. For example, "**3d2w**" deletes two words, repeated three times, for a total of six words.

## Replacing With One Character

The "**r**" command is not an operator. It waits for you to type a character, and will replace the character under the cursor with it. You could do the same with "**cl**" or with the "**s**" command, but with "**r**" you don't have to press ****

```
there is somerhing grong here 
rT
There is somerhing grong here 
 rt
There is something grong here
 rw
There is something wrong here
```

Using a count with "**r**" causes that many characters to be replaced with the same character. Example:

```
There is something wrong here 
 5rx
There is something xxxxx here
```

To replace a character with a line break use "**r**". This deletes one character and inserts a line break. Using a count here only applies to the number of characters deleted: "**4r**" replaces four characters with one line break.

## Repeating A Change

The "**.**" command is one of the most simple yet powerful commands in **vim**. It repeats the last change. For instance, suppose you are editing an [HTML](https://www.computerhope.com/jargon/h/html.htm) file and want to delete all the **** tags. You position the cursor on the first **<** and delete the **** with the command "**df>**". You then go to the **<** of the next **** and kill it using the "**.**" command. The "**.**" command executes the last change command (in this case, "**df>**"). To delete another tag, position the cursor on the **<** and use the "**.**" command.

```
		      To <B>generate</B> a table of <B>contents 
f< find first <     --->
df> delete to >	 -->
f< find next <	   --------->
. repeat df>			    --->
f< find next <		       ------------->
. repeat df>					    -->
```

The "**.**" command works for all changes you make, except for the "**u**" (undo), **Ctrl-R** (redo) and commands that start with a colon (**:**).

Another example: You want to change the word "four" to "five". It appears several times in your text. You can do this quickly with this sequence of commands:

| **/four**  | Find the first string "four". |
| ---------- | ----------------------------- |
| **cwfive** | Change the word to "five".    |
| **n**      | Find the next "four".         |
| **.**      | Repeat the change to "five".  |
| **n**      | Find the next "four".         |
| **.**      | Repeat the change.            |

etc.

## Visual Mode

To delete simple items the operator-motion changes work quite well. But often it's not so easy to decide what command moves over the text you want to change. Then you can use Visual mode.

You start Visual mode by pressing "**v**". You move the cursor over the text you want to work on. While you do this, the text is highlighted. Finally type the operator command.

For example, to delete from halfway one word to halfway another word:

```
This is an examination sample of visual mode 
                --------->
	 velllld
This is an example of visual mode
```

When doing this you don't really have to count how many times you have to press "**l**" to end up in the right position. You can immediately see what text will be deleted when you press "**d**".

If at any time you decide you don't want to do anything with the highlighted text, just press **** and Visual mode will stop without doing anything.

## Selecting Lines

If you want to work on whole lines, use "**V**" to start Visual mode. You will see right away that the whole line is highlighted, without moving around. When you move left or right nothing changes. When you move up or down the selection is extended whole lines at a time.

For example, select three lines with "**Vjj**":

```
                  ┌────────────────────────┐
                  | text more text         |
               >> | more text more text    | 
selected lines >> | text text text         | 
               >> | text more              | 
                  | more text more         |
                  └────────────────────────┘
```

## Selecting Blocks

If you want to work on a rectangular block of characters, use **Ctrl-V** to start Visual mode. This is very useful when working on tables.

```
name		Q1	Q2	Q3
pierre		123	455	234
john		0	90	39
steve		392	63	334
```

To delete the middle "**Q2**" column, move the cursor to the "**Q**" of "**Q2**". Press **Ctrl-V** to start blockwise Visual mode. Now move the cursor three lines down with "**3j**" and to the next word with "**w**". You can see the first character of the last column is included. To exclude it, use "**h**". Now press "**d**" and the middle column is gone.

## Going To The Other Side

If you have selected some text in Visual mode, and discover that you need to change the other end of the selection, use the "**o**" command. The cursor will go to the other end, and you can move the cursor to change where the selection starts. Pressing "**o**" again brings you back to the other end. When using blockwise selection, you have four corners. "**o**" only takes you to one of the other corners, diagonally. Use "**O**" to move to the other corner in the same line. Note that "**o**" and "**O**" in Visual mode work very differently from Normal mode, where they open a new line below or above the cursor.

## Moving Text

When you delete something with the "**d**", "**x**", or another command, the text is saved. You can paste it back by using the **p** command. (The **vim** name for this is "put").

Take a look at how this works. First you will delete an entire line, by putting the cursor on the line you want to delete and typing "**dd**". Now you move the cursor to where you want to put the line and use the "**p**" (put) command. The line is inserted on the line below the cursor.

```
	a line		a line	      a line
	line 2	 dd	line 3	 p line 3
	line 3			      line 2
```

Because you deleted an entire line, the "**p**" command placed the text line below the cursor. If you delete part of a line (a word, for instance), the "**p**" command puts it just after the cursor.

```
Some more boring try text to out commands. 
		 ---->
		 dw
Some more boring text to out commands. 
		 ------->
		 welp
Some more boring text to try out commands.
```

## Putting

The "**P**" command puts text like "**p**", but before the cursor. When you deleted a whole line with "**dd**", "**P**" will put it back above the cursor. When you deleted a word with "**dw**", "**P**" will put it back just before the cursor.

You can repeat putting as many times as you like. The same text will be used.

You can use a count with "**p**" and "**P**". The text will be repeated as many times as specified with the count. Thus "**dd**" and then "**3p**" puts three copies of the same deleted line.

## Swapping Characters

**vim** makes it easy to correct such problems such as accidentally typing "teh" for "the". Just put the cursor on the e of "teh" and execute the command "xp". This works as follows: "**x**" deletes the character e and places it in a register. "**p**" puts the text after the cursor, which is after the "h".

```
teh
x 
th
p
the
```

## Copying Text

To copy text from one place to another, you could delete it, use "**u**" to undo the deletion and then "**p**" to put it somewhere else. There is an easier way: yanking. The "**y**" operator copies text into a register. Then a "**p**" command can be used to put it.

Yanking is just a **vim** name for copying. The "**c**" letter was already used for the change operator, and "**y**" was still available. Calling this operator "yank" made it easier to remember to use the "**y**" key.

Since "**y**" is an operator, you use "**yw**" to yank a word. A count is possible as usual. To yank two words use "**y2w**". Example:

```
	let sqr = LongVariable * 
		 -------------->
		 y2w
	let sqr = LongVariable * 
			 p
	let sqr = LongVariable * LongVariable
```

Notice that "**yw**" includes the white space after a word. If you don't want this, use "**ye**".

The "**yy**" command yanks a whole line, just like "**dd**" deletes a whole line. Unexpectedly, while "**D**" deletes from the cursor to the end of the line, "**Y**" works like "**yy**", it yanks the whole line. Watch out for this inconsistency! Use "**y$**" to yank to the end of the line.

```
	a text line yy
        line 2
        last line
	a text line
	line 2 p
 	last line
	a text line
	line 2
	a text line
	last line
```

## Using The Clipboard

If you are using the GUI version of **vim** (**gvim**), you can find the "Copy" item in the "Edit" menu. First select some text with Visual mode, then use the Edit/Copy menu. The selected text is now copied to the clipboard. You can paste the text in other programs. In **vim** itself too.

If you have copied text to the clipboard in another application, you can paste it in **vim** with the Edit/Paste menu. This works in Normal mode and Insert mode. In Visual mode the selected text is replaced with the pasted text.

The "Cut" menu item deletes the text before it's put on the clipboard. The "Copy", "Cut" and "Paste" items are also available in the popup menu (only when there is a popup menu, of course). If your **vim** has a toolbar, you can also find these items there.

If you are not using the GUI, or if you don't like using a menu, you have to use another way. You use the normal "**y**" (yank) and "**p**" (put) commands, but prepend **"\*** (double-quote star) before it. To copy a line to the clipboard:

```
"*yy
```

To put text from the clipboard back into the text:

```
"*p
```

This only works on versions of **vim** that include clipboard support.

## Text Objects

If the cursor is in the middle of a word and you want to delete that word, you need to move back to its start before you can do "dw". There is a simpler way to do this: "**daw**".

```
	this is some example text. 
		 daw
	this is some text.
```

The "**d**" of "**daw**" is the delete operator. "**aw**" is a text object. Hint: "**aw**" stands for "A Word". Thus "**daw**" is "Delete A Word". To be precise, the white space after the word is also deleted (the white space before the word at the end of the line).

Using text objects is the third way to make changes in **vim**. We already had operator-motion and Visual mode. Now we add operator-text object.

It is very similar to operator-motion, but instead of operating on the text between the cursor position before and after a movement command, the text object is used as a whole. It doesn't matter where in the object the cursor was.

To change a whole sentence use "**cis**". Take this text:

```
	Hello there.  This 
	is an example.  Just 
	some text.
```

Move to the start of the second line, on "is an". Now use "cis":

```
	Hello there.    Just 
	some text.
```

The cursor is in between the blanks in the first line. Now you type the new sentence "Another line.":

```
	Hello there.  Another line.  Just 
	some text.
```

"**cis**" consists of the "**c**" (change) operator and the "is" text object. This stands for "Inner Sentence". There is also the "as" (a sentence) object. The difference is that "as" includes the white space after the sentence and "is" doesn't. If you would delete a sentence, you want to delete the white space at the same time, thus use "**das**". If you want to type new text the white space can remain, thus you use "**cis**".

You can also use text objects in Visual mode. It will include the text object in the Visual selection. Visual mode continues, thus you can do this several times. For example, start Visual mode with "**v**" and select a sentence with "**as**". Now you can repeat "**as**" to include more sentences. Finally you use an operator to do something with the selected sentences.

## Replace Mode

The "**R**" command causes **vim** to enter replace mode. In this mode, each character you type replaces the one under the cursor. This continues until you type ****.

In this example, you start Replace mode on the first "**t**" of "**text**":

```
This is text. 
Rinteresting.<Esc>
This is interesting.
```

You may have noticed that this command replaced 5 characters in the line with twelve others. The "**R**" command automatically extends the line if it runs out of characters to replace. It will not continue on the next line.

You can switch between Insert mode and Replace mode with the **** key.

When you use **** (backspace) to make correction, you will notice that the old text is put back. Thus it works like an undo command for the last typed character.

## Conclusion

The operators, movement commands and text objects give you the possibility to make lots of combinations. Now that you know how it works, you can use N operators with M movement commands to make N * M commands!

For example, there are other ways to delete pieces of text. Here are a few often used ones:

| **x**   | Delete character under the cursor (short for "**dl**").  |
| ------- | -------------------------------------------------------- |
| **X**   | Delete character before the cursor (short for "**dh**"). |
| **D**   | Delete from cursor to end of line (short for "**d$**").  |
| **dw**  | Delete from cursor to next start of word.                |
| **db**  | Delete from cursor to previous start of word.            |
| **diw** | Delete word under the cursor (excluding white space).    |
| **daw** | Delete word under the cursor (including white space).    |
| **dG**  | Delete until the end of the file.                        |
| **dgg** | Delete until the start of the file.                      |

If you use "**c**" instead of "**d**" they become change commands. And with "**y**" you yank the text. And so forth.

There are a few often used commands to make changes that didn't fit somewhere else:

| **~** | Change case of the character under the cursor, and move the cursor to the next character. This is not an operator (unless '**tildeop**' is set), thus you can't use it with a motion command. It does work in Visual mode and changes case for all the selected text then. |
| ----- | ------------------------------------------------------------ |
| **I** | Start Insert mode after moving the cursor to the first non-blank in the line. |
| **A** | Start Insert mode after moving the cursor to the end of the line. |

## The vimrc File

You probably got tired of typing commands that you use very often. To start **vim** with all your favorite option settings and mappings, you write them in what is called the **vimrc** file. **vim** executes the commands in this file when it starts up.

If you already have a **vimrc** file (e.g., when your sysadmin has one setup for you), you can edit it this way:

```
:edit $MYVIMRC
```

If you don't have a **vimrc** file yet, you can create one. The "**:version**" command mentions the name of the "user vimrc file" **vim** looks for.

For Unix and [Macintosh](https://www.computerhope.com/jargon/a/applemac.htm) this file is always used and is recommended: **~/.vimrc**

For MS-DOS and MS-Windows you can use one of these: **$HOME/_vimrc**, **$VIM/_vimrc**

The **vimrc** file can contain all the commands that you type after a colon. The most simple ones are for setting options. For example, if you want **vim** to always start with the '**incsearch**' option on, add this line you your **vimrc** file:

```
set incsearch
```

For this new line to take effect you need to exit **vim** and start it again. Later you will learn how to do this without exiting **vim**.

## Simple Mappings

A mapping enables you to bind a set of **vim** commands to a single key. Suppose, for example, that you need to surround certain words with curly braces. In other words, you need to change a word such as "amount" into "{amount}". With the **:map** command, you can tell **vim** that the **F5** key does this job. The command is as follows:

```
:map <F5> i{<Esc>ea}<Esc>
```

When entering this command, you must enter **** by typing four characters. Similarly, **** is not entered by pressing the **** key, but by typing five characters. Watch out for this difference.

Let's break this down:

| ****   | The **F5** function key. This is the trigger key that causes the command to be executed as the key is pressed. |
| ------ | ------------------------------------------------------------ |
| **i{** | Insert the **{** character. The **** key ends Insert mode.   |
| **e**  | Move to the end of the word.                                 |
| **a}** | Append the **}** to the word.                                |

After you execute the "**:map**" command, all you have to do to put **{}** around a word is to put the cursor on the first character and press **F5**.

In this example, the trigger is a single key; it can be any string. But when you use an existing **vim** command, that command will no longer be available. You better avoid that.

One key that can be used with mappings is the backslash. Since you probably want to define more than one mapping, add another character. You could map "**\p**" to add parentheses around a word, and "**\c**" to add curly braces, for example:

```
:map \p i(<Esc>ea)<Esc>
:map \c i{<Esc>ea}<Esc>
```

You need to type the **\** and the **p** quickly after another, so that **vim** knows they belong together.

The "**:map**" command (with no arguments) lists your current mappings. At least the ones for Normal mode.

## Adding A Global Plugin

**vim**'s functionality can be extended by adding plugins. A plugin is nothing more than a **vim** script file that is loaded automatically when **vim** starts. You can add a plugin very easily by dropping it in your plugin directory. {not available when **vim** was compiled without the |+eval| feature}

There are two types of plugins: global plugins, which are used for all kinds of files; and filetype plugins, which are only used for a specific type of file.

When you start **vim**, it will automatically load a number of global plugins. You don't have to do anything for this. They add functionality that most people will want to use, but which was implemented as a **vim** script instead of being compiled in.

You can add a global plugin to add functionality that will always be present when you use **vim**. There are only two steps for adding a global plugin: get a copy of the plugin, and drop it in the right directory.

## Getting A Global Plugin

Some global plugins come with **vim**. You can find them in the directory **$VIMRUNTIME/macros** and its [sub-directories](https://www.computerhope.com/jargon/s/subdirec.htm).

Others can be downloaded from the official **vim** website, https://vim.sourceforge.io/.

## Using A Global Plugin

First read the text in the plugin itself to check for any special conditions. Then copy the file to your plugin directory:

**system****plugin directory**

|             |                                                       |
| ----------- | ----------------------------------------------------- |
| Unix        | **~/.vim/plugin/**                                    |
| PC and OS/2 | **$HOME/vimfiles/plugin** or **$VIM/vimfiles/plugin** |
| Amiga       | **s:vimfiles/plugin**                                 |
| Macintosh   | **$VIM:vimfiles:plugin**                              |
| macOS X     | **~/.vim/plugin/**                                    |
| RISC-OS     | **Choices:vimfiles.plugin**                           |

Example for Unix (assuming you didn't have a plugin directory yet):

```
mkdir ~/.vim
mkdir ~/.vim/plugin
cp /usr/local/share/vim/vim60/macros/justify.vim ~/.vim/plugin
```

That's all! Now you can use the commands defined in this plugin to justify text.

Instead of putting plugins directly into the **plugin/** directory, you may better organize them by putting them into subdirectories under **plugin/**. As an example, consider using "**~/.vim/plugin/perl/\*.vim**" for all your [Perl](https://www.computerhope.com/jargon/p/perl.htm) plugins.

## Filetype Plugins

The **vim** distribution comes with a set of plugins for different filetypes that you can start using with this command:

```
:filetype plugin on
```

If you are missing a plugin for a filetype you are using, or you found a better one, you can add it. There are two steps for adding a filetype plugin: get a copy of the plugin, and drop it in the right directory.

## Often Used Options

vim is an extensive program, and so it has a lot of options! Most of them you will hardly ever use. Some of the more useful ones will be mentioned here. Don't forget you can find more help on these options with the "**:help**" command, with single quotes before and after the option name. For example:

```
:help 'wrap'
```

In case you have messed up an option value, you can set it back to the default by putting an [ampersand](https://www.computerhope.com/jargon/a/ampersand.htm) (&) after the option name. Example:

```
:set iskeyword&
```

**vim** normally wraps long lines, so that you can see all of the text. Sometimes it's better to let the text continue right of the window. Then you need to scroll the text left-right to see all of a long line. Switch wrapping off with this command:

```
:set nowrap
```

**vim** will automatically scroll the text when you move to text that is not displayed. To see a context of ten characters, do this:

```
:set sidescroll=10
```

This doesn't change the text in the file, only the way it is displayed.

Most commands for moving around will stop moving at the start and end of a line. You can change that with the '**whichwrap**' option. This sets it to the default value:

```
:set whichwrap=b,s
```

This allows the **** key, when used in the first position of a line, to move the cursor to the end of the previous line. And the **** key moves from the end of a line to the start of the next one.

To allow the cursor keys **** and **** to also wrap, use this command:

```
:set whichwrap=b,s,<,>
```

This is still only for Normal mode. To let **** and **** do this in Insert mode as well:

```
:set whichwrap=b,s,<,>,[,]
```

There are a few other flags that can be added, see '**whichwrap**'.

## Using Syntax Highlighting

It all starts with one simple command:

```
:syntax enable
```

That should work in most situations to get color in your files. The vim command will automagically detect the type of file and load the right syntax highlighting. Suddenly comments are blue, keywords brown and strings red. This makes it easy to overview the file. After a while you will find that black&white text slows you down!

If you always want to use syntax highlighting, put the "**:syntax enable**" command in your **vimrc** file.

If you want syntax highlighting only when the terminal supports colors, you can put this in your **vimrc** file:

```
if &t_Co > 1
   syntax enable
endif
```

If you want syntax highlighting only in the GUI version, put the "**:syntax enable**" command in your **gvimrc** file.

## Choosing Colors

**vim** guesses the background color that you are using. If it is black (or another dark color) it will use light colors for text. If it is white (or another light color) it will use dark colors for text. If **vim** guessed wrong the text will be hard to read. To solve this, set the '**background**' option. For a dark background:

```
:set background=dark
```

And for a light background:

```
:set background=light
```

Make sure you put this before the "**:syntax enable**" command, otherwise the colors will already have been set. You could do "**:syntax reset**" after setting '**background**' to make **vim** set the default colors again.

If you don't like the default colors, you can select another color scheme. In the GUI use the Edit/Color Scheme menu. You can also type the command:

```
:colorscheme evening
```

"**evening**" is the name of the color scheme. There are several others you might want to try out. Look in the directory **$VIMRUNTIME/colors**.

When you found the color scheme that you like, add the "**:colorscheme**" command to your **vimrc** file.

You could also write a color scheme. This is how you do it:

(1) Select a color scheme that comes close. Copy this file to your **vim** directory. For Unix, this should work. These commands are done from within **vim**:

```
:!mkdir ~/.vim/colors
:!cp $VIMRUNTIME/colors/morning.vim ~/.vim/colors/mine.vim
```

(2) Edit the color scheme file. These entries are useful:

| **term**    | attributes in a B&W terminal         |
| ----------- | ------------------------------------ |
| **cterm**   | attributes in a color terminal       |
| **ctermfg** | foreground color in a color terminal |
| **ctermbg** | background color in a color terminal |
| **gui**     | attributes in the GUI                |
| **guifg**   | foreground color in the GUI          |
| **guibg**   | background color in the GUI          |

For example, to make comments green:

```
:highlight Comment ctermfg=green guifg=green
```

Attributes you can use for "**cterm**" and "**gui**" are "**bold**" and "**underline**". If you want both, use "**bold,underline**".

(3) Tell **vim** to always use your color scheme. Put this line in your **vimrc**:

```
colorscheme mine
```

If you want to see what the most often used color combinations look like, use this command:

```
:runtime syntax/colortest.vim
```

You will see text in various color combinations. You can check which ones are readable and look nice.

## Editing Another File

Once you are in **vim**, you can start editing another file using this command:

```
:edit foo.txt
```

You can use any file name instead of "foo.txt". **vim** will close the current file and open the new one. If the current file has unsaved changes, however, **vim** displays an error message and does not open the new file:

```
E37: No write since last change (use ! to override)
```

**vim** puts an error ID at the start of each error message. If you do not understand the message or what caused it, look in the help system for this ID. In this case:

```
:help E37
```

At this point, you have a number of alternatives. You can write the file using this command:

```
:write
```

Or you can force **vim** to discard your changes and edit the new file, using the force (**!**) character:

```
:edit! foo.txt
```

If you want to edit another file, but not write the changes in the current file yet, you can make it hidden:

```
:hide edit foo.txt
```

The text with changes is still there, but you can't see it.

## Editing A List Of Files

You can start **vim** to edit a sequence of files. For example:

```
vim one.c two.c three.c
```

This command starts **vim** and tells it that you will be editing three files. **vim** displays just the first file. After you have done your thing in this file, to edit the next file you use this command:

```
:next
```

If you have unsaved changes in the current file, you will get an error message and the "**:next**" will not work. This is the same problem as with "**:edit**" mentioned in the previous section. To abandon the changes:

```
:next!
```

But mostly you want to save the changes and move on to the next file. There is a special command for this:

```
:wnext
```

This does the same as using two separate commands:

```
:write
:next
```

To see which file in the argument list you are editing, look in the window title. It should show something like "**(2 of 3)**". This means you are editing the second file out of three files.

If you want to see the list of files, use this command:

```
:args
```

This is short for "arguments". The output might look like this:

```
one.c [two.c] three.c
```

These are the files you started vim with. The one you are currently editing, "two.c", is in square brackets.

## Moving From File To File

To go back one file:

```
:previous
```

This is just like the "**:next**" command, except that it moves in the other direction. Again, there is a shortcut command for when you want to write the file first:

```
:wprevious
```

To move to the very last file in the list:

```
:last
```

And to move back to the first one again:

```
:first
```

There is no "**:wlast**" or "**:wfirst**" command however.

You can use a count for "**:next**" and "**:previous**". To skip two files forward:

```
:2next
```

## Backup Files

Usually **vim** does not produce a backup file. If you want to have one, all you need to do is execute the following command:

```
:set backup
```

The name of the backup file is the original file with a [tilde](https://www.computerhope.com/jargon/t/tilde.htm) ("**~**") added to the end. If your file is named **data.txt**, for example, the backup file name is **data.txt~**. If you do not like the fact that the backup files end with **~**, you can change the extension:

```
:set backupext=.bak
```

This will use **data.txt.bak** instead of **data.txt~**.

Another option that matters here is '**backupdir**'. It specifies where the backup file is written. The default, to write the backup in the same directory as the original file, will mostly be the right thing.

When the '**backup**' option isn't set but the '**writebackup**' is, **vim** will still create a backup file. However, it is deleted as soon as writing the file was completed successfully. This functions as a safety against losing your original file when writing fails in some way (disk full is the most common cause).

If you are editing source files, you might want to keep the file before you make any changes. But the backup file will be overwritten each time you write the file. Thus it only contains the previous version, not the first one.

To make **vim** keep the original file, set the 'patchmode' option. This specifies the extension used for the first backup of a changed file. Usually you would do this:

```
:set patchmode=.orig
```

When you now edit the file data.txt for the first time, make changes and write the file, **vim** will keep a copy of the unchanged file under the name "**data.txt.orig**".

If you make further changes to the file, **vim** will notice that "**data.txt.orig**" already exists and leave it alone. Further backup files will then be called "**data.txt~**" (or whatever you specified with '**backupext**').

If you leave '**patchmode**' empty (that is the default), the original file will not be kept.

## Using Registers

When you want to copy several pieces of text from one file to another, having to switch between the files and writing the target file takes a lot of time. To avoid this, copy each piece of text to its own register.

A register is a place where vim stores text. Here we will use the registers named a to z (later you will find out there are others). Let's copy a sentence to the **f** register (f for First):

```
"fyas
```

The "**yas**" command yanks a sentence like before. It's the **"f** that tells **vim** the text should be place in the **f** register. This must come just before the yank command.

Now yank three whole lines to the **l** register (**l** for line):

```
"l3Y
```

The count could be before the **"l** just as well. To yank a block of text to the **b** (for block) register:

```
Ctrl-Vjjww"by
```

Notice that the register specification "b is just before the "y" command. This is required. If you would have put it before the "w" command, it would not have worked.

Now you have three pieces of text in the **f**, **l** and **b** registers. Edit another file, move around and place the text where you want it:

```
"fp
```

Again, the register specification **"f** comes before the "**p**" command.

You can put the registers in any order. And the text stays in the register until you yank something else into it. Thus you can put it as many times as you like.

When you delete text, you can also specify a register. Use this to move several pieces of text around. For example, to delete-a-word and write it in the **w** register:

```
"wdaw
```

Again, the register specification comes before the delete command "**d**".

## Viewing A File Read-Only

Sometimes you only want to see what a file contains, without the intention to ever write it back. There is the risk that you type "**:w**" without thinking and overwrite the original file anyway. To avoid this, edit the file read-only.

To start **vim** in readonly mode, use this command:

```
vim -R file
```

On Unix this command should do the same thing:

```
view file
```

You are now editing "file" in read-only mode. When you try using ":w" you will get an error message and the file won't be written.

When you try to make a change to the file vim gives you a warning:

```
W10: Warning: Changing a readonly file
```

The change will be done though. This allows for formatting the file, for example, to be able to read it easily.

If you make changes to a file and forgot that it was read-only, you can still write it. Add the **!** to the write command to force writing.

If you really want to forbid making changes in a file, do this:

```
vim -M file
```

Now every attempt to change the text will fail. The help files are like this, for example. If you try to make a change you get this error message:

```
E21: Cannot make changes, 'modifiable' is off
```

You could use the **-M** argument to set up **vim** to work in a viewer mode. This is only voluntary though, since these commands will remove the protection:

```
:set modifiable
:set write
```

## Saving As A New File Name

A clever way to start editing a new file is by using an existing file that contains most of what you need. For example, you start writing a new program to move a file. You know that you already have a program that copies a file, thus you start with:

```
:edit copy.c
```

You can delete the stuff you don't need. Now you need to save the file under a new name. The "**:saveas**" command can be used for this:

```
:saveas move.c
```

**vim** will write the file under the given name, and edit that file. Thus the next time you do "**:write**", it will write "**move.c**". "**copy.c**" remains unmodified.

When you want to change the name of the file you are editing, but don't want to write the file, you can use this command:

```
:file move.c
```

**vim** will mark the file as "not edited". This means that vim knows this is not the file you started editing. When you try to write the file, you might get this message:

```
E13: File exists (use ! to override)
```

This protects you from accidentally overwriting another file.

## Splitting Windows

The easiest way to open a new window is to use the following command:

```
:split
```

This command splits the screen into two windows and leaves the cursor in the top one:

```
        ┌──────────────────────────────────┐
	|/* file one.c */		   |
	|~				   |
	|~				   |
	|one.c=============================|
	|/* file one.c */		   |
	|~				   |
	|one.c=============================|
	|				   |
        └──────────────────────────────────┘
```

What you see here is two windows on the same file. The line with "====" is that status line. It displays information about the window above it. In practice the status line will be in reverse video.

The two windows allow you to view two parts of the same file. For example, you could make the top window show the variable declarations of a program, and the bottom one the code that uses these variables.

The **Ctrl-W w** command can be used to jump between the windows. If you are in the top window, **Ctrl-W w** jumps to the window below it. If you are in the bottom window it will jump to the first window. **Ctrl-W Ctrl-W** does the same thing, in case you let go of the **Ctrl** key a bit later.

To close a window, use the command:

```
:close
```

Actually, any command that quits editing a file works, like "**:quit**" and "**ZZ**". But "**:close**" prevents you from accidentally exiting vim when you close the last window.

If you have opened a whole bunch of windows, but now want to concentrate on one of them, this command will be useful:

```
:only
```

This closes all windows, except for the current one. If any of the other windows has changes, you will get an error message and that window won't be closed.

## Splitting A Window On Another File

The following command opens a second window and starts editing the given file:

```
:split two.c
```

If you were editing **one.c**, then the result looks like this:

```
        ┌──────────────────────────────────┐
	|/* file two.c */		   |
	|~				   |
	|~				   |
	|two.c=============================|
	|/* file one.c */		   |
	|~				   |
	|one.c=============================|
	|				   |
        └──────────────────────────────────┘
```

To open a window on a new, empty file, use this:

```
:new
```

You can repeat the ":split" and ":new" commands to create as many windows as you like.

## Window Size

The "**:split**" command can take a number argument. If specified, this will be the height of the new window. For example, the following opens a new window three lines high and starts editing the file **alpha.c**:

```
:3split alpha.c
```

For existing windows you can change the size in several ways. When you have a working mouse, it is easy: Move the mouse pointer to the status line that separates two windows, and drag it up or down.

To increase the size of a window: **Ctrl-W +**

To decrease it: **Ctrl-W -**

Both of these commands take a count and increase or decrease the window size by that many lines. Thus "**4 Ctrl-W +**" make the window four lines higher.

To set the window height to a specified number of lines: **{height}Ctrl-W _**

That's: a number **{height}**, **Ctrl-W** and then an underscore. To make a window as high as it can be, use the **Ctrl-W _** command without a count.

## Using The Mouse

In **vim** you can do many things very quickly from the keyboard. Unfortunately, the window resizing commands require quite a bit of typing. In this case, using the mouse is faster. Position the mouse pointer on a status line. Now press the left mouse button and drag. The status line moves, thus making the window on one side higher and the other smaller.

## Options

The '**winheight**' option can be set to a minimal desired height of a window and '**winminheight**' to a hard minimum height. Likewise, there is '**winwidth**' for the minimal desired width and '**winminwidth**' for the hard minimum width. The '**equalalways**' option, when set, makes **vim** equalize the windows sizes when a window is closed or opened.

## Vertical splits

The "**:split**" command creates the new window above the current one. To make the window appear at the left side, use:

```
:vsplit
```

or:

```
:vsplit two.c
```

The result looks something like this:

```
        ┌──────────────────────────────────────┐
	|/* file two.c */  ||/* file one.c */  ||||
	|~		   ||~		       ||||
	|~		   ||~		       ||||
	|~		   ||~		       ||||
	|two.c===============one.c=============|
	|				       |
        └──────────────────────────────────────┘
```

Actually, the **||** lines in the middle will be in reverse video. This is called the vertical separator. It separates the two windows left and right of it.

There is also the "**:vnew**" command, to open a vertically split window on a new, empty file. Another way to do this:

```
:vertical new
```

The "**:vertical**" command can be inserted before another command that splits a window. This will cause that command to split the window vertically instead of horizontally. If the command doesn't split a window, it works unmodified.

## Moving Between Windows

Since you can split windows horizontally and vertically as much as you like, you can create almost any layout of windows. Then you can use these commands to move between them:

| **Ctrl-W h** | move to the window on the left  |
| ------------ | ------------------------------- |
| **Ctrl-W j** | move to the window below        |
| **Ctrl-W k** | move to the window above        |
| **Ctrl-W l** | move to the window on the right |
| **Ctrl-W t** | move to the TOP window          |
| **Ctrl-W b** | move to the BOTTOM window       |

You will notice the same letters as used for moving the cursor. And the cursor keys can also be used, if you like.

## Moving windows

You have split a few windows, but now they are in the wrong place. Then you need a command to move the window somewhere else. For example, you have three windows like this:

```
        ┌──────────────────────────────────┐
	|/* file two.c */		   |
	|~				   |
	|~				   |
	|two.c=============================|
	|/* file three.c */		   |
	|~				   |
	|~				   |
	|three.c===========================|
	|/* file one.c */		   |
	|~				   |
	|one.c=============================|
	|				   |
        └──────────────────────────────────┘
```

Clearly the last one should be at the top. Go to that window (using **Ctrl-W w**) and the type this command: **Ctrl-W K**

This uses the uppercase letter **K**. What happens is that the window is moved to the very top. You will notice that **K** is again used for moving upwards. When you have vertical splits, **Ctrl-W K** moves the current window to the top and make it occupy the full width of the **vim** window. If this is your layout:

```
        ┌───────────────────────────────────────────┐
	|/* two.c */ ||/* three.c */ ||/* one.c */  |
	|~	     ||~	     ||~	    |
	|~	     ||~	     ||~	    |
	|~	     ||~	     ||~	    |
	|~	     ||~	     ||~	    |
	|~	     ||~	     ||~	    |
	|two.c=========three.c=========one.c========|
	|					    |
        └───────────────────────────────────────────┘
```

Then using **Ctrl-W K** in the middle window (**three.c**) will result in:

```
	┌───────────────────────────────────────────┐
	|/* three.c */				    |
	|~					    |
	|~					    |
	|three.c====================================|
	|/* two.c */	      ||/* one.c */	    ||||
	|~		      ||~		    ||||
	|two.c==================one.c===============|
	|					    |
	└───────────────────────────────────────────┘
```

The other three similar commands (you can probably guess these now):

| **Ctrl-W H** | move window to the far left  |
| ------------ | ---------------------------- |
| **Ctrl-W J** | move window to the bottom    |
| **Ctrl-W L** | move window to the far right |

## Commands For All Windows

When you have several windows open and you want to quit **vim**, you can close each window separately. A quicker way is using this command:

```
:qall
```

This stands for "quit all". If any of the windows contain changes, **vim** will not exit. The cursor will automatically be positioned in a window with changes. You can then either use "**:write**" to save the changes, or "**:quit!**" to throw them away.

If you know there are windows with changes, and you want to save all these changes, use this command:

```
:wall
```

This stands for "write all". But actually, it only writes files with changes. The vim command knows it doesn't make sense to write files that were not changed.

And then there is the combination of "**:qall**" and "**:wall**": the "write and quit all" command:

```
:wqall
```

This writes all modified files and quits **vim**.

Finally, there is a command that quits **vim** and throws away all changes:

```
:qall!
```

Be careful, there is no way to undo this command!

## Opening A Window For All Files

To make **vim** open a window for each file, start it with the "**-o**" argument:

```
vim -o one.txt two.txt three.txt
```

This results in:

```
	┌───────────────────────────────┐
	|file one.txt			|
	|~				|
	|one.txt========================|
	|file two.txt			|
	|~				|
	|two.txt========================|
	|file three.txt			|
	|~				|
	|three.txt======================|
	|				|
	└───────────────────────────────┘
```

The "**-O**" argument is used to get vertically split windows.

When **vim** is already running, the "**:all**" command opens a window for each file in the argument list. "**:vertical all**" does it with vertical splits.

## Viewing Differences With vimdiff

There is a special way to start **vim**, which shows the differences between two files. Let's take a file "main.c" and insert a few characters in one line. Write this file with the 'backup' option set, so that the backup file "main.c~" will contain the previous version of the file.

Type this command in a shell (not in **vim**):

```
vimdiff main.c~ main.c
```

**vim** will start, with two windows side by side. You will only see the line in which you added characters, and a few lines above and below it.

```
	 VV		      VV
	┌─────────────────────────────────────────┐
	|+ +--123 lines: /* a|+ +--123 lines: /* a|  <- fold|||
	|  text		     |	text		  |
	|  text		     |	text		  |
	|  text		     |	text		  |
	|  text		     |	changed text	  |  <- changed line
	|  text		     |	text		  |
	|  text		     |	------------------|  <- deleted line
	|  text		     |	text		  |
	|  text		     |	text		  |
	|  text		     |	text		  |
	|+ +--432 lines: text|+ +--432 lines: text|  <- fold|||
	|  ~		     |	~		  |
	|  ~		     |	~		  |
	|main.c~==============main.c==============|
	|					  |
	└─────────────────────────────────────────┘
```

This picture doesn't show the highlighting, use the **vimdiff** command for a better look.

The lines that were not modified have been collapsed into one line. This is called a closed fold. They are indicated in the picture with "**<- fold**". Thus the single fold line at the top stands for 123 text lines. These lines are equal in both files.

The line marked with "**<- changed line**" is highlighted, and the inserted text is displayed with another color. This clearly shows what the difference is between the two files.

The line that was deleted is displayed with "**---**" in the main.c window. See the "**<- deleted line**" marker in the picture. These characters are not really there. They just fill up main.c, so that it displays the same number of lines as the other window.

## The Fold Column

Each window has a column on the left with a slightly different background. In the picture above these are indicated with "VV". You notice there is a plus character there, in front of each closed fold. Move the mouse pointer to that plus and click the left button. The fold will open, and you can see the text that it contains.

The fold column contains a minus sign for an open fold. If you click on this -, the fold will close. Obviously, this only works when you have a working mouse. You can also use "zo" to open a fold and "zc" to close it.

## Diffing In vim

Another way to start in diff mode can be done from inside **vim**. Edit the "main.c" file, then make a split and show the differences:

```
:edit main.c
:vertical diffsplit main.c~
```

The "**:vertical**" command is used to make the window split vertically. If you omit this, you will get a horizontal split.

If you have a patch or diff file, you can use the third way to start diff mode. First edit the file to which the patch applies. Then tell vim the name of the patch file:

```
:edit main.c
:vertical diffpatch main.c.diff
```

WARNING: The patch file must contain only one patch, for the file you are editing. Otherwise, you will get a lot of error messages, and some files might be patched unexpectedly.

The patching will only be done to the copy of the file in **vim**. The file on your harddisk will remain unmodified (until you decide to write the file).

## Scroll Binding

When the files have more changes, you can scroll in the usual way. **vim** will try to keep both the windows start at the same position, so you can easily see the differences side by side.

When you don't want this for a moment, use this command:

```
:set noscrollbind
```

## Jumping To Changes

When you have disabled folding in some way, it may be difficult to find the changes. Use this command to jump forward to the next change:

```
]c
```

To go the other way use:

```
[c
```

Prepended a count to jump further away.

## Removing Changes

You can move text from one window to the other. This either removes differences or adds new ones. The vim command doesn't keep the highlighting updated in all situations. To update it use this command:

```
:diffupdate
```

To remove a difference, you can move the text in a highlighted block from one window to another. Take the "main.c" and "main.c~" example above. Move the cursor to the left window, on the line that was deleted in the other window. Now type this command:

```
dp
```

The change will be removed by putting the text of the current window in the other window. "dp" stands for "diff put".

You can also do it the other way around. Move the cursor to the right window, to the line where "changed" was inserted. Now type this command:

```
do
```

The change will now be removed by getting the text from the other window. Since there are no changes left now, vim puts all text in a closed fold. "do" stands for "diff obtain". "dg" would have been better, but that already has a different meaning ("dgg" deletes from the cursor until the first line).

## Miscellaneous Options

The '**laststatus**' option can be used to specify when the last window has a statusline:

| **0** | never                                           |
| ----- | ----------------------------------------------- |
| **1** | only when there are split windows (the default) |
| **2** | always                                          |

Many commands that edit another file have a variant that splits the window. For Command-line commands this is done by prepending an "s". For example: "**:tag**" jumps to a tag, "**:stag**" splits the window and jumps to a tag.

For Normal mode commands a **Ctrl-W** is prepended. **Ctrl-^** jumps to the alternate file, **Ctrl-W Ctrl-^** splits the window and edits the alternate file.

The '**splitbelow**' option can be set to make a new window appear below the current window. The '**splitright**' option can be set to make a vertically split window appear right of the current window.

When splitting a window you can prepend a modifier command to tell where the window is to appear:

| **:leftabove {cmd}**  | left or above the current window         |
| --------------------- | ---------------------------------------- |
| **:aboveleft {cmd}**  | idem                                     |
| **:rightbelow {cmd}** | right or below the current window        |
| **:belowright {cmd}** | idem                                     |
| **:topleft {cmd}**    | at the top or left of the vim window     |
| **:botright {cmd}**   | at the bottom or right of the vim window |

## Tab Pages

You will have noticed that windows never overlap. That means you quickly run out of screen space. The solution for this is called Tab pages.

Assume you are editing "thisfile". To create a new tab page use this command:

```
:tabedit thatfile
```

This will edit the file "thatfile" in a window that occupies the whole vim window. And you will notice a bar at the top with the two file names:

```
	┌──────────────────────────────────┐
	| thisfile | /thatfile/ __________X|    (thatfile is bold)
	|/* thatfile */			   |
	|that				   |
	|that				   |
	|~				   |
	|~				   |
	|~				   |
	|				   |
	└──────────────────────────────────┘
```

You now have two tab pages. The first one has a window for "thisfile" and the second one a window for "thatfile". It's like two pages that are on top of each other, with a tab sticking out of each page showing the file name.

Now use the mouse to click on "thisfile" in the top line. The result is

```
	┌──────────────────────────────────┐
	| /thisfile/ | thatfile __________X|    (thisfile is bold)
	|/* thisfile */			   |
	|this				   |
	|this				   |
	|~				   |
	|~				   |
	|~				   |
	|				   |
	└──────────────────────────────────┘
```

Thus you can switch between tab pages by clicking on the label in the top line. If you don't have a mouse or don't want to use it, you can use the "gt" command. You can remember it as an abbreviation for "Goto Tab".

Now let's create another tab page with the command:

```
:tab split
```

This makes a new tab page with one window that is editing the same buffer as the window we were in:

```
	┌─────────────────────────────────────┐
	| thisfile | /thisfile/ | thatfile __X|   (thisfile is bold)
	|/* thisfile */			      |
	|this				      |
	|this				      |
	|~				      |
	|~				      |
	|~				      |
	|				      |
	└─────────────────────────────────────┘
```

You can put "**:tab**" before any Ex command that opens a window. The window will be opened in a new tab page. Another example:

```
:tab help gt
```

Will show the help text for "**gt**" in a new tab page.

A few more things you can do with tab pages:

- click with the mouse in the space after the last label. The next tab page will be selected, like with "**gt**".
- click with the mouse on the "X" in the top right corner. The current tab page will be closed. Unless there are unsaved changes in the current tab page.
- double click with the mouse in the top line. A new tab page will be created.
- the "**tabonly**" command. Closes all tab pages except the current one. Unless there are unsaved changes in other tab pages.

## Macros

The "**.**" command repeats the preceding change. But what if you want to do something more complex than a single change? That's where command recording comes in, better known as a [macro](https://www.computerhope.com/jargon/m/macro.htm). There are three steps:

(1) The "**q{register}**" command starts recording keystrokes into the register named **{register}**. The register name must be between **a** and **z**.

(2) Type your commands.

(3) To finish recording, press **q** (without any extra character).

You can now execute the macro by typing the command "**@{register**}". Take a look at how to use these commands in practice. You have a list of file names that look like this:

```
	stdio.h 
	fcntl.h 
	unistd.h 
	stdlib.h
```

And what you want is the following:

```
	#include "stdio.h" 
	#include "fcntl.h" 
	#include "unistd.h" 
	#include "stdlib.h" 
```

You start by moving to the first character of the first line. Next you execute the following commands:

| **qa**          | Start recording a macro in register **a**.                   |
| --------------- | ------------------------------------------------------------ |
| **^**           | Move to the beginning of the line.                           |
| **i#include "** | Insert the string **#include "** at the beginning of the line. |
| **$**           | Move to the end of the line.                                 |
| **a"**          | Append the character double quotation mark (**"**) to the end of the line. |
| **j**           | Go to the next line.                                         |
| **q**           | Stop recording the macro.                                    |

Now that you have done the work once, you can repeat the change by typing the command "**@a**" three times.

The "**@a**" command can be preceded by a count, which will cause the macro to be executed that number of times. In this case you would type:

```
3@a
```

## Move And Execute

You might have the lines you want to change in various places. Just move the cursor to each location and use the "**@a**" command. If you have done that once, you can do it again with "**@@**". That's a bit easier to type. If you now execute register **b** with "**@b**", the next "**@@**" will use register **b**.

If you compare the playback method with using "**.**", there are several differences. First of all, "**.**" can only repeat one change. As seen in the example above, "**@a**" can do several changes, and move around as well. Secondly, "**.**" can only remember the last change. Executing a register allows you to make any changes and then still use "**@a**" to replay the recorded commands. Finally, you can use 26 different registers. Thus you can remember 26 different command sequences to execute.

## Using Registers

The registers used for recording are the same ones you used for yank and delete commands. This allows you to mix recording with other commands to manipulate the registers.

Suppose you have recorded a few commands in register **n**. When you execute this with "**@n**" you notice you did something wrong. You could try recording again, but perhaps you will make another mistake. Instead, use this trick:

| **G**       | Go to the end of the file.                                   |
| ----------- | ------------------------------------------------------------ |
| **o**       | Create an empty line.                                        |
| **"np**     | Put the text from the **n** register. You now see the commands you typed as text in the file. |
| **{edits}** | Change the commands that were wrong. This is just like editing text. |
| **0**       | Go to the start of the line.                                 |
| **"ny$**    | Yank the corrected commands into the **n** register.         |
| **dd**      | Delete the scratch line.                                     |

Now you can execute the corrected commands with "**@n**". If your recorded commands include line breaks, adjust the last two items in the example to include all the lines.

## Appending To A Register

So far we have used a lowercase letter for the register name. To append to a register, use an uppercase letter.

Suppose you have recorded a command to change a word to register **c**. It works properly, but you would like to add a search for the next word to change. This can be done with:

```
qC/word\<Enter\>q
```

You start with "**qC**", which records to the c register and appends. Thus writing to an uppercase register name means to append to the register with the same letter, but lowercase.

This works both with recording and with yank and delete commands. For example, you want to collect a sequence of lines into the a register. Yank the first line with:

```
"aY
```

Now move to the second line, and type:

```
"AY
```

Repeat this command for all lines. The a register now contains all those lines, in the order you yanked them.

## Substitution

The "**:substitute**" command enables you to perform string replacements on a whole range of lines. The general form of this command is as follows:

```
:[range]substitute/from/to/[flags]
```

This command changes the "**from**" string to the "**to**" string in the lines specified with **[range]**. For example, you can change "Professor" to "Teacher" in all lines with the following command:

```
:%substitute/Professor/Teacher/
```

Note: The "**:substitute**" command is almost never spelled out completely. Most of the time, people use the abbreviated version "**:s**". From here on the abbreviation will be used.

The "**%**" before the command specifies the command works on all lines. Without a range, "**:s**" only works on the current line.

By default, the "**:substitute**" command changes only the first occurrence on each line. For example, the preceding command changes the line:

```
Professor Smith criticized Professor Johnson today.
```

to:

```
Teacher Smith criticized Professor Johnson today.
```

To change every occurrence on the line, you need to add the **g** (global) flag. The command:

```
:%s/Professor/Teacher/g
```

results in (starting with the original line):

```
Teacher Smith criticized Teacher Johnson today.
```

Other flags include **p** (print), which causes the "**:substitute**" command to print out the last line it changes. The **c** (confirm) flag tells "**:substitute**" to ask you for confirmation before it performs each substitution. Enter the following:

```
:%s/Professor/Teacher/c
```

**vim** finds the first occurrence of "Professor" and displays the text it is about to change. You get the following prompt:

```
replace with Teacher (y/n/a/q/l/^E/^Y)?
```

At this point, you must enter one of the following answers:

| **y**      | Yes; make this change.                                       |
| ---------- | ------------------------------------------------------------ |
| **n**      | No; skip this match.                                         |
| **a**      | All; make this change and all remaining ones without further confirmation. |
| **q**      | Quit; don't make any more changes.                           |
| **l**      | Last; make this change and then quit.                        |
| **Ctrl-E** | Scroll the text one line up.                                 |
| **Ctrl-Y** | Scroll the text one line down.                               |

The "from" part of the substitute command is actually a pattern. The same kind as used for the search command. For example, this command only substitutes "the" when it appears at the start of a line:

```
:s/^the/these/
```

If you are substituting with a "from" or "to" part that includes a slash, you need to put a backslash before it. A simpler way is to use another character instead of the slash. A plus, for example:

```
:s+one/two+one or two+
```

## Command ranges

The "**:substitute**" command, and other **:** commands, can be applied to a selection of lines. This is called a range.

The simple form of a range is **{number},{number}**. For example:

```
:1,5s/this/that/g
```

Executes the substitute command on the lines 1 to 5. Line 5 is included. The range is always placed before the command.

A single number can be used to address one specific line:

```
:54s/President/Fool/
```

Some commands work on the whole file when you do not specify a range. To make them work on the current line the "**.**" address is used. The "**:write**" command works like that. Without a range, it writes the whole file. To make it write only the current line into a file:

```
:.write otherfile
```

The first line always has number one. How about the last line? The "**$**" character is used for this. For example, to substitute in the lines from the cursor to the end:

```
:.,$s/yes/no/
```

The "**%**" range that we used before, is actually a short way to say "**1,$**", from the first to the last line.

## Using A Pattern In A Range

Suppose you are editing a chapter in a book, and want to replace all occurrences of "**grey**" with "**gray**". But only in this chapter, not in the next one. You know that only chapter boundaries have the word "Chapter" in the first column. This command will work then:

```
:?^Chapter?,/^Chapter/s=grey=gray=g
```

You can see a search pattern is used twice. The first "**?^Chapter?**" finds the line above the current position that matches this pattern. Thus the **?pattern?** range is used to search backwards. Similarly, "**/^Chapter/**" is used to search forward for the start of the next chapter.

To avoid confusion with the slashes, the "**=**" character was used in the substitute command here. A slash or another character would have worked as well.

## Add And Subtract

There is a slight error in the above command: If the title of the next chapter had included "grey" it would be replaced as well. Maybe that's what you wanted, but what if you didn't? Then you can specify an offset.

To search for a pattern and then use the line above it:

```
/Chapter/-1
```

You can use any number instead of the 1. To address the second line below the match:

```
/Chapter/+2
```

The offsets can also be used with the other items in a range. Look at this one:

```
:.+3,$-5
```

This specifies the range that starts three lines below the cursor and ends five lines before the last line in the file.

## Using Marks

Instead of figuring out the line numbers of certain positions, remembering them and typing them in a range, you can use marks.

Place the marks as mentioned in chapter 3. For example, use "**mt**" to mark the top of an area and "**mb**" to mark the bottom. Then you can use this range to specify the lines between the marks (including the lines with the marks):

```
:'t,'b
```

## Visual Mode And Ranges

You can select text with Visual mode. If you then press "**:**" to start a colon command, you will see this:

```
:'<,'>
```

Now you can type the command and it will be applied to the range of lines that was visually selected.

Note: When using Visual mode to select part of a line, or using **Ctrl-V** to select a block of text, the colon commands will still apply to whole lines.

The **'<** and **'>** are actually marks, placed at the start and end of the Visual selection. The marks remain at their position until another Visual selection is made. Thus you can use the "**'<**" command to jump to position where the Visual area started. And you can mix the marks with other items:

```
:'>,$
```

This addresses the lines from the end of the Visual area to the end of the file.

## A Number Of Lines

When you know how many lines you want to change, you can type the number and then "**:**". For example, when you type "**5:**", you will get:

```
:.,.+4
```

Now you can type the command you want to use. It will use the range "**.**" (current line) until "**.+4**" (four lines down). Thus it spans five lines.

## The Global Command

The "**:global**" command is one of the more powerful features of **vim**. It allows you to find a match for a pattern and execute a command there. The general form is:

```
:[range]global/{pattern}/{command}
```

This is similar to the "**:substitute**" command. But, instead of replacing the matched text with other text, the command **{command}** is executed.

Note: The command executed for "**:global**" must be one that starts with a colon. Normal mode commands can not be used directly. The **:normal** command can do this for you.

Suppose you want to change "foobar" to "barfoo", but only in C++ style comments. These comments start with "**//**". Use this command:

```
:g+//+s/foobar/barfoo/g
```

This starts with "**:g**". That is short for "**:global**", just like "**:s**" is short for "**:substitute**". Then the pattern, enclosed in plus characters. Since the pattern we are looking for contains a slash, this uses the plus character to separate the pattern. Next comes the substitute command that changes "foobar" into "barfoo".

The default range for the global command is the whole file. Thus no range was specified in this example. This is different from "**:substitute**", which works on one line without a range.

The command isn't perfect, since it also matches lines where "//" appears halfway a line, and the substitution will also take place before the "//".

Just like with "**:substitute**", any pattern can be used. When you learn more complicated patterns later, you can use them here.

## Visual Block Mode

With **Ctrl-V** you can start selection of a rectangular area of text. There are a few commands that do something special with the text block.

There is something special about using the "**$**" command in Visual block mode. When the last motion command used was "**$**", all lines in the Visual selection will extend until the end of the line, also when the line with the cursor is shorter. This remains effective until you use a motion command that moves the cursor horizontally. Thus using "**j**" keeps it, "**h**" stops it.

## Inserting Text

The command "**I{string}**" inserts the text **{string}** in each line, just left of the visual block. You start by pressing **Ctrl-V** to enter visual block mode. Now you move the cursor to define your block. Next you type **I** to enter Insert mode, followed by the text to insert. As you type, the text appears on the first line only.

After you press **** to end the insert, the text will magically be inserted in the rest of the lines contained in the visual selection. Example:

```
	include one 
	include two 
	include three 
	include four
```

Move the cursor to the "o" of "one" and press **Ctrl-V**. Move it down with "**3j**" to "four". You now have a block selection that spans four lines. Now type:

```
Imain.<Esc>
```

The result:

```
	include main.one 
	include main.two 
	include main.three 
	include main.four
```

If the block spans short lines that do not extend into the block, the text is not inserted in that line. For example, make a Visual block selection that includes the word "long" in the first and last line of this text, and thus has no text selected in the second line:

```
	This is a long line 
	short 
	Any other long line 
		  ^^^^ selected block
```

Now use the command "**Ivery **". The result is:

```
	This is a very long line 
	short 
	Any other very long line
```

In the short line no text was inserted.

If the string you insert contains a [newline](https://www.computerhope.com/jargon/n/newline.htm), the "**I**" acts just like a Normal insert command and affects only the first line of the block.

The "**A**" command works the same way, except that it appends after the right side of the block. And it does insert text in a short line. Thus you can make a choice whether you do or don't want to append text to a short line.

There is one special case for "**A**": Select a Visual block and then use "**$**" to make the block extend to the end of each line. Using "**A**" now will append the text to the end of each line.

Using the same example from above, and then typing **"$A XXX**, you get this result:

```
	This is a long line XXX 
	short XXX 
	Any other long line XXX 
```

This really requires using the "**$**" command. vim remembers that it was used. Making the same selection by moving the cursor to the end of the longest line with other movement commands will not have the same result.

## Changing Text

The Visual block "**c**" command deletes the block and then throws you into Insert mode to enable you to type in a string. The string will be inserted in each line in the block.

Starting with the same selection of the "long" words as above, then typing "**c_LONG_**", you get this:

```
	This is a _LONG_ line 
	short 
	Any other _LONG_ line
```

Just like with "**I**" the short line is not changed. Also, you can't enter a newline in the new text.

The "**C**" command deletes text from the left edge of the block to the end of line. It then puts you in Insert mode so that you can type in a string, which is added to the end of each line.

Starting with the same text again, and typing "**Cnew text**" you get:

```
	This is a new text 
	short 
	Any other new text
```

Notice that, even though only the "long" word was selected, the text after it is deleted as well. Thus only the location of the left edge of the visual block really matters.

Again, short lines that do not reach into the block are excluded.

Other commands that change the characters in the block:

| **~** | swap case (**a** -> **A** and **A** -> **a**)      |
| ----- | -------------------------------------------------- |
| **U** | make uppercase (**a** -> **A** and **A** -> **A**) |
| **u** | make lowercase (**a** -> **a** and **A** -> **a**) |

## Filling With A Character

To fill the whole block with one character, use the "**r**" command. Again, starting with the same example text from above, and then typing "**rx**":

```
	This is a xxxx line 
	short 
	Any other xxxx line
```

Note: If you want to include characters beyond the end of the line in the block, check out the '**virtualedit**' feature (you can type "**:help virtualedit**" in **vim** to learn more).

## Shifting

The command "**>**" shifts the selected text to the right one shift amount, inserting whitespace. The starting point for this shift is the left edge of the visual block.

With the same example again, "**>**" gives this result:

```
	This is a	  long line 
	short 
	Any other	  long line
```

The shift amount is specified with the '**shiftwidth**' option. To change it to use 4 spaces:

```
:set shiftwidth=4
```

The "**<**" command removes one shift amount of whitespace at the left edge of the block. This command is limited by the amount of text that is there; so if there is less than a shift amount of whitespace available, it removes what it can.

## Joining Lines

The "**J**" command joins all selected lines together into one line. Thus it removes the line breaks. Actually, the line break, leading white space and trailing white space is replaced by one space. Two spaces are used after a line ending (that can be changed with the '**joinspaces**' option).

Let's use the example that we got so familiar with now. The result of using the "**J**" command:

```
	This is a long line short Any other long line 
```

The "**J**" command doesn't require a blockwise selection. It works with "**v**" and "**V**" selection in exactly the same way.

If you don't want the white space to be changed, use the "**gJ**" command.

## Reading and writing part of a file

When you are writing an e-mail message, you may want to include another file. This can be done with the "**:read {filename}**" command. The text of the file is put below the cursor line.

Starting with this text:

```
	Hi John, 
	Here is the diff that fixes the bug: 
	Bye, Pierre.
```

Move the cursor to the second line and type:

```
	:read patch
```

The file named "**patch**" will be inserted, with this result:

```
	Hi John, 
	Here is the diff that fixes the bug: 
	2c2 
	<	for (i = 0; i <= length; ++i) 
	--- 
	>	for (i = 0; i < length; ++i) 
	Bye, Pierre.
```

The "**:read**" command accepts a range. The file will be put below the last line number of this range. Thus "**:$r patch**" appends the file "patch" at the end of the file.

What if you want to read the file above the first line? This can be done with the line number zero. This line doesn't really exist, you will get an error message when using it with most commands. But this command is allowed:

```
:0read patch
```

The file "patch" will be put above the first line of the file.

## Writing A Range Of Lines

To write a range of lines to a file, the "**:write**" command can be used. Without a range it writes the whole file. With a range only the specified lines are written:

```
:.,$write tempo
```

This writes the lines from the cursor until the end of the file into the file "tempo". If this file already exists you will get an error message. **vim** protects you from accidentally overwriting an existing file. If you know what you are doing and want to overwrite the file, append **!**:

```
:.,$write! tempo
```

CAREFUL: The **!** must follow the "**:write**" command immediately, without white space. Otherwise, it becomes a filter command, which is explained later on this page.

## Appending To A File

In the first section of this page was explained how to collect a number of lines into a register. The same can be done to collect lines in a file. Write the first line with this command:

```
:.write collection
```

Now move the cursor to the second line you want to collect, and type this:

```
:.write >>collection
```

The "**>>**" tells **vim** the "collection" file is not to be written as a new file, but the line must be appended at the end. You can repeat this as many times as you like.

## Formatting text

When you are typing plain text, it's nice if the length of each line is automatically trimmed to fit in the window. To make this happen while inserting text, set the '**textwidth**' option:

```
:set textwidth=72
```

To check the current value of '**textwidth**':

```
:set textwidth
```

Now lines will be broken to take only up to 72 characters. But when you insert text halfway a line, or when you delete a few words, the lines will get too long or too short. **vim** doesn't automatically reformat the text.

To tell **vim** to format the current paragraph:

```
gqap
```

This starts with the "**gq**" command, which is an operator. Following is "**ap**", the text object that stands for "a paragraph". A paragraph is separated from the next paragraph by an empty line.

Note: A blank line, which contains white space, does NOT separate paragraphs. This is hard to notice!

Instead of "**ap**" you could use any motion or text object. If your paragraphs are properly separated, you can use this command to format the whole file:

```
gggqG
```

"**gg**" takes you to the first line, "**gq**" is the format operator and "**G**" the motion that jumps to the last line. In case your paragraphs aren't clearly defined, you can format just the lines you manually select. Move the cursor to the first line you want to format. Start with the command "**gqj**". This formats the current line and the one below it. If the first line was short, words from the next line will be appended. If it was too long, words will be moved to the next line. The cursor moves to the second line. Now you can use "**.**" to repeat the command. Keep doing this until you are at the end of the text you want to format.

## Changing Case

You have text with section headers in lowercase. You want to make the word "section" all uppercase. Do this with the "gU" operator. Start with the cursor in the first column:

```
			     gUw
 	section header	    ---->      SECTION header
```

The "**gu**" operator does exactly the opposite:

```
			     guw
 	SECTION header	    ---->      section header
```

You can also use "**g~**" to swap case. All these are operators, thus they work with any motion command, with text objects and in Visual mode.

To make an operator work on lines you double it. The delete operator is "**d**", thus to delete a line you use "**dd**". Similarly, "**gugu**" makes a whole line lowercase. This can be shortened to "**guu**". "**gUgU**" is shortened to "**gUU**" and "**g~g~**" to "**g~~**". Example:

```
				g~~ 
 	Some GIRLS have Fun    ---->   sOME girls HAVE fUN 
```

## Using An External Program

**vim** has a very powerful set of commands, it can do anything. But there may still be something that an external command can do better or faster.

The command "**!{motion}{program}**" takes a block of text and filters it through an external program. In other words, it runs the system command represented by {program}, giving it the block of text represented by {motion} as input. The output of this command then replaces the selected block.

Because this summarizes badly if you are unfamiliar with UNIX filters, take a look at an example. The sort command sorts a file. If you execute the following command, the unsorted file input.txt will be sorted and written to output.txt. This works on both UNIX and Microsoft Windows.

```
sort <input.txt >output.txt
```

Now do the same thing in **vim**. You want to sort lines 1 through 5 of a file. You start by putting the cursor on line 1. Next you execute the following command:

```
!5G
```

The "**!**" tells **vim** that you are performing a filter operation. The **vim** editor expects a motion command to follow, indicating which part of the file to filter. The "**5G**" command tells vim to go to line 5, so it now knows that it is to filter lines 1 (the current line) through 5.

In anticipation of the filtering, the cursor drops to the bottom of the screen and a ! prompt displays. You can now type in the name of the filter program, in this case [sort](https://www.computerhope.com/unix/usort.htm). Therefore, your full command is as follows:

```
!5Gsort<Enter>
```

The result is that the sort program is run on the first 5 lines. The output of the program replaces these lines.

```
	line 55     -->    line 11
	line 33	    -->    line 22
	line 11	    -->    line 33
	line 22	    -->    line 44
	line 44	    -->    line 55
	last line   -->    last line
```

The "**!!**" command filters the current line through a filter. In Unix the [date](https://www.computerhope.com/unix/udate.htm) command prints the current time and date. "**!!date**" replaces the current line with the output of **date**. This is useful to add a [timestamp](https://www.computerhope.com/jargon/t/timestam.htm) to a file.

## When It Doesn't Work

Starting a [shell](https://www.computerhope.com/jargon/s/shell.htm), sending it text and capturing the output requires that **vim** knows how the shell works exactly. When you have problems with filtering, check the values of these options:

| '**shell**'        | specifies the program that **vim** uses to execute external programs. |
| ------------------ | ------------------------------------------------------------ |
| '**shellcmdflag**' | argument to pass a command to the shell                      |
| '**shellquote**'   | quote to be used around the command                          |
| '**shellxquote**'  | quote to be used around the command and redirection          |
| '**shelltype**'    | kind of shell (only for the Amiga)                           |
| '**shellslash**'   | use forward slashes in the command (only for MS-Windows and alikes) |
| '**shellredir**'   | string used to write the command output into a file          |

On Unix this is hardly ever a problem, because there are two kinds of shells: "[sh](https://www.computerhope.com/unix/ush.htm)"-like and "[csh](https://www.computerhope.com/unix/ucsh.htm)"-like. **vim** checks the '**shell**' option and sets related options automatically, depending on whether it sees "**csh**" somewhere in '**shell**'.

On MS-Windows, however, there are many different shells and you might have to tune the options to make filtering work. Check the help for the options for more information.

## Reading Command Output

To read the contents of the current directory into the file, use the following commands.

on Unix:

```
:read !ls
```

on MS Windows:

```
:read !dir
```

The output of the "[ls](https://www.computerhope.com/unix/uls.htm)" or "[dir](https://www.computerhope.com/jargon/d/dir.htm)" command is captured and inserted in the text, below the cursor. This is similar to reading a file, except that the "**!**" is used to tell **vim** that a command follows.

The command may have arguments. And a range can be used to tell where **vim** should put the lines:

```
:0read !date -u
```

This inserts the current time and date in UTC format at the top of the file. If you have a date command that accepts the "**-u**" argument. Note the difference with using "**!!date**": that replaced a line, while "**:read !date**" will insert a line.

## Writing Text To A Command

The Unix command [wc](https://www.computerhope.com/unix/uwc.htm) counts words. To count the words in the current file:

```
:write !wc
```

This is the same write command as before, but instead of a file name the "**!**" character is used and the name of an external command. The written text will be passed to the specified command as its standard input. The output could look like this:

```
       4      47     249 
```

The **wc** command isn't [verbose](https://www.computerhope.com/jargon/v/verbose.htm). This output means you have **4** lines, **47** words and **249** characters.

Watch out for this mistake:

```
:write! wc
```

This will write the file "**wc**" in the current directory, with force. (White space is important here!)

## Redrawing The Screen

If the external command produced an error message, the display may have been messed up. **vim** is very efficient and only redraws those parts of the screen that it knows need redrawing. But it can't know about what another program has written. To tell **vim** to redraw the screen, press **Ctrl-L**.

## Useful Tricks

The substitute command can be used to replace all occurrences of a word with another word:

```
:%s/four/4/g
```

The "**%**" range means to replace in all lines. The "**g**" flag at the end causes all words in a line to be replaced.

This will not do the right thing if your file also contains "thirtyfour". It would be replaced with "thirty4". To avoid this, use the "**\<**" item to match the start of a word:

```
:%s/\\<four/4/g
```

Obviously, this still goes wrong on "fourteen". Use "**\>**" to match the end of a word:

```
:%s/\<four\>/4/g
```

If you are programming, you might want to replace "four" in comments, but not in the code. Since this is difficult to specify, add the "**c**" flag to have the substitute command prompt you for each replacement:

```
:%s/\<four\>/4/gc
```

## Replacing In Several Files

Suppose you want to replace a word in more than one file. You could edit each file and type the command manually. It's a lot faster to use record and playback.

Let's assume you have a directory with C++ files, all ending in ".cpp". There is a function called "GetResp" that you want to rename to "GetAnswer".

| **vim \*.cpp**        | Start **vim**, defining the argument list to contain all the C++ files. You are now in the first file. |
| --------------------- | ------------------------------------------------------------ |
| **qq**                | Start recording into the **q** register                      |
| **:%s/\/GetAnswer/g** | Do the replacements in the first file.                       |
| **:wnext**            | Write this file and move to the next one.                    |
| **q**                 | Stop recording.                                              |
| **@q**                | Execute the **q** register. This will replay the substitution and "**:wnext**". You can verify that this doesn't produce an error message. |
| **999@q**             | Execute the **q** register on the remaining files. At the last file you will get an error message, because "**:wnext**" cannot move to the next file. This stops the execution, and everything is done. |

Note: When playing back a recorded sequence, an error stops the execution. Therefore, make sure you don't get an error message when recording.

There is one catch: If one of the .cpp files does not contain the word "GetResp", you will get an error and replacing will stop. To avoid this, add the "**e**" flag to the substitute command:

```
:%s/\<GetResp\>/GetAnswer/ge
```

The "**e**" flag tells "**:substitute**" that not finding a match is not an error.

In this next example, let's change the text "Last, First" to "First Last". Let's say you have a list of names in this form:

```
	Doe, John 
	Smith, Peter
```

You want to change that to:

```
	John Doe 
	Peter Smith
```

This can be done with just one command:

```
:%s/\([^,]*\), \(.*\)/\2 \1/
```

Let's break this down in parts. Obviously it starts with a substitute command. The "**%**" is the line range, which stands for the whole file. Thus the substitution is done in every line in the file. The arguments for the substitute command are "**/from/to/**". The slashes separate the "from" pattern and the "to" string. This is what the "from" pattern contains:

| The whole search string is:                        | `**\([^,]\*\), \(.\*\)**` |
| -------------------------------------------------- | ------------------------- |
| The first part between **\( \)** matches "Last":   | `**\(     \)**`           |
| by matching anything but a comma:                  | `**[^,]**`                |
| ...any number of times:                            | `*****`                   |
| ...then matching a "**,** " literally:             | `**,**`                   |
| The second part between **\( \)** matches "First": | `**\(  \)**`              |
| by matching any character:                         | `**.**`                   |
| ...any number of times:                            | `*****`                   |

In the "to" part we have "**\2**" and "**\1**". These are called backreferences. They refer to the text matched by the "**\( \)**" parts in the pattern. "**\2**" refers to the text matched by the second "**\( \)**", which is the "First" name. "**\1**" refers to the first "**\( \)**", which is the "Last" name.

You can use up to nine backreferences in the "to" part of a substitute command. "**\0**" stands for the whole matched pattern.

## Sort a list

In a [Makefile](https://www.computerhope.com/unix/umake.htm) you often have a list of files. For example:

```
	OBJS = \ 
		version.o \ 
		pch.o \ 
		getopt.o \ 
		util.o \ 
		getopt1.o \ 
		inp.o \ 
		patch.o \ 
		backup.o
```

To sort this list, filter the text through the external **sort** command:

```
/^OBJS
j
:.,/^$/-1!sort
```

This goes to the first line, where "OBJS" is the first thing in the line. Then it goes one line down and filters the lines until the next empty line. You could also select the lines in Visual mode and then use "**!sort**". That's easier to type, but more work when there are many lines.

The result is this:

```
	OBJS = \ 
		backup.o 
		getopt.o \ 
		getopt1.o \ 
		inp.o \ 
		patch.o \ 
		pch.o \ 
		util.o \ 
		version.o \
```

Notice that a backslash at the end of each line is used to indicate the line continues. After sorting, this is wrong! The "backup.o" line that was at the end didn't have a backslash. Now that it sorts to another place, it must have a backslash.

The simplest solution is to add the backslash with "**A \**". You can keep the backslash in the last line, if you make sure an empty line comes after it. That way you don't have this problem again.

## Reverse line order

The **:global** command can be combined with the **:move** command to move all the lines before the first line, resulting in a reversed file. The command is:

```
:global/^/m 0
```

Abbreviated:

```
:g/^/m 0
```

The "**^**" regular expression matches the beginning of the line (even if the line is blank). The **:move** command moves the matching line to after the mythical zeroth line, so the current matching line becomes the first line of the file. As the **:global** command is not confused by the changing line numbering, **:global** proceeds to match all remaining lines of the file and puts each as the first.

This also works on a range of lines. First move to above the first line and mark it with "mt". Then move the cursor to the last line in the range and type:

```
:'t+1,.g/^/m 't
```

## Count words

Sometimes you have to write a text with a maximum number of words. **vim** can count the words for you.

When the whole file is what you want to count the words in, use this command:

```
g Ctrl-G
```

Do not type a space after the **g**, this is just used here to make the command easy to read.

The output looks like this:

```
Col 1 of 0; Line 141 of 157; Word 748 of 774; Byte 4489 of 4976 
```

You can see on which word you are (748), and the total number of words in the file (774).

When the text is only part of a file, you could move to the start of the text, type "**g Ctrl-G**", move to the end of the text, type "**g Ctrl-G**" again, and then use your brain to compute the difference in the word position. That's a good exercise, but there is an easier way. With Visual mode, select the text you want to count words in. Then type **g Ctrl-G**. The result:

```
Selected 5 of 293 Lines; 70 of 1884 Words; 359 of 10928 Bytes 
```

## Find A man Page

While editing a shell script or C program, you are using a command or function that you want to find the man page for (this applies to Linux, not MS Windows). Let's first use a simple way: Move the cursor to the word you want to find help on and press **K**.

**vim** will run the external [man](https://www.computerhope.com/unix/uman.htm) program on the word. If the man page is found, it is displayed. This uses the normal pager to scroll through the text (mostly the [more](https://www.computerhope.com/unix/umore.htm) program). When you get to the end pressing **** will get you back into **vim**.

A disadvantage is that you can't see the man page and the text you are working on at the same time. There is a trick to make the man page appear in a vim window. First, load the man filetype plugin:

```
:runtime! ftplugin/man.vim
```

Put this command in your vimrc file if you intend to do this often. Now you can use the "**:Man**" command to open a window on a man page:

```
:Man csh
```

You can scroll around and the text is highlighted, which allows you to find the help you were looking for. Use **Ctrl-W w** to jump to the window with the text you were working on.

To find a man page in a specific section, put the section number first. For example, to look in section 3 for "[echo](https://www.computerhope.com/unix/uecho.htm)":

```
:Man 3 echo
```

To jump to another man page, which is in the text with the typical form "word(1)", press **Ctrl-]** on it. Further "**:Man**" commands will use the same window.

To display a man page for the word under the cursor, use the command **\K**.

(If you redefined the ****, use it instead of the backslash). For example, you want to know the return value of "**strstr()**" while editing this line:

```
if ( strstr (input, "aap") == ) 
```

Move the cursor to somewhere on "**strstr**" and type "**\K**". A window will open to display the man page for **strstr()**.

## Trim blanks

Some people find spaces and tabs at the end of a line useless, wasteful, and ugly. To remove whitespace at the end of every line, execute the following command:

```
:%s/\s\+$//
```

The line range "%" is used, thus this works on the whole file. The pattern that the "**:substitute**" command matches with is "**\s\+$**". This finds white space characters (\s), 1 or more of them (\+), before the end-of-line ($).

The "to" part of the substitute command is empty: "//". Thus it replaces with nothing, effectively deleting the matched white space.

Another wasteful use of spaces is placing them before a tab. Often these can be deleted without changing the amount of white space. But not always! Therefore, you can best do this manually. Use this search command: "**/**". You cannot see it, but there is a space before a tab in this command. Thus it's "**/**". Now use "**x**" to delete the space and check that the amount of white space doesn't change. You might have to insert a tab if it does change. Type "**n**" to find the next match. Repeat this until no more matches can be found.

## Find where a word is used

If you are a UNIX user, you can use a combination of **vim** and the grep command to edit all the files that contain a given word. This is extremely useful if you are working on a program and want to view or edit all the files that contain a specific variable.

For example, suppose you want to edit all the C program files that contain the word "frame_counter". To do this you use the command:

```
vim `grep -l frame_counter *.c`
```

Let's look at this command in detail. The grep command searches through a set of files for a given word. Because the **-l** argument is specified, the command will only list the files containing the word and not print the matching lines. The word it is searching for is "frame_counter". Actually, this can be any regular expression. Note: What grep uses for regular expressions is not exactly the same as what **vim** uses.

The entire command is enclosed in backticks ("**`**"). This tells the UNIX shell to run this command and pretend that the results were typed on the command line. So what happens is that the grep command is run and produces a list of files, these files are put on the **vim** command line. This results in **vim** editing the file list that is the output of [grep](https://www.computerhope.com/unix/ugrep.htm). You can then use commands like "**:next**" and "**:first**" to browse through the files.

## Finding Each Line

The above command only finds the files in which the word is found. You still have to find the word within the files.

**vim** has a built-in command that you can use to search a set of files for a given string. If you want to find all occurrences of "error_string" in all C program files, for example, enter the following command:

```
:grep error_string *.c
```

This causes **vim** to search for the string "error_string" in all the specified files (*.c). The editor will now open the first file where a match is found and position the cursor on the first matching line. To go to the next matching line (no matter in what file it is), use the "**:cnext**" command. To go to the previous match, use the "**:cprev**" command. Use "**:clist**" to see all the matches and where they are.

The "**:grep**" command uses the external commands grep (on Unix) or findstr (on Windows). You can change this by setting the option '**grepprg**'.

## Command Line Abbreviations

Some of the "**:**" commands are really long. We already mentioned that "**:substitute**" can be abbreviated to "**:s**". This is a generic mechanism, all "**:**" commands can be abbreviated.

How short can a command get? There are 26 letters, and many more commands. For example, "**:set**" also starts with "**:s**", but "**:s**" doesn't start a "**:set**" command. Instead "**:set**" can be abbreviated to "**:se**".

When the shorter form of a command could be used for two commands, it stands for only one of them. There is no logic behind which one, you have to learn them. In the help files the shortest form that works is mentioned. For example:

```
:s[ubstitute]
```

This means that the shortest form of "**:substitute**" is "**:s**". The following characters are optional. Thus "**:su**" and "**:sub**" also work.

In the user manual we will either use the full name of command, or a short version that is still readable. For example, "**:function**" can be abbreviated to "**:fu**". But since most people don't understand what that stands for, we will use "**:fun**". vim doesn't have a "**:funny**" command, otherwise "**:fun**" would be confusing too.

It is recommended that in **vim** scripts you write the full command name. That makes it easier to read back when you make later changes. Except for some often used commands like "**:w**" ("**:write**") and "**:r**" ("**:read**").

A particularly confusing one is "**:end**", which could stand for "**:endif**", "**:endwhile**" or "**:endfunction**". Therefore, always use the full name.

## Short Option Names

In the user manual the long version of the option names is used. Many options also have a short name. Unlike "**:**" commands, there is only one short name that works. For example, the short name of 'autoindent' is 'ai'. Thus these two commands do the same thing:

```
:set autoindent
:set ai
```

## Command Line Completion

This is one of those **vim** features that, by itself, is a reason to switch from **Vi** to **vim**. Once you have used this, you can't do without.

Suppose you have a directory that contains these files:

```
	info.txt
	intro.txt
	bodyofthepaper.txt
```

To edit the last one, you use the command:

```
:edit bodyofthepaper.txt
```

It's easy to type this wrong. A much quicker way is:

```
:edit b<Tab>
```

Which will result in the same command. What happened? The **** key does completion of the word before the cursor. In this case "**b**". **vim** looks in the directory and finds only one file that starts with a "**b**". That must be the one you are looking for, thus **vim** completes the file name for you.

Now type:

```
:edit i<Tab>
```

**vim** will beep, and give you:

```
:edit info.txt
```

The beep means that **vim** has found more than one match. It then uses the first match it found (alphabetically). If you press **** again, you get:

```
:edit intro.txt
```

Thus, if the first **** doesn't give you the file you were looking for, press it again. If there are more matches, you will see them all, one at a time.

If you press **** on the last matching entry, you will go back to what you first typed:

```
:edit i
```

Then it starts all over again. Thus **vim** cycles through the list of matches. Use **Ctrl-P** to go through the list in the other direction:

```
	      <────────────────────<Tab>──────────────────────────┐
								  |
		 <Tab> ──>		 <Tab> ──>
	:edit i		      :edit info.txt		   :edit intro.txt
		  <── Ctrl-P		       <── Ctrl-P
	   |
	   └───────────────────────Ctrl-P─────────────────────>
```

## Command Context

When you type "**:set i**" instead of "**:edit i**" and press **** you get:

```
:set icon
```

Hey, why didn't you get "**:set info.txt**"? That's because **vim** has context sensitive completion. The kind of words vim will look for depends on the command before it. The vim command knows that you cannot use a file name just after a "**:set**" command, but you can use an option name.

Again, if you repeat typing the ****, **vim** will cycle through all matches. There are quite a few, it's better to type more characters first:

```
:set isk<Tab>
```

Gives:

```
:set iskeyword
```

Now type "**=**" and press ****:

```
:set iskeyword=@,48-57,_,192-255
```

What happens here is that vim inserts the old value of the option. Now you can edit it.

What is completed with **** is what **vim** expects in that place. Just try it out to see how it works. In some situations, you will not get what you want. That's either because **vim** doesn't know what you want, or because completion was not implemented for that situation. In that case you will get a **** inserted (displayed as **^I**).

## Viewing List Matches

When there are many matches, you would like to see an overview. Do this by pressing **Ctrl-D**. For example, pressing **Ctrl-D** after:

```
:set is
```

results in:

```
:set is
incsearch  isfname    isident    iskeyword  isprint
:set is
```

**vim** lists the matches and then comes back with the text you typed. You can now check the list for the item you wanted. If it isn't there, you can use **** to correct the word. If there are many matches, type a few more characters before pressing **** to complete the rest.

If you have watched carefully, you will have noticed that "incsearch" doesn't start with "is". In this case "is" stands for the short name of "incsearch". Many options have a short and a long name. **vim** is clever enough to know that you might have wanted to expand the short name of the option into the long name.

## There Is More

The **Ctrl-L** command completes the word to the longest unambiguous string. If you type "**:edit i**" and there are files "info.txt" and "info_backup.txt" you will get "**:edit info**".

The '**wildmode**' option can be used to change the way completion works. The '**wildmenu**' option can be used to get a menu-like list of matches. Use the '**suffixes**' option to specify files that are less important and appear at the end of the list of files. The '**wildignore**' option specifies files that are not listed at all.

## Examples

```
vim
```

Launches **vim**, placing you in normal mode with a new document.

```
vim document.txt
```

Launches **vim** and opens the file **document.txt**, or a blank document if **document.txt** does not already exist.

## Related commands

[**ed**](https://www.computerhope.com/unix/ued.htm) — A simple text editor.
[**emacs**](https://www.computerhope.com/unix/uemacs.htm) — A highly extensible text editor.
[**ex**](https://www.computerhope.com/unix/uex.htm) — Line-editor mode of the vi text editor.
[**pico**](https://www.computerhope.com/unix/upico.htm) — A simple text editor.