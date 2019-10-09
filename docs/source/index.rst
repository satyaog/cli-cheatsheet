.. Command Line Cheat Sheet documentation master file, created by
   sphinx-quickstart on Wed Oct  9 15:43:28 2019.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Command Line Cheat Sheet
########################

\

.. list-table::
   :header-rows: 1

   * - `Navigate`_
     - `Help`_
     - `Disk Usage`_
     - `Session Utilities`_
     - `Executable`_
   * - | `ls`_
       | `cd`_
       | `Tab Key`_
     - | `man`_
       | `-h | \\-\\-help`_
       | `less`_
     - | `du`_
     - | `tmux`_
       | `nohup`_
       | `Ctrl+C`_
       | `Ctrl+Z`_
       | `jobs`_
       | `fg`_
       | `bg`_
       | `kill`_
     - | `chmod`_
       | `Execute Script`_

Navigate
********

ls
==

:``ls [-lh] [DIR]``: List file and directories

.. code-block:: bash

    $ ls
    file1	file2	proj1	proj2

    $ ls -lh
    -rw-r--r--  1 user   group     0B  4 oct 14:11 file1
    -rw-r--r--  1 user   group     0B  4 oct 14:11 file2
    drwxr-xr-x  2 user   group    64B  4 oct 14:11 proj1
    drwxr-xr-x  2 user   group    64B  4 oct 14:11 proj2

    $ ls -lh proj1
    -rw-r--r--  1 user   group     0B  4 oct 14:14 proj1_file1
    -rw-r--r--  1 user   group     0B  4 oct 14:14 proj1_file2

cd
==

:``cd DIR``: Change current location to a directory

.. code-block:: bash

    $ ls
    file1	file2	proj1	proj2
    $ cd proj1
    $ ls
    proj1_file1	proj1_file2

Tab Key
=======

:Tab key: Auto-complete the text

.. code-block:: bash

    $ cd p[tab]
    proj1/ proj2/
    $ cd proj

Help
****

man
===

:``man [command]``: Open the help manual (man page) of a command. The manual will
                    be shown in a pager. Not all commands have a man page entry.

.. code-block:: bash

    $ `man ls
    LS(1)                     BSD General Commands Manual                    LS(1)

    NAME
         ls -- list directory contents

    SYNOPSIS
         ls [-ABCFGHLOPRSTUW@abcdefghiklmnopqrstuwx1] [file ...]

    DESCRIPTION
         For each operand that names a file of a type other than directory, ls displays its name as well as any requested, associated informa-
         tion.  For each operand that names a file of type directory, ls displays the names of files contained within that directory, as well
         as any requested, associated information.
    [...]

-h | \\-\\-help
===============

:``command [-h|--help]``: Display help for a command. Commands might have either
                          or both options (`-h`, `--help`). The information will
                          be printed in the console.

.. code-block:: bash

    $ ls --help
    Usage: ls [OPTION]... [FILE]...
    List information about the FILEs (the current directory by default).
    Sort entries alphabetically if none of -cftuvSUX nor --sort is specified.

    Mandatory arguments to long options are mandatory for short options too.
      -a, --all                  do not ignore entries starting with .
    [...]

less
====

:``less``: Useful to scroll text in a pager rather than print it in the console

.. code-block:: bash

    $ ls --help | less
    Usage: ls [OPTION]... [FILE]...
    List information about the FILEs (the current directory by default).
    Sort entries alphabetically if none of -cftuvSUX nor --sort is specified.

    Mandatory arguments to long options are mandatory for short options too.
      -a, --all                  do not ignore entries starting with .
    [...]

Disk Usage
**********

du
==

:``du -sh DIR``: Print the disk usage of a directory

.. code-block:: bash

    $ du -sh proj1
    1.5K	proj1

Session Utilities
*****************

tmux
====
:``tmux``: Enables a number of terminals to be created, accessed, and controlled
           from a single screen.
:``tmux``: Open a new window
:``tmux attach``: Attach to the last detached window
:``tmux attach [index]``: Attach to a detached terminal

* Inside a tmux terminal:

  :Ctrl+b+%: Opens a new panel
  :Ctrl+b+Left, Right: Change to the left or right panel
  :Ctrl+b+x: Closes the current panel
  :Ctrl+b+d: Detach the current window

nohup
=====

:``nohup command &``: Run a command that will NOt HangUP when the terminal closes

Ctrl+C
======

:``Ctrl+C``: Interrupt the current command

Ctrl+Z
======

:``Ctrl+Z``: Stop (pause) and background the current command

jobs
====

:``jobs``: List the background jobs

.. code-block:: bash

    $ jobs
    [1]-  Stopped                 command1
    [2]+  Stopped                 command2

fg
==

:``fg``: Resume the job that's next in the queue

bg
==

:``bg``: Push the next job in the queue into the background

kill
====

:``kill [%1|pid]``: Kill a job or a process using the job index or the process id
                    respectively

.. code-block:: bash

    $ kill %1
    [1]+  Stopped                 command1

Executable
**********

chmod
=====

:``chmod +x script.sh``: Add the executable permission flag to a script file so it
                         can be executed

Execute Script
==============

:``./script.sh``: Execute a script
