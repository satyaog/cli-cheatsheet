.. Command Line Cheat Sheet documentation mVaster file, created by
   sphinx-quickstart on Wed Oct  9 15:43:28 2019.  You can adapt this file
   completely to your liking, but it should at least contain the root `toctree`
   directive.

########################
Command Line Cheat Sheet
########################

\

.. list-table::
   :header-rows: 1
   :stub-columns: 1
   :widths: auto

   * - `Browsing`_
     - `Access Rights`_
     - `Help`_
     - `Disk Usage`_
     - `Session Utilities`_
     - `Network Utilities`_
     - `Archiving`_
     - `Executable`_
   * - | `ls`_
       | `cd`_
       | `cp`_
       | `mv`_
       | `Tab Key`_
       | `less`_
     - | `chmod`_
       | `setfacl`_
     - | `man`_
       | `-h | --help`_
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
     - | `tar`_
     - | `chmod (execute bit)`_
       | `Execute Script`_

********
Browsing
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

``cp``
======

:``cp SRC DEST``:       Copy a file or directory.
:``cp -Rt DIR SRC...``: Copy files and/or directories to a directory.

``mv``
======

:``mv SRC DEST``:      Move or rename a file or directory.
:``mv -t DIR SRC...``: Move files and/or directories to a directory. 

Tab Key
=======

:Tab key: Auto-complete the text

.. code-block:: bash

    $ cd p[tab]
    proj1/ proj2/
    $ cd proj

``less``
========

:``less -r FILE``:    Visualize text in a pager rather than print it in the
                      console. Use `q` to quit.
:``less -r +F FILE``: Scroll forward the text of a log file and keep trying to
                      read to update the pager as new content gets written into
                      the file. Use `Ctrl+C`_ to interrupt the *following* and
                      scroll back.

.. code-block:: bash

    $ (for i in {1..10}; do (echo $i >> log_file.out; sleep 2) ; done) &
    $ less -r +F log_file.out
    [...]
    ~
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    Waiting for data... (interrupt to abort)

*************
Access Rights
*************

``chmod``
=========

:``chmod MODE[,MODE] FILE``: Set the file mode bits

``MODE`` format
---------------

The format of ``MODE`` is ``{ugo}{+-}perms[,...]``, where ``perms`` is one or
more letters from the set ``rwxX``

:``u``:  set user mode bits
:``g``:  set group mode bits
:``o``:  set other mode bits
:``+-``: add/remove mode bits
:``r``:  read bit
:``w``:  write bit
:``x``:  execute bit
:``X``:  execute bit if already set or if the target is a directory

``setfacl``
===========

:``setfacl {--set[-file]|--modify[-file]} MODE {DIR|FILE}``:

    Set (purge previous acl permissions) or modify file access control lists.
    ``--set[-file]`` requires permissions of user, group and other to be listed.

``MODE`` format
---------------

The format of ``MODE`` is ``u::perms,g::perms,o::perms[,...]``, where ``perms``
is one or more letters from the set ``rwxX``

``[u:]uid:perms``
    Set user mode bits where ``perms`` is one or more letters from the set
    ``rwxX``

``[g:]gid:perms``
    Set group mode bits where ``perms`` is one or more letters from the set
    ``rwxX``

``o:perms``
    Set other mode bits where ``perms`` is one or more letters from the set
    ``rwxX``

:``r``: read bit
:``w``: write bit
:``x``: execute bit
:``X``: execute bit if already set or if the target is a directory

.. code-block:: bash

    $ setfacl --set u::rwx,g::-,o::-,g:groupid:rwx dir/
    $ getfacl dir/
    # file: dir/
    # owner: ownerid
    # group: groupid
    user::rwx
    group::---
    group:groupid:rwx
    mask::rwx
    other::---

****
Help
****

``man``
=======

Open the help manual (man page) of a command. Not all commands have a man page
entry.

:``man COMMAND``: 
    Open the help manual (man page) of a command.
    
    `The manual will be shown in a pager.`

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

:``command (-h|--help)``:        | Display help for a command.
                                 | `Commands might have either or both options
                                    (` ``-h`` `,` ``--help`` `).`
:``command (-h|--help) | less``: Useful to scroll text in a pager rather than
                                 print it in the console

.. code-block:: bash

    $ ls --help
    Usage: ls [OPTION]... [FILE]...
    List information about the FILEs (the current directory by default).
    Sort entries alphabetically if none of -cftuvSUX nor --sort is specified.

    Mandatory arguments to long options are mandatory for short options too.
      -a, --all                  do not ignore entries starting with .
    [...]
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

:``nohup COMMAND &``: Run a command that will NOt HangUP when the terminal
                      closes

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

:``rsync -arLv SRC [SRC ...] DEST``: Recursively copy from source to
destination, locally or remotely

Additional Options
------------------

--partial            Keep partially transferred files
--relative
   Copy "implied directories" as well as the last part of ``SRC``. Ex.:
   **foo/bar/** in:
   
   ``rsync -arLv --relative /foo/bar/baz.c ...``

   Inserting a **./** in a ``SRC`` path will limit the amount of path
   information that is sent as implied directories. Ex.: **bar/** in:
   
   ``rsync -arLv --relative /foo/./bar/baz.c ...``
--bwlimit=RATE
   Specify the maximum transfer rate for the data sent over the *socket*,
   specified in units per second. Ex.: 10 megabytes/sec bandwidth:

   ``rsync -arLv --bwlimit=10mb REMOTE:/foo/ foo/``
   
   ``rsync -arLv --bwlimit=10mb foo/ REMOTE:/foo/``
-e <"ssh -p PORT">
   Use a non-standard SSH port

*********
Archiving
*********

``tar``
=======

:``tar -cvf TAR_NAME.tar DIR...``:     Create a .tar archive with the content of
                                       directories
:``tar -czvf TAR_NAME.tar.gz DIR...``: Create a .tar archive and compress it
                                       using gzip
:``tar -xf TAR_NAME.tar -C DIR``:      Extract a .tar archive into a directory
:``tar -xzf TAR_NAME.tar.gz -C DIR``:  Extract a .tar archive compressed with
                                       gzip into a directory

Additional Options
------------------
  
-r             Append files to the .tar archive. This replaces ``-c``.
--sort=name    Sort the directory entries on name.

**********
Executable
**********

``chmod`` (execute bit)
============================

:``chmod +x script.sh``: Add the execute mode bit to a script file so it can be
                         executed

Execute Script
==============

:``./script.sh``: Execute a script
