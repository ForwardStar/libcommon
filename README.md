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