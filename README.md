---
libcommon
---

libcommon is a set of miscellaneous utility routines, shared by 
multiple projects. The source code contains functions for profiling,
error reporting, system introspection and a commodity interface to 
sqlite3.

---
update for this version:
---

GCC 11 and later added ``-Wmismatched-dealloc`` to detect when you free a pointer using a function that doesn’t match how it was allocated.

In ``src/system_introspection.cpp``, each ``popen`` should be paired with ``pclose``. We fix this bug.

Another bug is very hidden and happens much more rarely: it happens only in POSIX systems without GNU tools. The bug occurs at the regular expression ``make -n -p | awk '/^srcdir\\s*:?=/ {print $NF}'`` in function ``git_get_srcdir_from_makefile`` in ``src/system_introspection.cpp``. The ``\s*`` does not work in POSIX BRE (Basic Regular Expressions). We change it to ``[[:space:]]*`` which works in both BRE and ERE (Extended Regular Expressions).