---
title: "linux c access函数"
date: 2022-02-25T09:57:09+08:00
description:
# weight: 1
# aliases: ["/first"]
draft: false
author: "嘟囔"
# author: ["Me", "You"] # multiple authors
tags: ["c", "access"]
categories: ["C"]
---

英文部分搬运自《Linux Programmer's Manual》

# NAME
       access - check real user's permissions for a file

# SYNOPSIS(简介、概要)

       #include <unistd.h>

       int access(const char *pathname, int mode);

# DESCRIPTION

       access()  checks  whether the calling process can access the file pathname.  If pathname is a
       symbolic link, it is dereferenced(解出引用).

       The mode specifies the accessibility check(s) to be performed, and is either the value  F_OK,
       or  a  mask  consisting of the bitwise OR of one or more of R_OK, W_OK, and X_OK.  F_OK tests
       for the existence of the file.  R_OK, W_OK, and X_OK test whether the file exists and  grants
       read, write, and execute permissions, respectively.

       The check is done using the calling process's real UID and GID, rather than the effective IDs
       as is done when actually attempting an operation (e.g., open(2)) on the  file.   This  allows
       set-user-ID programs to easily determine the invoking user's authority.

       If the calling process is privileged (i.e., its real UID is zero), then an X_OK check is suc‐
       cessful for a regular file if execute permission is enabled for any of the file owner, group,
       or other.

mode参数：  
F_OK        判断文件或目录是否存在
R_OK        已存在的文件或目录是否可读
W_OK        已存在的文件或目录是否可写
X_OK        已存在的文件或目录是否可执行

# RETURN VALUE

       On  success (all requested permissions granted, or mode is F_OK and the file exists), zero is
       returned.  On error (at least one bit in mode asked for a permission that is denied, or  mode
       is F_OK and the file does not exist, or some other error occurred), -1 is returned, and errno
       is set appropriately.

返回值成功返回0，失败返回-1，并设置errno

# ERRORS

       access() shall fail if:

       EACCES The requested access would be denied to the file, or search permission is  denied  for
              one of the directories in the path prefix of pathname.  (See also path_resolution(7).)
              权限不足

       ELOOP  Too many symbolic links were encountered in resolving pathname.
              解析路径遇到了太多的符号链接

       ENAMETOOLONG
              pathname is too long.
              路径太长

       ENOENT A component of pathname does not exist or is a dangling symbolic link.
              路径名的组件不存在或为悬空符号链接  

       ENOTDIR
              A component used as a directory in pathname is not, in fact, a directory.
              在pathname中作为目录使用的组件实际上不是一个目录。

       EROFS  Write permission was requested for a file on a read-only file system.
              只读文件系统上请求文件写权限。

       access() may fail if:
       
       EFAULT pathname points outside your accessible address space.
              越界

       EINVAL mode was incorrectly specified.

       EIO    An I/O error occurred.

       ENOMEM Insufficient kernel memory was available.
              内核内存不足

       ETXTBSY
              Write access was requested to an executable which is being executed.
              请求对正在执行的可执行文件进行写访问

# CONFORMING TO

       SVr4, 4.3BSD, POSIX.1-2001.

# NOTES

       Warning:  Using access() to check if a user is authorized to, for example, open a file before
       actually doing so using open(2) creates a security hole, because the user might  exploit  the
       short time interval between checking and opening the file to manipulate it.  For this reason,
       the use of this system call should be avoided.  (In  the  example  just  described,  a  safer
       alternative would be to temporarily switch the process's effective user ID to the real ID and
       then call open(2).)

       access() always dereferences symbolic links.  If you need to check the permissions on a  sym‐
       bolic link, use faccessat(2) with the flag AT_SYMLINK_NOFOLLOW.

       access()  returns  an error if any of the access types in mode is denied, even if some of the
       other access types in mode are permitted.

       If the calling process has appropriate privileges (i.e., is superuser), POSIX.1-2001  permits
       an implementation to indicate success for an X_OK check even if none of the execute file per‐
       mission bits are set.  Linux does not do this.

       A file is accessible only if the permissions on each of the directories in the path prefix of
       pathname  grant  search  (i.e.,  execute) access.  If any directory is inaccessible, then the
       access() call will fail, regardless of the permissions on the file itself.

       Only access bits are checked, not the file type or contents.  Therefore, if  a  directory  is
       found  to  be writable, it probably means that files can be created in the directory, and not
       that the directory can be written as a file.  Similarly, a DOS file may be found to be  "exe‐
       cutable," but the execve(2) call will still fail.

       access()  may  not  work  correctly on NFS file systems with UID mapping enabled, because UID
       mapping is done on the server and hidden from the client, which checks permissions.   Similar
       problems can occur to FUSE mounts.

# BUGS

       In kernel 2.4 (and earlier) there is some strangeness in the handling of X_OK tests for supe‐
       ruser.  If all categories of execute permission are disabled for a  nondirectory  file,  then
       the  only  access()  test  that returns -1 is when mode is specified as just X_OK; if R_OK or
       W_OK is also specified in mode, then access() returns 0 for such files.   Early  2.6  kernels
       (up to and including 2.6.3) also behaved in the same way as kernel 2.4.

       In kernels before 2.6.20, access() ignored the effect of the MS_NOEXEC flag if it was used to
       mount(2) the underlying file system.  Since kernel 2.6.20, access() honors this flag.


# DEMO

```c
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char** argv)
{
    int ret = access("test.txt", F_OK);
    if(ret == 0)
        printf("test.txt is exist.\n");
    return 0;
}
```