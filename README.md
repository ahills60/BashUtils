# BashUtils
BashUtils provides useful scripts for the Bourne Again Shell (BASH) including basic job queuing. BASH is supported by a various operating systems and is the default shell for Ubuntu and Mac OS X amongst other operating systems.

## Libraries
BashUtils currently consists of two libraries:

* `Iceberg Rewrites` for scripts related to the University of Sheffield's [HPC service](http://www.sheffield.ac.uk/wrgrid/).
* `QUtils` which provides rudimentary job queue management.

### Iceberg Rewrites
Two scripts within `Iceberg Rewrites` enable the submission of Python scripts to the [SGE](http://en.wikipedia.org/wiki/Oracle_Grid_Engine) on Iceberg:

* `pythonjob` runs a set of Python instructions and can take screen output if requested. This command is used by `qpy`.
* `qpy` submits Python jobs to the SGE in an interactive fashion. This avoids having to write ``qsub`` commands yourself.

The Python scripts require Python to be installed and available within the ``PATH``. The scripts should be placed in ``~/bin/pythonjob``.

A third file ``runmat`` is a replacement of the ``runmatlab`` script on iceberg. The script ``runmat`` provides additional functionality such as support for project names and email notification. This script may now be obsolete as the Iceberg admins have rewritten a few of their submission scripts.

### QUtils
QUtils provides basis queue functionality on systems that support BASH. Several files are included:

* `queueman` is the main script that acts as a queue manager. This script looks for new job files, parses the script file for notification information and sends email on job start and/or completion.
* `createjob` provides an interactive method for creating job scripts. The script can quickly accept and process MATLAB files but can accept other script files.
* `submitjob` submits a job script file created by `createjob` to the queue for processing.
* `qlist` displays the outstanding queue items and the item in the queue that currently being processed.
* `matlabjob` is a shortcut method for running MATLAB scripts in a non-interactive, non-graphical environment and optionally outputting stdout to a file. 
* `endqueue` allows the owner of the queue manager to stop the queue process.
* `qhelp` writes basic help information to the screen.

In addition to the above, the script files need to be accessible to all users that will be using QUtils (i.e. add the location of these files to the `PATH` and adjust permissions to executable). Additionally, job files will need to be stored in a location that's accessible to everyone and this should should be stored in a variable `QUEUEPATH`. The these variables can be defined in the `~/.bashrc` file using:

```bash
# Define QUEUEPATH:
export QUEUEPATH="/home/Queue/Queue/"
# Add QUtils to path:
export PATH="$PATH:/home/Queue/QUtils"
```

The variable updates need defining for all users who are to use QUtils. If all users are to use QUtils, then making changes to the global `bashrc` file (located in `/etc/`) is recommended. 

QUtils can be initiated through a Terminal window (or SSH session). I recommend using `screen` to keep the queue running in the background without having to keep Terminal windows (or SSH sessions) open. To start the queue manager, run ``queueman``.

Emailing is performed with the [sendEmail](http://caspian.dotconf.net/menu/Software/SendEmail/) program available for Linux and Windows.

*Note: A rather (unnecessarily) lengthy version of the development of this can be found on [my blog](http://andrew-hills.blogspot.co.uk/2008/02/simple-bash-based-queue-system.html). Writing styles change in time and so I may get around to rewriting the post in the future.*