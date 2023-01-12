---
создан: 06-01-2023T03:22:33 (UTC +03:00)
tags: []
исходник: https://www.mankier.com/1/tmux
автор: AuthorsNicholas Marriott <nicholas.marriott@gmail.com>
---

# tmux command man page | ManKier 

---
terminal multiplexer

[

## Examples (TL;DR)

](https://www.mankier.com/1/tmux#Examples_(TL;DR))

+   Start a new session: `tmux`
    
+   Start a new named session: `tmux new -s name`
    
+   List existing sessions: `tmux ls`
    
+   Attach to the most recently used session: `tmux attach`
    
+   Detach from the current session (inside a tmux session): `Ctrl-B d`
    
+   Create a new window (inside a tmux session): `Ctrl-B c`
    
+   Switch between sessions and windows (inside a tmux session): `Ctrl-B w`
    
+   Kill a session by name: `tmux kill-session -t name`
    

[tldr.sh](https://tldr.sh/)

[

## Synopsis

](https://www.mankier.com/1/tmux#Synopsis)

<table><tbody><tr><td><b>tmux</b></td><td>[-<a href="https://www.mankier.com/1/tmux#-2">2</a><a href="https://www.mankier.com/1/tmux#-C">C</a><a href="https://www.mankier.com/1/tmux#-D">D</a><a href="https://www.mankier.com/1/tmux#-l">l</a><a href="https://www.mankier.com/1/tmux#-u">u</a><a href="https://www.mankier.com/1/tmux#-v">v</a><a href="https://www.mankier.com/1/tmux#-V">V</a>] [<a href="https://www.mankier.com/1/tmux#-c">-c</a>&nbsp;<var>shell-command</var>] [<a href="https://www.mankier.com/1/tmux#-f">-f</a>&nbsp;<var>file</var>] [<a href="https://www.mankier.com/1/tmux#-L">-L</a>&nbsp;<var>socket-name</var>] [<a href="https://www.mankier.com/1/tmux#-S">-S</a>&nbsp;<var>socket-path</var>] [<a href="https://www.mankier.com/1/tmux#-T">-T</a>&nbsp;<var>features</var>] [<var>command</var>&nbsp;[<var>flags</var>]]</td></tr></tbody></table>

[

## Description

](https://www.mankier.com/1/tmux#Description)

**tmux** is a terminal multiplexer: it enables a number of terminals to be created, accessed, and controlled from a single screen. **tmux** may be detached from a screen and continue running in the background, then later reattached.

When **tmux** is started, it creates a new _session_ with a single _window_ and displays it on screen. A status line at the bottom of the screen shows information on the current session and is used to enter interactive commands.

A session is a single collection of _pseudo terminals_ under the management of **tmux**. Each session has one or more windows linked to it. A window occupies the entire screen and may be split into rectangular panes, each of which is a separate pseudo terminal (the pty(4) manual page documents the technical details of pseudo terminals). Any number of **tmux** instances may connect to the same session, and any number of windows may be present in the same session. Once all sessions are killed, **tmux** exits.

Each session is persistent and will survive accidental disconnection (such as [ssh(1)](https://www.mankier.com/1/ssh) connection timeout) or intentional detaching (with the ‘`C-b d`’ key strokes). **tmux** may be reattached using:

> `$ tmux attach`

In **tmux**, a session is displayed on screen by a _client_ and all sessions are managed by a single _server_. The server and each client are separate processes which communicate through a socket in `/tmp`.

The options are as follows:

[\-2](https://www.mankier.com/1/tmux#-2)

Force **tmux** to assume the terminal supports 256 colours. This is equivalent to [\-T](https://www.mankier.com/1/tmux#-T) 256.

[\-C](https://www.mankier.com/1/tmux#-C)

Start in control mode (see the [Control Mode](https://www.mankier.com/1/tmux#Control_Mode) section). Given twice (`-CC`) disables echo.

[\-c](https://www.mankier.com/1/tmux#-c) shell-command

Execute shell-command using the default shell. If necessary, the **tmux** server will be started to retrieve the `default-shell` option. This option is for compatibility with [sh(1)](https://www.mankier.com/1/bash) when **tmux** is used as a login shell.

[\-D](https://www.mankier.com/1/tmux#-D)

Do not start the **tmux** server as a daemon. This also turns the `exit-empty` option off. With [\-D](https://www.mankier.com/1/tmux#-D), command may not be specified.

[\-f](https://www.mankier.com/1/tmux#-f) file

Specify an alternative configuration file. By default, **tmux** loads the system configuration file from `/etc/tmux.conf`, if present, then looks for a user configuration file at `~/.tmux.conf,` `$XDG_CONFIG_HOME/tmux/tmux.conf` or `~/.config/tmux/tmux.conf`.

The configuration file is a set of **tmux** commands which are executed in sequence when the server is first started. **tmux** loads configuration files once when the server process has started. The `source-file` command may be used to load a file later.

**tmux** shows any error messages from commands in configuration files in the first session created, and continues to process the rest of the configuration file.

[\-L](https://www.mankier.com/1/tmux#-L) socket-name

**tmux** stores the server socket in a directory under `TMUX_TMPDIR` or `/tmp` if it is unset. The default socket is named _default_. This option allows a different socket name to be specified, allowing several independent **tmux** servers to be run. Unlike [\-S](https://www.mankier.com/1/tmux#-S) a full path is not necessary: the sockets are all created in a directory `tmux-UID` under the directory given by `TMUX_TMPDIR` or in `/tmp`. The `tmux-UID` directory is created by **tmux** and must not be world readable, writable or executable.

If the socket is accidentally removed, the `SIGUSR1` signal may be sent to the **tmux** server process to recreate it (note that this will fail if any parent directories are missing).

[\-l](https://www.mankier.com/1/tmux#-l)

Behave as a login shell. This flag currently has no effect and is for compatibility with other shells when using tmux as a login shell.

[\-N](https://www.mankier.com/1/tmux#-N)

Do not start the server even if the command would normally do so (for example `new-session` or `start-server`).

[\-S](https://www.mankier.com/1/tmux#-S) socket-path

Specify a full alternative path to the server socket. If [\-S](https://www.mankier.com/1/tmux#-S) is specified, the default socket directory is not used and any [\-L](https://www.mankier.com/1/tmux#-L) flag is ignored.

[\-u](https://www.mankier.com/1/tmux#-u)

Write UTF-8 output to the terminal even if the first environment variable of `LC_ALL`, `LC_CTYPE`, or `LANG` that is set does not contain "UTF-8" or "UTF8". This is equivalent to [\-T](https://www.mankier.com/1/tmux#-T) UTF-8.

[\-T](https://www.mankier.com/1/tmux#-T) features

Set terminal features for the client. This is a comma-separated list of features. See the `terminal-features` option.

[\-v](https://www.mankier.com/1/tmux#-v)

Request verbose logging. Log messages will be saved into `tmux-client-PID.log` and `tmux-server-PID.log` files in the current directory, where _PID_ is the PID of the server or client process. If [\-v](https://www.mankier.com/1/tmux#-v) is specified twice, an additional `tmux-out-PID.log` file is generated with a copy of everything **tmux** writes to the terminal.

The `SIGUSR2` signal may be sent to the **tmux** server process to toggle logging between on (as if [\-v](https://www.mankier.com/1/tmux#-v) was given) and off.

[\-V](https://www.mankier.com/1/tmux#-V)

Report the **tmux** version.

command \[flags\]

This specifies one of a set of commands used to control **tmux**, as described in the following sections. If no commands are specified, the `new-session` command is assumed.

[

## Default Key Bindings

](https://www.mankier.com/1/tmux#Default_Key_Bindings)

**tmux** may be controlled from an attached client by using a key combination of a prefix key, ‘`C-b`’ (Ctrl-b) by default, followed by a command key.

The default command key bindings are:

C-b

Send the prefix key (C-b) through to the application.

C-o

Rotate the panes in the current window forwards.

C-z

Suspend the **tmux** client.

!

Break the current pane out of the window.

"

Split the current pane into two, top and bottom.

#

List all paste buffers.

$

Rename the current session.

%

Split the current pane into two, left and right.

&

Kill the current window.

'

Prompt for a window index to select.

(

Switch the attached client to the previous session.

)

Switch the attached client to the next session.

,

Rename the current window.

\-

Delete the most recently copied buffer of text.

.

Prompt for an index to move the current window.

0 to 9

Select windows 0 to 9.

:

Enter the **tmux** command prompt.

;

Move to the previously active pane.

\=

Choose which buffer to paste interactively from a list.

?

List all key bindings.

D

Choose a client to detach.

L

Switch the attached client back to the last session.

\[

Enter copy mode to copy text or view the history.

\]

Paste the most recently copied buffer of text.

c

Create a new window.

d

Detach the current client.

f

Prompt to search for text in open windows.

i

Display some information about the current window.

l

Move to the previously selected window.

m

Mark the current pane (see `select-pane` `-m`).

M

Clear the marked pane.

n

Change to the next window.

o

Select the next pane in the current window.

p

Change to the previous window.

q

Briefly display pane indexes.

r

Force redraw of the attached client.

s

Select a new session for the attached client interactively.

t

Show the time.

w

Choose the current window interactively.

x

Kill the current pane.

z

Toggle zoom state of the current pane.

{

Swap the current pane with the previous pane.

}

Swap the current pane with the next pane.

~

Show previous messages from **tmux**, if any.

Page Up

Enter copy mode and scroll one page up.

Up, Down

Left, Right

Change to the pane above, below, to the left, or to the right of the current pane.

M-1 to M-5

Arrange panes in one of the five preset layouts: even-horizontal, even-vertical, main-horizontal, main-vertical, or tiled.

Space

Arrange the current window in the next preset layout.

M-n

Move to the next window with a bell or activity marker.

M-o

Rotate the panes in the current window backwards.

M-p

Move to the previous window with a bell or activity marker.

C-Up, C-Down

C-Left, C-Right

Resize the current pane in steps of one cell.

M-Up, M-Down

M-Left, M-Right

Resize the current pane in steps of five cells.

Key bindings may be changed with the `bind-key` and `unbind-key` commands.

[

## Разбор и выполнение команд

](https://www.mankier.com/1/tmux#Command_Parsing_and_Execution)

**tmux** поддерживает большое количество команд, которые можно использовать для управления его поведением. Каждая команда имеет имя и может принимать ноль или более флагов и аргументов. Они могут быть привязаны к ключу с помощью команды `bind-key` или запускаться из командной строки, сценария оболочки, файла конфигурации или командной строки. Например, одна и та же команда `set-option`, запускаемая из командной строки, из `~/.tmux.conf` и привязанная к ключу, может выглядеть так:

> ```
> $ tmux set-option -g status-style bg=cyan
> 
> set-option -g status-style bg=cyan
> 
> bind-key C set-option -g status-style bg=cyan
> 
> ```

Here, the command name is ‘`set-option`’, ‘`-g`’ is a flag and ‘`status-style`’ and ‘`bg=cyan`’ are arguments.

**tmux** distinguishes between command parsing and execution. In order to execute a command, **tmux** needs it to be split up into its name and arguments. This is command parsing. If a command is run from the shell, the shell parses it; from inside **tmux** or from a configuration file, **tmux** does. Examples of when **tmux** parses commands are:

+   in a configuration file;
    
+   typed at the command prompt (see `command-prompt`);
    
+   given to `bind-key`;
    
+   passed as arguments to `if-shell` or `confirm-before`.
    

To execute commands, each client has a ‘`command queue`’. A global command queue not attached to any client is used on startup for configuration files like `~/.tmux.conf`. Parsed commands added to the queue are executed in order. Some commands, like `if-shell` and `confirm-before`, parse their argument to create a new command which is inserted immediately after themselves. This means that arguments can be parsed twice or more - once when the parent command (such as `if-shell`) is parsed and again when it parses and executes its command. Commands like `if-shell`, `run-shell` and `display-panes` stop execution of subsequent commands on the queue until something happens - `if-shell` and `run-shell` until a shell command finishes and `display-panes` until a key is pressed. For example, the following commands:

> ```
> new-session; new-window
> if-shell "true" "split-window"
> kill-session
> 
> ```

Will execute `new-session`, `new-window`, `if-shell`, the shell command [true(1)](https://www.mankier.com/1/true), `split-window` and `kill-session` in that order.

The [Commands](https://www.mankier.com/1/tmux#Commands) section lists the **tmux** commands and their arguments.

[

## Parsing Syntax

](https://www.mankier.com/1/tmux#Parsing_Syntax)

This section describes the syntax of commands parsed by **tmux**, for example in a configuration file or at the command prompt. Note that when commands are entered into the shell, they are parsed by the shell - see for example ksh(1) or [csh(1)](https://www.mankier.com/1/tcsh).

Each command is terminated by a newline or a semicolon (;). Commands separated by semicolons together form a ‘`command sequence`’ - if a command in the sequence encounters an error, no subsequent commands are executed.

It is recommended that a semicolon used as a command separator should be written as an individual token, for example from [sh(1)](https://www.mankier.com/1/bash):

> ```
> $ tmux neww \; splitw
> 
> ```

Or:

> ```
> $ tmux neww ';' splitw
> 
> ```

Or from the tmux command prompt:

> ```
> neww ; splitw
> 
> ```

However, a trailing semicolon is also interpreted as a command separator, for example in these [sh(1)](https://www.mankier.com/1/bash) commands:

> ```
> $ tmux neww\\; splitw
> 
> ```

Or:

> ```
> $ tmux 'neww;' splitw
> 
> ```

As in these examples, when running tmux from the shell extra care must be taken to properly quote semicolons:

1.  Semicolons that should be interpreted as a command separator should be escaped according to the shell conventions. For [sh(1)](https://www.mankier.com/1/bash) this typically means quoted (such as ‘`neww ';' splitw`’) or escaped (such as ‘`neww \\\\; splitw`’).
    
2.  Individual semicolons or trailing semicolons that should be interpreted as arguments should be escaped twice: once according to the shell conventions and a second time for **tmux**; for example:
    
    > ```
    > $ tmux neww 'foo\\;' bar
    > $ tmux neww foo\\\\; bar
    >     
    > ```
    
3.  Semicolons that are not individual tokens or trailing another token should only be escaped once according to shell conventions; for example:
    
    > ```
    > $ tmux neww 'foo-;-bar'
    > $ tmux neww foo-\\;-bar
    >     
    > ```
    

Comments are marked by the unquoted # character - any remaining text after a comment is ignored until the end of the line.

If the last character of a line is \\, the line is joined with the following line (the \\ and the newline are completely removed). This is called line continuation and applies both inside and outside quoted strings and in comments, but not inside braces.

Command arguments may be specified as strings surrounded by single (') quotes, double quotes (") or braces ({}). This is required when the argument contains any special character. Single and double quoted strings cannot span multiple lines except with line continuation. Braces can span multiple lines.

Outside of quotes and inside double quotes, these replacements are performed:

+   Environment variables preceded by $ are replaced with their value from the global environment (see the [Global and Session Environment](https://www.mankier.com/1/tmux#Global_and_Session_Environment) section).
    
+   A leading ~ or ~user is expanded to the home directory of the current or specified user.
    
+   \\uXXXX or \\uXXXXXXXX is replaced by the Unicode codepoint corresponding to the given four or eight digit hexadecimal number.
    
+   When preceded (escaped) by a \\, the following characters are replaced: \\e by the escape character; \\r by a carriage return; \\n by a newline; and \\t by a tab.
    
+   \\ooo is replaced by a character of the octal value ooo. Three octal digits are required, for example \\001. The largest valid character is \\377.
    
+   Any other characters preceded by \\ are replaced by themselves (that is, the \\ is removed) and are not treated as having any special meaning - so for example \\; will not mark a command sequence and \\$ will not expand an environment variable.
    

Braces are parsed as a configuration file (so conditions such as ‘`%if`’ are processed) and then converted into a string. They are designed to avoid the need for additional escaping when passing a group of **tmux** commands as an argument (for example to `if-shell`). These two examples produce an identical command - note that no escaping is needed when using {}:

> ```
> if-shell true {
>     display -p 'brace-dollar-foo: }$foo'
> }
> 
> if-shell true "display -p 'brace-dollar-foo: }\$foo'"
> 
> ```

Braces may be enclosed inside braces, for example:

> ```
> bind x if-shell "true" {
>     if-shell "true" {
>         display "true!"
>     }
> }
> 
> ```

Environment variables may be set by using the syntax ‘`name=value`’, for example ‘`HOME=/home/user`’. Variables set during parsing are added to the global environment. A hidden variable may be set with ‘`%hidden`’, for example:

> ```
> %hidden MYVAR=42
> 
> ```

Hidden variables are not passed to the environment of processes created by tmux. See the [Global and Session Environment](https://www.mankier.com/1/tmux#Global_and_Session_Environment) section.

Commands may be parsed conditionally by surrounding them with ‘`%if`’, ‘`%elif`’, ‘`%else`’ and ‘`%endif`’. The argument to ‘`%if`’ and ‘`%elif`’ is expanded as a format (see [Formats](https://www.mankier.com/1/tmux#Formats)) and if it evaluates to false (zero or empty), subsequent text is ignored until the closing ‘`%elif`’, ‘`%else`’ or ‘`%endif`’. For example:

> ```
> %if "#{==:#{host},myhost}"
> set -g status-style bg=red
> %elif "#{==:#{host},myotherhost}"
> set -g status-style bg=green
> %else
> set -g status-style bg=blue
> %endif
> 
> ```

Will change the status line to red if running on ‘`myhost`’, green if running on ‘`myotherhost`’, or blue if running on another host. Conditionals may be given on one line, for example:

> ```
> %if #{==:#{host},myhost} set -g status-style bg=red %endif
> 
> ```

[

## Commands

](https://www.mankier.com/1/tmux#Commands)

This section describes the commands supported by **tmux**. Most commands accept the optional `-t` (and sometimes `-s`) argument with one of target-client, target-session, target-window, or target-pane. These specify the client, session, window or pane which a command should affect.

target-client should be the name of the client, typically the pty(4) file to which the client is connected, for example either of `/dev/ttyp1` or `ttyp1` for the client attached to `/dev/ttyp1`. If no client is specified, **tmux** attempts to work out the client currently in use; if that fails, an error is reported. Clients may be listed with the `list-clients` command.

target-session is tried as, in order:

1.  A session ID prefixed with a $.
    
2.  An exact name of a session (as listed by the `list-sessions` command).
    
3.  The start of a session name, for example ‘`mysess`’ would match a session named ‘`mysession`’.
    
4.  An [fnmatch(3)](https://www.mankier.com/3/fnmatch) pattern which is matched against the session name.
    

If the session name is prefixed with an ‘`=`’, only an exact match is accepted (so ‘`=mysess`’ will only match exactly ‘`mysess`’, not ‘`mysession`’).

If a single session is found, it is used as the target session; multiple matches produce an error. If a session is omitted, the current session is used if available; if no current session is available, the most recently used is chosen.

target-window (or src-window or dst-window) specifies a window in the form _session_:_window_. _session_ follows the same rules as for target-session, and _window_ is looked for in order as:

1.  A special token, listed below.
    
2.  A window index, for example ‘`mysession:1`’ is window 1 in session ‘`mysession`’.
    
3.  A window ID, such as @1.
    
4.  An exact window name, such as ‘`mysession:mywindow`’.
    
5.  The start of a window name, such as ‘`mysession:mywin`’.
    
6.  As an [fnmatch(3)](https://www.mankier.com/3/fnmatch) pattern matched against the window name.
    

Like sessions, a ‘`=`’ prefix will do an exact match only. An empty window name specifies the next unused index if appropriate (for example the `new-window` and `link-window` commands) otherwise the current window in _session_ is chosen.

The following special tokens are available to indicate particular windows. Each has a single-character alternative form.

<table><tbody><tr><td><b>Token</b></td><td><b></b></td><td><b>Meaning</b></td></tr><tr><td><code>{start}</code></td><td>^</td><td>The lowest-numbered window</td></tr><tr><td><code>{end}</code></td><td>$</td><td>The highest-numbered window</td></tr><tr><td><code>{last}</code></td><td>!</td><td>The last (previously current) window</td></tr><tr><td><code>{next}</code></td><td>+</td><td>The next window by number</td></tr><tr><td><code>{previous}</code></td><td>-</td><td>The previous window by number</td></tr></tbody></table>

target-pane (or src-pane or dst-pane) may be a pane ID or takes a similar form to target-window but with the optional addition of a period followed by a pane index or pane ID, for example: ‘`mysession:mywindow.1`’. If the pane index is omitted, the currently active pane in the specified window is used. The following special tokens are available for the pane index:

<table><tbody><tr><td><b>Token</b></td><td><b></b></td><td><b>Meaning</b></td></tr><tr><td><code>{last}</code></td><td>!</td><td>The last (previously active) pane</td></tr><tr><td><code>{next}</code></td><td>+</td><td>The next pane by number</td></tr><tr><td><code>{previous}</code></td><td>-</td><td>The previous pane by number</td></tr><tr><td><code>{top}</code></td><td></td><td>The top pane</td></tr><tr><td><code>{bottom}</code></td><td></td><td>The bottom pane</td></tr><tr><td><code>{left}</code></td><td></td><td>The leftmost pane</td></tr><tr><td><code>{right}</code></td><td></td><td>The rightmost pane</td></tr><tr><td><code>{top-left}</code></td><td></td><td>The top-left pane</td></tr><tr><td><code>{top-right}</code></td><td></td><td>The top-right pane</td></tr><tr><td><code>{bottom-left}</code></td><td></td><td>The bottom-left pane</td></tr><tr><td><code>{bottom-right}</code></td><td></td><td>The bottom-right pane</td></tr><tr><td><code>{up-of}</code></td><td></td><td>The pane above the active pane</td></tr><tr><td><code>{down-of}</code></td><td></td><td>The pane below the active pane</td></tr><tr><td><code>{left-of}</code></td><td></td><td>The pane to the left of the active pane</td></tr><tr><td><code>{right-of}</code></td><td></td><td>The pane to the right of the active pane</td></tr></tbody></table>

The tokens ‘`+`’ and ‘`-`’ may be followed by an offset, for example:

> ```
> select-window -t:+2
> 
> ```

In addition, _target-session_, _target-window_ or _target-pane_ may consist entirely of the token ‘`{mouse}`’ (alternative form ‘`=`’) to specify the session, window or pane where the most recent mouse event occurred (see the [Mouse Support](https://www.mankier.com/1/tmux#Mouse_Support) section) or ‘`{marked}`’ (alternative form ‘`~`’) to specify the marked pane (see `select-pane` `-m`).

Sessions, window and panes are each numbered with a unique ID; session IDs are prefixed with a ‘`$`’, windows with a ‘`@`’, and panes with a ‘`%`’. These are unique and are unchanged for the life of the session, window or pane in the **tmux** server. The pane ID is passed to the child process of the pane in the `TMUX_PANE` environment variable. IDs may be displayed using the ‘`session_id`’, ‘`window_id`’, or ‘`pane_id`’ formats (see the [Formats](https://www.mankier.com/1/tmux#Formats) section) and the `display-message`, `list-sessions`, `list-windows` or `list-panes` commands.

shell-command arguments are [sh(1)](https://www.mankier.com/1/bash) commands. This may be a single argument passed to the shell, for example:

> ```
> new-window 'vi ~/.tmux.conf'
> 
> ```

Will run:

> ```
> /bin/sh -c 'vi ~/.tmux.conf'
> 
> ```

Additionally, the `new-window`, `new-session`, `split-window`, `respawn-window` and `respawn-pane` commands allow shell-command to be given as multiple arguments and executed directly (without ‘`sh [-c](https://www.mankier.com/1/tmux#-c)`’). This can avoid issues with shell quoting. For example:

> ```
> $ tmux new-window vi ~/.tmux.conf
> 
> ```

Will run [vi(1)](https://www.mankier.com/1/vim) directly without invoking the shell.

command \[arguments\] refers to a **tmux** command, either passed with the command and arguments separately, for example:

> ```
> bind-key F1 set-option status off
> 
> ```

Or passed as a single string argument in `.tmux.conf`, for example:

> ```
> bind-key F1 { set-option status off }
> 
> ```

Example **tmux** commands include:

> ```
> refresh-client -t/dev/ttyp2
> 
> rename-session -tfirst newname
> 
> set-option -wt:0 monitor-activity on
> 
> new-window ; split-window -d
> 
> bind-key R source-file ~/.tmux.conf \; \
> display-message "source-file done"
> 
> ```

Or from [sh(1)](https://www.mankier.com/1/bash):

> ```
> $ tmux kill-window -t :1
> 
> $ tmux new-window \; split-window -d
> 
> $ tmux new-session -d 'vi ~/.tmux.conf' \; split-window -d \; attach
> 
> ```

[

## Clients and Sessions

](https://www.mankier.com/1/tmux#Clients_and_Sessions)

The **tmux** server manages clients, sessions, windows and panes. Clients are attached to sessions to interact with them, either when they are created with the `new-session` command, or later with the `attach-session` command. Each session has one or more windows _linked_ into it. Windows may be linked to multiple sessions and are made up of one or more panes, each of which contains a pseudo terminal. Commands for creating, linking and otherwise manipulating windows are covered in the [Windows and Panes](https://www.mankier.com/1/tmux#Windows_and_Panes) section.

The following commands are available to manage clients and sessions:

attach-session \[-dErx\] \[[\-c](https://www.mankier.com/1/tmux#-c) working-directory\] \[[\-f](https://www.mankier.com/1/tmux#-f) flags\] \[-t target-session\]

> (alias: `attach`)

If run from outside **tmux**, create a new client in the current terminal and attach it to target-session. If used from inside, switch the current client. If `-d` is specified, any other clients attached to the session are detached. If `-x` is given, send `SIGHUP` to the parent process of the client as well as detaching the client, typically causing it to exit. [\-f](https://www.mankier.com/1/tmux#-f) sets a comma-separated list of client flags. The flags are:

active-pane

the client has an independent active pane

ignore-size

the client does not affect the size of other clients

no-output

the client does not receive pane output in control mode

pause-after=seconds

output is paused once the pane is seconds behind in control mode

read-only

the client is read-only

wait-exit

wait for an empty line input before exiting in control mode

A leading ‘`!`’ turns a flag off if the client is already attached. `-r` is an alias for [\-f](https://www.mankier.com/1/tmux#-f) read-only,ignore-size. When a client is read-only, only keys bound to the `detach-client` or `switch-client` commands have any effect. A client with the active-pane flag allows the active pane to be selected independently of the window's active pane used by clients without the flag. This only affects the cursor position and commands issued from the client; other features such as hooks and styles continue to use the window's active pane.

If no server is started, `attach-session` will attempt to start it; this will fail unless sessions are created in the configuration file.

The target-session rules for `attach-session` are slightly adjusted: if **tmux** needs to select the most recently used session, it will prefer the most recently used _unattached_ session.

[\-c](https://www.mankier.com/1/tmux#-c) will set the session working directory (used for new windows) to working-directory.

If `-E` is used, the `update-environment` option will not be applied.

detach-client \[-aP\] \[-E shell-command\] \[-s target-session\] \[-t target-client\]

> (alias: `detach`)

Detach the current client if bound to a key, the client specified with `-t`, or all clients currently attached to the session specified by `-s`. The `-a` option kills all but the client given with `-t`. If `-P` is given, send `SIGHUP` to the parent process of the client, typically causing it to exit. With `-E`, run shell-command to replace the client.

has-session \[-t target-session\]

> (alias: `has`)

Report an error and exit with 1 if the specified session does not exist. If it does exist, exit with 0.

kill-server

Kill the **tmux** server and clients and destroy all sessions.

kill-session \[-aC\] \[-t target-session\]

Destroy the given session, closing any windows linked to it and no other sessions, and detaching all clients attached to it. If `-a` is given, all sessions but the specified one is killed. The [\-C](https://www.mankier.com/1/tmux#-C) flag clears alerts (bell, activity, or silence) in all windows linked to the session.

list-clients \[-F format\] \[-t target-session\]

> (alias: `lsc`)

List all clients attached to the server. For the meaning of the `-F` flag, see the [Formats](https://www.mankier.com/1/tmux#Formats) section. If target-session is specified, list only clients connected to that session.

list-commands \[-F format\] \[command\]

> (alias: `lscm`)

List the syntax of command or - if omitted - of all commands supported by **tmux**.

list-sessions \[-F format\] \[[\-f](https://www.mankier.com/1/tmux#-f) filter\]

> (alias: `ls`)

List all sessions managed by the server. `-F` specifies the format of each line and [\-f](https://www.mankier.com/1/tmux#-f) a filter. Only sessions for which the filter is true are shown. See the [Formats](https://www.mankier.com/1/tmux#Formats) section.

lock-client \[-t target-client\]

> (alias: `lockc`)

Lock target-client, see the `lock-server` command.

lock-session \[-t target-session\]

> (alias: `locks`)

Lock all clients attached to target-session.

new-session \[-AdDEPX\] \[[\-c](https://www.mankier.com/1/tmux#-c) start-directory\] \[-e environment\] \[[\-f](https://www.mankier.com/1/tmux#-f) flags\] \[-F format\] \[-n window-name\] \[-s session-name\] \[-t group-name\] \[-x width\] \[-y height\] \[shell-command\]

> (alias: `new`)

Create a new session with name session-name.

The new session is attached to the current terminal unless `-d` is given. window-name and shell-command are the name of and shell command to execute in the initial window. With `-d`, the initial size comes from the global `default-size` option; `-x` and `-y` can be used to specify a different size. ‘`-`’ uses the size of the current client if any. If `-x` or `-y` is given, the `default-size` option is set for the session. [\-f](https://www.mankier.com/1/tmux#-f) sets a comma-separated list of client flags (see `attach-session`).

If run from a terminal, any termios(4) special characters are saved and used for new windows in the new session.

The `-A` flag makes `new-session` behave like `attach-session` if session-name already exists; in this case, [\-D](https://www.mankier.com/1/tmux#-D) behaves like `-d` to `attach-session`, and `-X` behaves like `-x` to `attach-session`.

If `-t` is given, it specifies a `session group`. Sessions in the same group share the same set of windows - new windows are linked to all sessions in the group and any windows closed removed from all sessions. The current and previous window and any session options remain independent and any session in a group may be killed without affecting the others. The group-name argument may be:

1.  the name of an existing group, in which case the new session is added to that group;
    
2.  the name of an existing session - the new session is added to the same group as that session, creating a new group if necessary;
    
3.  the name for a new group containing only the new session.
    

`-n` and shell-command are invalid if `-t` is used.

The `-P` option prints information about the new session after it has been created. By default, it uses the format ‘`#{session_name}:`’ but a different format may be specified with `-F`.

If `-E` is used, the `update-environment` option will not be applied. `-e` takes the form ‘`VARIABLE=value`’ and sets an environment variable for the newly created session; it may be specified multiple times.

refresh-client \[-cDLRSU\] \[-A pane:state\] \[-B name:what:format\] \[[\-C](https://www.mankier.com/1/tmux#-C) size\] \[[\-f](https://www.mankier.com/1/tmux#-f) flags\] \[[\-l](https://www.mankier.com/1/tmux#-l) \[target-pane\]\] \[-t target-client\] \[adjustment\]

> (alias: `refresh`)

Refresh the current client if bound to a key, or a single client if one is given with `-t`. If [\-S](https://www.mankier.com/1/tmux#-S) is specified, only update the client's status line.

The `-U`, [\-D](https://www.mankier.com/1/tmux#-D), [\-L](https://www.mankier.com/1/tmux#-L) `-R`, and [\-c](https://www.mankier.com/1/tmux#-c) flags allow the visible portion of a window which is larger than the client to be changed. `-U` moves the visible part up by adjustment rows and [\-D](https://www.mankier.com/1/tmux#-D) down, [\-L](https://www.mankier.com/1/tmux#-L) left by adjustment columns and `-R` right. [\-c](https://www.mankier.com/1/tmux#-c) returns to tracking the cursor automatically. If adjustment is omitted, 1 is used. Note that the visible position is a property of the client not of the window, changing the current window in the attached session will reset it.

[\-C](https://www.mankier.com/1/tmux#-C) sets the width and height of a control mode client or of a window for a control mode client, size must be one of ‘`widthxheight`’ or ‘`window ID:widthxheight`’, for example ‘`80x24`’ or ‘`@0:80x24`’. `-A` allows a control mode client to trigger actions on a pane. The argument is a pane ID (with leading ‘`%`’), a colon, then one of ‘`on`’, ‘`off`’, ‘`continue`’ or ‘`pause`’. If ‘`off`’, **tmux** will not send output from the pane to the client and if all clients have turned the pane off, will stop reading from the pane. If ‘`continue`’, **tmux** will return to sending output to the pane if it was paused (manually or with the pause-after flag). If ‘`pause`’, **tmux** will pause the pane. `-A` may be given multiple times for different panes.

`-B` sets a subscription to a format for a control mode client. The argument is split into three items by colons: name is a name for the subscription; what is a type of item to subscribe to; format is the format. After a subscription is added, changes to the format are reported with the `%subscription-changed` notification, at most once a second. If only the name is given, the subscription is removed. what may be empty to check the format only for the attached session, or one of: a pane ID such as ‘`%0`’; ‘`%*`’ for all panes in the attached session; a window ID such as ‘`@0`’; or ‘`@*`’ for all windows in the attached session.

[\-f](https://www.mankier.com/1/tmux#-f) sets a comma-separated list of client flags, see `attach-session`.

[\-l](https://www.mankier.com/1/tmux#-l) requests the clipboard from the client using the [xterm(1)](https://www.mankier.com/1/xterm) escape sequence. If Ar target-pane is given, the clipboard is sent (in encoded form), otherwise it is stored in a new paste buffer.

[\-L](https://www.mankier.com/1/tmux#-L), `-R`, `-U` and [\-D](https://www.mankier.com/1/tmux#-D) move the visible portion of the window left, right, up or down by adjustment, if the window is larger than the client. [\-c](https://www.mankier.com/1/tmux#-c) resets so that the position follows the cursor. See the `window-size` option.

rename-session \[-t target-session\] new-name

> (alias: `rename`)

Rename the session to new-name.

server-access \[-adlrw\] \[user\]

Change the access or read/write permission of user. The user running the **tmux** server (its owner) and the root user cannot be changed and are always permitted access.

`-a` and `-d` are used to give or revoke access for the specified user. If the user is already attached, the `-d` flag causes their clients to be detached.

`-r` and `-w` change the permissions for user: `-r` makes their clients read-only and `-w` writable. [\-l](https://www.mankier.com/1/tmux#-l) lists current access permissions.

By default, the access list is empty and **tmux** creates sockets with file system permissions preventing access by any user other than the owner (and root). These permissions must be changed manually. Great care should be taken not to allow access to untrusted users even read-only.

show-messages \[-JT\] \[-t target-client\]

> (alias: `showmsgs`)

Show server messages or information. Messages are stored, up to a maximum of the limit set by the message-limit server option. `-J` and [\-T](https://www.mankier.com/1/tmux#-T) show debugging information about jobs and terminals.

source-file \[-Fnqv\] path ...

> (alias: `source`)

Execute commands from one or more files specified by path (which may be [glob(7)](https://www.mankier.com/7/glob) patterns). If `-F` is present, then path is expanded as a format. If `-q` is given, no error will be returned if path does not exist. With `-n`, the file is parsed but no commands are executed. [\-v](https://www.mankier.com/1/tmux#-v) shows the parsed commands and line numbers if possible.

start-server

> (alias: `start`)

Start the **tmux** server, if not already running, without creating any sessions.

Note that as by default the **tmux** server will exit with no sessions, this is only useful if a session is created in `~/.tmux.conf`, `exit-empty` is turned off, or another command is run as part of the same command sequence. For example:

> ```
> $ tmux start \; show -g
>     
> ```

suspend-client \[-t target-client\]

> (alias: `suspendc`)

Suspend a client by sending `SIGTSTP` (tty stop).

switch-client \[-ElnprZ\] \[[\-c](https://www.mankier.com/1/tmux#-c) target-client\] \[-t target-session\] \[[\-T](https://www.mankier.com/1/tmux#-T) key-table\]

> (alias: `switchc`)

Switch the current session for client target-client to target-session. As a special case, `-t` may refer to a pane (a target that contains ‘`:`’, ‘`.`’ or ‘`%`’), to change session, window and pane. In that case, `-Z` keeps the window zoomed if it was zoomed. If [\-l](https://www.mankier.com/1/tmux#-l), `-n` or `-p` is used, the client is moved to the last, next or previous session respectively. `-r` toggles the client `read-only` and `ignore-size` flags (see the `attach-session` command).

If `-E` is used, `update-environment` option will not be applied.

[\-T](https://www.mankier.com/1/tmux#-T) sets the client's key table; the next key from the client will be interpreted from key-table. This may be used to configure multiple prefix keys, or to bind commands to sequences of keys. For example, to make typing ‘`abc`’ run the `list-keys` command:

> ```
> bind-key -Ttable2 c list-keys
> bind-key -Ttable1 b switch-client -Ttable2
> bind-key -Troot   a switch-client -Ttable1
>     
> ```

[

## Windows and Panes

](https://www.mankier.com/1/tmux#Windows_and_Panes)

Each window displayed by **tmux** may be split into one or more _panes_; each pane takes up a certain area of the display and is a separate terminal. A window may be split into panes using the `split-window` command. Windows may be split horizontally (with the `-h` flag) or vertically. Panes may be resized with the `resize-pane` command (bound to ‘`C-Up`’, ‘`C-Down`’ ‘`C-Left`’ and ‘`C-Right`’ by default), the current pane may be changed with the `select-pane` command and the `rotate-window` and `swap-pane` commands may be used to swap panes without changing their position. Panes are numbered beginning from zero in the order they are created.

By default, a **tmux** pane permits direct access to the terminal contained in the pane. A pane may also be put into one of several modes:

+   Copy mode, which permits a section of a window or its history to be copied to a _paste buffer_ for later insertion into another window. This mode is entered with the `copy-mode` command, bound to ‘`[`’ by default. Copied text can be pasted with the `paste-buffer` command, bound to ‘`]`’.
    
+   View mode, which is like copy mode but is entered when a command that produces output, such as `list-keys`, is executed from a key binding.
    
+   Choose mode, which allows an item to be chosen from a list. This may be a client, a session or window or pane, or a buffer. This mode is entered with the `choose-buffer`, `choose-client` and `choose-tree` commands.
    

In copy mode an indicator is displayed in the top-right corner of the pane with the current position and the number of lines in the history.

Commands are sent to copy mode using the `-X` flag to the `send-keys` command. When a key is pressed, copy mode automatically uses one of two key tables, depending on the `mode-keys` option: `copy-mode` for emacs, or `copy-mode-vi` for vi. Key tables may be viewed with the `list-keys` command.

The following commands are supported in copy mode:

<table><tbody><tr><td><b>Command</b></td><td><b>vi</b></td><td><b>emacs</b></td></tr><tr><td><a href="https://www.mankier.com/1/tmux#append-selection" id="append-selection"><code>append-selection</code></a></td><td></td><td></td></tr><tr><td><a href="https://www.mankier.com/1/tmux#append-selection-and-cancel" id="append-selection-and-cancel"><code>append-selection-and-cancel</code></a></td><td>A</td><td></td></tr><tr><td><a href="https://www.mankier.com/1/tmux#back-to-indentation" id="back-to-indentation"><code>back-to-indentation</code></a></td><td>^</td><td>M-m</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#begin-selection" id="begin-selection"><code>begin-selection</code></a></td><td>Space</td><td>C-Space</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#bottom-line" id="bottom-line"><code>bottom-line</code></a></td><td>L</td><td></td></tr><tr><td><a href="https://www.mankier.com/1/tmux#cancel" id="cancel"><code>cancel</code></a></td><td>q</td><td>Escape</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#clear-selection" id="clear-selection"><code>clear-selection</code></a></td><td>Escape</td><td>C-g</td></tr><tr><td><code>copy-end-of-line [&lt;prefix&gt;]</code></td><td></td><td></td></tr><tr><td><code>copy-end-of-line-and-cancel [&lt;prefix&gt;]</code></td><td></td><td></td></tr><tr><td><code>copy-pipe-end-of-line [&lt;command&gt;] [&lt;prefix&gt;]</code></td><td></td><td></td></tr><tr><td><code>copy-pipe-end-of-line-and-cancel [&lt;command&gt;] [&lt;prefix&gt;]</code></td><td>D</td><td>C-k</td></tr><tr><td><code>copy-line [&lt;prefix&gt;]</code></td><td></td><td></td></tr><tr><td><code>copy-line-and-cancel [&lt;prefix&gt;]</code></td><td></td><td></td></tr><tr><td><code>copy-pipe-line [&lt;command&gt;] [&lt;prefix&gt;]</code></td><td></td><td></td></tr><tr><td><code>copy-pipe-line-and-cancel [&lt;command&gt;] [&lt;prefix&gt;]</code></td><td></td><td></td></tr><tr><td><code>copy-pipe [&lt;command&gt;] [&lt;prefix&gt;]</code></td><td></td><td></td></tr><tr><td><code>copy-pipe-no-clear [&lt;command&gt;] [&lt;prefix&gt;]</code></td><td></td><td></td></tr><tr><td><code>copy-pipe-and-cancel [&lt;command&gt;] [&lt;prefix&gt;]</code></td><td></td><td></td></tr><tr><td><code>copy-selection [&lt;prefix&gt;]</code></td><td></td><td></td></tr><tr><td><code>copy-selection-no-clear [&lt;prefix&gt;]</code></td><td></td><td></td></tr><tr><td><code>copy-selection-and-cancel [&lt;prefix&gt;]</code></td><td>Enter</td><td>M-w</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#cursor-down" id="cursor-down"><code>cursor-down</code></a></td><td>j</td><td>Down</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#cursor-down-and-cancel" id="cursor-down-and-cancel"><code>cursor-down-and-cancel</code></a></td><td></td><td></td></tr><tr><td><a href="https://www.mankier.com/1/tmux#cursor-left" id="cursor-left"><code>cursor-left</code></a></td><td>h</td><td>Left</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#cursor-right" id="cursor-right"><code>cursor-right</code></a></td><td>l</td><td>Right</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#cursor-up" id="cursor-up"><code>cursor-up</code></a></td><td>k</td><td>Up</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#end-of-line" id="end-of-line"><code>end-of-line</code></a></td><td>$</td><td>C-e</td></tr><tr><td><code>goto-line &lt;line&gt;</code></td><td>:</td><td>g</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#halfpage-down" id="halfpage-down"><code>halfpage-down</code></a></td><td>C-d</td><td>M-Down</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#halfpage-down-and-cancel" id="halfpage-down-and-cancel"><code>halfpage-down-and-cancel</code></a></td><td></td><td></td></tr><tr><td><a href="https://www.mankier.com/1/tmux#halfpage-up" id="halfpage-up"><code>halfpage-up</code></a></td><td>C-u</td><td>M-Up</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#history-bottom" id="history-bottom"><code>history-bottom</code></a></td><td>G</td><td>M-&gt;</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#history-top" id="history-top"><code>history-top</code></a></td><td>g</td><td>M-&lt;</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#jump-again" id="jump-again"><code>jump-again</code></a></td><td>;</td><td>;</td></tr><tr><td><code>jump-backward &lt;to&gt;</code></td><td>F</td><td>F</td></tr><tr><td><code>jump-forward &lt;to&gt;</code></td><td>f</td><td>f</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#jump-reverse" id="jump-reverse"><code>jump-reverse</code></a></td><td>,</td><td>,</td></tr><tr><td><code>jump-to-backward &lt;to&gt;</code></td><td>T</td><td></td></tr><tr><td><code>jump-to-forward &lt;to&gt;</code></td><td>t</td><td></td></tr><tr><td><a href="https://www.mankier.com/1/tmux#jump-to-mark" id="jump-to-mark"><code>jump-to-mark</code></a></td><td>M-x</td><td>M-x</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#middle-line" id="middle-line"><code>middle-line</code></a></td><td>M</td><td>M-r</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#next-matching-bracket" id="next-matching-bracket"><code>next-matching-bracket</code></a></td><td>%</td><td>M-C-f</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#next-paragraph" id="next-paragraph"><code>next-paragraph</code></a></td><td>}</td><td>M-}</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#next-space" id="next-space"><code>next-space</code></a></td><td>W</td><td></td></tr><tr><td><a href="https://www.mankier.com/1/tmux#next-space-end" id="next-space-end"><code>next-space-end</code></a></td><td>E</td><td></td></tr><tr><td><a href="https://www.mankier.com/1/tmux#next-word" id="next-word"><code>next-word</code></a></td><td>w</td><td></td></tr><tr><td><a href="https://www.mankier.com/1/tmux#next-word-end" id="next-word-end"><code>next-word-end</code></a></td><td>e</td><td>M-f</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#other-end" id="other-end"><code>other-end</code></a></td><td>o</td><td></td></tr><tr><td><a href="https://www.mankier.com/1/tmux#page-down" id="page-down"><code>page-down</code></a></td><td>C-f</td><td>PageDown</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#page-down-and-cancel" id="page-down-and-cancel"><code>page-down-and-cancel</code></a></td><td></td><td></td></tr><tr><td><a href="https://www.mankier.com/1/tmux#page-up" id="page-up"><code>page-up</code></a></td><td>C-b</td><td>PageUp</td></tr><tr><td><code>pipe [&lt;command&gt;] [&lt;prefix&gt;]</code></td><td></td><td></td></tr><tr><td><code>pipe-no-clear [&lt;command&gt;] [&lt;prefix&gt;]</code></td><td></td><td></td></tr><tr><td><code>pipe-and-cancel [&lt;command&gt;] [&lt;prefix&gt;]</code></td><td></td><td></td></tr><tr><td><a href="https://www.mankier.com/1/tmux#previous-matching-bracket" id="previous-matching-bracket"><code>previous-matching-bracket</code></a></td><td></td><td>M-C-b</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#previous-paragraph" id="previous-paragraph"><code>previous-paragraph</code></a></td><td>{</td><td>M-{</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#previous-space" id="previous-space"><code>previous-space</code></a></td><td>B</td><td></td></tr><tr><td><a href="https://www.mankier.com/1/tmux#previous-word" id="previous-word"><code>previous-word</code></a></td><td>b</td><td>M-b</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#rectangle-on" id="rectangle-on"><code>rectangle-on</code></a></td><td></td><td></td></tr><tr><td><a href="https://www.mankier.com/1/tmux#rectangle-off" id="rectangle-off"><code>rectangle-off</code></a></td><td></td><td></td></tr><tr><td><a href="https://www.mankier.com/1/tmux#rectangle-toggle" id="rectangle-toggle"><code>rectangle-toggle</code></a></td><td>v</td><td>R</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#refresh-from-pane" id="refresh-from-pane"><code>refresh-from-pane</code></a></td><td>r</td><td>r</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#scroll-down" id="scroll-down"><code>scroll-down</code></a></td><td>C-e</td><td>C-Down</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#scroll-down-and-cancel" id="scroll-down-and-cancel"><code>scroll-down-and-cancel</code></a></td><td></td><td></td></tr><tr><td><a href="https://www.mankier.com/1/tmux#scroll-up" id="scroll-up"><code>scroll-up</code></a></td><td>C-y</td><td>C-Up</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#search-again" id="search-again"><code>search-again</code></a></td><td>n</td><td>n</td></tr><tr><td><code>search-backward &lt;for&gt;</code></td><td>?</td><td></td></tr><tr><td><code>search-backward-incremental &lt;for&gt;</code></td><td></td><td>C-r</td></tr><tr><td><code>search-backward-text &lt;for&gt;</code></td><td></td><td></td></tr><tr><td><code>search-forward &lt;for&gt;</code></td><td>/</td><td></td></tr><tr><td><code>search-forward-incremental &lt;for&gt;</code></td><td></td><td>C-s</td></tr><tr><td><code>search-forward-text &lt;for&gt;</code></td><td></td><td></td></tr><tr><td><a href="https://www.mankier.com/1/tmux#search-reverse" id="search-reverse"><code>search-reverse</code></a></td><td>N</td><td>N</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#select-line" id="select-line"><code>select-line</code></a></td><td>V</td><td></td></tr><tr><td><a href="https://www.mankier.com/1/tmux#select-word" id="select-word"><code>select-word</code></a></td><td></td><td></td></tr><tr><td><a href="https://www.mankier.com/1/tmux#set-mark" id="set-mark"><code>set-mark</code></a></td><td>X</td><td>X</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#start-of-line" id="start-of-line"><code>start-of-line</code></a></td><td>0</td><td>C-a</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#stop-selection" id="stop-selection"><code>stop-selection</code></a></td><td></td><td></td></tr><tr><td><a href="https://www.mankier.com/1/tmux#toggle-position" id="toggle-position"><code>toggle-position</code></a></td><td>P</td><td>P</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#top-line" id="top-line"><code>top-line</code></a></td><td>H</td><td>M-R</td></tr></tbody></table>

The search commands come in several varieties: ‘`search-forward`’ and ‘`search-backward`’ search for a regular expression; the ‘`-text`’ variants search for a plain text string rather than a regular expression; ‘`-incremental`’ perform an incremental search and expect to be used with the `-i` flag to the `command-prompt` command. ‘`search-again`’ repeats the last search and ‘`search-reverse`’ does the same but reverses the direction (forward becomes backward and backward becomes forward).

Copy commands may take an optional buffer prefix argument which is used to generate the buffer name (the default is ‘`buffer`’ so buffers are named ‘`buffer0`’, ‘`buffer1`’ and so on). Pipe commands take a command argument which is the command to which the selected text is piped. ‘`copy-pipe`’ variants also copy the selection. The ‘`-and-cancel`’ variants of some commands exit copy mode after they have completed (for copy commands) or when the cursor reaches the bottom (for scrolling commands). ‘`-no-clear`’ variants do not clear the selection.

The next and previous word keys skip over whitespace and treat consecutive runs of either word separators or other letters as words. Word separators can be customized with the _word-separators_ session option. Next word moves to the start of the next word, next word end to the end of the next word and previous word to the start of the previous word. The three next and previous space keys work similarly but use a space alone as the word separator. Setting _word-separators_ to the empty string makes next/previous word equivalent to next/previous space.

The jump commands enable quick movement within a line. For instance, typing ‘`f`’ followed by ‘`/`’ will move the cursor to the next ‘`/`’ character on the current line. A ‘`;`’ will then jump to the next occurrence.

Commands in copy mode may be prefaced by an optional repeat count. With vi key bindings, a prefix is entered using the number keys; with emacs, the Alt (meta) key and a number begins prefix entry.

The synopsis for the `copy-mode` command is:

copy-mode \[-eHMqu\] \[-s src-pane\] \[-t target-pane\]

Enter copy mode. The [\-u](https://www.mankier.com/1/tmux#-u) option scrolls one page up. `-M` begins a mouse drag (only valid if bound to a mouse key binding, see [Mouse Support](https://www.mankier.com/1/tmux#Mouse_Support)). `-H` hides the position indicator in the top right. `-q` cancels copy mode and any other modes. `-s` copies from src-pane instead of target-pane.

`-e` specifies that scrolling to the bottom of the history (to the visible screen) should exit copy mode. While in copy mode, pressing a key other than those used for scrolling will disable this behaviour. This is intended to allow fast scrolling through a pane's history, for example with:

> ```
> bind PageUp copy-mode -eu
>     
> ```

A number of preset arrangements of panes are available, these are called layouts. These may be selected with the `select-layout` command or cycled with `next-layout` (bound to ‘`Space`’ by default); once a layout is chosen, panes within it may be moved and resized as normal.

The following layouts are supported:

even-horizontal

Panes are spread out evenly from left to right across the window.

even-vertical

Panes are spread evenly from top to bottom.

main-horizontal

A large (main) pane is shown at the top of the window and the remaining panes are spread from left to right in the leftover space at the bottom. Use the _main-pane-height_ window option to specify the height of the top pane.

main-vertical

Similar to `main-horizontal` but the large pane is placed on the left and the others spread from top to bottom along the right. See the _main-pane-width_ window option.

tiled

Panes are spread out as evenly as possible over the window in both rows and columns.

In addition, `select-layout` may be used to apply a previously used layout - the `list-windows` command displays the layout of each window in a form suitable for use with `select-layout`. For example:

> ```
> $ tmux list-windows
> 0: ksh [159x48]
>     layout: bb62,159x48,0,0{79x48,0,0,79x48,80,0}
> $ tmux select-layout bb62,159x48,0,0{79x48,0,0,79x48,80,0}
> 
> ```

**tmux** automatically adjusts the size of the layout for the current window size. Note that a layout cannot be applied to a window with more panes than that from which the layout was originally defined.

Commands related to windows and panes are as follows:

break-pane \[-abdP\] \[-F format\] \[-n window-name\] \[-s src-pane\] \[-t dst-window\]

> (alias: `breakp`)

Break src-pane off from its containing window to make it the only pane in dst-window. With `-a` or `-b`, the window is moved to the next index after or before (existing windows are moved if necessary). If `-d` is given, the new window does not become the current window. The `-P` option prints information about the new window after it has been created. By default, it uses the format ‘`#{session_name}:#{window_index}.#{pane_index}`’ but a different format may be specified with `-F`.

capture-pane \[-aepPqCJN\] \[-b buffer-name\] \[-E end-line\] \[[\-S](https://www.mankier.com/1/tmux#-S) start-line\] \[-t target-pane\]

> (alias: `capturep`)

Capture the contents of a pane. If `-p` is given, the output goes to stdout, otherwise to the buffer specified with `-b` or a new buffer if omitted. If `-a` is given, the alternate screen is used, and the history is not accessible. If no alternate screen exists, an error will be returned unless `-q` is given. If `-e` is given, the output includes escape sequences for text and background attributes. [\-C](https://www.mankier.com/1/tmux#-C) also escapes non-printable characters as octal \\xxx. [\-N](https://www.mankier.com/1/tmux#-N) preserves trailing spaces at each line's end and `-J` preserves trailing spaces and joins any wrapped lines. `-P` captures only any output that the pane has received that is the beginning of an as-yet incomplete escape sequence.

[\-S](https://www.mankier.com/1/tmux#-S) and `-E` specify the starting and ending line numbers, zero is the first line of the visible pane and negative numbers are lines in the history. ‘`-`’ to [\-S](https://www.mankier.com/1/tmux#-S) is the start of the history and to `-E` the end of the visible pane. The default is to capture only the visible contents of the pane.

choose-client \[-NrZ\] \[-F format\] \[[\-f](https://www.mankier.com/1/tmux#-f) filter\] \[-K key-format\] \[-O sort-order\] \[-t target-pane\] \[template\]

Put a pane into client mode, allowing a client to be selected interactively from a list. Each client is shown on one line. A shortcut key is shown on the left in brackets allowing for immediate choice, or the list may be navigated and an item chosen or otherwise manipulated using the keys below. `-Z` zooms the pane. The following keys may be used in client mode:

<table><tbody><tr><td><b>Key</b></td><td><b>Function</b></td></tr><tr><td><a href="https://www.mankier.com/1/tmux#Enter" id="Enter"><code>Enter</code></a></td><td>Choose selected client</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#Up" id="Up"><code>Up</code></a></td><td>Select previous client</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#Down" id="Down"><code>Down</code></a></td><td>Select next client</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#C-s" id="C-s"><code>C-s</code></a></td><td>Search by name</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#n" id="n"><code>n</code></a></td><td>Repeat last search</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#t" id="t"><code>t</code></a></td><td>Toggle if client is tagged</td></tr><tr><td><code>T</code></td><td>Tag no clients</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#C-t" id="C-t"><code>C-t</code></a></td><td>Tag all clients</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#d" id="d"><code>d</code></a></td><td>Detach selected client</td></tr><tr><td><code>D</code></td><td>Detach tagged clients</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#x" id="x"><code>x</code></a></td><td>Detach and HUP selected client</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#X" id="X"><code>X</code></a></td><td>Detach and HUP tagged clients</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#z" id="z"><code>z</code></a></td><td>Suspend selected client</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#Z" id="Z"><code>Z</code></a></td><td>Suspend tagged clients</td></tr><tr><td><code>f</code></td><td>Enter a format to filter items</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#O" id="O"><code>O</code></a></td><td>Change sort field</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#r" id="r"><code>r</code></a></td><td>Reverse sort order</td></tr><tr><td><code>v</code></td><td>Toggle preview</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#q" id="q"><code>q</code></a></td><td>Exit mode</td></tr></tbody></table>

After a client is chosen, ‘`%%`’ is replaced by the client name in template and the result executed as a command. If template is not given, "detach-client -t '%%'" is used.

`-O` specifies the initial sort field: one of ‘`name`’, ‘`size`’, ‘`creation`’, or ‘`activity`’. `-r` reverses the sort order. [\-f](https://www.mankier.com/1/tmux#-f) specifies an initial filter: the filter is a format - if it evaluates to zero, the item in the list is not shown, otherwise it is shown. If a filter would lead to an empty list, it is ignored. `-F` specifies the format for each item in the list and `-K` a format for each shortcut key; both are evaluated once for each line. [\-N](https://www.mankier.com/1/tmux#-N) starts without the preview. This command works only if at least one client is attached.

choose-tree \[-GNrswZ\] \[-F format\] \[[\-f](https://www.mankier.com/1/tmux#-f) filter\] \[-K key-format\] \[-O sort-order\] \[-t target-pane\] \[template\]

Put a pane into tree mode, where a session, window or pane may be chosen interactively from a tree. Each session, window or pane is shown on one line. A shortcut key is shown on the left in brackets allowing for immediate choice, or the tree may be navigated and an item chosen or otherwise manipulated using the keys below. `-s` starts with sessions collapsed and `-w` with windows collapsed. `-Z` zooms the pane. The following keys may be used in tree mode:

<table><tbody><tr><td><b>Key</b></td><td><b>Function</b></td></tr><tr><td><code>Enter</code></td><td>Choose selected item</td></tr><tr><td><code>Up</code></td><td>Select previous item</td></tr><tr><td><code>Down</code></td><td>Select next item</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#+" id="+"><code>+</code></a></td><td>Expand selected item</td></tr><tr><td><code>-</code></td><td>Collapse selected item</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#M-+" id="M-+"><code>M-+</code></a></td><td>Expand all items</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#M--" id="M--"><code>M--</code></a></td><td>Collapse all items</td></tr><tr><td><code>x</code></td><td>Kill selected item</td></tr><tr><td><code>X</code></td><td>Kill tagged items</td></tr><tr><td><code>&lt;</code></td><td>Scroll list of previews left</td></tr><tr><td><code>&gt;</code></td><td>Scroll list of previews right</td></tr><tr><td><code>C-s</code></td><td>Search by name</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#m" id="m"><code>m</code></a></td><td>Set the marked pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#M" id="M"><code>M</code></a></td><td>Clear the marked pane</td></tr><tr><td><code>n</code></td><td>Repeat last search</td></tr><tr><td><code>t</code></td><td>Toggle if item is tagged</td></tr><tr><td><code>T</code></td><td>Tag no items</td></tr><tr><td><code>C-t</code></td><td>Tag all items</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#:" id=":"><code>:</code></a></td><td>Run a command for each tagged item</td></tr><tr><td><code>f</code></td><td>Enter a format to filter items</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#H" id="H"><code>H</code></a></td><td>Jump to the starting pane</td></tr><tr><td><code>O</code></td><td>Change sort field</td></tr><tr><td><code>r</code></td><td>Reverse sort order</td></tr><tr><td><code>v</code></td><td>Toggle preview</td></tr><tr><td><code>q</code></td><td>Exit mode</td></tr></tbody></table>

After a session, window or pane is chosen, the first instance of ‘`%%`’ and all instances of ‘`%1`’ are replaced by the target in template and the result executed as a command. If template is not given, "switch-client -t '%%'" is used.

`-O` specifies the initial sort field: one of ‘`index`’, ‘`name`’, or ‘`time`’. `-r` reverses the sort order. [\-f](https://www.mankier.com/1/tmux#-f) specifies an initial filter: the filter is a format - if it evaluates to zero, the item in the list is not shown, otherwise it is shown. If a filter would lead to an empty list, it is ignored. `-F` specifies the format for each item in the tree and `-K` a format for each shortcut key; both are evaluated once for each line. [\-N](https://www.mankier.com/1/tmux#-N) starts without the preview. `-G` includes all sessions in any session groups in the tree rather than only the first. This command works only if at least one client is attached.

customize-mode \[-NZ\] \[-F format\] \[[\-f](https://www.mankier.com/1/tmux#-f) filter\] \[-t target-pane\] \[template\]

Put a pane into customize mode, where options and key bindings may be browsed and modified from a list. Option values in the list are shown for the active pane in the current window. `-Z` zooms the pane. The following keys may be used in customize mode:

<table><tbody><tr><td><b>Key</b></td><td><b>Function</b></td></tr><tr><td><code>Enter</code></td><td>Set pane, window, session or global option value</td></tr><tr><td><code>Up</code></td><td>Select previous item</td></tr><tr><td><code>Down</code></td><td>Select next item</td></tr><tr><td><code>+</code></td><td>Expand selected item</td></tr><tr><td><code>-</code></td><td>Collapse selected item</td></tr><tr><td><code>M-+</code></td><td>Expand all items</td></tr><tr><td><code>M--</code></td><td>Collapse all items</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#s" id="s"><code>s</code></a></td><td>Set option value or key attribute</td></tr><tr><td><code>S</code></td><td>Set global option value</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#w" id="w"><code>w</code></a></td><td>Set window option value, if option is for pane and window</td></tr><tr><td><code>d</code></td><td>Set an option or key to the default</td></tr><tr><td><code>D</code></td><td>Set tagged options and tagged keys to the default</td></tr><tr><td><code>u</code></td><td>Unset an option (set to default value if global) or unbind a key</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#U" id="U"><code>U</code></a></td><td>Unset tagged options and unbind tagged keys</td></tr><tr><td><code>C-s</code></td><td>Search by name</td></tr><tr><td><code>n</code></td><td>Repeat last search</td></tr><tr><td><code>t</code></td><td>Toggle if item is tagged</td></tr><tr><td><code>T</code></td><td>Tag no items</td></tr><tr><td><code>C-t</code></td><td>Tag all items</td></tr><tr><td><code>f</code></td><td>Enter a format to filter items</td></tr><tr><td><code>v</code></td><td>Toggle option information</td></tr><tr><td><code>q</code></td><td>Exit mode</td></tr></tbody></table>

[\-f](https://www.mankier.com/1/tmux#-f) specifies an initial filter: the filter is a format - if it evaluates to zero, the item in the list is not shown, otherwise it is shown. If a filter would lead to an empty list, it is ignored. `-F` specifies the format for each item in the tree. [\-N](https://www.mankier.com/1/tmux#-N) starts without the option information. This command works only if at least one client is attached.

display-panes \[-bN\] \[-d duration\] \[-t target-client\] \[template\]

> (alias: `displayp`)

Display a visible indicator of each pane shown by target-client. See the `display-panes-colour` and `display-panes-active-colour` session options. The indicator is closed when a key is pressed (unless [\-N](https://www.mankier.com/1/tmux#-N) is given) or duration milliseconds have passed. If `-d` is not given, `display-panes-time` is used. A duration of zero means the indicator stays until a key is pressed. While the indicator is on screen, a pane may be chosen with the ‘`0`’ to ‘`9`’ keys, which will cause template to be executed as a command with ‘`%%`’ substituted by the pane ID. The default template is "select-pane -t '%%'". With `-b`, other commands are not blocked from running until the indicator is closed.

find-window \[-iCNrTZ\] \[-t target-pane\] match-string

> (alias: `findw`)

Search for a [fnmatch(3)](https://www.mankier.com/3/fnmatch) pattern or, with `-r`, regular expression match-string in window names, titles, and visible content (but not history). The flags control matching behavior: [\-C](https://www.mankier.com/1/tmux#-C) matches only visible window contents, [\-N](https://www.mankier.com/1/tmux#-N) matches only the window name and [\-T](https://www.mankier.com/1/tmux#-T) matches only the window title. `-i` makes the search ignore case. The default is `-CNT`. `-Z` zooms the pane.

This command works only if at least one client is attached.

join-pane \[-bdfhv\] \[[\-l](https://www.mankier.com/1/tmux#-l) size\] \[-s src-pane\] \[-t dst-pane\]

> (alias: `joinp`)

Like `split-window`, but instead of splitting dst-pane and creating a new pane, split it and move src-pane into the space. This can be used to reverse `break-pane`. The `-b` option causes src-pane to be joined to left of or above dst-pane.

If `-s` is omitted and a marked pane is present (see `select-pane` `-m`), the marked pane is used rather than the current pane.

kill-pane \[-a\] \[-t target-pane\]

> (alias: `killp`)

Destroy the given pane. If no panes remain in the containing window, it is also destroyed. The `-a` option kills all but the pane given with `-t`.

kill-window \[-a\] \[-t target-window\]

> (alias: `killw`)

Kill the current window or the window at target-window, removing it from any sessions to which it is linked. The `-a` option kills all but the window given with `-t`.

last-pane \[-deZ\] \[-t target-window\]

> (alias: `lastp`)

Select the last (previously selected) pane. `-Z` keeps the window zoomed if it was zoomed. `-e` enables or `-d` disables input to the pane.

last-window \[-t target-session\]

> (alias: `last`)

Select the last (previously selected) window. If no target-session is specified, select the last window of the current session.

link-window \[-abdk\] \[-s src-window\] \[-t dst-window\]

> (alias: `linkw`)

Link the window at src-window to the specified dst-window. If dst-window is specified and no such window exists, the src-window is linked there. With `-a` or `-b` the window is moved to the next index after or before dst-window (existing windows are moved if necessary). If `-k` is given and dst-window exists, it is killed, otherwise an error is generated. If `-d` is given, the newly linked window is not selected.

list-panes \[-as\] \[-F format\] \[[\-f](https://www.mankier.com/1/tmux#-f) filter\] \[-t target\]

> (alias: `lsp`)

If `-a` is given, target is ignored and all panes on the server are listed. If `-s` is given, target is a session (or the current session). If neither is given, target is a window (or the current window). `-F` specifies the format of each line and [\-f](https://www.mankier.com/1/tmux#-f) a filter. Only panes for which the filter is true are shown. See the [Formats](https://www.mankier.com/1/tmux#Formats) section.

list-windows \[-a\] \[-F format\] \[[\-f](https://www.mankier.com/1/tmux#-f) filter\] \[-t target-session\]

> (alias: `lsw`)

If `-a` is given, list all windows on the server. Otherwise, list windows in the current session or in target-session. `-F` specifies the format of each line and [\-f](https://www.mankier.com/1/tmux#-f) a filter. Only windows for which the filter is true are shown. See the [Formats](https://www.mankier.com/1/tmux#Formats) section.

move-pane \[-bdfhv\] \[[\-l](https://www.mankier.com/1/tmux#-l) size\] \[-s src-pane\] \[-t dst-pane\]

> (alias: `movep`)

Does the same as `join-pane`.

move-window \[-abrdk\] \[-s src-window\] \[-t dst-window\]

> (alias: `movew`)

This is similar to `link-window`, except the window at src-window is moved to dst-window. With `-r`, all windows in the session are renumbered in sequential order, respecting the `base-index` option.

new-window \[-abdkPS\] \[[\-c](https://www.mankier.com/1/tmux#-c) start-directory\] \[-e environment\] \[-F format\] \[-n window-name\] \[-t target-window\] \[shell-command\]

> (alias: `neww`)

Create a new window. With `-a` or `-b`, the new window is inserted at the next index after or before the specified target-window, moving windows up if necessary; otherwise target-window is the new window location.

If `-d` is given, the session does not make the new window the current window. target-window represents the window to be created; if the target already exists an error is shown, unless the `-k` flag is used, in which case it is destroyed. If [\-S](https://www.mankier.com/1/tmux#-S) is given and a window named window-name already exists, it is selected (unless `-d` is also given in which case the command does nothing).

shell-command is the command to execute. If shell-command is not specified, the value of the `default-command` option is used. [\-c](https://www.mankier.com/1/tmux#-c) specifies the working directory in which the new window is created.

When the shell command completes, the window closes. See the `remain-on-exit` option to change this behaviour.

`-e` takes the form ‘`VARIABLE=value`’ and sets an environment variable for the newly created window; it may be specified multiple times.

The `TERM` environment variable must be set to ‘`screen`’ or ‘`tmux`’ for all programs running _inside_ **tmux**. New windows will automatically have ‘`TERM=screen`’ added to their environment, but care must be taken not to reset this in shell start-up files or by the `-e` option.

The `-P` option prints information about the new window after it has been created. By default, it uses the format ‘`#{session_name}:#{window_index}`’ but a different format may be specified with `-F`.

next-layout \[-t target-window\]

> (alias: `nextl`)

Move a window to the next layout and rearrange the panes to fit.

next-window \[-a\] \[-t target-session\]

> (alias: `next`)

Move to the next window in the session. If `-a` is used, move to the next window with an alert.

pipe-pane \[-IOo\] \[-t target-pane\] \[shell-command\]

> (alias: `pipep`)

Pipe output sent by the program in target-pane to a shell command or vice versa. A pane may only be connected to one command at a time, any existing pipe is closed before shell-command is executed. The shell-command string may contain the special character sequences supported by the `status-left` option. If no shell-command is given, the current pipe (if any) is closed.

`-I` and `-O` specify which of the shell-command output streams are connected to the pane: with `-I` stdout is connected (so anything shell-command prints is written to the pane as if it were typed); with `-O` stdin is connected (so any output in the pane is piped to shell-command). Both may be used together and if neither are specified, `-O` is used.

The `-o` option only opens a new pipe if no previous pipe exists, allowing a pipe to be toggled with a single key, for example:

> ```
> bind-key C-p pipe-pane -o 'cat >>~/output.#I-#P'
>     
> ```

previous-layout \[-t target-window\]

> (alias: `prevl`)

Move to the previous layout in the session.

previous-window \[-a\] \[-t target-session\]

> (alias: `prev`)

Move to the previous window in the session. With `-a`, move to the previous window with an alert.

rename-window \[-t target-window\] new-name

> (alias: `renamew`)

Rename the current window, or the window at target-window if specified, to new-name.

resize-pane \[-DLMRTUZ\] \[-t target-pane\] \[-x width\] \[-y height\] \[adjustment\]

> (alias: `resizep`)

Resize a pane, up, down, left or right by adjustment with `-U`, [\-D](https://www.mankier.com/1/tmux#-D), [\-L](https://www.mankier.com/1/tmux#-L) or `-R`, or to an absolute size with `-x` or `-y`. The adjustment is given in lines or columns (the default is 1); `-x` and `-y` may be a given as a number of lines or columns or followed by ‘`%`’ for a percentage of the window size (for example ‘`-x 10%`’). With `-Z`, the active pane is toggled between zoomed (occupying the whole of the window) and unzoomed (its normal position in the layout).

`-M` begins mouse resizing (only valid if bound to a mouse key binding, see [Mouse Support](https://www.mankier.com/1/tmux#Mouse_Support)).

[\-T](https://www.mankier.com/1/tmux#-T) trims all lines below the current cursor position and moves lines out of the history to replace them.

resize-window \[-aADLRU\] \[-t target-window\] \[-x width\] \[-y height\] \[adjustment\]

> (alias: `resizew`)

Resize a window, up, down, left or right by adjustment with `-U`, [\-D](https://www.mankier.com/1/tmux#-D), [\-L](https://www.mankier.com/1/tmux#-L) or `-R`, or to an absolute size with `-x` or `-y`. The adjustment is given in lines or cells (the default is 1). `-A` sets the size of the largest session containing the window; `-a` the size of the smallest. This command will automatically set `window-size` to manual in the window options.

respawn-pane \[-k\] \[[\-c](https://www.mankier.com/1/tmux#-c) start-directory\] \[-e environment\] \[-t target-pane\] \[shell-command\]

> (alias: `respawnp`)

Reactivate a pane in which the command has exited (see the `remain-on-exit` window option). If shell-command is not given, the command used when the pane was created or last respawned is executed. The pane must be already inactive, unless `-k` is given, in which case any existing command is killed. [\-c](https://www.mankier.com/1/tmux#-c) specifies a new working directory for the pane. The `-e` option has the same meaning as for the `new-window` command.

respawn-window \[-k\] \[[\-c](https://www.mankier.com/1/tmux#-c) start-directory\] \[-e environment\] \[-t target-window\] \[shell-command\]

> (alias: `respawnw`)

Reactivate a window in which the command has exited (see the `remain-on-exit` window option). If shell-command is not given, the command used when the window was created or last respawned is executed. The window must be already inactive, unless `-k` is given, in which case any existing command is killed. [\-c](https://www.mankier.com/1/tmux#-c) specifies a new working directory for the window. The `-e` option has the same meaning as for the `new-window` command.

rotate-window \[-DUZ\] \[-t target-window\]

> (alias: `rotatew`)

Rotate the positions of the panes within a window, either upward (numerically lower) with `-U` or downward (numerically higher). `-Z` keeps the window zoomed if it was zoomed.

select-layout \[-Enop\] \[-t target-pane\] \[layout-name\]

> (alias: `selectl`)

Choose a specific layout for a window. If layout-name is not given, the last preset layout used (if any) is reapplied. `-n` and `-p` are equivalent to the `next-layout` and `previous-layout` commands. `-o` applies the last set layout if possible (undoes the most recent layout change). `-E` spreads the current pane and any panes next to it out evenly.

select-pane \[-DdeLlMmRUZ\] \[[\-T](https://www.mankier.com/1/tmux#-T) title\] \[-t target-pane\]

> (alias: `selectp`)

Make pane target-pane the active pane in its window. If one of [\-D](https://www.mankier.com/1/tmux#-D), [\-L](https://www.mankier.com/1/tmux#-L), `-R`, or `-U` is used, respectively the pane below, to the left, to the right, or above the target pane is used. `-Z` keeps the window zoomed if it was zoomed. [\-l](https://www.mankier.com/1/tmux#-l) is the same as using the `last-pane` command. `-e` enables or `-d` disables input to the pane. [\-T](https://www.mankier.com/1/tmux#-T) sets the pane title.

`-m` and `-M` are used to set and clear the _marked pane_. There is one marked pane at a time, setting a new marked pane clears the last. The marked pane is the default target for `-s` to `join-pane`, `move-pane`, `swap-pane` and `swap-window`.

select-window \[-lnpT\] \[-t target-window\]

> (alias: `selectw`)

Select the window at target-window. [\-l](https://www.mankier.com/1/tmux#-l), `-n` and `-p` are equivalent to the `last-window`, `next-window` and `previous-window` commands. If [\-T](https://www.mankier.com/1/tmux#-T) is given and the selected window is already the current window, the command behaves like `last-window`.

split-window \[-bdfhIvPZ\] \[[\-c](https://www.mankier.com/1/tmux#-c) start-directory\] \[-e environment\] \[[\-l](https://www.mankier.com/1/tmux#-l) size\] \[-t target-pane\] \[shell-command\] \[-F format\]

> (alias: `splitw`)

Create a new pane by splitting target-pane: `-h` does a horizontal split and [\-v](https://www.mankier.com/1/tmux#-v) a vertical split; if neither is specified, [\-v](https://www.mankier.com/1/tmux#-v) is assumed. The [\-l](https://www.mankier.com/1/tmux#-l) option specifies the size of the new pane in lines (for vertical split) or in columns (for horizontal split); size may be followed by ‘`%`’ to specify a percentage of the available space. The `-b` option causes the new pane to be created to the left of or above target-pane. The [\-f](https://www.mankier.com/1/tmux#-f) option creates a new pane spanning the full window height (with `-h`) or full window width (with [\-v](https://www.mankier.com/1/tmux#-v)), instead of splitting the active pane. `-Z` zooms if the window is not zoomed, or keeps it zoomed if already zoomed.

An empty shell-command ('') will create a pane with no command running in it. Output can be sent to such a pane with the `display-message` command. The `-I` flag (if shell-command is not specified or empty) will create an empty pane and forward any output from stdin to it. For example:

> ```
> $ make 2>&1|tmux splitw -dI &
>     
> ```

All other options have the same meaning as for the `new-window` command.

swap-pane \[-dDUZ\] \[-s src-pane\] \[-t dst-pane\]

> (alias: `swapp`)

Swap two panes. If `-U` is used and no source pane is specified with `-s`, dst-pane is swapped with the previous pane (before it numerically); [\-D](https://www.mankier.com/1/tmux#-D) swaps with the next pane (after it numerically). `-d` instructs **tmux** not to change the active pane and `-Z` keeps the window zoomed if it was zoomed.

If `-s` is omitted and a marked pane is present (see `select-pane` `-m`), the marked pane is used rather than the current pane.

swap-window \[-d\] \[-s src-window\] \[-t dst-window\]

> (alias: `swapw`)

This is similar to `link-window`, except the source and destination windows are swapped. It is an error if no window exists at src-window. If `-d` is given, the new window does not become the current window.

If `-s` is omitted and a marked pane is present (see `select-pane` `-m`), the window containing the marked pane is used rather than the current window.

unlink-window \[-k\] \[-t target-window\]

> (alias: `unlinkw`)

Unlink target-window. Unless `-k` is given, a window may be unlinked only if it is linked to multiple sessions - windows may not be linked to no sessions; if `-k` is specified and the window is linked to only one session, it is unlinked and destroyed.

[

## Key Bindings

](https://www.mankier.com/1/tmux#Key_Bindings)

**tmux** allows a command to be bound to most keys, with or without a prefix key. When specifying keys, most represent themselves (for example ‘`A`’ to ‘`Z`’). Ctrl keys may be prefixed with ‘`C-`’ or ‘`^`’, Shift keys with ‘`S-`’ and Alt (meta) with ‘`M-`’. In addition, the following special key names are accepted: _Up_, _Down_, _Left_, _Right_, _BSpace_, _BTab_, _DC_ (Delete), _End_, _Enter_, _Escape_, _F1_ to _F12_, _Home_, _IC_ (Insert), _NPage/PageDown/PgDn_, _PPage/PageUp/PgUp_, _Space_, and _Tab_. Note that to bind the ‘`"`’ or ‘`'`’ keys, quotation marks are necessary, for example:

> ```
> bind-key '"' split-window
> bind-key "'" new-window
> 
> ```

A command bound to the _Any_ key will execute for all keys which do not have a more specific binding.

Commands related to key bindings are as follows:

bind-key \[-nr\] \[[\-N](https://www.mankier.com/1/tmux#-N) note\] \[[\-T](https://www.mankier.com/1/tmux#-T) key-table\] key command \[arguments\]

> (alias: `bind`)

Bind key key to command. Keys are bound in a key table. By default (without [\-T](https://www.mankier.com/1/tmux#-T)), the key is bound in the _prefix_ key table. This table is used for keys pressed after the prefix key (for example, by default ‘`c`’ is bound to `new-window` in the _prefix_ table, so ‘`C-b c`’ creates a new window). The _root_ table is used for keys pressed without the prefix key: binding ‘`c`’ to `new-window` in the _root_ table (not recommended) means a plain ‘`c`’ will create a new window. `-n` is an alias for [\-T](https://www.mankier.com/1/tmux#-T) root. Keys may also be bound in custom key tables and the `switch-client` [\-T](https://www.mankier.com/1/tmux#-T) command used to switch to them from a key binding. The `-r` flag indicates this key may repeat, see the `repeat-time` option. [\-N](https://www.mankier.com/1/tmux#-N) attaches a note to the key (shown with `list-keys` [\-N](https://www.mankier.com/1/tmux#-N)).

To view the default bindings and possible commands, see the `list-keys` command.

list-keys \[-1aN\] \[-P prefix-string [\-T](https://www.mankier.com/1/tmux#-T) key-table\] \[key\]

> (alias: `lsk`)

List key bindings. There are two forms: the default lists keys as `bind-key` commands; [\-N](https://www.mankier.com/1/tmux#-N) lists only keys with attached notes and shows only the key and note for each key.

With the default form, all key tables are listed by default. [\-T](https://www.mankier.com/1/tmux#-T) lists only keys in key-table.

With the [\-N](https://www.mankier.com/1/tmux#-N) form, only keys in the _root_ and _prefix_ key tables are listed by default; [\-T](https://www.mankier.com/1/tmux#-T) also lists only keys in key-table. `-P` specifies a prefix to print before each key and `-1` lists only the first matching key. `-a` lists the command for keys that do not have a note rather than skipping them.

send-keys \[-FHlMRX\] \[[\-N](https://www.mankier.com/1/tmux#-N) repeat-count\] \[-t target-pane\] key ...

> (alias: `send`)

Send a key or keys to a window. Each argument key is the name of the key (such as ‘`C-a`’ or ‘`NPage`’) to send; if the string is not recognised as a key, it is sent as a series of characters. All arguments are sent sequentially from first to last. If no keys are given and the command is bound to a key, then that key is used.

The [\-l](https://www.mankier.com/1/tmux#-l) flag disables key name lookup and processes the keys as literal UTF-8 characters. The `-H` flag expects each key to be a hexadecimal number for an ASCII character.

The `-R` flag causes the terminal state to be reset.

`-M` passes through a mouse event (only valid if bound to a mouse key binding, see [Mouse Support](https://www.mankier.com/1/tmux#Mouse_Support)).

`-X` is used to send a command into copy mode - see the [Windows and Panes](https://www.mankier.com/1/tmux#Windows_and_Panes) section. [\-N](https://www.mankier.com/1/tmux#-N) specifies a repeat count and `-F` expands formats in arguments where appropriate.

send-prefix \[[\-2](https://www.mankier.com/1/tmux#-2)\] \[-t target-pane\]

Send the prefix key, or with [\-2](https://www.mankier.com/1/tmux#-2) the secondary prefix key, to a window as if it was pressed.

unbind-key \[-anq\] \[[\-T](https://www.mankier.com/1/tmux#-T) key-table\] key

> (alias: `unbind`)

Unbind the command bound to key. `-n` and [\-T](https://www.mankier.com/1/tmux#-T) are the same as for `bind-key`. If `-a` is present, all key bindings are removed. The `-q` option prevents errors being returned.

[

## Options

](https://www.mankier.com/1/tmux#Options)

The appearance and behaviour of **tmux** may be modified by changing the value of various options. There are four types of option: _server options_, _session options_, _window options_, and _pane options_.

The **tmux** server has a set of global server options which do not apply to any particular window or session or pane. These are altered with the `set-option` `-s` command, or displayed with the `show-options` `-s` command.

In addition, each individual session may have a set of session options, and there is a separate set of global session options. Sessions which do not have a particular option configured inherit the value from the global session options. Session options are set or unset with the `set-option` command and may be listed with the `show-options` command. The available server and session options are listed under the `set-option` command.

Similarly, a set of window options is attached to each window and a set of pane options to each pane. Pane options inherit from window options. This means any pane option may be set as a window option to apply the option to all panes in the window without the option set, for example these commands will set the background colour to red for all panes except pane 0:

> ```
> set -w window-style bg=red
> set -pt:.0 window-style bg=blue
> 
> ```

There is also a set of global window options from which any unset window or pane options are inherited. Window and pane options are altered with `set-option` `-w` and `-p` commands and displayed with `show-option` `-w` and `-p`.

**tmux** also supports user options which are prefixed with a ‘`@`’. User options may have any name, so long as they are prefixed with ‘`@`’, and be set to any string. For example:

> ```
> $ tmux set -wq @foo "abc123"
> $ tmux show -wv @foo
> abc123
> 
> ```

Commands which set options are as follows:

set-option \[-aFgopqsuUw\] \[-t target-pane\] option value

> (alias: `set`)

Set a pane option with `-p`, a window option with `-w`, a server option with `-s`, otherwise a session option. If the option is not a user option, `-w` or `-s` may be unnecessary - **tmux** will infer the type from the option name, assuming `-w` for pane options. If `-g` is given, the global session or window option is set.

`-F` expands formats in the option value. The [\-u](https://www.mankier.com/1/tmux#-u) flag unsets an option, so a session inherits the option from the global options (or with `-g`, restores a global option to the default). `-U` unsets an option (like [\-u](https://www.mankier.com/1/tmux#-u)) but if the option is a pane option also unsets the option on any panes in the window. value depends on the option and may be a number, a string, or a flag (on, off, or omitted to toggle).

The `-o` flag prevents setting an option that is already set and the `-q` flag suppresses errors about unknown or ambiguous options.

With `-a`, and if the option expects a string or a style, value is appended to the existing setting. For example:

> ```
> set -g status-left "foo"
> set -ag status-left "bar"
>     
> ```

Will result in ‘`foobar`’. And:

> ```
> set -g status-style "bg=red"
> set -ag status-style "fg=blue"
>     
> ```

Will result in a red background _and_ blue foreground. Without `-a`, the result would be the default background and a blue foreground.

show-options \[-AgHpqsvw\] \[-t target-pane\] \[option\]

> (alias: `show`)

Show the pane options (or a single option if option is provided) with `-p`, the window options with `-w`, the server options with `-s`, otherwise the session options. If the option is not a user option, `-w` or `-s` may be unnecessary - **tmux** will infer the type from the option name, assuming `-w` for pane options. Global session or window options are listed if `-g` is used. [\-v](https://www.mankier.com/1/tmux#-v) shows only the option value, not the name. If `-q` is set, no error will be returned if option is unset. `-H` includes hooks (omitted by default). `-A` includes options inherited from a parent set of options, such options are marked with an asterisk.

Available server options are:

backspace key

Set the key sent by **tmux** for backspace.

buffer-limit number

Set the number of buffers; as new buffers are added to the top of the stack, old ones are removed from the bottom if necessary to maintain this maximum length.

command-alias\[\] name=value

This is an array of custom aliases for commands. If an unknown command matches name, it is replaced with value. For example, after:

> `set -s command-alias[100] zoom='resize-pane -Z'`

Using:

> `zoom -t:.1`

Is equivalent to:

> `resize-pane -Z -t:.1`

Note that aliases are expanded when a command is parsed rather than when it is executed, so binding an alias with `bind-key` will bind the expanded form.

default-terminal terminal

Set the default terminal for new windows created in this session - the default value of the `TERM` environment variable. For **tmux** to work correctly, this _must_ be set to ‘`screen`’, ‘`tmux`’ or a derivative of them.

copy-command shell-command

Give the command to pipe to if the `copy-pipe` copy mode command is used without arguments.

escape-time time

Set the time in milliseconds for which **tmux** waits after an escape is input to determine if it is part of a function or meta key sequences. The default is 500 milliseconds.

editor shell-command

Set the command used when **tmux** runs an editor.

exit-empty \[on | off\]

If enabled (the default), the server will exit when there are no active sessions.

exit-unattached \[on | off\]

If enabled, the server will exit when there are no attached clients.

extended-keys \[on | off | always\]

When `on` or `always`, the escape sequence to enable extended keys is sent to the terminal, if **tmux** knows that it is supported. **tmux** always recognises extended keys itself. If this option is `on`, **tmux** will only forward extended keys to applications when they request them; if `always`, **tmux** will always forward the keys.

focus-events \[on | off\]

When enabled, focus events are requested from the terminal if supported and passed through to applications running in **tmux**. Attached clients should be detached and attached again after changing this option.

history-file path

If not empty, a file to which **tmux** will write command prompt history on exit and load it from on start.

message-limit number

Set the number of error or information messages to save in the message log for each client.

prompt-history-limit number

Set the number of history items to save in the history file for each type of command prompt.

set-clipboard \[on | external | off\]

Attempt to set the terminal clipboard content using the [xterm(1)](https://www.mankier.com/1/xterm) escape sequence, if there is an _Ms_ entry in the [terminfo(5)](https://www.mankier.com/5/terminfo) description (see the [Terminfo Extensions](https://www.mankier.com/1/tmux#Terminfo_Extensions) section).

If set to `on`, **tmux** will both accept the escape sequence to create a buffer and attempt to set the terminal clipboard. If set to `external`, **tmux** will attempt to set the terminal clipboard but ignore attempts by applications to set **tmux** buffers. If `off`, **tmux** will neither accept the clipboard escape sequence nor attempt to set the clipboard.

Note that this feature needs to be enabled in [xterm(1)](https://www.mankier.com/1/xterm) by setting the resource:

> ```
> disallowedWindowOps: 20,21,SetXprop
>     
> ```

Or changing this property from the [xterm(1)](https://www.mankier.com/1/xterm) interactive menu when required.

terminal-features\[\] string

Set terminal features for terminal types read from [terminfo(5)](https://www.mankier.com/5/terminfo). **tmux** has a set of named terminal features. Each will apply appropriate changes to the [terminfo(5)](https://www.mankier.com/5/terminfo) entry in use.

**tmux** can detect features for a few common terminals; this option can be used to easily tell tmux about features supported by terminals it cannot detect. The `terminal-overrides` option allows individual [terminfo(5)](https://www.mankier.com/5/terminfo) capabilities to be set instead, `terminal-features` is intended for classes of functionality supported in a standard way but not reported by [terminfo(5)](https://www.mankier.com/5/terminfo). Care must be taken to configure this only with features the terminal actually supports.

This is an array option where each entry is a colon-separated string made up of a terminal type pattern (matched using [fnmatch(3)](https://www.mankier.com/3/fnmatch)) followed by a list of terminal features. The available features are:

256

Supports 256 colours with the SGR escape sequences.

clipboard

Allows setting the system clipboard.

ccolour

Allows setting the cursor colour.

cstyle

Allows setting the cursor style.

extkeys

Supports extended keys.

focus

Supports focus reporting.

margins

Supports DECSLRM margins.

mouse

Supports [xterm(1)](https://www.mankier.com/1/xterm) mouse sequences.

osc7

Supports the OSC 7 working directory extension.

overline

Supports the overline SGR attribute.

rectfill

Supports the DECFRA rectangle fill escape sequence.

RGB

Supports RGB colour with the SGR escape sequences.

strikethrough

Supports the strikethrough SGR escape sequence.

sync

Supports synchronized updates.

title

Supports [xterm(1)](https://www.mankier.com/1/xterm) title setting.

usstyle

Allows underscore style and colour to be set.

terminal-overrides\[\] string

Allow terminal descriptions read using [terminfo(5)](https://www.mankier.com/5/terminfo) to be overridden. Each entry is a colon-separated string made up of a terminal type pattern (matched using [fnmatch(3)](https://www.mankier.com/3/fnmatch)) and a set of _name=value_ entries.

For example, to set the ‘`clear`’ [terminfo(5)](https://www.mankier.com/5/terminfo) entry to ‘`\e[H\e[2J`’ for all terminal types matching ‘`rxvt*`’:

> `rxvt*:clear=\e[H\e[2J`

The terminal entry value is passed through strunvis(3) before interpretation.

user-keys\[\] key

Set list of user-defined key escape sequences. Each item is associated with a key named ‘`User0`’, ‘`User1`’, and so on.

For example:

> ```
> set -s user-keys[0] "\e[5;30012~"
> bind User0 resize-pane -L 3
>     
> ```

Available session options are:

activity-action \[any | none | current | other\]

Set action on window activity when `monitor-activity` is on. `any` means activity in any window linked to a session causes a bell or message (depending on `visual-activity`) in the current window of that session, `none` means all activity is ignored (equivalent to `monitor-activity` being off), `current` means only activity in windows other than the current window are ignored and `other` means activity in the current window is ignored but not those in other windows.

assume-paste-time milliseconds

If keys are entered faster than one in milliseconds, they are assumed to have been pasted rather than typed and **tmux** key bindings are not processed. The default is one millisecond and zero disables.

base-index index

Set the base index from which an unused index should be searched when a new window is created. The default is zero.

bell-action \[any | none | current | other\]

Set action on a bell in a window when `monitor-bell` is on. The values are the same as those for `activity-action`.

default-command shell-command

Set the command used for new windows (if not specified when the window is created) to shell-command, which may be any [sh(1)](https://www.mankier.com/1/bash) command. The default is an empty string, which instructs **tmux** to create a login shell using the value of the `default-shell` option.

default-shell path

Specify the default shell. This is used as the login shell for new windows when the `default-command` option is set to empty, and must be the full path of the executable. When started **tmux** tries to set a default value from the first suitable of the `SHELL` environment variable, the shell returned by [getpwuid(3)](https://www.mankier.com/3/getpwnam), or `/bin/sh`. This option should be configured when **tmux** is used as a login shell.

default-size XxY

Set the default size of new windows when the `window-size` option is set to manual or when a session is created with `new-session` `-d`. The value is the width and height separated by an ‘`x`’ character. The default is 80x24.

destroy-unattached \[on | off\]

If enabled and the session is no longer attached to any clients, it is destroyed.

detach-on-destroy \[off | on | no-detached\]

If on (the default), the client is detached when the session it is attached to is destroyed. If off, the client is switched to the most recently active of the remaining sessions. If `no-detached`, the client is detached only if there are no detached sessions; if detached sessions exist, the client is switched to the most recently active.

display-panes-active-colour colour

Set the colour used by the `display-panes` command to show the indicator for the active pane.

display-panes-colour colour

Set the colour used by the `display-panes` command to show the indicators for inactive panes.

display-panes-time time

Set the time in milliseconds for which the indicators shown by the `display-panes` command appear.

display-time time

Set the amount of time for which status line messages and other on-screen indicators are displayed. If set to 0, messages and indicators are displayed until a key is pressed. time is in milliseconds.

history-limit lines

Set the maximum number of lines held in window history. This setting applies only to new windows - existing window histories are not resized and retain the limit at the point they were created.

key-table key-table

Set the default key table to key-table instead of _root_.

lock-after-time number

Lock the session (like the `lock-session` command) after number seconds of inactivity. The default is not to lock (set to 0).

lock-command shell-command

Command to run when locking each client. The default is to run lock(1) with `-np`.

message-command-style style

Set status line message command style. This is used for the command prompt with [vi(1)](https://www.mankier.com/1/vim) keys when in command mode. For how to specify style, see the [Styles](https://www.mankier.com/1/tmux#Styles) section.

message-style style

Set status line message style. This is used for messages and for the command prompt. For how to specify style, see the [Styles](https://www.mankier.com/1/tmux#Styles) section.

mouse \[on | off\]

If on, **tmux** captures the mouse and allows mouse events to be bound as key bindings. See the [Mouse Support](https://www.mankier.com/1/tmux#Mouse_Support) section for details.

prefix key

Set the key accepted as a prefix key. In addition to the standard keys described under [Key Bindings](https://www.mankier.com/1/tmux#Key_Bindings), `prefix` can be set to the special key ‘`None`’ to set no prefix.

prefix2 key

Set a secondary key accepted as a prefix key. Like `prefix`, `prefix2` can be set to ‘`None`’.

renumber-windows \[on | off\]

If on, when a window is closed in a session, automatically renumber the other windows in numerical order. This respects the `base-index` option if it has been set. If off, do not renumber the windows.

repeat-time time

Allow multiple commands to be entered without pressing the prefix-key again in the specified time milliseconds (the default is 500). Whether a key repeats may be set when it is bound using the `-r` flag to `bind-key`. Repeat is enabled for the default keys bound to the `resize-pane` command.

set-titles \[on | off\]

Attempt to set the client terminal title using the _tsl_ and _fsl_ [terminfo(5)](https://www.mankier.com/5/terminfo) entries if they exist. **tmux** automatically sets these to the \\e\]0;...\\007 sequence if the terminal appears to be [xterm(1)](https://www.mankier.com/1/xterm). This option is off by default.

set-titles-string string

String used to set the client terminal title if `set-titles` is on. Formats are expanded, see the [Formats](https://www.mankier.com/1/tmux#Formats) section.

silence-action \[any | none | current | other\]

Set action on window silence when `monitor-silence` is on. The values are the same as those for `activity-action`.

status \[off | on | 2 | 3 | 4 | 5\]

Show or hide the status line or specify its size. Using `on` gives a status line one row in height; `2`, `3`, `4` or `5` more rows.

status-format\[\] format

Specify the format to be used for each line of the status line. The default builds the top status line from the various individual status options below.

status-interval interval

Update the status line every interval seconds. By default, updates will occur every 15 seconds. A setting of zero disables redrawing at interval.

status-justify \[left | centre | right | absolute-centre\]

Set the position of the window list in the status line: left, centre or right. centre puts the window list in the relative centre of the available free space; absolute-centre uses the centre of the entire horizontal space.

status-keys \[vi | emacs\]

Use vi or emacs-style key bindings in the status line, for example at the command prompt. The default is emacs, unless the `VISUAL` or `EDITOR` environment variables are set and contain the string ‘`vi`’.

status-left string

Display string (by default the session name) to the left of the status line. string will be passed through [strftime(3)](https://www.mankier.com/3/strftime). Also see the [Formats](https://www.mankier.com/1/tmux#Formats) and [Styles](https://www.mankier.com/1/tmux#Styles) sections.

For details on how the names and titles can be set see the [Names and Titles](https://www.mankier.com/1/tmux#Names_and_Titles) section.

Examples are:

> ```
> #(sysctl vm.loadavg)
> #[fg=yellow,bold]#(apm -l)%%#[default] [#S]
>     
> ```

The default is ‘`[#S]` ’.

status-left-length length

Set the maximum length of the left component of the status line. The default is 10.

status-left-style style

Set the style of the left part of the status line. For how to specify style, see the [Styles](https://www.mankier.com/1/tmux#Styles) section.

status-position \[top | bottom\]

Set the position of the status line.

status-right string

Display string to the right of the status line. By default, the current pane title in double quotes, the date and the time are shown. As with `status-left`, string will be passed to [strftime(3)](https://www.mankier.com/3/strftime) and character pairs are replaced.

status-right-length length

Set the maximum length of the right component of the status line. The default is 40.

status-right-style style

Set the style of the right part of the status line. For how to specify style, see the [Styles](https://www.mankier.com/1/tmux#Styles) section.

status-style style

Set status line style. For how to specify style, see the [Styles](https://www.mankier.com/1/tmux#Styles) section.

update-environment\[\] variable

Set list of environment variables to be copied into the session environment when a new session is created or an existing session is attached. Any variables that do not exist in the source environment are set to be removed from the session environment (as if `-r` was given to the `set-environment` command).

visual-activity \[on | off | both\]

If on, display a message instead of sending a bell when activity occurs in a window for which the `monitor-activity` window option is enabled. If set to both, a bell and a message are produced.

visual-bell \[on | off | both\]

If on, a message is shown on a bell in a window for which the `monitor-bell` window option is enabled instead of it being passed through to the terminal (which normally makes a sound). If set to both, a bell and a message are produced. Also see the `bell-action` option.

visual-silence \[on | off | both\]

If `monitor-silence` is enabled, prints a message after the interval has expired on a given window instead of sending a bell. If set to both, a bell and a message are produced.

word-separators string

Sets the session's conception of what characters are considered word separators, for the purposes of the next and previous word commands in copy mode.

Available window options are:

aggressive-resize \[on | off\]

Aggressively resize the chosen window. This means that **tmux** will resize the window to the size of the smallest or largest session (see the `window-size` option) for which it is the current window, rather than the session to which it is attached. The window may resize when the current window is changed on another session; this option is good for full-screen programs which support `SIGWINCH` and poor for interactive programs such as shells.

automatic-rename \[on | off\]

Control automatic window renaming. When this setting is enabled, **tmux** will rename the window automatically using the format specified by `automatic-rename-format`. This flag is automatically disabled for an individual window when a name is specified at creation with `new-window` or `new-session`, or later with `rename-window`, or with a terminal escape sequence. It may be switched off globally with:

> ```
> set-option -wg automatic-rename off
>     
> ```

automatic-rename-format format

The format (see [Formats](https://www.mankier.com/1/tmux#Formats)) used when the `automatic-rename` option is enabled.

clock-mode-colour colour

Set clock colour.

clock-mode-style \[12 | 24\]

Set clock hour format.

fill-character character

Set the character used to fill areas of the terminal unused by a window.

main-pane-height height

main-pane-width width

Set the width or height of the main (left or top) pane in the `main-horizontal` or `main-vertical` layouts. If suffixed by ‘`%`’, this is a percentage of the window size.

copy-mode-match-style style

Set the style of search matches in copy mode. For how to specify style, see the [Styles](https://www.mankier.com/1/tmux#Styles) section.

copy-mode-mark-style style

Set the style of the line containing the mark in copy mode. For how to specify style, see the [Styles](https://www.mankier.com/1/tmux#Styles) section.

copy-mode-current-match-style style

Set the style of the current search match in copy mode. For how to specify style, see the [Styles](https://www.mankier.com/1/tmux#Styles) section.

mode-keys \[vi | emacs\]

Use vi or emacs-style key bindings in copy mode. The default is emacs, unless `VISUAL` or `EDITOR` contains ‘`vi`’.

mode-style style

Set window modes style. For how to specify style, see the [Styles](https://www.mankier.com/1/tmux#Styles) section.

monitor-activity \[on | off\]

Monitor for activity in the window. Windows with activity are highlighted in the status line.

monitor-bell \[on | off\]

Monitor for a bell in the window. Windows with a bell are highlighted in the status line.

monitor-silence \[interval\]

Monitor for silence (no activity) in the window within `interval` seconds. Windows that have been silent for the interval are highlighted in the status line. An interval of zero disables the monitoring.

other-pane-height height

Set the height of the other panes (not the main pane) in the `main-horizontal` layout. If this option is set to 0 (the default), it will have no effect. If both the `main-pane-height` and `other-pane-height` options are set, the main pane will grow taller to make the other panes the specified height, but will never shrink to do so. If suffixed by ‘`%`’, this is a percentage of the window size.

other-pane-width width

Like `other-pane-height`, but set the width of other panes in the `main-vertical` layout.

pane-active-border-style style

Set the pane border style for the currently active pane. For how to specify style, see the [Styles](https://www.mankier.com/1/tmux#Styles) section. Attributes are ignored.

pane-base-index index

Like `base-index`, but set the starting index for pane numbers.

pane-border-format format

Set the text shown in pane border status lines.

pane-border-indicators \[off | colour | arrows | both\]

Indicate active pane by colouring only half of the border in windows with exactly two panes, by displaying arrow markers, by drawing both or neither.

pane-border-lines type

Set the type of characters used for drawing pane borders. type may be one of:

single

single lines using ACS or UTF-8 characters

double

double lines using UTF-8 characters

heavy

heavy lines using UTF-8 characters

simple

simple ASCII characters

number

the pane number

‘`double`’ and ‘`heavy`’ will fall back to standard ACS line drawing when UTF-8 is not supported.

pane-border-status \[off | top | bottom\]

Turn pane border status lines off or set their position.

pane-border-style style

Set the pane border style for panes aside from the active pane. For how to specify style, see the [Styles](https://www.mankier.com/1/tmux#Styles) section. Attributes are ignored.

popup-style style

Set the popup style. For how to specify style, see the [Styles](https://www.mankier.com/1/tmux#Styles) section. Attributes are ignored.

popup-border-style style

Set the popup border style. For how to specify style, see the [Styles](https://www.mankier.com/1/tmux#Styles) section. Attributes are ignored.

popup-border-lines type

Set the type of characters used for drawing popup borders. type may be one of:

single

single lines using ACS or UTF-8 characters (default)

rounded

variation of single with rounded corners using UTF-8 characters

double

double lines using UTF-8 characters

heavy

heavy lines using UTF-8 characters

simple

simple ASCII characters

padded

simple ASCII space character

none

no border

‘`double`’ and ‘`heavy`’ will fall back to standard ACS line drawing when UTF-8 is not supported.

window-status-activity-style style

Set status line style for windows with an activity alert. For how to specify style, see the [Styles](https://www.mankier.com/1/tmux#Styles) section.

window-status-bell-style style

Set status line style for windows with a bell alert. For how to specify style, see the [Styles](https://www.mankier.com/1/tmux#Styles) section.

window-status-current-format string

Like window-status-format, but is the format used when the window is the current window.

window-status-current-style style

Set status line style for the currently active window. For how to specify style, see the [Styles](https://www.mankier.com/1/tmux#Styles) section.

window-status-format string

Set the format in which the window is displayed in the status line window list. See the [Formats](https://www.mankier.com/1/tmux#Formats) and [Styles](https://www.mankier.com/1/tmux#Styles) sections.

window-status-last-style style

Set status line style for the last active window. For how to specify style, see the [Styles](https://www.mankier.com/1/tmux#Styles) section.

window-status-separator string

Sets the separator drawn between windows in the status line. The default is a single space character.

window-status-style style

Set status line style for a single window. For how to specify style, see the [Styles](https://www.mankier.com/1/tmux#Styles) section.

window-size largest | smallest | manual | latest

Configure how **tmux** determines the window size. If set to largest, the size of the largest attached session is used; if smallest, the size of the smallest. If manual, the size of a new window is set from the `default-size` option and windows are resized automatically. With latest, **tmux** uses the size of the client that had the most recent activity. See also the `resize-window` command and the `aggressive-resize` option.

wrap-search \[on | off\]

If this option is set, searches will wrap around the end of the pane contents. The default is on.

Available pane options are:

allow-passthrough \[on | off\]

Allow programs in the pane to bypass **tmux** using a terminal escape sequence (\\ePtmux;...\\e\\\\).

allow-rename \[on | off\]

Allow programs in the pane to change the window name using a terminal escape sequence (\\ek...\\e\\\\).

alternate-screen \[on | off\]

This option configures whether programs running inside the pane may use the terminal alternate screen feature, which allows the _smcup_ and _rmcup_ [terminfo(5)](https://www.mankier.com/5/terminfo) capabilities. The alternate screen feature preserves the contents of the window when an interactive application starts and restores it on exit, so that any output visible before the application starts reappears unchanged after it exits.

cursor-colour colour

Set the colour of the cursor.

pane-colours\[\] colour

The default colour palette. Each entry in the array defines the colour **tmux** uses when the colour with that index is requested. The index may be from zero to 255.

cursor-style style

Set the style of the cursor. Available styles are: `default`, `blinking-block`, `block`, `blinking-underline`, `underline`, `blinking-bar`, `bar`.

remain-on-exit \[on | off | failed\]

A pane with this flag set is not destroyed when the program running in it exits. If set to `failed`, then only when the program exit status is not zero. The pane may be reactivated with the `respawn-pane` command.

remain-on-exit-format string

Set the text shown at the bottom of exited panes when `remain-on-exit` is enabled.

scroll-on-clear \[on | off\]

When the entire screen is cleared and this option is on, scroll the contents of the screen into history before clearing it.

synchronize-panes \[on | off\]

Duplicate input to all other panes in the same window where this option is also on (only for panes that are not in any mode).

window-active-style style

Set the pane style when it is the active pane. For how to specify style, see the [Styles](https://www.mankier.com/1/tmux#Styles) section.

window-style style

Set the pane style. For how to specify style, see the [Styles](https://www.mankier.com/1/tmux#Styles) section.

[

## Hooks

](https://www.mankier.com/1/tmux#Hooks)

**tmux** allows commands to run on various triggers, called _hooks_. Most **tmux** commands have an _after_ hook and there are a number of hooks not associated with commands.

Hooks are stored as array options, members of the array are executed in order when the hook is triggered. Like options different hooks may be global or belong to a session, window or pane. Hooks may be configured with the `set-hook` or `set-option` commands and displayed with `show-hooks` or `show-options` `-H`. The following two commands are equivalent:

> ```
> set-hook -g pane-mode-changed[42] 'set -g status-left-style bg=red'
> set-option -g pane-mode-changed[42] 'set -g status-left-style bg=red'
> 
> ```

Setting a hook without specifying an array index clears the hook and sets the first member of the array.

A command's after hook is run after it completes, except when the command is run as part of a hook itself. They are named with an ‘`after-`’ prefix. For example, the following command adds a hook to select the even-vertical layout after every `split-window`:

> ```
> set-hook -g after-split-window "selectl even-vertical"
> 
> ```

All the notifications listed in the [Control Mode](https://www.mankier.com/1/tmux#Control_Mode) section are hooks (without any arguments), except `%exit`. The following additional hooks are available:

alert-activity

Run when a window has activity. See `monitor-activity`.

alert-bell

Run when a window has received a bell. See `monitor-bell`.

alert-silence

Run when a window has been silent. See `monitor-silence`.

client-active

Run when a client becomes the latest active client of its session.

client-attached

Run when a client is attached.

client-detached

Run when a client is detached

client-focus-in

Run when focus enters a client

client-focus-out

Run when focus exits a client

client-resized

Run when a client is resized.

client-session-changed

Run when a client's attached session is changed.

pane-died

Run when the program running in a pane exits, but `remain-on-exit` is on so the pane has not closed.

pane-exited

Run when the program running in a pane exits.

pane-focus-in

Run when the focus enters a pane, if the `focus-events` option is on.

pane-focus-out

Run when the focus exits a pane, if the `focus-events` option is on.

pane-set-clipboard

Run when the terminal clipboard is set using the [xterm(1)](https://www.mankier.com/1/xterm) escape sequence.

session-created

Run when a new session created.

session-closed

Run when a session closed.

session-renamed

Run when a session is renamed.

window-linked

Run when a window is linked into a session.

window-renamed

Run when a window is renamed.

window-resized

Run when a window is resized. This may be after the client-resized hook is run.

window-unlinked

Run when a window is unlinked from a session.

Hooks are managed with these commands:

set-hook \[-agpRuw\] \[-t target-pane\] hook-name command

Without `-R`, sets (or with [\-u](https://www.mankier.com/1/tmux#-u) unsets) hook hook-name to command. The flags are the same as for `set-option`.

With `-R`, run hook-name immediately.

show-hooks \[-gpw\] \[-t target-pane\]

Shows hooks. The flags are the same as for `show-options`.

[

## Mouse Support

](https://www.mankier.com/1/tmux#Mouse_Support)

If the `mouse` option is on (the default is off), **tmux** allows mouse events to be bound as keys. The name of each key is made up of a mouse event (such as ‘`MouseUp1`’) and a location suffix, one of the following:

<table><tbody><tr><td><a href="https://www.mankier.com/1/tmux#Pane" id="Pane"><code>Pane</code></a></td><td>the contents of a pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#Border" id="Border"><code>Border</code></a></td><td>a pane border</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#Status" id="Status"><code>Status</code></a></td><td>the status line window list</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#StatusLeft" id="StatusLeft"><code>StatusLeft</code></a></td><td>the left part of the status line</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#StatusRight" id="StatusRight"><code>StatusRight</code></a></td><td>the right part of the status line</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#StatusDefault" id="StatusDefault"><code>StatusDefault</code></a></td><td>any other part of the status line</td></tr></tbody></table>

The following mouse events are available:

<table><tbody><tr><td><a href="https://www.mankier.com/1/tmux#WheelUp" id="WheelUp"><code>WheelUp</code></a></td><td>WheelDown</td><td></td></tr><tr><td><a href="https://www.mankier.com/1/tmux#MouseDown1" id="MouseDown1"><code>MouseDown1</code></a></td><td>MouseUp1</td><td>MouseDrag1</td><td>MouseDragEnd1</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#MouseDown2" id="MouseDown2"><code>MouseDown2</code></a></td><td>MouseUp2</td><td>MouseDrag2</td><td>MouseDragEnd2</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#MouseDown3" id="MouseDown3"><code>MouseDown3</code></a></td><td>MouseUp3</td><td>MouseDrag3</td><td>MouseDragEnd3</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#SecondClick1" id="SecondClick1"><code>SecondClick1</code></a></td><td>SecondClick2</td><td>SecondClick3</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#DoubleClick1" id="DoubleClick1"><code>DoubleClick1</code></a></td><td>DoubleClick2</td><td>DoubleClick3</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#TripleClick1" id="TripleClick1"><code>TripleClick1</code></a></td><td>TripleClick2</td><td>TripleClick3</td></tr></tbody></table>

The ‘`SecondClick`’ events are fired for the second click of a double click, even if there may be a third click which will fire ‘`TripleClick`’ instead of ‘`DoubleClick`’.

Each should be suffixed with a location, for example ‘`MouseDown1Status`’.

The special token ‘`{mouse}`’ or ‘`=`’ may be used as target-window or target-pane in commands bound to mouse key bindings. It resolves to the window or pane over which the mouse event took place (for example, the window in the status line over which button 1 was released for a ‘`MouseUp1Status`’ binding, or the pane over which the wheel was scrolled for a ‘`WheelDownPane`’ binding).

The `send-keys` `-M` flag may be used to forward a mouse event to a pane.

The default key bindings allow the mouse to be used to select and resize panes, to copy text and to change window using the status line. These take effect if the `mouse` option is turned on.

[

## Formats

](https://www.mankier.com/1/tmux#Formats)

Certain commands accept the `-F` flag with a format argument. This is a string which controls the output format of the command. Format variables are enclosed in ‘`#{`’ and ‘`}`’, for example ‘`#{session_name}`’. The possible variables are listed in the table below, or the name of a **tmux** option may be used for an option's value. Some variables have a shorter alias such as ‘`#S`’; ‘`##`’ is replaced by a single ‘`#`’, ‘`#,`’ by a ‘`,`’ and ‘`#}`’ by a ‘`}`’.

Conditionals are available by prefixing with ‘`?`’ and separating two alternatives with a comma; if the specified variable exists and is not zero, the first alternative is chosen, otherwise the second is used. For example ‘`#{?session_attached,attached,not attached}`’ will include the string ‘`attached`’ if the session is attached and the string ‘`not attached`’ if it is unattached, or ‘`#{?automatic-rename,yes,no}`’ will include ‘`yes`’ if `automatic-rename` is enabled, or ‘`no`’ if not. Conditionals can be nested arbitrarily. Inside a conditional, ‘`,`’ and ‘`}`’ must be escaped as ‘`#,`’ and ‘`#}`’, unless they are part of a ‘`#{...}`’ replacement. For example:

> ```
> #{?pane_in_mode,#[fg=white#,bg=red],#[fg=red#,bg=white]}#W .
> 
> ```

String comparisons may be expressed by prefixing two comma-separated alternatives by ‘`==`’, ‘`!=`’, ‘`<`’, ‘`>`’, ‘`<=`’ or ‘`>=`’ and a colon. For example ‘`#{==:#{host},myhost}`’ will be replaced by ‘`1`’ if running on ‘`myhost`’, otherwise by ‘`0`’. ‘`||`’ and ‘`&&`’ evaluate to true if either or both of two comma-separated alternatives are true, for example ‘`#{||:#{pane_in_mode},#{alternate_on}}`’.

An ‘`m`’ specifies an [fnmatch(3)](https://www.mankier.com/3/fnmatch) or regular expression comparison. The first argument is the pattern and the second the string to compare. An optional argument specifies flags: ‘`r`’ means the pattern is a regular expression instead of the default [fnmatch(3)](https://www.mankier.com/3/fnmatch) pattern, and ‘`i`’ means to ignore case. For example: ‘`#{m:*foo*,#{host}}`’ or ‘`#{m/ri:^A,MYVAR}`’. A ‘`C`’ performs a search for an [fnmatch(3)](https://www.mankier.com/3/fnmatch) pattern or regular expression in the pane content and evaluates to zero if not found, or a line number if found. Like ‘`m`’, an ‘`r`’ flag means search for a regular expression and ‘`i`’ ignores case. For example: ‘`#{C/r:^Start}`’

Numeric operators may be performed by prefixing two comma-separated alternatives with an ‘`e`’ and an operator. An optional ‘`f`’ flag may be given after the operator to use floating point numbers, otherwise integers are used. This may be followed by a number giving the number of decimal places to use for the result. The available operators are: addition ‘`+`’, subtraction ‘`-`’, multiplication ‘`*`’, division ‘`/`’, modulus ‘`m`’ or ‘`%`’ (note that ‘`%`’ must be escaped as ‘`%%`’ in formats which are also expanded by [strftime(3)](https://www.mankier.com/3/strftime)) and numeric comparison operators ‘`==`’, ‘`!=`’, ‘`<`’, ‘`<=`’, ‘`>`’ and ‘`>=`’. For example, ‘`#{e|*|f|4:5.5,3}`’ multiplies 5.5 by 3 for a result with four decimal places and ‘`#{e|%%:7,3}`’ returns the modulus of 7 and 3. ‘`a`’ replaces a numeric argument by its ASCII equivalent, so ‘`#{a:98}`’ results in ‘`b`’. ‘`c`’ replaces a **tmux** colour by its six-digit hexadecimal RGB value.

A limit may be placed on the length of the resultant string by prefixing it by an ‘`=`’, a number and a colon. Positive numbers count from the start of the string and negative from the end, so ‘`#{=5:pane_title}`’ will include at most the first five characters of the pane title, or ‘`#{=-5:pane_title}`’ the last five characters. A suffix or prefix may be given as a second argument - if provided then it is appended or prepended to the string if the length has been trimmed, for example ‘`#{=/5/...:pane_title}`’ will append ‘`...`’ if the pane title is more than five characters. Similarly, ‘`p`’ pads the string to a given width, for example ‘`#{p10:pane_title}`’ will result in a width of at least 10 characters. A positive width pads on the left, a negative on the right. ‘`n`’ expands to the length of the variable and ‘`w`’ to its width when displayed, for example ‘`#{n:window_name}`’.

Prefixing a time variable with ‘`t:`’ will convert it to a string, so if ‘`#{window_activity}`’ gives ‘`1445765102`’, ‘`#{t:window_activity}`’ gives ‘`Sun Oct 25 09:25:02 2015`’. Adding ‘`p (`’ ‘`` `t/p` ``’) will use shorter but less accurate time format for times in the past. A custom format may be given using an ‘`f`’ suffix (note that ‘`%`’ must be escaped as ‘`%%`’ if the format is separately being passed through [strftime(3)](https://www.mankier.com/3/strftime), for example in the `status-left` option): ‘`#{t/f/%%H#:%%M:window_activity}`’, see [strftime(3)](https://www.mankier.com/3/strftime).

The ‘`b:`’ and ‘`d:`’ prefixes are [basename(3)](https://www.mankier.com/3/basename) and [dirname(3)](https://www.mankier.com/3/basename) of the variable respectively. ‘`q:`’ will escape [sh(1)](https://www.mankier.com/1/bash) special characters or with a ‘`h`’ suffix, escape hash characters (so ‘`#`’ becomes ‘`##`’). ‘`E:`’ will expand the format twice, for example ‘`#{E:status-left}`’ is the result of expanding the content of the `status-left` option rather than the option itself. ‘`T:`’ is like ‘`E:`’ but also expands [strftime(3)](https://www.mankier.com/3/strftime) specifiers. ‘`S:`’, ‘`W:`’ or ‘`P:`’ will loop over each session, window or pane and insert the format once for each. For windows and panes, two comma-separated formats may be given: the second is used for the current window or active pane. For example, to get a list of windows formatted like the status line:

> ```
> #{W:#{E:window-status-format} ,#{E:window-status-current-format} }
> 
> ```

‘`N:`’ checks if a window (without any suffix or with the ‘`w`’ suffix) or a session (with the ‘`s`’ suffix) name exists, for example ‘`` `N/w:foo` ``’ is replaced with 1 if a window named ‘`foo`’ exists.

A prefix of the form ‘`s/foo/bar/:`’ will substitute ‘`foo`’ with ‘`bar`’ throughout. The first argument may be an extended regular expression and a final argument may be ‘`i`’ to ignore case, for example ‘`s/a(.)/\1x/i:`’ would change ‘`abABab`’ into ‘`bxBxbx`’.

In addition, the last line of a shell command's output may be inserted using ‘`#()`’. For example, ‘`#(uptime)`’ will insert the system's uptime. When constructing formats, **tmux** does not wait for ‘`#()`’ commands to finish; instead, the previous result from running the same command is used, or a placeholder if the command has not been run before. If the command hasn't exited, the most recent line of output will be used, but the status line will not be updated more than once a second. Commands are executed using `/bin/sh` and with the **tmux** global environment set (see the [Global and Session Environment](https://www.mankier.com/1/tmux#Global_and_Session_Environment) section).

An ‘`l`’ specifies that a string should be interpreted literally and not expanded. For example ‘`#{l:#{?pane_in_mode,yes,no}}`’ will be replaced by ‘`#{?pane_in_mode,yes,no}`’.

The following variables are available, where appropriate:

<table><tbody><tr><td><b>Variable name</b></td><td><b>Alias</b></td><td><b>Replaced with</b></td></tr><tr><td><a href="https://www.mankier.com/1/tmux#active_window_index" id="active_window_index"><code>active_window_index</code></a></td><td></td><td>Index of active window in session</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#alternate_on" id="alternate_on"><code>alternate_on</code></a></td><td></td><td>1 if pane is in alternate screen</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#alternate_saved_x" id="alternate_saved_x"><code>alternate_saved_x</code></a></td><td></td><td>Saved cursor X in alternate screen</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#alternate_saved_y" id="alternate_saved_y"><code>alternate_saved_y</code></a></td><td></td><td>Saved cursor Y in alternate screen</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#buffer_created" id="buffer_created"><code>buffer_created</code></a></td><td></td><td>Time buffer created</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#buffer_name" id="buffer_name"><code>buffer_name</code></a></td><td></td><td>Name of buffer</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#buffer_sample" id="buffer_sample"><code>buffer_sample</code></a></td><td></td><td>Sample of start of buffer</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#buffer_size" id="buffer_size"><code>buffer_size</code></a></td><td></td><td>Size of the specified buffer in bytes</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#client_activity" id="client_activity"><code>client_activity</code></a></td><td></td><td>Time client last had activity</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#client_cell_height" id="client_cell_height"><code>client_cell_height</code></a></td><td></td><td>Height of each client cell in pixels</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#client_cell_width" id="client_cell_width"><code>client_cell_width</code></a></td><td></td><td>Width of each client cell in pixels</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#client_control_mode" id="client_control_mode"><code>client_control_mode</code></a></td><td></td><td>1 if client is in control mode</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#client_created" id="client_created"><code>client_created</code></a></td><td></td><td>Time client created</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#client_discarded" id="client_discarded"><code>client_discarded</code></a></td><td></td><td>Bytes discarded when client behind</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#client_flags" id="client_flags"><code>client_flags</code></a></td><td></td><td>List of client flags</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#client_height" id="client_height"><code>client_height</code></a></td><td></td><td>Height of client</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#client_key_table" id="client_key_table"><code>client_key_table</code></a></td><td></td><td>Current key table</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#client_last_session" id="client_last_session"><code>client_last_session</code></a></td><td></td><td>Name of the client's last session</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#client_name" id="client_name"><code>client_name</code></a></td><td></td><td>Name of client</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#client_pid" id="client_pid"><code>client_pid</code></a></td><td></td><td>PID of client process</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#client_prefix" id="client_prefix"><code>client_prefix</code></a></td><td></td><td>1 if prefix key has been pressed</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#client_readonly" id="client_readonly"><code>client_readonly</code></a></td><td></td><td>1 if client is read-only</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#client_session" id="client_session"><code>client_session</code></a></td><td></td><td>Name of the client's session</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#client_termfeatures" id="client_termfeatures"><code>client_termfeatures</code></a></td><td></td><td>Terminal features of client, if any</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#client_termname" id="client_termname"><code>client_termname</code></a></td><td></td><td>Terminal name of client</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#client_termtype" id="client_termtype"><code>client_termtype</code></a></td><td></td><td>Terminal type of client, if available</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#client_tty" id="client_tty"><code>client_tty</code></a></td><td></td><td>Pseudo terminal of client</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#client_uid" id="client_uid"><code>client_uid</code></a></td><td></td><td>UID of client process</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#client_user" id="client_user"><code>client_user</code></a></td><td></td><td>User of client process</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#client_utf8" id="client_utf8"><code>client_utf8</code></a></td><td></td><td>1 if client supports UTF-8</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#client_width" id="client_width"><code>client_width</code></a></td><td></td><td>Width of client</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#client_written" id="client_written"><code>client_written</code></a></td><td></td><td>Bytes written to client</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#command" id="command"><code>command</code></a></td><td></td><td>Name of command in use, if any</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#command_list_alias" id="command_list_alias"><code>command_list_alias</code></a></td><td></td><td>Command alias if listing commands</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#command_list_name" id="command_list_name"><code>command_list_name</code></a></td><td></td><td>Command name if listing commands</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#command_list_usage" id="command_list_usage"><code>command_list_usage</code></a></td><td></td><td>Command usage if listing commands</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#config_files" id="config_files"><code>config_files</code></a></td><td></td><td>List of configuration files loaded</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#copy_cursor_line" id="copy_cursor_line"><code>copy_cursor_line</code></a></td><td></td><td>Line the cursor is on in copy mode</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#copy_cursor_word" id="copy_cursor_word"><code>copy_cursor_word</code></a></td><td></td><td>Word under cursor in copy mode</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#copy_cursor_x" id="copy_cursor_x"><code>copy_cursor_x</code></a></td><td></td><td>Cursor X position in copy mode</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#copy_cursor_y" id="copy_cursor_y"><code>copy_cursor_y</code></a></td><td></td><td>Cursor Y position in copy mode</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#current_file" id="current_file"><code>current_file</code></a></td><td></td><td>Current configuration file</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#cursor_character" id="cursor_character"><code>cursor_character</code></a></td><td></td><td>Character at cursor in pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#cursor_flag" id="cursor_flag"><code>cursor_flag</code></a></td><td></td><td>Pane cursor flag</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#cursor_x" id="cursor_x"><code>cursor_x</code></a></td><td></td><td>Cursor X position in pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#cursor_y" id="cursor_y"><code>cursor_y</code></a></td><td></td><td>Cursor Y position in pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#history_bytes" id="history_bytes"><code>history_bytes</code></a></td><td></td><td>Number of bytes in window history</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#history_limit" id="history_limit"><code>history_limit</code></a></td><td></td><td>Maximum window history lines</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#history_size" id="history_size"><code>history_size</code></a></td><td></td><td>Size of history in lines</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#hook" id="hook"><code>hook</code></a></td><td></td><td>Name of running hook, if any</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#hook_client" id="hook_client"><code>hook_client</code></a></td><td></td><td>Name of client where hook was run, if any</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#hook_pane" id="hook_pane"><code>hook_pane</code></a></td><td></td><td>ID of pane where hook was run, if any</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#hook_session" id="hook_session"><code>hook_session</code></a></td><td></td><td>ID of session where hook was run, if any</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#hook_session_name" id="hook_session_name"><code>hook_session_name</code></a></td><td></td><td>Name of session where hook was run, if any</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#hook_window" id="hook_window"><code>hook_window</code></a></td><td></td><td>ID of window where hook was run, if any</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#hook_window_name" id="hook_window_name"><code>hook_window_name</code></a></td><td></td><td>Name of window where hook was run, if any</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#host" id="host"><code>host</code></a></td><td>#H</td><td>Hostname of local host</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#host_short" id="host_short"><code>host_short</code></a></td><td>#h</td><td>Hostname of local host (no domain name)</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#insert_flag" id="insert_flag"><code>insert_flag</code></a></td><td></td><td>Pane insert flag</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#keypad_cursor_flag" id="keypad_cursor_flag"><code>keypad_cursor_flag</code></a></td><td></td><td>Pane keypad cursor flag</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#keypad_flag" id="keypad_flag"><code>keypad_flag</code></a></td><td></td><td>Pane keypad flag</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#last_window_index" id="last_window_index"><code>last_window_index</code></a></td><td></td><td>Index of last window in session</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#line" id="line"><code>line</code></a></td><td></td><td>Line number in the list</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#mouse_all_flag" id="mouse_all_flag"><code>mouse_all_flag</code></a></td><td></td><td>Pane mouse all flag</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#mouse_any_flag" id="mouse_any_flag"><code>mouse_any_flag</code></a></td><td></td><td>Pane mouse any flag</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#mouse_button_flag" id="mouse_button_flag"><code>mouse_button_flag</code></a></td><td></td><td>Pane mouse button flag</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#mouse_line" id="mouse_line"><code>mouse_line</code></a></td><td></td><td>Line under mouse, if any</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#mouse_sgr_flag" id="mouse_sgr_flag"><code>mouse_sgr_flag</code></a></td><td></td><td>Pane mouse SGR flag</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#mouse_standard_flag" id="mouse_standard_flag"><code>mouse_standard_flag</code></a></td><td></td><td>Pane mouse standard flag</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#mouse_utf8_flag" id="mouse_utf8_flag"><code>mouse_utf8_flag</code></a></td><td></td><td>Pane mouse UTF-8 flag</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#mouse_word" id="mouse_word"><code>mouse_word</code></a></td><td></td><td>Word under mouse, if any</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#mouse_x" id="mouse_x"><code>mouse_x</code></a></td><td></td><td>Mouse X position, if any</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#mouse_y" id="mouse_y"><code>mouse_y</code></a></td><td></td><td>Mouse Y position, if any</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#next_session_id" id="next_session_id"><code>next_session_id</code></a></td><td></td><td>Unique session ID for next new session</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#origin_flag" id="origin_flag"><code>origin_flag</code></a></td><td></td><td>Pane origin flag</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_active" id="pane_active"><code>pane_active</code></a></td><td></td><td>1 if active pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_at_bottom" id="pane_at_bottom"><code>pane_at_bottom</code></a></td><td></td><td>1 if pane is at the bottom of window</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_at_left" id="pane_at_left"><code>pane_at_left</code></a></td><td></td><td>1 if pane is at the left of window</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_at_right" id="pane_at_right"><code>pane_at_right</code></a></td><td></td><td>1 if pane is at the right of window</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_at_top" id="pane_at_top"><code>pane_at_top</code></a></td><td></td><td>1 if pane is at the top of window</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_bg" id="pane_bg"><code>pane_bg</code></a></td><td></td><td>Pane background colour</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_bottom" id="pane_bottom"><code>pane_bottom</code></a></td><td></td><td>Bottom of pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_current_command" id="pane_current_command"><code>pane_current_command</code></a></td><td></td><td>Current command if available</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_current_path" id="pane_current_path"><code>pane_current_path</code></a></td><td></td><td>Current path if available</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_dead" id="pane_dead"><code>pane_dead</code></a></td><td></td><td>1 if pane is dead</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_dead_signal" id="pane_dead_signal"><code>pane_dead_signal</code></a></td><td></td><td>Exit signal of process in dead pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_dead_status" id="pane_dead_status"><code>pane_dead_status</code></a></td><td></td><td>Exit status of process in dead pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_dead_time" id="pane_dead_time"><code>pane_dead_time</code></a></td><td></td><td>Exit time of process in dead pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_fg" id="pane_fg"><code>pane_fg</code></a></td><td></td><td>Pane foreground colour</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_format" id="pane_format"><code>pane_format</code></a></td><td></td><td>1 if format is for a pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_height" id="pane_height"><code>pane_height</code></a></td><td></td><td>Height of pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_id" id="pane_id"><code>pane_id</code></a></td><td>#D</td><td>Unique pane ID</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_in_mode" id="pane_in_mode"><code>pane_in_mode</code></a></td><td></td><td>1 if pane is in a mode</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_index" id="pane_index"><code>pane_index</code></a></td><td>#P</td><td>Index of pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_input_off" id="pane_input_off"><code>pane_input_off</code></a></td><td></td><td>1 if input to pane is disabled</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_last" id="pane_last"><code>pane_last</code></a></td><td></td><td>1 if last pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_left" id="pane_left"><code>pane_left</code></a></td><td></td><td>Left of pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_marked" id="pane_marked"><code>pane_marked</code></a></td><td></td><td>1 if this is the marked pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_marked_set" id="pane_marked_set"><code>pane_marked_set</code></a></td><td></td><td>1 if a marked pane is set</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_mode" id="pane_mode"><code>pane_mode</code></a></td><td></td><td>Name of pane mode, if any</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_path" id="pane_path"><code>pane_path</code></a></td><td></td><td>Path of pane (can be set by application)</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_pid" id="pane_pid"><code>pane_pid</code></a></td><td></td><td>PID of first process in pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_pipe" id="pane_pipe"><code>pane_pipe</code></a></td><td></td><td>1 if pane is being piped</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_right" id="pane_right"><code>pane_right</code></a></td><td></td><td>Right of pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_search_string" id="pane_search_string"><code>pane_search_string</code></a></td><td></td><td>Last search string in copy mode</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_start_command" id="pane_start_command"><code>pane_start_command</code></a></td><td></td><td>Command pane started with</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_start_path" id="pane_start_path"><code>pane_start_path</code></a></td><td></td><td>Path pane started with</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_synchronized" id="pane_synchronized"><code>pane_synchronized</code></a></td><td></td><td>1 if pane is synchronized</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_tabs" id="pane_tabs"><code>pane_tabs</code></a></td><td></td><td>Pane tab positions</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_title" id="pane_title"><code>pane_title</code></a></td><td>#T</td><td>Title of pane (can be set by application)</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_top" id="pane_top"><code>pane_top</code></a></td><td></td><td>Top of pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_tty" id="pane_tty"><code>pane_tty</code></a></td><td></td><td>Pseudo terminal of pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pane_width" id="pane_width"><code>pane_width</code></a></td><td></td><td>Width of pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#pid" id="pid"><code>pid</code></a></td><td></td><td>Server PID</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#rectangle_toggle" id="rectangle_toggle"><code>rectangle_toggle</code></a></td><td></td><td>1 if rectangle selection is activated</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#scroll_position" id="scroll_position"><code>scroll_position</code></a></td><td></td><td>Scroll position in copy mode</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#scroll_region_lower" id="scroll_region_lower"><code>scroll_region_lower</code></a></td><td></td><td>Bottom of scroll region in pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#scroll_region_upper" id="scroll_region_upper"><code>scroll_region_upper</code></a></td><td></td><td>Top of scroll region in pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#search_match" id="search_match"><code>search_match</code></a></td><td></td><td>Search match if any</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#search_present" id="search_present"><code>search_present</code></a></td><td></td><td>1 if search started in copy mode</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#selection_active" id="selection_active"><code>selection_active</code></a></td><td></td><td>1 if selection started and changes with the cursor in copy mode</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#selection_end_x" id="selection_end_x"><code>selection_end_x</code></a></td><td></td><td>X position of the end of the selection</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#selection_end_y" id="selection_end_y"><code>selection_end_y</code></a></td><td></td><td>Y position of the end of the selection</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#selection_present" id="selection_present"><code>selection_present</code></a></td><td></td><td>1 if selection started in copy mode</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#selection_start_x" id="selection_start_x"><code>selection_start_x</code></a></td><td></td><td>X position of the start of the selection</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#selection_start_y" id="selection_start_y"><code>selection_start_y</code></a></td><td></td><td>Y position of the start of the selection</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#session_activity" id="session_activity"><code>session_activity</code></a></td><td></td><td>Time of session last activity</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#session_alerts" id="session_alerts"><code>session_alerts</code></a></td><td></td><td>List of window indexes with alerts</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#session_attached" id="session_attached"><code>session_attached</code></a></td><td></td><td>Number of clients session is attached to</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#session_attached_list" id="session_attached_list"><code>session_attached_list</code></a></td><td></td><td>List of clients session is attached to</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#session_created" id="session_created"><code>session_created</code></a></td><td></td><td>Time session created</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#session_format" id="session_format"><code>session_format</code></a></td><td></td><td>1 if format is for a session</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#session_group" id="session_group"><code>session_group</code></a></td><td></td><td>Name of session group</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#session_group_attached" id="session_group_attached"><code>session_group_attached</code></a></td><td></td><td>Number of clients sessions in group are attached to</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#session_group_attached_list" id="session_group_attached_list"><code>session_group_attached_list</code></a></td><td></td><td>List of clients sessions in group are attached to</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#session_group_list" id="session_group_list"><code>session_group_list</code></a></td><td></td><td>List of sessions in group</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#session_group_many_attached" id="session_group_many_attached"><code>session_group_many_attached</code></a></td><td></td><td>1 if multiple clients attached to sessions in group</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#session_group_size" id="session_group_size"><code>session_group_size</code></a></td><td></td><td>Size of session group</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#session_grouped" id="session_grouped"><code>session_grouped</code></a></td><td></td><td>1 if session in a group</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#session_id" id="session_id"><code>session_id</code></a></td><td></td><td>Unique session ID</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#session_last_attached" id="session_last_attached"><code>session_last_attached</code></a></td><td></td><td>Time session last attached</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#session_many_attached" id="session_many_attached"><code>session_many_attached</code></a></td><td></td><td>1 if multiple clients attached</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#session_marked" id="session_marked"><code>session_marked</code></a></td><td></td><td>1 if this session contains the marked pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#session_name" id="session_name"><code>session_name</code></a></td><td>#S</td><td>Name of session</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#session_path" id="session_path"><code>session_path</code></a></td><td></td><td>Working directory of session</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#session_stack" id="session_stack"><code>session_stack</code></a></td><td></td><td>Window indexes in most recent order</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#session_windows" id="session_windows"><code>session_windows</code></a></td><td></td><td>Number of windows in session</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#socket_path" id="socket_path"><code>socket_path</code></a></td><td></td><td>Server socket path</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#start_time" id="start_time"><code>start_time</code></a></td><td></td><td>Server start time</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#uid" id="uid"><code>uid</code></a></td><td></td><td>Server UID</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#user" id="user"><code>user</code></a></td><td></td><td>Server user</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#version" id="version"><code>version</code></a></td><td></td><td>Server version</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_active" id="window_active"><code>window_active</code></a></td><td></td><td>1 if window active</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_active_clients" id="window_active_clients"><code>window_active_clients</code></a></td><td></td><td>Number of clients viewing this window</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_active_clients_list" id="window_active_clients_list"><code>window_active_clients_list</code></a></td><td></td><td>List of clients viewing this window</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_active_sessions" id="window_active_sessions"><code>window_active_sessions</code></a></td><td></td><td>Number of sessions on which this window is active</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_active_sessions_list" id="window_active_sessions_list"><code>window_active_sessions_list</code></a></td><td></td><td>List of sessions on which this window is active</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_activity" id="window_activity"><code>window_activity</code></a></td><td></td><td>Time of window last activity</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_activity_flag" id="window_activity_flag"><code>window_activity_flag</code></a></td><td></td><td>1 if window has activity</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_bell_flag" id="window_bell_flag"><code>window_bell_flag</code></a></td><td></td><td>1 if window has bell</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_bigger" id="window_bigger"><code>window_bigger</code></a></td><td></td><td>1 if window is larger than client</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_cell_height" id="window_cell_height"><code>window_cell_height</code></a></td><td></td><td>Height of each cell in pixels</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_cell_width" id="window_cell_width"><code>window_cell_width</code></a></td><td></td><td>Width of each cell in pixels</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_end_flag" id="window_end_flag"><code>window_end_flag</code></a></td><td></td><td>1 if window has the highest index</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_flags" id="window_flags"><code>window_flags</code></a></td><td>#F</td><td>Window flags with # escaped as ##</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_format" id="window_format"><code>window_format</code></a></td><td></td><td>1 if format is for a window</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_height" id="window_height"><code>window_height</code></a></td><td></td><td>Height of window</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_id" id="window_id"><code>window_id</code></a></td><td></td><td>Unique window ID</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_index" id="window_index"><code>window_index</code></a></td><td>#I</td><td>Index of window</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_last_flag" id="window_last_flag"><code>window_last_flag</code></a></td><td></td><td>1 if window is the last used</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_layout" id="window_layout"><code>window_layout</code></a></td><td></td><td>Window layout description, ignoring zoomed window panes</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_linked" id="window_linked"><code>window_linked</code></a></td><td></td><td>1 if window is linked across sessions</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_linked_sessions" id="window_linked_sessions"><code>window_linked_sessions</code></a></td><td></td><td>Number of sessions this window is linked to</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_linked_sessions_list" id="window_linked_sessions_list"><code>window_linked_sessions_list</code></a></td><td></td><td>List of sessions this window is linked to</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_marked_flag" id="window_marked_flag"><code>window_marked_flag</code></a></td><td></td><td>1 if window contains the marked pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_name" id="window_name"><code>window_name</code></a></td><td>#W</td><td>Name of window</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_offset_x" id="window_offset_x"><code>window_offset_x</code></a></td><td></td><td>X offset into window if larger than client</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_offset_y" id="window_offset_y"><code>window_offset_y</code></a></td><td></td><td>Y offset into window if larger than client</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_panes" id="window_panes"><code>window_panes</code></a></td><td></td><td>Number of panes in window</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_raw_flags" id="window_raw_flags"><code>window_raw_flags</code></a></td><td></td><td>Window flags with nothing escaped</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_silence_flag" id="window_silence_flag"><code>window_silence_flag</code></a></td><td></td><td>1 if window has silence alert</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_stack_index" id="window_stack_index"><code>window_stack_index</code></a></td><td></td><td>Index in session most recent stack</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_start_flag" id="window_start_flag"><code>window_start_flag</code></a></td><td></td><td>1 if window has the lowest index</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_visible_layout" id="window_visible_layout"><code>window_visible_layout</code></a></td><td></td><td>Window layout description, respecting zoomed window panes</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_width" id="window_width"><code>window_width</code></a></td><td></td><td>Width of window</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#window_zoomed_flag" id="window_zoomed_flag"><code>window_zoomed_flag</code></a></td><td></td><td>1 if window is zoomed</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#wrap_flag" id="wrap_flag"><code>wrap_flag</code></a></td><td></td><td>Pane wrap flag</td></tr></tbody></table>

[

## Styles

](https://www.mankier.com/1/tmux#Styles)

**tmux** offers various options to specify the colour and attributes of aspects of the interface, for example `status-style` for the status line. In addition, embedded styles may be specified in format options, such as `status-left`, by enclosing them in ‘`#[`’ and ‘`]`’.

A style may be the single term ‘`default`’ to specify the default style (which may come from an option, for example `status-style` in the status line) or a space or comma separated list of the following:

fg=colour

Set the foreground colour. The colour is one of: `black`, `red`, `green`, `yellow`, `blue`, `magenta`, `cyan`, `white`; if supported the bright variants `brightred`, `brightgreen`, `brightyellow`; `colour0` to `colour255` from the 256-colour set; `default` for the default colour; `terminal` for the terminal default colour; or a hexadecimal RGB string such as ‘`#ffffff`’.

bg=colour

Set the background colour.

none

Set no attributes (turn off any active attributes).

acs, bright (or bold), dim, underscore, blink, reverse, hidden, italics, overline, strikethrough, double-underscore, curly-underscore, dotted-underscore, dashed-underscore

Set an attribute. Any of the attributes may be prefixed with ‘`no`’ to unset. `acs` is the terminal alternate character set.

align=left (or noalign), align=centre, align=right

Align text to the left, centre or right of the available space if appropriate.

fill=colour

Fill the available space with a background colour if appropriate.

list=on, list=focus, list=left-marker, list=right-marker, nolist

Mark the position of the various window list components in the `status-format` option: `list=on` marks the start of the list; `list=focus` is the part of the list that should be kept in focus if the entire list won't fit in the available space (typically the current window); `list=left-marker` and `list=right-marker` mark the text to be used to mark that text has been trimmed from the left or right of the list if there is not enough space.

push-default, pop-default

Store the current colours and attributes as the default or reset to the previous default. A `push-default` affects any subsequent use of the `default` term until a `pop-default`. Only one default may be pushed (each `push-default` replaces the previous saved default).

range=left, range=right, range=window|X, norange

Mark a range in the `status-format` option. `range=left` and `range=right` are the text used for the ‘`StatusLeft`’ and ‘`StatusRight`’ mouse keys. `range=window|X` is the range for a window passed to the ‘`Status`’ mouse key, where ‘`X`’ is a window index.

Examples are:

> ```
> fg=yellow bold underscore blink
> bg=black,fg=default,noreverse
> 
> ```

[

## Names and Titles

](https://www.mankier.com/1/tmux#Names_and_Titles)

**tmux** distinguishes between names and titles. Windows and sessions have names, which may be used to specify them in targets and are displayed in the status line and various lists: the name is the **tmux** identifier for a window or session. Only panes have titles. A pane's title is typically set by the program running inside the pane using an escape sequence (like it would set the [xterm(1)](https://www.mankier.com/1/xterm) window title in X(7)). Windows themselves do not have titles - a window's title is the title of its active pane. **tmux** itself may set the title of the terminal in which the client is running, see the `set-titles` option.

A session's name is set with the `new-session` and `rename-session` commands. A window's name is set with one of:

1.  A command argument (such as `-n` for `new-window` or `new-session`).
    
2.  An escape sequence (if the `allow-rename` option is turned on):
    
    > ```
    > $ printf '\033kWINDOW_NAME\033\\'
    >     
    > ```
    
3.  Automatic renaming, which sets the name to the active command in the window's active pane. See the `automatic-rename` option.
    

When a pane is first created, its title is the hostname. A pane's title can be set via the title setting escape sequence, for example:

> ```
> $ printf '\033]2;My Title\033\\'
> 
> ```

It can also be modified with the `select-pane` [\-T](https://www.mankier.com/1/tmux#-T) command.

[

## Global and Session Environment

](https://www.mankier.com/1/tmux#Global_and_Session_Environment)

When the server is started, **tmux** copies the environment into the _global environment_; in addition, each session has a _session environment_. When a window is created, the session and global environments are merged. If a variable exists in both, the value from the session environment is used. The result is the initial environment passed to the new process.

The `update-environment` session option may be used to update the session environment from the client when a new session is created or an old reattached. **tmux** also initialises the `TMUX` variable with some internal information to allow commands to be executed from inside, and the `TERM` variable with the correct terminal setting of ‘`screen`’.

Variables in both session and global environments may be marked as hidden. Hidden variables are not passed into the environment of new processes and instead can only be used by tmux itself (for example in formats, see the [Formats](https://www.mankier.com/1/tmux#Formats) section).

Commands to alter and view the environment are:

set-environment \[-Fhgru\] \[-t target-session\] name \[value\]

> (alias: `setenv`)

Set or unset an environment variable. If `-g` is used, the change is made in the global environment; otherwise, it is applied to the session environment for target-session. If `-F` is present, then value is expanded as a format. The [\-u](https://www.mankier.com/1/tmux#-u) flag unsets a variable. `-r` indicates the variable is to be removed from the environment before starting a new process. `-h` marks the variable as hidden.

show-environment \[-hgs\] \[-t target-session\] \[variable\]

> (alias: `showenv`)

Display the environment for target-session or the global environment with `-g`. If variable is omitted, all variables are shown. Variables removed from the environment are prefixed with ‘`-`’. If `-s` is used, the output is formatted as a set of Bourne shell commands. `-h` shows hidden variables (omitted by default).

[

## Status Line

](https://www.mankier.com/1/tmux#Status_Line)

**tmux** includes an optional status line which is displayed in the bottom line of each terminal.

By default, the status line is enabled and one line in height (it may be disabled or made multiple lines with the `status` session option) and contains, from left-to-right: the name of the current session in square brackets; the window list; the title of the active pane in double quotes; and the time and date.

Each line of the status line is configured with the `status-format` option. The default is made of three parts: configurable left and right sections (which may contain dynamic content such as the time or output from a shell command, see the `status-left`, `status-left-length`, `status-right`, and `status-right-length` options below), and a central window list. By default, the window list shows the index, name and (if any) flag of the windows present in the current session in ascending numerical order. It may be customised with the window-status-format and window-status-current-format options. The flag is one of the following symbols appended to the window name:

<table><tbody><tr><td><b>Symbol</b></td><td><b>Meaning</b></td></tr><tr><td><a href="https://www.mankier.com/1/tmux#*" id="*"><code>*</code></a></td><td>Denotes the current window.</td></tr><tr><td><code>-</code></td><td>Marks the last window (previously selected).</td></tr><tr><td><code>#</code></td><td>Window activity is monitored and activity has been detected.</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#!" id="!"><code>!</code></a></td><td>Window bells are monitored and a bell has occurred in the window.</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#~" id="~"><code>~</code></a></td><td>The window has been silent for the monitor-silence interval.</td></tr><tr><td><code>M</code></td><td>The window contains the marked pane.</td></tr><tr><td><code>Z</code></td><td>The window's active pane is zoomed.</td></tr></tbody></table>

The # symbol relates to the `monitor-activity` window option. The window name is printed in inverted colours if an alert (bell, activity or silence) is present.

The colour and attributes of the status line may be configured, the entire status line using the `status-style` session option and individual windows using the `window-status-style` window option.

The status line is automatically refreshed at interval if it has changed, the interval may be controlled with the `status-interval` session option.

Commands related to the status line are as follows:

clear-prompt-history \[[\-T](https://www.mankier.com/1/tmux#-T) prompt-type\]

> (alias: `clearphist`)

Clear status prompt history for prompt type prompt-type. If [\-T](https://www.mankier.com/1/tmux#-T) is omitted, then clear history for all types. See `command-prompt` for possible values for prompt-type.

command-prompt \[-1bFikN\] \[-I inputs\] \[-p prompts\] \[-t target-client\] \[[\-T](https://www.mankier.com/1/tmux#-T) prompt-type\] \[template\]

Open the command prompt in a client. This may be used from inside **tmux** to execute commands interactively.

If template is specified, it is used as the command. With `-F`, template is expanded as a format.

If present, `-I` is a comma-separated list of the initial text for each prompt. If `-p` is given, prompts is a comma-separated list of prompts which are displayed in order; otherwise a single prompt is displayed, constructed from template if it is present, or ‘`:`’ if not.

Before the command is executed, the first occurrence of the string ‘`%%`’ and all occurrences of ‘`%1`’ are replaced by the response to the first prompt, all ‘`%2`’ are replaced with the response to the second prompt, and so on for further prompts. Up to nine prompt responses may be replaced (‘`%1`’ to ‘`%9`’). ‘`%%%`’ is like ‘`%%`’ but any quotation marks are escaped.

`-1` makes the prompt only accept one key press, in this case the resulting input is a single character. `-k` is like `-1` but the key press is translated to a key name. [\-N](https://www.mankier.com/1/tmux#-N) makes the prompt only accept numeric key presses. `-i` executes the command every time the prompt input changes instead of when the user exits the command prompt.

[\-T](https://www.mankier.com/1/tmux#-T) tells **tmux** the prompt type. This affects what completions are offered when _Tab_ is pressed. Available types are: ‘`command`’, ‘`search`’, ‘`target`’ and ‘`window-target`’.

The following keys have a special meaning in the command prompt, depending on the value of the `status-keys` option:

<table><tbody><tr><td><b>Function</b></td><td><b>vi</b></td><td><b>emacs</b></td></tr><tr><td><code>Cancel command prompt</code></td><td>q</td><td>Escape</td></tr><tr><td><code>Delete from cursor to start of word</code></td><td></td><td>C-w</td></tr><tr><td><code>Delete entire command</code></td><td>d</td><td>C-u</td></tr><tr><td><code>Delete from cursor to end</code></td><td>D</td><td>C-k</td></tr><tr><td><code>Execute command</code></td><td>Enter</td><td>Enter</td></tr><tr><td><code>Get next command from history</code></td><td></td><td>Down</td></tr><tr><td><code>Get previous command from history</code></td><td></td><td>Up</td></tr><tr><td><code>Insert top paste buffer</code></td><td>p</td><td>C-y</td></tr><tr><td><code>Look for completions</code></td><td>Tab</td><td>Tab</td></tr><tr><td><code>Move cursor left</code></td><td>h</td><td>Left</td></tr><tr><td><code>Move cursor right</code></td><td>l</td><td>Right</td></tr><tr><td><code>Move cursor to end</code></td><td>$</td><td>C-e</td></tr><tr><td><code>Move cursor to next word</code></td><td>w</td><td>M-f</td></tr><tr><td><code>Move cursor to previous word</code></td><td>b</td><td>M-b</td></tr><tr><td><code>Move cursor to start</code></td><td>0</td><td>C-a</td></tr><tr><td><code>Transpose characters</code></td><td></td><td>C-t</td></tr></tbody></table>

With `-b`, the prompt is shown in the background and the invoking client does not exit until it is dismissed.

confirm-before \[-b\] \[-p prompt\] \[-t target-client\] command

> (alias: `confirm`)

Ask for confirmation before executing command. If `-p` is given, prompt is the prompt to display; otherwise a prompt is constructed from command. It may contain the special character sequences supported by the `status-left` option. With `-b`, the prompt is shown in the background and the invoking client does not exit until it is dismissed.

display-menu \[-O\] \[[\-c](https://www.mankier.com/1/tmux#-c) target-client\] \[-t target-pane\] \[[\-T](https://www.mankier.com/1/tmux#-T) title\] \[-x position\] \[-y position\] name key command ...

> (alias: `menu`)

Display a menu on target-client. target-pane gives the target for any commands run from the menu.

A menu is passed as a series of arguments: first the menu item name, second the key shortcut (or empty for none) and third the command to run when the menu item is chosen. The name and command are formats, see the [Formats](https://www.mankier.com/1/tmux#Formats) and [Styles](https://www.mankier.com/1/tmux#Styles) sections. If the name begins with a hyphen (-), then the item is disabled (shown dim) and may not be chosen. The name may be empty for a separator line, in which case both the key and command should be omitted.

[\-T](https://www.mankier.com/1/tmux#-T) is a format for the menu title (see [Formats](https://www.mankier.com/1/tmux#Formats)).

`-x` and `-y` give the position of the menu. Both may be a row or column number, or one of the following special values:

<table><tbody><tr><td><b>Value</b></td><td><b>Flag</b></td><td><b>Meaning</b></td></tr><tr><td><code>C</code></td><td>Both</td><td>The centre of the terminal</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#R" id="R"><code>R</code></a></td><td><code>-x</code></td><td>The right side of the terminal</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#P" id="P"><code>P</code></a></td><td>Both</td><td>The bottom left of the pane</td></tr><tr><td><code>M</code></td><td>Both</td><td>The mouse position</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#W" id="W"><code>W</code></a></td><td>Both</td><td>The window position on the status line</td></tr><tr><td><code>S</code></td><td><code>-y</code></td><td>The line above or below the status line</td></tr></tbody></table>

Or a format, which is expanded including the following additional variables:

<table><tbody><tr><td><b>Variable name</b></td><td><b>Replaced with</b></td></tr><tr><td><a href="https://www.mankier.com/1/tmux#popup_centre_x" id="popup_centre_x"><code>popup_centre_x</code></a></td><td>Centered in the client</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#popup_centre_y" id="popup_centre_y"><code>popup_centre_y</code></a></td><td>Centered in the client</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#popup_height" id="popup_height"><code>popup_height</code></a></td><td>Height of menu or popup</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#popup_mouse_bottom" id="popup_mouse_bottom"><code>popup_mouse_bottom</code></a></td><td>Bottom of at the mouse</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#popup_mouse_centre_x" id="popup_mouse_centre_x"><code>popup_mouse_centre_x</code></a></td><td>Horizontal centre at the mouse</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#popup_mouse_centre_y" id="popup_mouse_centre_y"><code>popup_mouse_centre_y</code></a></td><td>Vertical centre at the mouse</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#popup_mouse_top" id="popup_mouse_top"><code>popup_mouse_top</code></a></td><td>Top at the mouse</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#popup_mouse_x" id="popup_mouse_x"><code>popup_mouse_x</code></a></td><td>Mouse X position</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#popup_mouse_y" id="popup_mouse_y"><code>popup_mouse_y</code></a></td><td>Mouse Y position</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#popup_pane_bottom" id="popup_pane_bottom"><code>popup_pane_bottom</code></a></td><td>Bottom of the pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#popup_pane_left" id="popup_pane_left"><code>popup_pane_left</code></a></td><td>Left of the pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#popup_pane_right" id="popup_pane_right"><code>popup_pane_right</code></a></td><td>Right of the pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#popup_pane_top" id="popup_pane_top"><code>popup_pane_top</code></a></td><td>Top of the pane</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#popup_status_line_y" id="popup_status_line_y"><code>popup_status_line_y</code></a></td><td>Above or below the status line</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#popup_width" id="popup_width"><code>popup_width</code></a></td><td>Width of menu or popup</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#popup_window_status_line_x" id="popup_window_status_line_x"><code>popup_window_status_line_x</code></a></td><td>At the window position in status line</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#popup_window_status_line_y" id="popup_window_status_line_y"><code>popup_window_status_line_y</code></a></td><td>At the status line showing the window</td></tr></tbody></table>

Each menu consists of items followed by a key shortcut shown in brackets. If the menu is too large to fit on the terminal, it is not displayed. Pressing the key shortcut chooses the corresponding item. If the mouse is enabled and the menu is opened from a mouse key binding, releasing the mouse button with an item selected chooses that item and releasing the mouse button without an item selected closes the menu. `-O` changes this behaviour so that the menu does not close when the mouse button is released without an item selected the menu is not closed and a mouse button must be clicked to choose an item.

The following keys are also available:

<table><tbody><tr><td><b>Key</b></td><td><b>Function</b></td></tr><tr><td><code>Enter</code></td><td>Choose selected item</td></tr><tr><td><code>Up</code></td><td>Select previous item</td></tr><tr><td><code>Down</code></td><td>Select next item</td></tr><tr><td><code>q</code></td><td>Exit menu</td></tr></tbody></table>

display-message \[-aINpv\] \[[\-c](https://www.mankier.com/1/tmux#-c) target-client\] \[-d delay\] \[-t target-pane\] \[message\]

> (alias: `display`)

Display a message. If `-p` is given, the output is printed to stdout, otherwise it is displayed in the target-client status line for up to delay milliseconds. If delay is not given, the `display-time` option is used; a delay of zero waits for a key press. ‘`N`’ ignores key presses and closes only after the delay expires. The format of message is described in the [Formats](https://www.mankier.com/1/tmux#Formats) section; information is taken from target-pane if `-t` is given, otherwise the active pane.

[\-v](https://www.mankier.com/1/tmux#-v) prints verbose logging as the format is parsed and `-a` lists the format variables and their values.

`-I` forwards any input read from stdin to the empty pane given by target-pane.

display-popup \[-BCE\] \[-b border-lines\] \[[\-c](https://www.mankier.com/1/tmux#-c) target-client\] \[-d start-directory\] \[-e environment\] \[-h height\] \[-s style\] \[[\-S](https://www.mankier.com/1/tmux#-S) border-style\] \[-t target-pane\] \[[\-T](https://www.mankier.com/1/tmux#-T) title\] \[-w width\] \[-x position\] \[-y position\] \[shell-command\]

> (alias: `popup`)

Display a popup running shell-command on target-client. A popup is a rectangular box drawn over the top of any panes. Panes are not updated while a popup is present.

`-E` closes the popup automatically when shell-command exits. Two `-E` closes the popup only if shell-command exited with success.

`-x` and `-y` give the position of the popup, they have the same meaning as for the `display-menu` command. `-w` and `-h` give the width and height - both may be a percentage (followed by ‘`%`’). If omitted, half of the terminal size is used.

`-B` does not surround the popup by a border.

`-b` sets the type of border line for the popup. When `-B` is specified, the `-b` option is ignored. See `popup-border-lines` for possible values for border-lines.

`-s` sets the style for the popup and [\-S](https://www.mankier.com/1/tmux#-S) sets the style for the popup border. For how to specify style, see the [Styles](https://www.mankier.com/1/tmux#Styles) section.

`-e` takes the form ‘`VARIABLE=value`’ and sets an environment variable for the popup; it may be specified multiple times.

[\-T](https://www.mankier.com/1/tmux#-T) is a format for the popup title (see [Formats](https://www.mankier.com/1/tmux#Formats)).

The [\-C](https://www.mankier.com/1/tmux#-C) flag closes any popup on the client.

show-prompt-history \[[\-T](https://www.mankier.com/1/tmux#-T) prompt-type\]

> (alias: `showphist`)

Display status prompt history for prompt type prompt-type. If [\-T](https://www.mankier.com/1/tmux#-T) is omitted, then show history for all types. See `command-prompt` for possible values for prompt-type.

[

## Buffers

](https://www.mankier.com/1/tmux#Buffers)

**tmux** maintains a set of named _paste buffers_. Each buffer may be either explicitly or automatically named. Explicitly named buffers are named when created with the `set-buffer` or `load-buffer` commands, or by renaming an automatically named buffer with `set-buffer` `-n`. Automatically named buffers are given a name such as ‘`buffer0001`’, ‘`buffer0002`’ and so on. When the `buffer-limit` option is reached, the oldest automatically named buffer is deleted. Explicitly named buffers are not subject to `buffer-limit` and may be deleted with the `delete-buffer` command.

Buffers may be added using `copy-mode` or the `set-buffer` and `load-buffer` commands, and pasted into a window using the `paste-buffer` command. If a buffer command is used and no buffer is specified, the most recently added automatically named buffer is assumed.

A configurable history buffer is also maintained for each window. By default, up to 2000 lines are kept; this can be altered with the `history-limit` option (see the `set-option` command above).

The buffer commands are as follows:

choose-buffer \[-NZr\] \[-F format\] \[[\-f](https://www.mankier.com/1/tmux#-f) filter\] \[-K key-format\] \[-O sort-order\] \[-t target-pane\] \[template\]

Put a pane into buffer mode, where a buffer may be chosen interactively from a list. Each buffer is shown on one line. A shortcut key is shown on the left in brackets allowing for immediate choice, or the list may be navigated and an item chosen or otherwise manipulated using the keys below. `-Z` zooms the pane. The following keys may be used in buffer mode:

<table><tbody><tr><td><b>Key</b></td><td><b>Function</b></td></tr><tr><td><code>Enter</code></td><td>Paste selected buffer</td></tr><tr><td><code>Up</code></td><td>Select previous buffer</td></tr><tr><td><code>Down</code></td><td>Select next buffer</td></tr><tr><td><code>C-s</code></td><td>Search by name or content</td></tr><tr><td><code>n</code></td><td>Repeat last search</td></tr><tr><td><code>t</code></td><td>Toggle if buffer is tagged</td></tr><tr><td><code>T</code></td><td>Tag no buffers</td></tr><tr><td><code>C-t</code></td><td>Tag all buffers</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#p" id="p"><code>p</code></a></td><td>Paste selected buffer</td></tr><tr><td><code>P</code></td><td>Paste tagged buffers</td></tr><tr><td><code>d</code></td><td>Delete selected buffer</td></tr><tr><td><code>D</code></td><td>Delete tagged buffers</td></tr><tr><td><a href="https://www.mankier.com/1/tmux#e" id="e"><code>e</code></a></td><td>Open the buffer in an editor</td></tr><tr><td><code>f</code></td><td>Enter a format to filter items</td></tr><tr><td><code>O</code></td><td>Change sort field</td></tr><tr><td><code>r</code></td><td>Reverse sort order</td></tr><tr><td><code>v</code></td><td>Toggle preview</td></tr><tr><td><code>q</code></td><td>Exit mode</td></tr></tbody></table>

After a buffer is chosen, ‘`%%`’ is replaced by the buffer name in template and the result executed as a command. If template is not given, "paste-buffer -b '%%'" is used.

`-O` specifies the initial sort field: one of ‘`time`’, ‘`name`’ or ‘`size`’. `-r` reverses the sort order. [\-f](https://www.mankier.com/1/tmux#-f) specifies an initial filter: the filter is a format - if it evaluates to zero, the item in the list is not shown, otherwise it is shown. If a filter would lead to an empty list, it is ignored. `-F` specifies the format for each item in the list and `-K` a format for each shortcut key; both are evaluated once for each line. [\-N](https://www.mankier.com/1/tmux#-N) starts without the preview. This command works only if at least one client is attached.

clear-history \[-t target-pane\]

> (alias: `clearhist`)

Remove and free the history for the specified pane.

delete-buffer \[-b buffer-name\]

> (alias: `deleteb`)

Delete the buffer named buffer-name, or the most recently added automatically named buffer if not specified.

list-buffers \[-F format\] \[[\-f](https://www.mankier.com/1/tmux#-f) filter\]

> (alias: `lsb`)

List the global buffers. `-F` specifies the format of each line and [\-f](https://www.mankier.com/1/tmux#-f) a filter. Only buffers for which the filter is true are shown. See the [Formats](https://www.mankier.com/1/tmux#Formats) section.

load-buffer \[-w\] \[-b buffer-name\] \[-t target-client\] path

> (alias: `loadb`)

Load the contents of the specified paste buffer from path. If `-w` is given, the buffer is also sent to the clipboard for target-client using the [xterm(1)](https://www.mankier.com/1/xterm) escape sequence, if possible.

paste-buffer \[-dpr\] \[-b buffer-name\] \[-s separator\] \[-t target-pane\]

> (alias: `pasteb`)

Insert the contents of a paste buffer into the specified pane. If not specified, paste into the current one. With `-d`, also delete the paste buffer. When output, any linefeed (LF) characters in the paste buffer are replaced with a separator, by default carriage return (CR). A custom separator may be specified using the `-s` flag. The `-r` flag means to do no replacement (equivalent to a separator of LF). If `-p` is specified, paste bracket control codes are inserted around the buffer if the application has requested bracketed paste mode.

save-buffer \[-a\] \[-b buffer-name\] path

> (alias: `saveb`)

Save the contents of the specified paste buffer to path. The `-a` option appends to rather than overwriting the file.

set-buffer \[-aw\] \[-b buffer-name\] \[-t target-client\] \[-n new-buffer-name\] data

> (alias: `setb`)

Set the contents of the specified buffer to data. If `-w` is given, the buffer is also sent to the clipboard for target-client using the [xterm(1)](https://www.mankier.com/1/xterm) escape sequence, if possible. The `-a` option appends to rather than overwriting the buffer. The `-n` option renames the buffer to new-buffer-name.

show-buffer \[-b buffer-name\]

> (alias: `showb`)

Display the contents of the specified buffer.

[

## Miscellaneous

](https://www.mankier.com/1/tmux#Miscellaneous)

Miscellaneous commands are as follows:

clock-mode \[-t target-pane\]

Display a large clock.

if-shell \[-bF\] \[-t target-pane\] shell-command command \[command\]

> (alias: `if`)

Execute the first command if shell-command (run with `/bin/sh`) returns success or the second command otherwise. Before being executed, shell-command is expanded using the rules specified in the [Formats](https://www.mankier.com/1/tmux#Formats) section, including those relevant to target-pane. With `-b`, shell-command is run in the background.

If `-F` is given, shell-command is not executed but considered success if neither empty nor zero (after formats are expanded).

lock-server

> (alias: `lock`)

Lock each client individually by running the command specified by the `lock-command` option.

run-shell \[-bC\] \[-d delay\] \[-t target-pane\] \[shell-command\]

> (alias: `run`)

Execute shell-command using `/bin/sh` or (with [\-C](https://www.mankier.com/1/tmux#-C)) a **tmux** command in the background without creating a window. Before being executed, shell-command is expanded using the rules specified in the [Formats](https://www.mankier.com/1/tmux#Formats) section. With `-b`, the command is run in the background. `-d` waits for delay seconds before starting the command. If [\-C](https://www.mankier.com/1/tmux#-C) is not given, any output to stdout is displayed in view mode (in the pane specified by `-t` or the current pane if omitted) after the command finishes. If the command fails, the exit status is also displayed.

wait-for \[[\-L](https://www.mankier.com/1/tmux#-L) | [\-S](https://www.mankier.com/1/tmux#-S) | -U\] channel

> (alias: `wait`)

When used without options, prevents the client from exiting until woken using `wait-for` [\-S](https://www.mankier.com/1/tmux#-S) with the same channel. When [\-L](https://www.mankier.com/1/tmux#-L) is used, the channel is locked and any clients that try to lock the same channel are made to wait until the channel is unlocked with `wait-for` `-U`.

[

## Exit Messages

](https://www.mankier.com/1/tmux#Exit_Messages)

When a **tmux** client detaches, it prints a message. This may be one of:

detached (from session ...)

The client was detached normally.

detached and SIGHUP

The client was detached and its parent sent the `SIGHUP` signal (for example with `detach-client` `-P`).

lost tty

The client's [tty(4)](https://www.mankier.com/4/tty) or pty(4) was unexpectedly destroyed.

terminated

The client was killed with `SIGTERM`.

too far behind

The client is in control mode and became unable to keep up with the data from **tmux**.

exited

The server exited when it had no sessions.

server exited

The server exited when it received `SIGTERM`.

server exited unexpectedly

The server crashed or otherwise exited without telling the client the reason.

[

## Terminfo Extensions

](https://www.mankier.com/1/tmux#Terminfo_Extensions)

**tmux** understands some unofficial extensions to [terminfo(5)](https://www.mankier.com/5/terminfo). It is not normally necessary to set these manually, instead the `terminal-features` option should be used.

_AX_

An existing extension that tells **tmux** the terminal supports default colours.

_Bidi_

Tell **tmux** that the terminal supports the VTE bidirectional text extensions.

_Cs_, _Cr_

Set the cursor colour. The first takes a single string argument and is used to set the colour; the second takes no arguments and restores the default cursor colour. If set, a sequence such as this may be used to change the cursor colour from inside **tmux**:

> ```
> $ printf '\033]12;red\033\\'
>     
> ```

The colour is an X(7) colour, see [XParseColor(3)](https://www.mankier.com/3/XQueryColor).

_Cmg, Clmg, Dsmg_, _Enmg_

Set, clear, disable or enable DECSLRM margins. These are set automatically if the terminal reports it is _VT420_ compatible.

_Dsbp_, _Enbp_

Disable and enable bracketed paste. These are set automatically if the _XT_ capability is present.

_Dseks_, _Eneks_

Disable and enable extended keys.

_Dsfcs_, _Enfcs_

Disable and enable focus reporting. These are set automatically if the _XT_ capability is present.

_Rect_

Tell **tmux** that the terminal supports rectangle operations.

_Smol_

Enable the overline attribute.

_Smulx_

Set a styled underscore. The single parameter is one of: 0 for no underscore, 1 for normal underscore, 2 for double underscore, 3 for curly underscore, 4 for dotted underscore and 5 for dashed underscore.

_Setulc_, _ol_

Set the underscore colour or reset to the default. The argument is (red \* 65536) + (green \* 256) + blue where each is between 0 and 255.

_Ss_, _Se_

Set or reset the cursor style. If set, a sequence such as this may be used to change the cursor to an underline:

> ```
> $ printf '\033[4 q'
>     
> ```

If _Se_ is not set, Ss with argument 0 will be used to reset the cursor style instead.

_Swd_

Set the opening sequence for the working directory notification. The sequence is terminated using the standard _fsl_ capability.

_Sync_

Start (parameter is 1) or end (parameter is 2) a synchronized update.

_Tc_

Indicate that the terminal supports the ‘`direct colour`’ RGB escape sequence (for example, \\e\[38;2;255;255;255m).

If supported, this is used for the initialize colour escape sequence (which may be enabled by adding the ‘`initc`’ and ‘`ccc`’ capabilities to the **tmux** [terminfo(5)](https://www.mankier.com/5/terminfo) entry).

This is equivalent to the _RGB_ [terminfo(5)](https://www.mankier.com/5/terminfo) capability.

_Ms_

Store the current buffer in the host terminal's selection (clipboard). See the _set-clipboard_ option above and the [xterm(1)](https://www.mankier.com/1/xterm) man page.

_XT_

This is an existing extension capability that tmux uses to mean that the terminal supports the [xterm(1)](https://www.mankier.com/1/xterm) title set sequences and to automatically set some of the capabilities above.

[

## Control Mode

](https://www.mankier.com/1/tmux#Control_Mode)

**tmux** offers a textual interface called _control mode_. This allows applications to communicate with **tmux** using a simple text-only protocol.

In control mode, a client sends **tmux** commands or command sequences terminated by newlines on standard input. Each command will produce one block of output on standard output. An output block consists of a _%begin_ line followed by the output (which may be empty). The output block ends with a _%end_ or _%error_. _%begin_ and matching _%end_ or _%error_ have three arguments: an integer time (as seconds from epoch), command number and flags (currently not used). For example:

> ```
> %begin 1363006971 2 1
> 0: ksh* (1 panes) [80x24] [layout b25f,80x24,0,0,2] @2 (active)
> %end 1363006971 2 1
> 
> ```

The `refresh-client` [\-C](https://www.mankier.com/1/tmux#-C) command may be used to set the size of a client in control mode.

In control mode, **tmux** outputs notifications. A notification will never occur inside an output block.

The following notifications are defined:

%client-detached client

The client has detached.

%client-session-changed client session-id name

The client is now attached to the session with ID session-id, which is named name.

%continue pane-id

The pane has been continued after being paused (if the pause-after flag is set, see `refresh-client` `-A`).

%exit \[reason\]

The **tmux** client is exiting immediately, either because it is not attached to any session or an error occurred. If present, reason describes why the client exited.

%extended-output pane-id age ... : value

New form of `%output` sent when the pause-after flag is set. age is the time in milliseconds for which tmux had buffered the output before it was sent. Any subsequent arguments up until a single ‘`:`’ are for future use and should be ignored.

%layout-change window-id window-layout window-visible-layout window-flags

The layout of a window with ID window-id changed. The new layout is window-layout. The window's visible layout is window-visible-layout and the window flags are window-flags.

%output pane-id value

A window pane produced output. value escapes non-printable characters and backslash as octal \\xxx.

%pane-mode-changed pane-id

The pane with ID pane-id has changed mode.

%pause pane-id

The pane has been paused (if the pause-after flag is set).

%session-changed session-id name

The client is now attached to the session with ID session-id, which is named name.

%session-renamed name

The current session was renamed to name.

%session-window-changed session-id window-id

The session with ID session-id changed its active window to the window with ID window-id.

%sessions-changed

A session was created or destroyed.

%subscription-changed name session-id window-id window-index pane-id ... : value

The value of the format associated with subscription name has changed to value. See `refresh-client` `-B`. Any arguments after pane-id up until a single ‘`:`’ are for future use and should be ignored.

%unlinked-window-add window-id

The window with ID window-id was created but is not linked to the current session.

%unlinked-window-close window-id

The window with ID window-id, which is not linked to the current session, was closed.

%unlinked-window-renamed window-id

The window with ID window-id, which is not linked to the current session, was renamed.

%window-add window-id

The window with ID window-id was linked to the current session.

%window-close window-id

The window with ID window-id closed.

%window-pane-changed window-id pane-id

The active pane in the window with ID window-id changed to the pane with ID pane-id.

%window-renamed window-id name

The window with ID window-id was renamed to name.

[

## Environment

](https://www.mankier.com/1/tmux#Environment)

When **tmux** is started, it inspects the following environment variables:

[EDITOR](https://www.mankier.com/1/tmux#EDITOR)

If the command specified in this variable contains the string ‘`vi`’ and `VISUAL` is unset, use vi-style key bindings. Overridden by the `mode-keys` and `status-keys` options.

[HOME](https://www.mankier.com/1/tmux#HOME)

The user's login directory. If unset, the [passwd(5)](https://www.mankier.com/5/passwd) database is consulted.

[LC\_CTYPE](https://www.mankier.com/1/tmux#LC_CTYPE)

The character encoding [locale(1)](https://www.mankier.com/1/locale). It is used for two separate purposes. For output to the terminal, UTF-8 is used if the [\-u](https://www.mankier.com/1/tmux#-u) option is given or if `LC_CTYPE` contains "UTF-8" or "UTF8". Otherwise, only ASCII characters are written and non-ASCII characters are replaced with underscores (‘`_`’). For input, **tmux** always runs with a UTF-8 locale. If en\_US.UTF-8 is provided by the operating system, it is used and `LC_CTYPE` is ignored for input. Otherwise, `LC_CTYPE` tells **tmux** what the UTF-8 locale is called on the current system. If the locale specified by `LC_CTYPE` is not available or is not a UTF-8 locale, **tmux** exits with an error message.

[LC\_TIME](https://www.mankier.com/1/tmux#LC_TIME)

The date and time format [locale(1)](https://www.mankier.com/1/locale). It is used for locale-dependent [strftime(3)](https://www.mankier.com/3/strftime) format specifiers.

[PWD](https://www.mankier.com/1/tmux#PWD)

The current working directory to be set in the global environment. This may be useful if it contains symbolic links. If the value of the variable does not match the current working directory, the variable is ignored and the result of [getcwd(3)](https://www.mankier.com/3/getcwd) is used instead.

[SHELL](https://www.mankier.com/1/tmux#SHELL)

The absolute path to the default shell for new windows. See the `default-shell` option for details.

[TMUX\_TMPDIR](https://www.mankier.com/1/tmux#TMUX_TMPDIR)

The parent directory of the directory containing the server sockets. See the [\-L](https://www.mankier.com/1/tmux#-L) option for details.

[VISUAL](https://www.mankier.com/1/tmux#VISUAL)

If the command specified in this variable contains the string ‘`vi`’, use vi-style key bindings. Overridden by the `mode-keys` and `status-keys` options.

[

## Files

](https://www.mankier.com/1/tmux#Files)

~/.tmux.conf

$XDG\_CONFIG\_HOME/tmux/tmux.conf

~/.config/tmux/tmux.conf

Default **tmux** configuration file.

/etc/tmux.conf

System-wide configuration file.

[

## Examples

](https://www.mankier.com/1/tmux#Examples)

To create a new **tmux** session running [vi(1)](https://www.mankier.com/1/vim):

> `$ tmux new-session vi`

Most commands have a shorter form, known as an alias. For new-session, this is `new`:

> `$ tmux new vi`

Alternatively, the shortest unambiguous form of a command is accepted. If there are several options, they are listed:

> ```
> $ tmux n
> ambiguous command: n, could be: new-session, new-window, next-window
> 
> ```

Within an active session, a new window may be created by typing ‘`C-b c`’ (Ctrl followed by the ‘`b`’ key followed by the ‘`c`’ key).

Windows may be navigated with: ‘`C-b 0`’ (to select window 0), ‘`C-b 1`’ (to select window 1), and so on; ‘`C-b n`’ to select the next window; and ‘`C-b p`’ to select the previous window.

A session may be detached using ‘`C-b d`’ (or by an external event such as [ssh(1)](https://www.mankier.com/1/ssh) disconnection) and reattached with:

> `$ tmux attach-session`

Typing ‘`C-b ?`’ lists the current key bindings in the current window; up and down may be used to navigate the list or ‘`q`’ to exit from it.

Commands to be run when the **tmux** server is started may be placed in the `~/.tmux.conf` configuration file. Common examples include:

Changing the default prefix key:

> ```
> set-option -g prefix C-a
> unbind-key C-b
> bind-key C-a send-prefix
> 
> ```

Turning the status line off, or changing its colour:

> ```
> set-option -g status off
> set-option -g status-style bg=blue
> 
> ```

Setting other options, such as the default command, or locking after 30 minutes of inactivity:

> ```
> set-option -g default-command "exec /bin/ksh"
> set-option -g lock-after-time 1800
> 
> ```

Creating new key bindings:

> ```
> bind-key b set-option status
> bind-key / command-prompt "split-window 'exec man %%'"
> bind-key S command-prompt "new-window -n %1 'ssh %1'"
> 
> ```

[

## See Also

](https://www.mankier.com/1/tmux#See_Also)

pty(4)

[

## Referenced By

](https://www.mankier.com/1/tmux#Referenced_By)

[abduco(1)](https://www.mankier.com/1/abduco), [byobu(1)](https://www.mankier.com/1/byobu), [byobu-keybindings(1)](https://www.mankier.com/1/byobu-keybindings), [byobu-layout(1)](https://www.mankier.com/1/byobu-layout), [byobu-select-backend(1)](https://www.mankier.com/1/byobu-select-backend), [byobu-tmux(1)](https://www.mankier.com/1/byobu-tmux), [logind.conf(5)](https://www.mankier.com/5/logind.conf), [pty(7)](https://www.mankier.com/7/pty), [termy-server(1)](https://www.mankier.com/1/termy-server), [tq(1)](https://www.mankier.com/1/tq), [user\_caps(5)](https://www.mankier.com/5/user_caps), [xpanes(1)](https://www.mankier.com/1/xpanes).

The man page tmate(1) is an alias of tmux(1).

December 11, 2022
