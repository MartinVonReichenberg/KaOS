# Tree (Unix Tree)

### [HOME](https://mama.indstate.edu/users/ice/tree/) | [SOURCE (1)](https://gitlab.com/OldManProgrammer/unix-tree) | [SOURCE (2)](https://github.com/Old-Man-Programmer/tree)

___

A directory listing program displaying a depth indented list of files.

Tree is a recursive directory listing command that produces a depth indented listing of files, which is colorized ala dircolors if the `LS_COLORS` environment variable is set and output is to `tty`. Tree has been ported and reported to work under the following operating systems: Linux, FreeBSD, OS X, Solaris, HP/UX, Cygwin, HP Nonstop and OS/2.

*Here is an example of the output of tree:*

```
~> tree -d /proc/self/
/proc/self/
|-- attr
|-- cwd -> /proc
|-- fd
|   `-- 3 -> /proc/15589/fd
|-- fdinfo
|-- net
|   |-- dev_snmp6
|   |-- netfilter
|   |-- rpc
|   |   |-- auth.rpcsec.context
|   |   |-- auth.rpcsec.init
|   |   |-- auth.unix.gid
|   |   |-- auth.unix.ip
|   |   |-- nfs4.idtoname
|   |   |-- nfs4.nametoid
|   |   |-- nfsd.export
|   |   `-- nfsd.fh
|   `-- stat
|-- root -> /
`-- task
    `-- 15589
        |-- attr
        |-- cwd -> /proc
        |-- fd
        | `-- 3 -> /proc/15589/task/15589/fd
        |-- fdinfo
        `-- root -> /

27 directories
```

___

#### NOTE:

*The HOMEpage URL seems to be shutdown . . .*

___

#### Install:

```
kcp -i tree
```
