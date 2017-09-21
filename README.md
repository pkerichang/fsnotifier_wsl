Modification of IntelliJ's fsnotifier binary to work on WSL.

the changes are:

1. as of 2017/09/21, WSL inotify does not have maximum user watch limit.  As
   the result, we need to modify fsnotifier to hard set a limit.  I modify
   read_watch_descriptors_count() method in inotify.c to return a hard coded
   number.

2. modify make.sh to always create 64-bit binary.


to compile:

1. install clang with apt-get.
2. run:

bash make.sh

to create the binary


to test:

0. make sure /proc/self/mounts is sym-linked to /etc/mtab.  For some
   reason WSL did not do this.
1. in main.c, set self_test variable to true.
2. compile.
3. run fsnotifier64 binary.
