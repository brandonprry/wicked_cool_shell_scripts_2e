#!/bin/bash
# archivedir--Creates a compressed archive of the specified directory.

maxarchivedir=10           # Size, in blocks, of 'big' directory
compress=gzip              # Change to your favorite compress app.
progname=$(basename $0)    # Nicer output format for error messages

if [ $# -eq 0 ] ; then      # No args? That's a problem.
  echo "Usage: $progname directory" >&2 ;exit 1
fi

if [ ! -d $1 ] ; then
  echo "${progname}: can't find directory $1 to archive." >&2; exit 1
fi

if [ "$(basename $1)" != "$1" -o "$1" = "." ] ; then
  echo "${progname}: you must specify a subdirectory" >&2
  exit 1
fi

if [ ! -w . ] ; then
  echo "${progname}: cannot write archive file to current directory." >&2
  exit 1
fi

# Is the resultant archive going to be dangerously big? Let's check...

dirsize="$(du -s $1 | awk '{print $1}')"

if [ $dirsize -gt $maxarchivedir ] ; then
  echo -n "Warning: directory $1 is $dirsize blocks. Proceed? [n] " 
  read answer
  answer="$(echo $answer | tr '[:upper:]' '[:lower:]' | cut -c1)"
  if [ "$answer" != "y" ] ; then
    echo "${progname}: archive of directory $1 canceled." >&2
    exit 0
  fi
fi

archivename="$1.tgz"

if tar cf - $1 | $compress > $archivename ; then
  echo "Directory $1 archived as $archivename"
else
  echo "Warning: tar encountered errors archiving $1"
fi

exit 0
