# Installation
This library will be installed as a dependency by other PNU utilities.

# LIBPNU(3)

## NAME
libpnu — Common utility functions for the PNU project

## SYNOPSIS
import **libpnu**

*libpnu*.**initialize_debugging**(String *program_name*)

*libpnu*.**handle_interrupt_signals**(Function *handler_function*)

String *libpnu*.**get_home_directory**()

String *libpnu*.**get_caching_directory**(String *name*)

List *libpnu*.**locate_directory**(String *directory*)

List *libpnu*.**load_strings_from_file**(String *filename*)

## DESCRIPTION
The **initialize_debugging()** function sets up the Python logging module with a syslog style kind of console log using *program_name* as the program name.
By default, the logging level is set at WARNING or more, but can be lowered by calling **logging.disable()**,
for example with the *logging.NOTSET* parameter to get DEBUG or more logging level.

The **handle_interrupt_signals()** function calls the specified *handler_function* to process the SIGINT and SIGPIPE signals,
usually to avoid an ugly trace dump to the console in case of interrupt (Control-C pressed or broken pipe).

The **get_home_directory()** function returns the location of the user's home directory in a string
depending on the operating system used (Unix, Windows).

The **get_caching_directory()** function returns the location of a user writable directory for caching files in a string
depending on the operating system used (Unix, Windows).
The provided *name* will be the last directory part of this location.

The **locate_directory()** function searches the specified *directory* in a variety of possible other directories,
depending on the operating system used (Unix, Windows) and the fact that a package can be user or system installed.
It is intended to be used when the directory can't be directly found, and returns a list of paths where the directory searched has been found.

For example, if the argument is "/usr/local/etc/man.d", we'll search for "usr/local/etc/man.d", "local/etc/man.d", "etc/man.d" (more likely) and "man.d"
in a list of user's local Python package directories
("$HOME/.local" on Unix, "$APPDATA/python", "$HOMEPATH/appdata/roaming/python", "$USERPROFILE/appdata/roaming/python" on Windows)
and system wide Python package base directories (given by *sys.base_prefix*: "/usr/local" on Unix, "C:/Program Files/Python3x" on Windows).

The **load_strings_from_file()** function returns a list of strings from the given *filename*,
filtering out blank or commented lines, as well as end-of-line comments (with '#' being the comment character).

## ENVIRONMENT
The following environment variables can be used to identify the user identity and home directory,
or find a caching directory.

On Unix: *HOME*, *LNAME*, *LOGNAME*, *TMP*, *TMPDIR*, *USER* and *USERNAME*.

On Windows: *APPDATA*, *HOME*, *HOMEPATH*, *LOCALAPPDATA*, *TMP* and *USERPROFILE*.

## STANDARDS
The **libpnu** library is not a standard UNIX one.

It tries to follow the [PEP 8](https://www.python.org/dev/peps/pep-0008/) style guide for [Python](https://www.python.org/) code.

## PORTABILITY
Tested OK under Windows.

## HISTORY
This library was made for the [PNU project](https://github.com/HubTou/PNU).

## LICENSE
It is available under the [3-clause BSD license](https://opensource.org/licenses/BSD-3-Clause).

## AUTHORS
[Hubert Tournier](https://github.com/HubTou)

