---
description: "Learn more about: Directory Control"
title: "Directory Control"
ms.date: "11/04/2016"
helpviewer_keywords: ["controls [C++], directory", "directory control routines"]
ms.assetid: a72dcf6f-f366-4d20-8850-0e19cc53ca18
---
# Directory control

These routines access, modify, and obtain information about the directory structure.

## Directory-control routines

|Routine|Use|
|-------------|---------|
|[`_chdir`, `_wchdir`](./reference/chdir-wchdir.md)|Change current working directory|
|[`_chdrive`](./reference/chdrive.md)|Change current drive|
|[`_getcwd`, `_wgetcwd`](./reference/getcwd-wgetcwd.md)|Get current working directory for default drive|
|[`_getdcwd`, `_wgetdcwd`](./reference/getdcwd-wgetdcwd.md)|Get current working directory for specified drive|
|[`_getdiskfree`](./reference/getdiskfree.md)|Populates a **_diskfree_t** structure with information about a disk drive.|
|[`_getdrive`](./reference/getdrive.md)|Get current (default) drive|
|[`_getdrives`](./reference/getdrives.md)|Returns a bitmask representing the currently available disk drives.|
|[`_mkdir`, `_wmkdir`](./reference/mkdir-wmkdir.md)|Make new directory|
|[`_rmdir`, `_wrmdir`](./reference/rmdir-wrmdir.md)|Remove directory|
|[`_searchenv`, `_wsearchenv`](./reference/searchenv-wsearchenv.md), [`_searchenv_s`, `_wsearchenv_s`](./reference/searchenv-s-wsearchenv-s.md)|Search for given file on specified paths|

## See also

[Universal C runtime routines by category](./run-time-routines-by-category.md)\
[File handling](./file-handling.md)\
[System calls](./system-calls.md)
