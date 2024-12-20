
## make-install

_make-install_ is a script that reads a file layout and generates shell
code to install and uninstall files.

    make-install <base> [<layout>]

where

 - **base** is the base directory under which the files should be
   installed (usually _/usr_ or _/usr/local_), and

 - **layout** is the layout file describing which file goes into which
   directory.  _files.list_ is used if this parameter is missing.

An example layout file is

    +lib/make-install:
        README.md
        make-install
        +uninstall

Directory names are unindented and a colon `:` may be appended.  The
leading `+` tells _make-install_ to create the directory.  Otherwise,
the directory would be tested for existence.  With

    $ make-install /usr

_README.md_ and _make-install_ would be installed in
_/usr/lib/make-install_.

The leading `+` in `+uninstall` determines _uninstall_ as the
uninstallation script.  Is it created from the installation commands
and removes files and directories if executed.

_make-install_'s output is shell code to install the files and must be
executed by piping it to _sh_, e.g.

    $ ./make-install /usr | sudo sh

after verifying that the script does what is intended.


### Installation

_make-install_ is not meant to be installed to create installation
script.  Instead it should be distributed with the released files to
allow the end user to create his own installation code (and decide
where the files should go).

