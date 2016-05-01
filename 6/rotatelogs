#!/bin/bash
# rotatelogs--Rolls logfiles in /var/log for archival purposes and to ensure
#   that the files don't get unmanageably large. This script uses a config
#   file to allow customization of how frequently each log should be rolled.
#   The config file is in 
#     logfilename=duration
#   format, where duration is in days. If, in the config file, an entry is 
#   missing for a particular logfilename, rotatelogs won't rotate the file
#   more frequently than every seven days. If duration is set to zero, the
#   script will ignore that particular set of log files.

logdir="/var/log"	     # Your logfile directory could vary
config="$logdir/rotatelogs.conf"
mv="/bin/mv"
default_duration=7     # We'll default to a 7-day rotation schedule.
count=0

duration=$default_duration

if [ ! -f $config ] ; then
  # No config file for this script? We're out. You could also
  #   safely remove this test and simply ignore customizations 
  #   when the config file is missing.
  echo "$0: no config file found. Can't proceed." >&2; exit 1
fi

if [ ! -w $logdir -o ! -x $logdir ] ; then
  # -w is write permission and –x is execute. You need both to create new
  #   files in a Unix or Linux directory. If you don't have 'em, we fail.
  echo "$0: you don't have the appropriate permissions in $logdir" >&2
  exit 1
fi

cd $logdir

# While we'd like to use a standardized set notation like ':digit:' with 
#   the find, many versions of find don't support POSIX character class
#   identifiers--hence [0-9].

# This is a pretty gnarly 'find' statement that's explained in the 
#   prose further in this section. Keep reading if you're curious!

for name in $(find . -maxdepth 1 -type f -size +0c ! -name '*[0-9]*' \
     ! -name '\.*' ! -name '*conf' -print | sed 's/^\.\///')
do

  count=$(( $count + 1 ))

  # Grab the matching entry from the config file for this particular log file.

  duration="$(grep "^${name}=" $config|cut -d= -f2)"   

  if [ -z "$duration" ] ; then 
    duration=$default_duration   # If there' no match, use the default value.
  elif [ "$duration" = "0" ] ; then
    echo "Duration set to zero: skipping $name"
    continue
  fi

  # Set up the rotation filenames. Easy enough:

  back1="${name}.1"; back2="${name}.2";
  back3="${name}.3"; back4="${name}.4";

  # If the most recently rolled log file (back1) has been modified within 
  #   the specific quantum, then it's not time to rotate it. This can be 
  #   found with the "-mtime" modification time test to "find".

  if [ -f "$back1" ] ; then
    if [ -z "$(find \"$back1\" -mtime +$duration -print 2>/dev/null)" ] 
    then
      echo -n "$name's most recent backup is more recent than $duration "
      echo "days: skipping" ;   continue
    fi
  fi

  echo "Rotating log $name (using a $duration day schedule)"

  # Rotate, starting with the oldest log, but be careful in case one
  #   or more files simply don't exist yet.

  if [ -f "$back3" ] ; then
    echo "... $back3 -> $back4" ; $mv -f "$back3" "$back4"
  fi
  if [ -f "$back2" ] ; then
    echo "... $back2 -> $back3" ; $mv -f "$back2" "$back3"
  fi
  if [ -f "$back1" ] ; then
    echo "... $back1 -> $back2" ; $mv -f "$back1" "$back2"
  fi
  if [ -f "$name" ] ; then
    echo "... $name -> $back1" ; $mv -f "$name" "$back1"
  fi
  touch "$name"
  chmod 0600 "$name"    # Last step: Change file to rw------- for privacy
done

if [ $count -eq 0 ] ; then
  echo "Nothing to do: no log files big enough or old enough to rotate"
fi

exit 0
