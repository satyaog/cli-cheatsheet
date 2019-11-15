.. Command Line Cheat Sheet documentation master file, created by
   sphinx-quickstart on Wed Oct  9 15:43:28 2019.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

########################
Command Line Cheat Sheet
########################

\

.. list-table::
   :header-rows: 1

   * - `Navigate`_
     - `Help`_
     - `Disk Usage`_
     - `Session Utilities`_
     - `Network Utilities`_
     - `Executable`_
   * - | `ls`_
       | `cd`_
       | `Tab Key`_
     - | `man`_
       | `-h | --help`_
       | `less`_
     - | `du`_
     - | `tmux`_
       | `nohup`_
       | `Ctrl+C`_
       | `Ctrl+Z`_
       | `jobs`_
       | `fg`_
       | `bg`_
       | `ps`_
       | `kill`_
     - | `rsync`_
     - | `chmod`_
       | `Execute Script`_

********
Navigate
********

``ls``
======

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

``cd``
======

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

****
Help
****

``man``
=======

Open the help manual (man page) of a command. Not all commands have a man page
entry.

:``man COMMAND``: | Open the help manual (man page) of a command.
                  | `The manual will be shown in a pager.`

.. code-block:: bash

    $ `man ls
    LS(1)                     BSD General Commands Manual                    LS(1)

    NAME
         ls -- list directory contents

    SYNOPSIS
         ls [-ABCFGHLOPRSTUW@abcdefghiklmnopqrstuwx1] [file ...]

    DESCRIPTION
         For each operand that names a file of a type other than directory, ls displays its name as
         well as any requested, associated information.  For each operand that names a file of type
         directory, ls displays the names of files contained within that directory, as well as any
         requested, associated information.
    [...]

``-h`` | ``--help``
===================

Display help for a command. The information will be printed in the console.

:``command -h|--help``: | Display help for a command.
                        | `Commands might have either or both options
                           (` ``-h`` `,` ``--help`` `).`

.. code-block:: bash

    $ ls --help
    Usage: ls [OPTION]... [FILE]...
    List information about the FILEs (the current directory by default).
    Sort entries alphabetically if none of -cftuvSUX nor --sort is specified.

    Mandatory arguments to long options are mandatory for short options too.
      -a, --all                  do not ignore entries starting with .
    [...]

``less``
========

:``less``: Useful to scroll text in a pager rather than print it in the console

.. code-block:: bash

    $ ls --help | less
    Usage: ls [OPTION]... [FILE]...
    List information about the FILEs (the current directory by default).
    Sort entries alphabetically if none of -cftuvSUX nor --sort is specified.

    Mandatory arguments to long options are mandatory for short options too.
      -a, --all                  do not ignore entries starting with .
    [...]

**********
Disk Usage
**********

``du``
======

:``du -sh [DIR]``: Print the disk usage of a directory

.. code-block:: bash

    $ du -sh proj1
    1.5K	proj1

*****************
Session Utilities
*****************

``tmux``
========

Enables a number of terminals to be created, accessed, and controlled from a
single screen.

:``tmux``:           Open a new window
:``tmux ls|list``:   List sessions
:``tmux attach``:    Attach to the last detached window
:``tmux attach -t SESSION_INDEX``: Attach to a detached session

Inside a tmux terminal
----------------------

Sessions
^^^^^^^^

:<Ctrl+b>+s: List sessions
:<Ctrl+b>+$: Rename current session

Windows
^^^^^^^

:<Ctrl+b>+w: List all windows
:<Ctrl+b>+c: Create a new window
:<Ctrl+b>+d: Detach the current window
:<Ctrl+b>+,: Rename current window

Panes
^^^^^

:<Ctrl+b>+%: Opens a new pane
:<Ctrl+b>+Left, Right: Change to the left or right pane
:<Ctrl+b>+x: Closes the current pane

``nohup``
=========

:``nohup COMMAND &``: Run a command that will NOt HangUP when the terminal closes

Ctrl+C
======

:``Ctrl+C``: Interrupt the current command

Ctrl+Z
======

:``Ctrl+Z``: Stop (pause) and background the current command

``jobs``
========

:``jobs``: List the background jobs

.. code-block:: bash

    $ jobs
    [1]-  Stopped                 command1
    [2]+  Stopped                 command2

``fg``
======

:``fg``: Resume the job that's next in the queue

``bg``
======

:``bg``: Push the next job in the queue into the background

``ps``
======

:``ps -fju $USER --forest``: Display the user's process tree

.. code-block:: bash

    UID        PID  PPID  PGID   SID  C STIME TTY          TIME CMD
    user     26468 25983 25983 25983  0 10:20 ?        00:00:00 sshd: user@pts/0
    user     26591 26468 26591 26591  0 10:20 pts/0    00:00:00  \_ -bash
    user     32650 26591 32650 26591  0 10:44 pts/0    00:00:00      \_ ps -fju user --forest

``kill``
========

:``kill %JOB_INDEX``: Kill a job using the job's index
:``kill PID``: Kill a process using the process's id
:``kill -- -PGID``: Kill all process belonging to the process group id

.. code-block:: bash

    $ kill %1
    [1]+  Stopped                 command1

*****************
Network Utilities
*****************

``rsync``
=========

:``rsync -arv SRC DEST``: Recursively copy from source to destination, locally or remotely

Additional Options
------------------

--partial            Keep partially transferred files
-e <"ssh -p PORT">   Use a non-standard SSH port

**********
Executable
**********

``chmod``
=========

:``chmod +x script.sh``: Add the executable permission flag to a script file so
                         it can be executed

Execute Script
==============

:``./script.sh``: Execute a script
