# lintouch
A shell script that mimics an old dotnet Windows app for changing timestamps

```
Usage: lintouch -p <file> -t <value> <options>

Help:
  -h, --help        print this message

Standard options:
  -p <file>         Input file
  -t <value>        Change timestamp to <value>

Timestamp selection options:
  -c                Change the creation timestamp
  -m                Change the modification timestamp
```

Currently, it only supports changing the modification and 'creation' timestamps,
not any of the others.

'Creation' timestamps
---------------------

btime/crtime timestamps on Linux cannot be modified under normal circumstances,
and there is little-to-no possibility of those being made mutable on the kernel
level. Most discussions of this bring up the use of xattrs to handle this
use-case instead, and for that reason, that's what this script does.

When using the `-c` option, it sets the custom xattr `user.date.created`.
The `stattr` script can be used to display this new 'Created' timestamp alongside
the rest of the output of `stat`.