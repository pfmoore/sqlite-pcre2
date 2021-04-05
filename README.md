# A REGEXP library for sqlite3

This is a loadable extension for sqlite3 that provides a REGEXP implementation
based on the pcre2 library.

It is based on sources taken from https://github.com/ralight/sqlite3-pcre,
which were in turn originally based on code by Alexey Tourbin. The
README file from the original project is reproduced below.

Unlike the original, this code uses the newer PCRE2 library as its regular
expression engine. I have also replaced the original build scripts with a
CMake based build, to improve portability between different systems and
tool chains.

The build statically links PCRE2, so that the resulting DLL is self-contained.
I may add an option to link to a system-provided PCRE2 library, but as my
main platform is Windows, where system-provided libraries other than the OS
components are rarely seen, this is not a high priority for me.

## Original readme

This is sqlite3-pcre, an extension for sqlite3 that uses libpcre to provide
the REGEXP() function.

The code was written by Alexey Tourbin and can be found at:

http://git.altlinux.org/people/at/packages/?p=sqlite3-pcre.git

